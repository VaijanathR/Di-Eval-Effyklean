# EffyKlean — Read-Only Sub-Agent Investigation
## Zoho-Managed Shipment Lifecycle Synchronization
### HU+DI Working Direction — 19 October 2026

## 1. Assignment and authorization

Perform a **focused, READ-ONLY repository investigation** into adapting the EffyKlean.in website to the existing Zoho Inventory + Shiprocket shipment lifecycle.

This assignment is for the sub-agent only. Do not interrupt, redirect, or clear the main agent's context.

**Authorized:** inspect source code, tests, configuration, specifications, architecture/decision records, and existing documentation; run narrowly scoped read-only inspection commands; report findings and recommend the smallest safe implementation change.

**Not authorized:**
- Modify, create, delete, format, or regenerate repository files.
- Stage, commit, push, merge, or rebase.
- Change frozen specifications or architecture/decision records.
- Deploy or create/modify cloud resources.
- Call Zoho, Shiprocket, payment, email, or other external provider APIs.
- Change environment variables, credentials, database records, or provider settings.
- Enable shipment dispatch, retries, scheduled jobs, workers, or live integrations.
- Assume permission to run tests that write to a database or invoke external services.
- Clear or reset the main agent's context.

If any command could modify files, migrate a database, contact a provider, or create external side effects, do not run it without further authorization.

## 2. HU+DI's established business direction

EffyKlean.com has used the existing Zoho workflow for approximately two years. HU confirms that the established process is understood and should be preserved.

**Do not redesign the existing Zoho–Shiprocket business workflow. Adapt the EffyKlean.in website to it.**

The intended process is:

1. EffyKlean.in receives an order and confirms payment according to existing business rules.
2. The website sends the appropriate sales-order information to Zoho using the existing authorized integration.
3. Zoho remains responsible for its existing shipment creation and carrier-assignment process, including its existing Shiprocket integration.
4. Zoho notifies EffyKlean.in when shipment lifecycle events occur.
5. Subsequent Shiprocket updates reach Zoho and are synchronized to EffyKlean.in through Zoho.
6. EffyKlean.in updates its local shipment record, status history, and customer-facing tracking information.
7. The website does not independently create a Shiprocket shipment or call an unsupported Zoho shipment-creation operation.

Notification names may differ between Zoho, Shiprocket, and the website. The website must map event semantics to its own stable internal shipment states; it must not rely on literal event-name equality.

Expected lifecycle stages include:

- Shipment created.
- Carrier assigned and tracking details available.
- Package picked up.
- Package in transit.
- Out for delivery.
- Package delivered.

Relevant exceptions should be assessed if supported by the existing workflow: pickup failure, delivery attempt failure, cancellation, return-to-origin, and other shipment exceptions. Do not invent events or assume the exact external event names.

This is the agreed working direction. Any conflict with the frozen specification or approved order-state model must be reported for **STOP → REPORT → HU+DI DECIDE**. Do not resolve it unilaterally.

## 3. Known issue from the previous audit

The prior audit reported:

- `modules/orders/checkout.py:757-788` contains `request_shipment`, which transitions an order to `SHIPMENT_PENDING`, creates a local `Shipment(REQUESTED)`, and enqueues a `SHIPMENT` outbox task.
- The outbox worker invokes `_run_shipment` → `_attempt_fulfilment` → `zoho.request_fulfilment`.
- `integrations/zoho_inventory.py:736-740` reportedly raises `ZohoNotSupportedError` because EffyKlean does not create shipments directly.
- The existing stub can pass tests by pretending to create shipments, masking the real-adapter incompatibility.
- After repeated failures, the local order may reach `SHIPMENT_FAILED` with an action-required message.
- The previous audit found no verified inbound Zoho/Shiprocket tracking-status synchronization path and noted that post-shipment states were not approved.

These are leads from the previous report, **not a substitute for rechecking the current repository**. Confirm exact current paths, symbols, and behavior. If the repository has changed, report the current facts and differences.

## 4. Investigation tasks

### A. Establish the exact repository checkpoint

Report:
- Current branch and HEAD commit.
- Whether the working tree is clean or dirty, using read-only commands.
- Whether relevant files are modified or untracked.
- Whether there are uncommitted changes that make the current implementation unstable to assess.

Do not reset, stash, clean, stage, or otherwise change the tree. Do not assume HEAD is the approved deployment source.

### B. Trace the current shipment lifecycle

Read the actual implementation and tests. Trace:

- Order/payment eligibility for shipment handoff.
- Creation and state changes of `Shipment`.
- Creation, claiming, retry, and completion of `SHIPMENT` outbox tasks.
- Calls to `zoho.request_fulfilment` or equivalent.
- Error handling and retry behavior.
- How the order and shipment states change on success or failure.
- Existing admin actions, manual retries, management commands, scheduled jobs, and workers that may trigger this path.

Provide the exact file paths, symbol names, and line ranges where available.

Determine which part is appropriate for the existing Zoho-managed handoff and which part incorrectly assumes that the website itself creates a shipment.

### C. Inspect existing inbound integration infrastructure

Read-only inspect the existing webhook/callback/API patterns, including relevant:

- URL routing and views.
- Authentication/signature verification.
- Payload validation and provider identity checks.
- Event persistence and deduplication.
- Transaction handling and outbox usage.
- Retry/replay and error logging.
- Idempotency safeguards.
- Existing integration models, audit records, and tests.

Do not create an endpoint or register a webhook.

Determine whether existing infrastructure can safely receive Zoho-originated shipment notifications, or whether a new endpoint/event model would be needed. Prefer existing proven patterns where appropriate.

