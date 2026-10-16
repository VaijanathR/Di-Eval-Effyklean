# EffyKlean Storefront Content Security Policy (CSP) — Implementation Proposal

**Status:** Proposal for coding-agent assessment; not an authorization to enforce a policy blindly or to deploy to production.  
**Scope:** Storefront responses only. Do not change the existing Admin CSP in this task.  
**Prepared:** 16 October 2026  
**Decision owner:** HU+DI

## Objective

Introduce a carefully tested Content-Security-Policy for EffyKlean's public storefront, starting in report-only mode and tightening it based on the resources the actual application needs. Protect the storefront without breaking catalogue images, checkout, or the Zoho Payments hosted-checkout navigation.

## Reference research

- A public URLscan capture for Flipkart showed a CSP using directives such as `default-src`, `script-src`, `style-src`, `img-src`, `frame-src`, `connect-src`, and `base-uri`. Its policy is tailored to a large platform and contains broad allowances. Do **not** copy its allow-list or permissive wildcards into EffyKlean.
- OWASP recommends delivering CSP through an HTTP response header and using `Content-Security-Policy-Report-Only` to observe violations before enforcement.
- MDN documents that CSP controls permitted resource origins and that adding multiple enforcing policies only tightens the effective policy.

References:
- Flipkart header observation (third-party URLscan capture): https://urlscan.io/result/01970b3f-df10-7585-817a-7a90cb067bc6
- OWASP CSP Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html
- MDN CSP header reference: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy

The Flipkart capture is an illustrative comparison, not proof of current policy on every Indian e-commerce site and not a template to copy.

## Candidate starting policy — REPORT ONLY

Use this as a diagnostic starting point, after checking the current templates and actual resource origins:

```http
Content-Security-Policy-Report-Only: default-src 'self'; base-uri 'self'; object-src 'none'; frame-ancestors 'none'; form-action 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: blob:; font-src 'self' data:; connect-src 'self'; frame-src 'none'
```

This is intentionally a **report-only candidate**, not an approved enforcement header. It may report violations from current inline scripts, externally hosted product images, fonts, analytics, or other dependencies. Determine which are legitimate from the repository and browser evidence before changing the policy. Do not add broad wildcards merely to silence violations.

The current agent report says the customer is sent to Zoho Payments hosted checkout by a normal link. Top-level navigation to that provider should not require adding Zoho to `script-src`, `connect-src`, or `frame-src`. Verify the actual implementation before relying on this. Do not embed hosted checkout in an iframe or change the payment flow as part of CSP work.

## Required implementation approach

1. Inspect current middleware/settings, storefront response paths, templates, static assets, product-image URLs, checkout forms, and the existing Admin CSP. Confirm exactly where the storefront policy can be applied without altering Admin behaviour.
2. Add the candidate as `Content-Security-Policy-Report-Only` for local/test storefront responses first. If the app has a supported reporting endpoint, assess it; do not invent a new endpoint or add persistent collection without review. Browser-console violation evidence is acceptable for the first local diagnostic pass.
3. Exercise at least: storefront home, product listing (expected 15 active products), product detail, cart, checkout, Pay Now navigation, payment return, and relevant error pages. Include the existing local end-to-end test and confirm the policy does not alter payment/order state.
4. Classify each violation as legitimate application dependency, avoidable inline content, unwanted third-party resource, or unexplained. Record actual origins and the evidence. Avoid authorizing origins based solely on a browser warning.
5. Propose the final enforcing policy separately. Prefer removing inline scripts or using supported nonce/hash mechanisms over allowing arbitrary scripts. Keep any `unsafe-inline` allowance limited and justified; never introduce `unsafe-eval` or broad `*` source allowances without a documented, approved reason.
6. Only enforce after the required storefront paths have been exercised and violations reconciled. Do not silently enforce a policy that breaks required pages. If a business/architecture decision is needed, STOP and report it for HU+DI.
7. Preserve the existing Admin CSP and existing approved/unrelated changes. Do not change payment integration, provider settings, or external business workflows as a side effect.
8. Add proportionate tests for the header's presence/scope and relevant response paths. Run focused tests first; use the project's normal broader gate at the appropriate checkpoint.
9. Update the applicable plan/status register and project continuity records with the exact policy, report-only/enforcement state, tests, evidence, known limitations, and remaining work.

## Acceptance evidence

- The CSP header is present on intended storefront responses and not unintentionally applied to unrelated routes.
- Admin policy and behaviour remain unchanged.
- Report-only browser checks cover the specified storefront and checkout journey; each observed violation is classified.
- Product imagery and all 15 intended active products remain usable.
- Checkout and Zoho Payments hosted navigation still work; payment return, idempotency, and the AD-10 NO PAYMENT → NO DISPATCH gate remain intact.
- Tests and resulting repository state are reported precisely. Report-only evidence must not be described as proof that enforcement is safe.

## Explicit boundaries

- Local/test validation only unless HU separately authorizes a production deployment.
- No live payments, production provider writes, production webhook changes, or deployment.
- No broad source wildcards copied from a large marketplace.
- No changes to the Admin CSP, payment architecture, product source of truth, or unrelated approved work.
- This document is a proposal. The coding agent should assess it against the current repository and report any material conflict before enforcement; it must not treat the candidate policy as an unconditional instruction to ship.
