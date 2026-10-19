Final consolidated report: Zoho-managed shipment lifecycle synchronization (read-only)

This follows the SSD §11 format. It also carries the instruction's §5 sections 1–10 as Part B. The checks were done in this session from the saved transcript and one fresh read-only git check; I contacted no provider.

1. Overall status

PARTIAL. This is not "complete". Tasks A, B, C, D and H are DONE (verified). Tasks E, F and G are PARTIAL. Each is a complete design proposal, but each depends on inputs only HU+DI can give. Three of the instruction's §6 stop conditions apply: the inbound authentication mechanism is not established, a migration or order-state decision is needed, and the repository changed during the work.

2. Original task ledger

Task IDs and wording are from AgntInstDigiOcnImplmntatn_19OCT2026_1505.md.

┌─────┬─────────────────────┬─────────────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┬───────────────────────────────────────┐
│ ID  │     Requirement     │   Status    │                                                        Evidence                                                         │               Remaining               │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ §1  │ Read-only, no side  │ DONE        │ I edited, staged, committed, pushed and deployed nothing. I ran no tests and no manage.py, and made no provider calls.  │ None                                  │
│     │ effects             │ (verified)  │ The Zoho API documentation was fetched with curl from public pages, which is not an API call.                           │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│     │                     │             │ Branch main, HEAD 625e210. 0 commits behind origin/main and 3 ahead. 0 staged, 0 stashes, 89 modified, 24 untracked, 89 │                                       │
│ A   │ Repository          │ DONE        │  files changed, +2025/−229. The relevant files are modified but uncommitted: checkout.py, models.py, payment_flow.py,   │ None                                  │
│     │ checkpoint          │ (verified)  │ zoho.py, zoho_inventory.py, run_outbox.py, and tests test_outbox.py, test_order_operations.py, test_f05_checkout.py,    │                                       │
│     │                     │             │ test_i04_checkout.py, test_zoho_inventory.py.                                                                           │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ B   │ Trace the shipment  │ DONE        │ See B1 below.                                                                                                           │ None                                  │
│     │ lifecycle           │ (verified)  │                                                                                                                         │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│     │ Inbound integration │ DONE        │                                                                                                                         │ The Zoho Inventory authentication     │
│ C   │  infrastructure     │ (verified)  │ See C1 below.                                                                                                           │ mechanism is unestablished, which is  │
│     │                     │             │                                                                                                                         │ a finding and not unfinished reading. │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ D   │ Data model          │ DONE        │ See D1 below.                                                                                                           │ None                                  │
│     │                     │ (verified)  │                                                                                                                         │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ E   │ Semantic event      │ PARTIAL     │ The design is complete (Part B, section 4). The real Zoho and Shiprocket values were never observed.                    │ See section 8, blockers 1 and 3       │
│     │ mapping             │             │                                                                                                                         │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ F   │ Smallest safe       │ PARTIAL     │ The two-phase design is checked against ARCHITECTURE.md §10–17 and the Zoho documentation (Part B, section 5). It has   │ See section 8, blockers 1, 2 and 3    │
│     │ change              │             │ not been checked against a real notification.                                                                           │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ G   │ Spec and security   │ PARTIAL     │ The conflicts and security assessment are complete (Part B, sections 6–7). The inbound authentication option is UNR.    │ See section 8, blockers 2 and 3       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ H   │ Targeted tests      │ DONE        │ I read the assertions of every shipment-related test. The classification is in Part B, section 8.                       │ None                                  │
│     │                     │ (verified)  │                                                                                                                         │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ §5  │ 10-section response │ DONE        │ Part B below.                                                                                                           │ None                                  │
│     │  format             │ (verified)  │                                                                                                                         │                                       │
├─────┼─────────────────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ §6  │ Stop conditions     │ DONE        │ Applied and reported.                                                                                                   │ None                                  │
│     │                     │ (verified)  │                                                                                                                         │                                       │
└─────┴─────────────────────┴─────────────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┴───────────────────────────────────────┘