Do not assume that payment-webhook signing can automatically authenticate Zoho Inventory events; verify the actual mechanisms and credentials separately.

### D. Map the website's shipment data model

Inspect the current `Order`, `Shipment`, outbox, integration-log, and related models and their constraints.

Report:
- Existing states and legal transitions.
- Fields for Zoho sales-order ID, Zoho shipment ID, carrier, tracking number, tracking URL, event timestamps, and delivery status.
- Whether external event IDs, deduplication keys, or an immutable event history already exist.
- Whether the model supports multiple shipments per order, partial shipments, carrier reassignment, cancellations, returns, or exception states.
- Which capabilities are genuinely required for the confirmed workflow versus speculative future scope.

Do not modify the frozen order-state model. Identify any required specification or migration decision for HU+DI.

### E. Propose a semantic event-mapping design

Recommend a mapping from incoming Zoho notification semantics to stable internal website states.

At minimum, address:

1. Shipment created.
2. Carrier assigned.
3. Picked up.
4. In transit.
5. Out for delivery.
6. Delivered.

Also assess supported exceptions, without inventing external payload fields or event names.

Explain how the design would handle:
- Duplicate deliveries of the same notification.
- Retries after endpoint failures.
- Out-of-order or delayed events.
- Events that lack a usable shipment or order correlation ID.
- Conflicting carrier/tracking information.
- A delivered event arriving before an earlier event.
- Unknown event names or schema changes.
- Events referring to a shipment that the website has not yet correlated.

Use an event log or equivalent durable mechanism if the current architecture supports or needs one. Do not silently discard unknown events. Recommend reconciliation through Zoho if notifications can be missed.

The mapping must reflect the event's meaning, not merely a text comparison. Do not assume every "shipped" event means physical pickup unless the actual source semantics confirm that meaning.

### F. Propose the smallest safe code change

Compare at least these options:

1. Reusing existing integration callback/webhook infrastructure.
2. Adding a dedicated authenticated Zoho shipment-notification endpoint and event processor.
3. Reusing the outbox for asynchronous processing of incoming events while keeping provider shipment creation out of the worker.

Recommend the smallest architecture-consistent option. It may combine these approaches if justified.

Explicitly distinguish:
- Outbound website-to-Zoho sales-order work.
- Zoho-managed shipment creation and carrier assignment.
- Inbound Zoho-to-website shipment notifications.
- Website-side processing and customer-facing status updates.

The website's outbox must not continue invoking an unsupported direct shipment-creation operation. Explain how the existing `SHIPMENT` task should be replaced, repurposed, or retired, but do not implement that change.

Do not propose direct website-to-Shiprocket shipment creation.

### G. Identify specification and security implications

Identify any conflicts with frozen specifications, architecture, ADRs, or existing authorization gates.

Assess:
- Authentication of inbound Zoho events.
- Replay protection and idempotency.
- Data validation and safe logging.
- Protection against arbitrary order/status updates.
- Auditability.
- Handling of PII and tracking URLs.
- Whether callbacks require a public HTTPS endpoint and a registered Zoho webhook.
- Any required schema migrations.

Do not invent secret names, signatures, or authentication capabilities. Mark unknowns explicitly.

### H. Recommend targeted tests

Propose tests for:
- Valid events for each lifecycle stage.
- Duplicate-event delivery.
- Out-of-order notifications.
- Invalid authentication and malformed payloads.
- Unknown event types.
- Missing or conflicting correlation IDs.
- Transaction rollback and retry behavior.
- Reconciliation after missed notifications.
- Ensuring the website does not call `zoho.request_fulfilment` to create shipments.
- Regression of existing payment/order behavior.
- Customer-visible status and tracking presentation.

Identify the existing tests that should be adjusted and new tests that would be required.

Do not run the full suite for this read-only investigation. Do not run any tests that may write to external systems or a shared database.

## 5. Required response format

Return a concise but evidence-backed report with these sections:

1. **Repository checkpoint** — branch, HEAD, working-tree status.
2. **Current implementation facts** — exact paths/symbols and the verified current behavior.
3. **Gap analysis** — what prevents the established Zoho workflow from working end to end on the website.
4. **Proposed event/state mapping** — source semantics to website states, noting any unknowns.
5. **Recommended minimal implementation** — files likely to change and responsibilities, without editing them.
6. **Security, idempotency and recovery** — callback security, duplicates, event ordering and reconciliation.
7. **Specification/architecture conflicts** — explicitly flag anything requiring STOP → REPORT → HU+DI DECIDE.
8. **Targeted validation plan** — tests and evidence needed before a later full-suite checkpoint.
9. **Open questions for HU+DI** — only genuinely necessary business decisions; do not ask HU to re-explain the established Zoho process.
10. **Authorization boundary** — confirm no files were changed, no tests with side effects were run, no external provider calls were made, and no commits/pushes/deployments occurred.

Use evidence from the current repository, not assumptions. Distinguish verified facts, inferences, and recommendations. If the current repository is changing concurrently, say so and identify the limits of the audit.

## 6. Stop conditions

Stop and report without changing anything if:
- Current implementation conflicts with frozen order-state or fulfillment specifications.
- The required inbound Zoho authentication mechanism is not established.
- The solution appears to require live credentials or provider-side changes.
- A migration or order-state change needs a decision.
- The repository changes while the investigation is in progress.

**Success means a clear, minimal, evidence-backed implementation proposal that HU+DI can review. It does not mean code has been changed or deployed.**
