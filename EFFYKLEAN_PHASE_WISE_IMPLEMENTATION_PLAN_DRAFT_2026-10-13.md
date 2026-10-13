# EffyKlean.in — Phase-Wise Implementation Plan

**Status:** DRAFT FOR HU REVIEW — not yet approved as the controlling roadmap  
**Prepared:** 2026-10-13  
**Source:** HU-provided Claude Code response to “What is pending implementation in our EffyKlean project?”  
**Repository:** Public decision/analysis repository. This document contains no credentials or secrets.

## 1. Controlling implementation rule

**HU's explicit instruction: implement every task listed in the referenced agent response. Each listed implementation task is marked YES for implementation. Work phase by phase.** This instruction overrides conflicting older wording that says no item may start until it is separately named or approved.

- **YES** means the task is in implementation scope; it is not merely a recommendation.
- Dependencies such as credentials, sandbox access, provider configuration, or missing operational details are tracked as execution dependencies, not as a reason to change YES to NO.
- Frozen specifications, approved architecture, security controls, and recorded business invariants continue to govern implementation details. If a genuine contradiction makes a task unsafe or technically impossible to implement as written, STOP → REPORT → HU+DI DECIDE; continue independent work.
- The four items the agent explicitly listed as “out of scope without a decision” are recorded separately in Section 9. They are not pending tasks from the response and are not silently added to this YES list.
- This plan is presented for HU review. It becomes the controlling roadmap only after HU approves it.

## 2. Phase 0 — Baseline and register reconciliation

All tasks in this phase are **YES — IMPLEMENT**.

- **A-02 — YES:** Review and record the current uncommitted-work baseline, preserving all changes.
- **A-04 — YES:** Commit the reviewed baseline when the working tree and change set have been reviewed and the appropriate commit is authorised; then rerun the full test suite on that committed tree. Do not discard or overwrite uncommitted work.
- **J-10 — YES:** Work toward satisfying the release gate; record each unmet criterion and its evidence.
- Reconcile all tasks in this plan with `docs/foundation/PRODUCTION_READINESS_REGISTER.md`, preserving the agent's identifiers and mapping each item to its phase.
- Record the current branch, HEAD, working-tree state, migrations and test baseline from repository evidence. The reported 1,819-test pass was on an earlier tree and must not be represented as current validation.

**Exit evidence:** preserved baseline; current test result; reconciled task-to-phase mapping; explicit list of remaining release-gate criteria.

## 3. Phase 1 — Credential-free engineering and local quality

All tasks in this phase are **YES — IMPLEMENT**.

- **B-14 — YES:** Implement the shared Zoho Payments token cache.
- **J-03 — YES:** Define the scheduler for `run_outbox`, reconciliation and `dispatch_orders`.
- **J-02 — YES:** Resolve and implement the storefront header/CSRF requirements in line with the approved security architecture.
- **A-05 — YES:** Add a CI workflow that calls `scripts/ci.sh`.
- **A-03 — YES:** Map acceptance criteria to tests.
- **F-01 — YES:** Add combo-discount regression coverage.
- **J-08 — YES:** Establish and record a loading-time baseline.
- **E-07 — YES:** Rerun responsive checks and record the results.
- **Development migration — YES:** Review and safely apply/validate the reported new `orders.0022` migration against the development database.

**Exit evidence:** relevant tests, full-suite result, lint and framework checks, migration validation, responsive-check result, loading-time baseline, and updated project log.

## 4. Phase 2 — Local end-to-end order journey with stubs

All tasks in this phase are **YES — IMPLEMENT AND TEST**.

Build and test one complete local journey using one or two products and stubs/mocks for external providers before deployment. Include:

- Product selection, SKU/order lines, pricing and applicable discounts.
- Checkout and order creation.
- Payment-session creation and success/failure result handling using a stub.
- Enforcement of **NO PAYMENT → NO DISPATCH**.
- Inventory read/order handoff boundaries using stubs where needed.
- Shipping handoff and tracking/status return boundaries using a stub.
- Relevant customer-facing order status and notification events.
- Failure, duplicate-event/idempotency and reconciliation cases relevant to this journey.

**Exit evidence:** repeatable automated E2E result on the approved local PostgreSQL setup; success and failure paths; no real provider write or production dispatch during stub tests; known limitations recorded.

## 5. Phase 3 — Zoho Payments and Zoho Inventory sandbox proof

All tasks in this phase are **YES — IMPLEMENT AND VERIFY**.

- **B-01 — YES:** Run and verify the Zoho Payments sandbox session flow.
- **B-02 — YES:** Run and verify the payment webhook flow.
- **B-05 — YES:** Verify the Zoho Inventory stock-read flow.
- **B-06 — YES:** Verify Zoho Inventory Sales Order creation.
- **B-11 — YES:** Verify the end-to-end consistency between the amount successfully paid and the Sales Order total.
- Use one TESTCODE order for the proof.
- Obtain/use the required Zoho test organisation and OAuth credentials; record missing access as a concrete dependency.
- Verify order reference, amount/currency, webhook validation, duplicate-event handling and reconciliation as applicable.
- Zoho Payments is the intended provider direction. Do not introduce new Razorpay dependencies or perform a live cutover as part of sandbox verification.