B1. Shipment lifecycle trace (verified by reading; line numbers as of the last read, and the tree is still moving)
- Gate. modules/orders/checkout.py:761 request_shipment requires ORDER_READY, a succeeded payment, an earlier IST day and no staff hold. It sets SHIPMENT_PENDING, creates Shipment(REQUESTED), enqueues OutboxKind.SHIPMENT (models.py:880) and calls _attempt_fulfilment (:792).
- Outbox. outbox.py:125 _run_shipment, :182 RUNNERS, :190 _claim (select_for_update(skip_locked=True), 5-minute lease), _finish, :255 run_due. There are 3 total attempts, and the worker calls retry_shipment (checkout.py:861).
- Failure handling. _attempt_fulfilment catches all exceptions and records a failure. After 3 failures, SHIPMENT_PENDING → SHIPMENT_FAILED with an action-required log entry (:843).
- Real adapter. integrations/zoho_inventory.py:736-741 request_fulfilment always raises ZohoNotSupportedError("…EffyKlean does not create shipments").
- Stub. integrations/zoho.py:164-179 LocalZohoStub.request_fulfilment delegates to LocalShiprocketStub, so tests pass.
- Four triggers.
  - dispatch_orders and the scheduled dispatch job, through dispatch_ready_orders (checkout.py:916).
  - The admin retry retry_ship (backoffice/order_actions.py:247).
  - retry_integrations, through retry_pending_integrations (checkout.py:888-915), which retries every SHIPMENT_PENDING order with a REQUESTED shipment.
  - The outbox job and worker.
- All order-state transition sites.
  - PAYMENT_CONFIRMED → ORDER_READY (:673).
  - PAYMENT_CONFIRMED → ZOHO_SYNC_FAILED (:720).
  - ZOHO_SYNC_FAILED → PAYMENT_CONFIRMED (:749).
  - ORDER_READY → SHIPMENT_PENDING (:782).
  - SHIPMENT_PENDING → SHIPMENT_FAILED (:843).
  - SHIPMENT_FAILED → SHIPMENT_PENDING (:881).
  - Any → CANCELLED (operations.py:181).
  - Orders are created at PAYMENT_CONFIRMED (payment_flow.py:258).
- What fits the Zoho-managed handoff.
  - submit_to_zoho / confirm_order (PAYMENT_CONFIRMED → ORDER_READY, zoho_order_reference).
  - Shipment.delivery_status, delivered_at, tracking_reference and tracking_url (models.py:280-296).
  - operations.apply_delivery_update (:430-468, idempotent, with the _DELIVERY_NEXT transition table at :411 and an integration log entry).
  - The customer view (customer_view.py:42-46,104-115).
- What wrongly assumes the website creates the shipment. request_shipment, _attempt_fulfilment, retry_shipment, retry_pending_integrations, the SHIPMENT outbox kind and the dispatch job.
- The only caller of apply_delivery_update is order_actions.delivery_update (:347), a simulation button that is stub-only (LOCAL_PROVIDER_STUBS). No inbound Zoho or Shiprocket path exists.

C1. Inbound infrastructure (verified by reading)
- Route. config/urls.py:150 is the Zoho Payments webhook route, which points at storefront/views.py:132-162 zoho_payments_webhook. There is no inbound shipment route. modules/storefront/urls.py has only quote, orders and orders/<reference>.
- Processing. payment_flow.py:405-480 process_zoho_webhook treats the webhook as a notification and then re-fetches from Zoho. reconcile_attempt (:124) and reconcile_unresolved_attempts (:213) do the reconciliation.
- Deduplication. WebhookEvent (models.py:245) is keyed by a digest.
- Rejected deliveries. RejectedWebhookDelivery (models.py:255) is metadata only. record_rejected_webhook (payment_flow.py:385-402) stores reason and size, is bounded at 500 rows and never raises.
- Signature. integrations/zoho_payments.py:399-418 verify_webhook_signature uses HMAC-SHA256 over <timestamp>.<raw body> with the Zoho Payments webhook key. It enforces no timestamp tolerance. That key belongs to Zoho Payments and cannot authenticate Zoho Inventory events.
- Scheduling. backoffice/scheduling.py has the JOBS table (outbox every minute, reconcile-payments */10, dispatch hourly) and the advisory-lock run_locked.
- Conclusion. The deduplication, recording, re-fetch and rejection-log patterns are reusable. The authentication and the event model are not.

