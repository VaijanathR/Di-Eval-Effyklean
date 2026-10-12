# HU+DI Decisions and Resume Checkpoint — 2026-10-13

**Status:** Decision and continuity note. This file records the latest HU+DI direction so Di can refer to it when the conversation resumes. It is not an implementation authorization.

## Repository purpose

This note belongs in the public analysis/decision repository, `VaijanathR/Di-Eval-Effyklean`, so the decisions are available for continuity. It is not a request to modify the local `EffyKleanProject` implementation repository. Keep credentials, tokens, secrets, private session logs, and other sensitive operational information out of this public repository.

## Confirmed HU+DI decisions

### 1. Payment provider direction

**HU+DI decision (2026-10-13): Zoho Payments is intended to replace Razorpay for EffyKlean.in.**

This settles the intended provider direction. It does **not** by itself authorize immediate code changes, deleting the existing Razorpay implementation, or production cutover.

Zoho Payments sandbox supplied by Hu:
- https://paymentssandbox.zoho.in/app/60091728822

Next technical step: perform read-only discovery of the current payment implementation, settings, tests, webhook handling, and architecture/specification constraints. Then recommend the smallest safe migration plan. Preserve existing order/payment state invariants and test coverage. Do not paste or commit credentials.

Payment safety invariant: **NO PAYMENT → NO DISPATCH**.

Planned payment test coverage should include, as applicable:
- successful and failed payments;
- interrupted or abandoned checkout;
- webhook signature verification and rejection of invalid events;
- duplicate/replayed events and idempotency;
- verification of amount, currency, and order reference before marking an order paid;
- preventing dispatch unless payment is verified.

### 2. Zoho Inventory sandbox and inventory authority

Zoho Inventory sandbox supplied by Hu:
- https://inventory.zoho.in/app/60091726840#/home/gettingstarted

**Existing business rule:** Zoho Inventory remains the stock authority.

Before proposing changes, inspect and document the current product/SKU mapping, stock and warehouse/location setup, order synchronisation, existing Zoho Flow, and Zoho–Shiprocket workflow. The sandbox URL alone is not evidence that the application is connected or that synchronisation is operational. Do not replace or modify existing workflows without evidence and the required HU+DI review.

### 3. Local end-to-end validation

Retain the agreed approach: exercise one or two products end to end locally before deployment. Use payment and shipping provider stubs where appropriate, while separately identifying what still requires real sandbox verification. Demonstrate that payment verification, order creation/state transitions, inventory behaviour, and fulfilment safeguards work together.

### 4. Implementation priority order

Hu's priority order is:

1. **Admin and integrations**
2. **Storefront functionality**
3. **Customer communication and updates**
4. **Beautification**

Explicit release blockers must still be surfaced even if they fall within a later workstream; do not silently reorder the priorities.

### 5. Governance and next action

- The next step is **read-only discovery and planning**, not implementation.
- Inspect the repository, frozen specification, architecture/decision records, current implementation evidence, tests, and production-readiness register before asking Hu to repeat information.
- Keep the frozen specification and architecture intact unless a genuine conflict requires a HU+DI decision.
- Distinguish business decisions from engineering recommendations.
- Recommendations and roadmaps are not implementation authorization.
- Raise genuine, irreconcilable conflicts using the agreed **STOP → REPORT → HU+DI DECIDE** process.
- Never use `git add -A` as a shortcut; preserve precise change control in the implementation repository.

Recommended discovery output: current capability and test evidence; missing sandbox setup/access; provider and integration risks; dependencies and release blockers; and a proposed implementation/test sequence aligned with the four priorities. Identify only questions that genuinely require Hu's decision.

## Resume note

Hu and Di agreed to pause after a productive work session and resume after a relaxing break. The next session should start from this checkpoint, review the latest evidence, and continue calmly without re-opening decisions already settled here.

**Last updated:** 2026-10-13