**Exit evidence:** recorded sandbox outcomes and identifiers, verified payment/Sales Order amount consistency, and no unapproved production writes.

## 6. Phase 4 — Zoho mappings and shipping

All tasks in this phase are **YES — IMPLEMENT**.

### Zoho mappings
- **B-07 — YES:** Implement the approved GST/tax/invoice mapping.
- **B-08 — YES:** Implement customer mapping to Zoho contacts.
- **B-16 — YES:** Complete the required HSN/tax mapping and validation.
- Inspect and document whether the existing Zoho Flow conflicts with EffyKlean writes; validate the interaction and prevent duplicate/conflicting order writes. Do not replace or modify the existing flow without the required HU+DI review.

### Shipping
- **C-01 — YES:** Implement the Zoho → Shiprocket handoff; remove the current “refuses to ship” limitation through the approved adapter behaviour.
- **C-02 — YES:** Implement the shipment tracking/status return path.
- **C-04 — YES:** Establish and implement the weight/dimension master.
- **C-05 — YES:** Establish and implement pickup mapping.

**Exit evidence:** documented mappings and test results; tested shipping handoff/status path; Zoho Inventory remains the stock authority; any provider-dependent limitation is explicit.

## 7. Phase 5 — Customer-facing capabilities and media

Every task listed in this section is **YES — IMPLEMENT**. Any missing provider/configuration/content is an execution dependency to resolve as part of the task, not grounds to omit it.

- **D-06 — YES:** Implement correct customer-facing GST amounts.
- **D-07 — YES:** Implement invoice generation/delivery behaviour.
- **D-09 — YES:** Complete the specified customer-facing order/payment experience.
- **B-13 — YES:** Complete the associated customer-facing payment/order capability.
- **N1–N11 — YES:** Implement the transactional email requirements, including provider integration, sender-domain configuration and approved message wording.
- **H-05 — YES:** Implement the Contact Form capability, including privacy wording, retention and email-provider requirements.
- **H-06 — YES:** Implement the Subscribe capability, including privacy wording, retention and email-provider requirements.
- **E-08 — YES:** Migrate videos currently hot-linked from the old site to approved storage.
- **DC-22/DC-25 — YES:** Complete the associated video/media migration requirements.
- **D-08 — YES:** Implement replacement video-upload storage and retention.
- **G-03 — YES:** Implement bank-transfer/UPI assisted orders.
- **G-04 — YES:** Implement distributor GST handling during a Zoho outage.
- **I-03 — YES:** Implement the low-stock view using the real Zoho stock read.
- **I-04 — YES:** Implement analytics with cookie-consent behaviour.

**Exit evidence:** each capability has implementation and test evidence; privacy, retention, sender and provider configuration is documented; media no longer depends on the old site's hot-linked video files.

## 8. Phase 6 — Infrastructure and release readiness

All tasks in this phase are **YES — IMPLEMENT/PREPARE AND VERIFY**. The agent grouped these under J-01 through J-07; retain the register's exact identifier-to-requirement mapping rather than inventing mappings where the report did not specify one.

- **J-01 to J-07 — YES:** Complete the registered infrastructure requirements, including:
  - Hosting preparation and approved deployment configuration.
  - HTTPS and HSTS settings.
  - Operational scheduler for `run_outbox`, reconciliation and `dispatch_orders`.
  - Secrets management.
  - Monitoring and alerts.
  - Backups and a successful restore drill.
  - Safe application/validation of required migrations.
- **J-10 — YES:** Verify the release gate against its recorded acceptance criteria and evidence.

**Boundary:** Infrastructure implementation and readiness work are in scope. Actual hosting/deployment or public launch remains subject to the existing separate hosting/launch authorisation boundary; this plan does not itself grant permission to launch publicly.

**Exit evidence:** security and operational settings verified; scheduler operation verified; backup restore demonstrated; migrations validated; monitoring/alerts checked; release-gate status supported by evidence.

## 9. Items the agent said were out of scope without a decision

These are **not included as YES implementation tasks in this plan**, because the agent did not list them as pending work and explicitly called them out of scope without a decision:

- Wishlist.
- Reviews and recommendations.
- Server-side cart.
- Related-product links.

Do not implement these unless the authoritative decision records or a later HU+DI decision places them in scope.

## 10. Execution and progress rules

- Work in phase order and complete each phase's exit evidence before progressing, unless HU+DI resolves a genuine blocker or sequencing issue.
- Maintain `PROJECT_LOG.md`, the readiness register and this implementation plan with task status and evidence.
- Use the exact task identifiers above; do not drop items when reorganising the plan.
- Preserve existing work. Never reset, clean, stash or overwrite changes to make the tree appear clean; never use `git add -A`.
- Do not commit, push, alter live provider settings or deploy without the appropriate authorisation.
- Credentials and sandbox access are dependencies to obtain safely; never commit secrets.
- If a task reveals a genuine contradiction with an established business invariant, STOP → REPORT → HU+DI DECIDE. Do not silently change the invariant or abandon unrelated work.

## 11. Definition of complete

The plan is complete when every YES task in Sections 2–8 has been implemented and validated with evidence, the release gate is supported by evidence, and all remaining external limitations are explicitly recorded. The four out-of-scope items in Section 9 remain excluded unless later decided otherwise.