D1. Data model (verified by reading)
- Shipment (models.py:280-296) is OneToOne to Order. Its fields are status (REQUESTED, CREATED or CANCELLED), correlation_id, tracking_reference, tracking_url, delivery_status and delivered_at.
- Missing fields. There is no Zoho shipment ID, no carrier, no event ID, no event history and no timestamps per event.
- Not modelled. Multiple shipments per order, partial shipments, carrier reassignment, returns and exception states.
- Order.zoho_order_reference exists.
- OrderStatus has exactly nine values, pinned by tests/test_f05_boundaries.py:276.
- models.py:6-13 says post-shipment states are not approved.
- Required for the confirmed workflow: a Zoho shipment ID, a carrier, and a durable event log. Multiple shipments per order and partial shipments are speculative, because the instruction describes one shipment lifecycle.

Differences from the previous audit's leads. The line ranges moved (request_shipment was 757, now 761; the adapter raise was 736-740, now 736-741). The behavior matches, and the previous audit missed the fourth trigger, retry_integrations.

3. Completion-claim timeline

1. First report (shipment investigation). I said A–H were analysed. C, D, F and H were only partly read at that point. That was too strong.
2. First report, scopes claim. I said the Zoho token has "only four read scopes". This was stale: PROJECT_LOG.md 17 Oct records write scopes (items/contacts/salesorders CREATE, salesorders UPDATE). I corrected it later.
3. Second report (gap-closure ledger). I marked F and H "DONE". F had not been checked against ARCHITECTURE.md, and H's test list was unread.
4. Third report. I downgraded those, but still marked E, F and G "DONE" in some places, though source semantics were unobserved. I then restated them as PARTIAL.
5. Audit wording. I wrote that I "could not" re-read the SSD audit requirement. That was avoidable and wrong; I have now re-read it in full.
6. Earlier statement that HU+DI's direction "conflicts" with the frozen architecture. This was inaccurate. ARCHITECTURE.md §15 (lines 332–335) lists Zoho→Shiprocket mechanics, status propagation and event mapping as DEFERRED. The wording to amend is §11 and §15 line 334.
7. The H report. H is DONE (verified). This report is the first single consolidated one. Before it, the work was split into separate reports, which breaks the one-report rule.

4. Shortcuts and integrity findings

- I changed nothing. I weakened, skipped or edited no tests, wrote no placeholders, and left no TODO, pass or swallowed-error code of mine in the repo.
- Pre-existing, disclosed.
  - Stub masking. LocalZohoStub.request_fulfilment hides the real adapter's refusal.
  - Broad exception catch. _attempt_fulfilment catches all exceptions, so an unsupported-operation error and a transient error look the same.
  - Simulation button. The admin delivery_update is stub-only.
  - Retired path. The SHIPMENT outbox kind and the dispatch job are no longer valid under Zoho-managed shipping.
- Documentation evidence. The Zoho field names come from official public documentation fetched with curl. They are not observed from a live call, and the documented example values (FedEx, "Delivered") are illustrative only.
- I did the work myself, not in a sub-agent, although the instruction describes a sub-agent. My standing rule is not to spawn sub-agents unless you ask.

5. Validation

- No tests, linters, commands or migrations were run. The instruction forbids it, and there was no database-safe option.
- No CI evidence. I did not check whether CI ran.
- Read-only commands used. git status, rev-list, stash and diff stat; grep; file reads; curl of public documentation pages.
- Fresh check at the end of this pass:
  625e210, main, 0 3 behind/ahead of origin/main, 0 staged, 0 stashes, 89 modified, 24 untracked, 89 files changed, 2025 insertions(+), 229 deletions(-).

6. Repository reconciliation

- Position. Branch main, HEAD 625e210, 3 commits ahead of origin/main (02aeb80, 7a13cf8, 625e210), not pushed.
- Working tree. 0 staged, 0 stashes, 89 modified, 24 untracked. Insertions went from 2021 to 2024 to 2025 during this work. I made none of those edits, so the tree is changing from outside this session. That limits the audit, because the line numbers above may shift.
- Untracked file seen in the relevant set: modules/backoffice/audit_outbox.py. The 2026-10-19 state paragraph in CLAUDE.md records it as the AC-26.2 integration-failure audit event.
- Authorization. I did nothing that needs authorization. The HEAD is not necessarily the approved deployment source.

7. Assumptions and unverified behavior

- Real Zoho and Shiprocket event names, payloads and values are unobserved. No shipment event has ever appeared in the sandbox. The confirmed Sales Orders read back as shipped_status: pending, with no invoices and no packages.
- The integer shipment_status meaning is undocumented.
- A tracking URL source is unknown. The documentation example shows no such field.
- Whether Zoho's notification can carry a custom header or token is unknown. Validation record E-09 says custom headers and parameters are available, but this is not confirmed for HU's workflow.
- Phase 1 works only if Zoho writes shipment data into the Sales Order's packages[] in HU's setup. That is unverified.
- The 15-minute cron minimum on DigitalOcean is taken from earlier research.

8. Blocker audit

#: 1
Blocker: Real Zoho and Shiprocket field values, the shipment_status meaning, and any tracking URL source
Evidence it is genuine: The sandbox has no shipment events, and the instruction forbids contacting providers
Could I have done it now?: No
Next action: HU provides a sample notification or the Flow definition, or enables the Zoho shipping automation in the sandbox and authorizes a read-only read of one Sales Order
────────────────────────────────────────
#: 2
Blocker: Authentication option for any Phase 2 endpoint
Evidence it is genuine: E-09 states no signature scheme. Nothing in the repo establishes one.
Could I have done it now?: No
Next action: HU answers whether the notification can send a header or token. Phase 1 does not need it.
────────────────────────────────────────
#: 3
Blocker: Approvals: shipment sub-states, event-log table, Shipment fields (migration), ARCHITECTURE.md §11/§15 wording, cancellation "handover" meaning, exception display to staff
Evidence it is genuine: Frozen SPEC.md §15.4 and §16.2/§18.6/§18.9, models.py:6-13
Could I have done it now?: No. It is a decision, not an investigation.
Next action: HU+DI decide
────────────────────────────────────────
#: 4
Blocker: New: where the dispatch gates live
Evidence it is genuine: request_shipment enforces three gates, tested by test_no_payment_no_dispatch_even_if_a_paid_order_loses_its_successful_payment,
test_same_day_dispatch_is_refused_and_next_day_is_permitted, test_the_dispatch_day_is_the_ist_day_not_the_utc_day and test_a_held_order_is_not_handed_to_fulfilment. If Zoho confirms the Sales Order at
payment, the website no longer enforces them.
Could I have done it now?: No. It is a business decision.
Next action: HU+DI decide. One option is to delay confirmation of the Sales Order until the day-after and hold checks pass. I did not choose.
────────────────────────────────────────
#: 5
Blocker: The Zoho token scopes for reading packages directly
Evidence it is genuine: PROJECT_LOG.md 17 Oct lists no packages or shipmentorders scopes, and no repo code requests them
Could I have done it now?: Not needed for Phase 1, because the Sales Order read uses the existing salesorders.READ
Next action: Only if HU wants direct package or shipment reads

None of these was a failure to use an available tool. Items 1–2 are blocked by the instruction's no-provider-contact rule.

9. Highest risks and discrepancies

1. Real adapter plus any live trigger sends every paid order to SHIPMENT_FAILED. The four triggers are the dispatch job, admin shipment retry, retry_integrations and the outbox path. This is safe only while they stay unused.
2. Dispatch gates (blocker 4). Under Zoho-managed shipping, the same-day, no-payment and hold rules would no longer be enforced. This conflicts with a stated business rule and with ORD-085.
3. Cancellation after shipment. The cutoff keys on Shipment.status == CREATED (operations.py:98-107, :300-312). With no website-created row, a customer could cancel after Zoho has shipped.
4. No inbound path. The site shows no tracking or delivery from Zoho.
5. Stub masking. Tests pass while the real adapter always refuses.
6. Moving tree. Everything above is against a tree that changed during this work.

10. Next actionable step

Nothing further can change the proposal without blockers 1–4. This needs HU+DI's decision, not more reading. After approval, the smallest batch is:
1. Retire the four shipment-creation triggers.
2. Add the event log and the Shipment fields (migration).
3. Add the Phase 1 Sales Order poll.
4. Map the statuses.
5. Rewrite the retired-path tests and add the new ones (Part B, section 8).

---

Part B: the instruction's §5 response format (sections 1–10)

1. Repository checkpoint

- VF: Branch main, HEAD 625e210, 3 commits ahead of origin/main. The tree is dirty: 89 modified, 24 untracked, 0 staged, 0 stashes, +2025/−229.
- VF: The relevant files are modified but uncommitted: checkout.py, models.py, payment_flow.py, zoho.py, zoho_inventory.py.
- VF: The tree changed during the work (insertions 2021 → 2024 → 2025; request_shipment moved from 757 to 761).
- Limit: This is an assessment of a moving working tree, not an approved deployment source.

2. Current implementation facts

See B1 above. In summary, the only shipment-creation path in the website is request_shipment → outbox SHIPMENT → retry_shipment → _attempt_fulfilment → zoho.request_fulfilment, and the real adapter refuses it.

3. Gap analysis

1. After Zoho confirms a Sales Order the order sits at ORDER_READY. The scheduled dispatch job would push it into the failing path.
2. Nothing receives or fetches shipment status from Zoho, so tracking and delivery never reach the site.
3. apply_delivery_update requires shipment.status == CREATED and order.status == SHIPMENT_PENDING. Both are set only by the failing website-created path.
4. The Shipment model cannot express the Zoho-managed handoff (D1).
5. The cancellation cutoff is undefined under Zoho-managed shipping (section 9, risk 3).
6. The dispatch gates have no home in the new flow (blocker 4).

4. Proposed event and state mapping

The Zoho field names are documented. Their real values are unobserved. The mapping is by meaning, not by event name.

┌─────────────────────────────────────┬──────────────────────────────────────────────────────────────────┬───────────────────────────────────────────────────────────────────────────────────────────────────┐
│               Meaning               │                     Documented source field                      │                                          Website mapping                                          │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Shipment created                    │ A package with shipment_id / shipment_number                     │ Create the Shipment (status CREATED) and set the new Zoho shipment ID. Whether "created" equals   │
│                                     │                                                                  │ physical handover is UNR.                                                                         │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Carrier assigned, tracking          │ carrier, tracking_number                                         │ Fill the new carrier field and tracking_reference. tracking_url has no documented source: UNR.    │
│ available                           │                                                                  │                                                                                                   │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Picked up                           │ detailed_status (courier text), shipment_status (integer,        │ New internal sub-state. Customer text stays "Shipped".                                            │
│                                     │ meaning undocumented)                                            │                                                                                                   │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ In transit                          │ Same                                                             │ New internal sub-state. Same text.                                                                │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Out for delivery                    │ detailed_status, status                                          │ OUT_FOR_DELIVERY (exists)                                                                         │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Delivered                           │ status (Delivered is a documented filter value)                  │ DELIVERED. Final, and set only from a report (SPEC 12.14).                                        │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Delivery attempt failed             │ detailed_status                                                  │ DELIVERY_UNSUCCESSFUL, shown as "Delivery Unsuccessful"                                           │
├─────────────────────────────────────┼──────────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Pickup failure, cancelled, return   │ Not documented                                                   │ Not mapped. Stored as unclassified for staff. SPEC 18.9 forbids exposing NDR/RTO to customers.    │
│ to origin                           │                                                                  │                                                                                                   │
└─────────────────────────────────────┴──────────────────────────────────────────────────────────────────┴───────────────────────────────────────────────────────────────────────────────────────────────────┘

Handling of messy inputs (REC):
- Duplicates and retries: Record each event once by a digest or external event ID, like WebhookEvent. Return 2xx on a duplicate and record before processing.
- Out of order and delayed: Never move a shipment backwards. Use the transition table. A delivered event arriving before earlier ones still sets DELIVERED, and the earlier steps are filled as "unknown time".
- Conflicting carrier or tracking: Keep the history. Show the latest from the source of truth and flag the conflict for reconciliation.
- No usable correlation ID, or an uncorrelated shipment: Store the event as unmatched and visible in Admin. Never discard it.
- Unknown event names or schema changes: Store verbatim as metadata and mark "unclassified".
- Rule: Do not treat every "shipped" as physical pickup. Reconciliation through Zoho covers missed notifications.

5. Recommended minimal implementation (REC, nothing edited)

Comparison:
1. Reuse the payment-webhook path. Not suitable as-is. It authenticates with Zoho Payments' own signature and the event model is payment-specific.
2. Dedicated authenticated endpoint plus event processor. Valid, but it depends on an authentication mechanism that isn't established.
3. Outbox for processing incoming events. Fits the existing pattern (row lock, skip_locked, 3 attempts), with no provider shipment creation in the worker.

Recommended: a two-phase combination.
- Phase 1, no public endpoint. A scheduled read-only poll of the Sales Order through _sales_order (zoho_inventory.py:462, GET /salesorders/{id}, existing salesorders.READ scope). It updates the website from packages[]. This needs no inbound authentication or registered webhook. App Platform cron runs at most every 15 minutes, which is acceptable for tracking.
- Phase 2, optional. An authenticated endpoint that works only as a hint. It stores the event, then re-reads Zoho before changing anything, the same way process_zoho_webhook treats Zoho Payments.

The four concerns, kept separate:
- Outbound website-to-Zoho sales-order work: unchanged (submit_to_zoho / confirm_order).
- Zoho-managed shipment creation and carrier assignment: Zoho's, not the website's.
- Inbound Zoho-to-website notifications: Phase 1 poll, then optional Phase 2.
- Website-side processing and customer status: the new event processor, then the existing apply_delivery_update and customer view.

Files likely to change and their responsibilities:
- modules/orders/models.py: event log table and new Shipment fields (Zoho shipment ID, carrier). A migration.
- A new event processor module in modules/orders/: idempotent event recording and mapping.
- integrations/zoho_inventory.py: read methods for the shipment state.
- modules/orders/checkout.py, outbox.py, backoffice/scheduling.py: retire the website-created shipment path.
- modules/orders/operations.py: loosen apply_delivery_update preconditions and rework the cancellation cutoff (decision needed).
- config/urls.py and modules/storefront/views.py: Phase 2 only.

Retiring the SHIPMENT task:
- Stop enqueueing it in request_shipment.
- Make the runner return a terminal "handled by Zoho" result for old rows.
- Keep the enum value so history stays readable.
- Remove the dispatch job.
- Disable the admin shipment retry and the shipment half of retry_integrations.
- Propose no direct Shiprocket call.

6. Security, idempotency and recovery

- Authentication (UNR): E-09 (docs/architecture/ARCHITECTURE_CAPABILITY_VALIDATION.md:214-217) records no stated signature scheme and no retry guarantee for Zoho Inventory webhooks. It says a scheduled pull is required. E-12 records Shiprocket webhooks with an optional token. The payment key cannot authenticate these events, and I invented no secret name or scheme.
- If Phase 2 goes ahead (REC): A shared secret in a custom header or query parameter, only if Zoho supports it for this workflow. Never trust the payload, re-fetch from Zoho, cap the body size, and reject by metadata only.
- Public URL: Needed only for Phase 2, with a registration by HU in Zoho. The Zoho Payments webhook is still unregistered.
- Arbitrary updates: All status changes go through the transition table. Look up the shipment by Order.zoho_order_reference.
- Tracking URLs: Already guarded when rendered (checkout_pages.py:1018 _safe_link).
- PII: Log event type and IDs only, never addresses or phone numbers.
- Recovery: The poll is the safety net for missed notifications.
- Audit: Write status changes through the transition table and the integration log.

7. Specification and architecture conflicts (STOP → REPORT → HU+DI DECIDE)

1. SPEC.md §15.4 and models.py:6-13: post-shipment states are not approved, so new sub-states need approval.
2. SPEC.md §16.2/§15.5/§18.6: what counts as "handover" when Zoho creates the shipment, and the cancellation and edit cutoff.
3. SPEC.md §18.9: customer states are limited to Order Confirmed → Processing → Shipped → Out for Delivery → Delivered, plus Delivery Unsuccessful. NDR, RTO and reattempt stay hidden, so "picked up" and "in transit" can only be internal.
4. SPEC.md §12.14: DELIVERED is set only when Shiprocket or the courier reports it. The report would arrive via Zoho. The meaning is consistent but needs confirming.
5. SPEC.md §15.7: Admin must distinguish EffyKlean, Zoho and Shiprocket information. Data arriving through Zoho needs a defined label.
6. ARCHITECTURE.md §11 ("Order ready + Shiprocket unavailable → … bounded retries") and §15 line 334 need amending. §15 lines 332–335 list these mechanics as DEFERRED, so this is a wording amendment, not a conflict with a decision.
7. Migration: the event log and Shipment fields need approval.
8. New: the dispatch gates (blocker 4).

8. Targeted validation plan (nothing run)

Retire or rewrite (they assert behavior that goes away):

┌────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┬───────────────────────────────────────┐
│                                                                                Test                                                                                │            What goes away             │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│                                                                                                                                                                    │ Worker retries, exhaustion and        │
│ test_outbox.py::test_failed_shipment_is_retried_by_the_worker_then_exhausted, test_shipment_recovers_once_and_is_never_duplicated                                  │ recovery of a website-created         │
│                                                                                                                                                                    │ shipment                              │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ test_retry_paths.py::test_shipment_is_created_once_whichever_path_runs_first, test_shipment_attempts_are_three_in_total_across_both_paths                          │ Three attempts shared across two      │
│                                                                                                                                                                    │ creation paths                        │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ test_order_operations.py::test_shipment_failure_is_retried_then_becomes_an_exception_state, test_an_operator_can_retry_a_failed_shipment_and_it_is_not_duplicated, │ The retry cycle and the               │
│  test_the_retry_command_runs_a_pass_and_reports_counts, test_the_retry_pass_touches_only_orders_inside_their_budget                                                │ retry_integrations shipment half      │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ test_e2e_prototype.py::test_dispatch_and_retry_passes_never_duplicate_shipments,                                                                                   │ Dispatch and retry duplicate          │
│ test_shiprocket_outage_is_retried_then_visible_then_recoverable_without_duplicates                                                                                 │ protection                            │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ test_adapter_stub_contracts.py::test_shipping_failure_reports_not_created_and_no_tracking,                                                                         │ Stub shipment creation                │
│ test_fulfilment_is_idempotent_per_correlation_id_and_distinct_across_ids                                                                                           │                                       │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼───────────────────────────────────────┤
│ test_f06_api.py line 56                                                                                                                                            │ A test double overriding              │
│                                                                                                                                                                    │ request_fulfilment                    │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┴───────────────────────────────────────┘

Keep the rule, change the setup (their setup calls request_shipment, dispatch_ready_orders or the stub shipment path):
- Cancellation cutoff (needs the "handover" decision): test_e2e_prototype.py::test_cancellation_after_handover_is_refused, test_cancellation_before_handover_stops_dispatch_and_records_a_simulated_refund; test_order_operations.py::test_cancellation_is_refused_once_the_shipment_is_handed_over, test_a_pending_shipment_request_is_cancelled_with_the_order, test_a_cancelled_order_is_never_dispatched_or_retried; test_customer_order_actions.py::test_cancellation_is_refused_after_handover; test_admin_order_actions.py::test_cancel_is_refused_after_handover.
- Dispatch gates (blocker 4):
  - The four tests named there.
  - test_phase1_payments.py::test_an_order_whose_zoho_confirmation_is_pending_is_not_dispatched and test_dispatch_command_needs_debug_for_as_of_and_dispatches_next_day.
  - test_f05_checkout.py::test_an_unpaid_order_cannot_be_dispatched and test_zoho_unavailable_means_not_ready_and_no_dispatch.
  - test_testcodes.py::test_the_dispatch_gate_is_unchanged_for_a_test_order.
  - test_local_acceptance.py::test_two_product_journey_with_zoho_outage_recovery_and_no_dispatch_without_payment.
- Journeys that end in a shipment: test_positive_e2e_purchase_journey, test_correlation_ids_are_stable_unique_and_deterministic, test_guest_journey_from_cart_to_delivery_with_distinct_statuses, test_a_delayed_confirmation_places_exactly_one_order_and_dispatch_waits_a_day, test_duplicate_notifications_and_browser_returns_make_one_order_and_one_shipment, test_zoho_outage_after_payment_is_visible_preserved_and_recoverable, test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund, test_a_later_status_update_attaches_to_its_own_order_only, test_admin_ux.py::test_orders_list_detail_and_filters_are_read_only, test_replacement_evidence.py (setup line 66), test_i04_checkout.py (helper line 153), test_admin_commands.py::test_seed_creates_labelled_test_data_in_every_lifecycle_state_idempotently.
- Delivery presentation (assertions stay): test_an_unsuccessful_delivery_is_shown_in_the_approved_words, test_delivery_updates_follow_the_allowed_progression, test_delivery_cannot_be_reported_before_the_shipment_exists, test_tracking_shows_delivery_progress_in_the_approved_words.

Keep unchanged:
- test_zoho_inventory.py::test_no_second_shipment_writer.
- test_zoho_sync_tasks.py::test_sync_success_is_not_proof_of_payment_and_never_dispatches.
- test_sec_f02_f03_checkout_integrity.py::test_sequential_duplicate_submission_creates_one_order.
- test_admin_orders_list.py::test_delivery_column_separates_delivery_from_shipment_and_tracking.
- test_returned_packages.py.
- test_integration_visibility.py::test_outbox_card_counts_the_real_table, which needs a change only if the SHIPMENT kind is removed.
- test_f06_api.py lines 502–507.
- test_f05_boundaries.py::test_f05_states_are_exactly_the_approved_minimum. It pins OrderStatus to nine values, so new detail goes on Shipment, not on Order.

New tests required:
1. A valid event for each lifecycle stage: created, carrier and tracking assigned, picked up, in transit, out for delivery, delivered.
2. Duplicate delivery of the same event, and the same state read twice from a poll.
3. Out-of-order and delayed events, including delivered arriving first, with no backward movement.
4. Missing or conflicting correlation ID, and an event for an uncorrelated shipment.
5. Unknown event or status values stored unclassified.
6. Conflicting carrier or tracking data.
7. Rollback and retry on a processing error.
8. Reconciliation after missed notifications.
9. Phase 2 only: rejected authentication and malformed payloads, with metadata-only logging.
10. A guard that no code path calls request_fulfilment to create a shipment.
11. Customer-visible status and tracking, with no NDR, RTO or reattempt wording.
12. Regression of payment, order creation and the dispatch gates.

Evidence needed before a later full-suite checkpoint: one read of a real sandbox Sales Order that has a Zoho-created shipment. That needs HU's Zoho-side automation enabled and your authorization.

9. Open questions for HU+DI

1. Show one sample notification, or the Flow or custom-function definition, so I can see the real fields and identifiers. I am not asking you to re-explain the process.
2. Is there an authentication option for Zoho's notification (custom header or token)? If not, do Phase 1 (polling only) first.
3. What does "handover" mean for the cancellation cutoff when Zoho creates the shipment?
4. Approve the event log table, the new Shipment fields and the new internal states.
5. How should exceptions (pickup failure, cancelled shipment, return to origin) be shown to staff, given SPEC 18.9 hides them from customers?
6. New: where do the same-day, no-payment and staff-hold gates live now that Zoho owns shipping?
7. May the Zoho token get packages.READ / shipmentorders.READ? This is optional, because Phase 1 needs neither. (The earlier "four read scopes" statement was stale and is withdrawn.)

10. Authorization boundary

- Confirmed: I created, edited, deleted, staged, committed, pushed, stashed and deployed nothing.
- Confirmed: I ran no tests, manage.py commands or migrations, and made no calls to Zoho, Shiprocket, payment, email or any provider. I read local files only, plus public Zoho documentation via curl.
- Confirmed: I did not read .env or any secret.
- Confirmed: I enabled no dispatch, retries, workers, scheduled jobs or live integration.
- Confirmed: My scratchpad files are removed.
- Not sub-agent work: I did it myself, as disclosed in section 4.
