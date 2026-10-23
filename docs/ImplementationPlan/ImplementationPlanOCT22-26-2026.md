## Current status reconciliation — 23 October 2026 (supersedes prior totals)

The 245-row BUILD ledger has 83 unique items marked `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. All 83 DONE rows are mapped to Implemented in the 597-item primary disposition because the implementation and test evidence is recorded for each. External/provider/legal/operational follow-ups remain explicitly recorded as gates; they are not misrepresented as completed. In particular, MF-089's code and tests are implemented, but the host still must schedule the contact-retention job and HU legal review of wording remains outstanding. Therefore MF-089 is counted as Implemented at code/feature level, not as operationally scheduled or legally approved.

**Current 597-item primary-disposition totals: 340 Implemented + 160 BUILD + 10 LATER + 9 INVESTIGATE + 78 EXCLUDE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; MA-ORD-103 and MA-ORD-105 remain DEFERRED as implementation items but are EXCLUDE from current scope, leaving 160 active BUILD items (62 PARTIAL + 98 DEFERRED). The 83 reviewed DONE rows and their recorded evidence, limitations, and follow-ups are mapped in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv). The 22-Oct primary register and 18-Oct snapshot remain historical records; apply the current reconciliation overlay for future counts. This does not authorize production writes, deployment, provider actions, or implementation of deferred rows.

---

## Current status reconciliation — 23 October 2026 (supersedes 22-Oct totals)

The per-item BUILD ledger contains 245 unique IDs: 83 are `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. Reconciliation against the 597-item primary-disposition register promotes all 83 verified-DONE BUILD rows to `Implemented`. MF-089 is counted as `Implemented` at code/feature level; the host must still schedule the contact-retention job and HU legal review of wording remains outstanding. These external gates are not claimed complete. No item was promoted based on aggregate arithmetic alone; each promotion is listed in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv) with its row-level implementation, resolved-path, validation, evidence and limits.

**Current 597-item primary-disposition totals: 340 Implemented + 160 BUILD + 10 LATER + 9 INVESTIGATE + 78 EXCLUDE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; MA-ORD-103 and MA-ORD-105 remain DEFERRED as implementation items but are EXCLUDE from current scope, leaving 160 active BUILD items (62 PARTIAL + 98 DEFERRED). This is the current count to use in future queries. The 22-Oct 597-row register and the 18-Oct source snapshot remain preserved as historical evidence; apply the 23-Oct reconciliation overlay for the current status. This does not authorize production writes, deployment, provider actions or work on deferred rows.

---

## Corrected disposition reconciliation — 22 October 2026

The row-level disposition register and HU+DI decision log have been corrected. The first update had changed the primary classification of 17 activities that were already marked Implemented; those original classifications have been restored. A further 32 prior HU YES/NO decisions were recovered from the canonical 122-capability decision master where no later 22-Oct batch entry superseded them. The historical 18-Oct source snapshot remains unchanged.

The earlier count of 250 purportedly unanswered rows was provisional and is superseded by the historical-answer reconciliation. The 22-Oct baseline had 256 Implemented, 245 BUILD, 10 LATER, 10 INVESTIGATE and 76 EXCLUDE (597 total) before the 23-Oct evidence-based implementation-status reconciliation, after recording MF-089 BUILD, MF-093 LATER and MF-105 BUILD. The prior decision ledger, canonical 122-capability master and explicit 18-Oct HU clarifications have now been mapped into the register; prior answers are not to be asked again. Before reconciliation, 87 rows were marked INVESTIGATE; this was never a fresh-question count. Of those, 49 MA rows with recovered prior YES answers were reconciled into BUILD (41) or EXCLUDE (8), and composite MF-116 was resolved from existing decisions into BUILD; no original question was repeated. The current register has 10 INVESTIGATE rows, not 87. The remaining 10 INVESTIGATE rows comprise two MA rows with an already-recorded direction/composite-scope note and eight MF cross-cutting/technical/evidence/access/dependency rows. Di must first resolve matters already decided by frozen rules, prepare evidence-backed proposals for genuine conflicts, and distinguish HU decisions from technical verification. On 22 October, the 32 MF rows that previously lacked row-level decision metadata were checked against the persistent HU answer log and known project directions. Their metadata now records prior answers, evidence/validation-only work, deferred dependencies, or the specific unresolved policy issue; these 32 are not 32 new questions. HU approved MF-089 as BUILD on 22 October; implementation and control evidence remain outstanding, and legal sufficiency is not implied by the operational approval. Do not ask HU about implementation, access, validation or provider facts that can be established from evidence. The older 443 YES / 50 NO / 1 evidence-only split across 494 MA rows remains a working, not fully source-verified tally and must not be blindly applied.

Corrected primary-disposition totals after historical-answer reconciliation across all 597 rows: **Current: 340 Implemented + 0 confirmed duplicate + 162 BUILD + 10 LATER + 9 INVESTIGATE + 76 EXCLUDE = 597**. The dispositions were updated from recorded prior HU answers and explicit clarifications; BUILD remains scope disposition, not authorization to execute.

The 76 annotated rows in the 22-Oct log are not 76 new disposition decisions. Scope preferences for activities already marked Implemented do not replace the Implemented primary classification. The 32 recovered prior YES/NO answers are recorded separately; BUILD/EXCLUDE are scope dispositions, not blanket authorization to execute. Do not ask HU to repeat an already recorded decision.

See the [corrected 597-row working register](./RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv), [HU+DI disposition log](./HUDI_DISPOSITION_DECISIONS_2026-10-22.md), and [corrected implementation summary](./IMPLEMENTATION_SUmmary_22Oct26_1250.md).

---

# EffyKlean — Consolidated Implementation Plan and Status Baseline
**Plan date:** 22 October 2026  
**Status:** HU+DI working plan; not blanket authorisation to execute every task. Each implementation batch still requires HU approval under the existing governance rules.  
**Repository:** `VaijanathR/Di-Eval-Effyklean` (public decision/continuity mirror)  
**Primary assessment:** [GAP_ASSESSMENT_211020261727.md](../../AgntGapAnalysis/GAP_ASSESSMENT_211020261727.md), revision 3, 22 October 2026  
**Previous controlling plan:** [EffyKlean Delta Implementation Plan](../../AgentImplementationRecords/EffyKlean_Delta_Implementation_Plan_13Oct2026.md)  
**Previous status register:** [EffyKlean Delta Implementation Status Register](../../AgentImplementationRecords/EffyKlean_Delta_Implementation_Status_Register.md)  
**Decision authority:** [HU+DI 122-capability master](../foundation/HU_DI_122_CAPABILITY_DECISION_AND_REFINEMENT_MASTER_2026-10-16.md), the original decision ledger, the conflict-reconciliation record, frozen SPEC v0.8 and ARCHITECTURE, and later explicit HU decisions.

## Latest HU+DI disposition updates — 22 October 2026

- **MF-089 — BUILD:** HU approved the operational contact-form privacy/retention baseline. Implementation must verify actual fields, publish the approved notice, restrict/audit access, enforce 180-day post-closure deletion/anonymization with documented exceptions, and keep the form fail-closed until required controls are implemented. This does not establish legal sufficiency.
- **MF-093 — LATER:** preserve the earlier HU decision; optional analytics/marketing tracking stays disabled until approved consent permits it. Do not reopen the existing analytics scope answer.
- **MF-105 — BUILD:** preserve the earlier HU decision and split into customer sign-in assistance and customer data-request export while retaining MF-105 as the source ID. Staff never view/set passwords; use verified time-limited single-use reset links. Export requires identity verification, customer-only data, exclusion of other customers' data/secrets, audit, and legal-hold/required-record handling.

These dispositions do not authorize implementation. The 10 remaining INVESTIGATE rows are separate and remain for the next HU+DI triage. The 18-Oct historical CSV remains unchanged.

## 1. Purpose and status rules

This document consolidates the assessment, the controlling Delta plan, the status register, the 597-activity inventory, and later HU+DI decisions into one task-oriented plan. It replaces neither the frozen SPEC/ARCHITECTURE nor the original decision ledger. It is the current plan/status view; preserve historical records rather than silently rewriting history.

Use exactly these status labels:

- **IMPLEMENTATION COMPLETED** — the implementation scope of this task is present and supported by code/documentary evidence. This label alone does not claim that a fresh test run, external-provider verification, sandbox end-to-end run, or production verification occurred. Evidence level and remaining verification are stated separately.
- **INCOMPLETE — PARTIALLY COMPLETE** — meaningful implementation exists, but at least one defined outcome or required verification remains.
- **INCOMPLETE — NOT STARTED** — no meaningful implementation of the defined task has been established.
- **INCOMPLETE — DEFERRED** — work is intentionally parked pending a recorded HU+DI decision, user-supplied data/legal wording, external access, cost approval, or a dependency. Deferred is not completed.
- **NotToBeIMPLEMENTED-inEffyklean** — the capability is explicitly excluded by an authoritative HU decision, frozen business rule, or architectural boundary. Do not implement it unless HU formally changes the decision.

For INCOMPLETE tasks, the category is mandatory and is part of the status. A feature can be implemented in a local stub or sandbox while the production workflow remains incomplete; split these scopes and state that distinction. Do not turn a blocked item into an exclusion, or infer a NO from missing evidence. Do not mark an item completed solely because a test name exists or an earlier agent reported a pass.

## 2. Evidence and source reconciliation

### 2.1 Assessment review

The 250,758-character, 1,554-line assessment was reviewed in numbered sections and line-range passes, including its requirement inventory, prior-agent claim audit, 76-gap register, 21 minor findings, proposed 63-task plan, decision list DEC-01…DEC-32, 147 SPEC acceptance criteria, 60 non-AC deliverables and the 597-row activity inventory. Its own limits remain binding: it did not run the 2,491-test suite, access the development database or provider consoles, re-run browser tests, or verify production. It reports code reading, collection/static checks and earlier-agent/provider evidence separately. Read the assessment's exact evidence and limitations before treating any result as runtime or production proof.

### 2.2 Comparison with the Delta plan and status register

The Delta plan is the controlling plan for the controlled local implementation scope established on 13 October; its original header is historical. The public plan copies and the public status register are historical mirrors, not a fresh measurement of today's private application repository. The status register ends with updates dated 16 October and repeatedly says Batch 1 was not formally accepted. Do not copy its older blocker assumptions over later HU reports.

The assessment reports the local application tree at HEAD `625e2102335a3e9b4a094466fb260fd023050fe8`, three commits ahead of `origin/main`, with 113 pre-existing changed paths (89 modified, 24 untracked), including migrations 0025–0027. This is the assessor's 22-Oct snapshot, not a live measurement made by this plan update. Do not stage, commit, reset, stash, clean, synchronize, or otherwise alter that private tree as part of maintaining this public plan.

### 2.4 Full 597-row disposition working register

The source register is now published at [RECONCILED_597_STATUS_2026-10-18.csv](./RECONCILED_597_STATUS_2026-10-18.csv). Its original ten columns are preserved as the historical source snapshot. A companion [597-row disposition working register](./RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv) adds a draft primary disposition, next action, **row-specific Definition of Done**, and validation-evidence method for every source ID. These 597 entries include implemented capabilities and unresolved, deferred or excluded activities—not 597 authorized implementation tasks. For INVESTIGATE rows, the DoD is decision/evidence resolution before implementation; for BUILD rows, it requires approved scope and feature-specific acceptance before work starts. See the [updated implementation summary](./IMPLEMENTATION_SUmmary_22Oct26_1250.md) for coverage and counts.

The historical-answer reconciliation and explicit 18-Oct/22-Oct clarifications changed the current working counts to 340 Implemented, 162 BUILD, 10 LATER, 9 INVESTIGATE / HU+DI DECISION REQUIRED, 76 EXCLUDE, and 0 confirmed duplicate-and-implemented; total 597. The 49 prior-YES MA rows formerly in INVESTIGATE have been reconciled to BUILD (41) or EXCLUDE (8), composite MF-116 has been resolved to BUILD, and 24 additional MF rows were dispositioned from existing reference evidence or prior directions (14 BUILD, 8 EXCLUDE, 2 LATER). These changes do not authorize execution. The remaining 10 INVESTIGATE rows are not 10 unanswered questions: two MA rows have an already-recorded direction/composite-scope note, and eight MF rows are cross-cutting, technical, evidence, access, validation, dependency or policy items. These remain working classifications, not blanket implementation authorization. No duplicate relationships have yet been evidenced, which does not mean no duplicates exist.

Do not infer BUILD from legacy `source_disposition=IMPLEMENT` alone, or EXCLUDE from combined “deferred/excluded/not authorized” wording. Before any implementation batch is authorized, verify each row against the original decision ledger, establish duplicate relationships with evidence, and obtain HU+DI decisions where needed. The register is a planning aid only and authorizes no implementation, deployment or external action.

### 2.3 Later HU facts that supersede older status wording

- HU explicitly reported on 18 October that **Zoho Payments sandbox is working**. Treat the old “Payments sandbox blocked” wording as stale. Payment-session/sandbox readiness is not equivalent to registered webhook, a webhook-first end-to-end proof, settlement reconciliation, or production readiness.
- HU explicitly reported that **Zoho Inventory sandbox is integrated with Shiprocket sandbox**. Treat the sandbox-side integration as completed/known in HU+DI continuity records. The gap assessment separately identifies the EffyKlean application's real-adapter fulfilment function as raising/not implemented and no production inbound delivery-status path. Do not conflate the Zoho-side integration with a complete EffyKlean-to-customer lifecycle or production evidence.
- Zoho Inventory sandbox read checks and selected authorized test writes were completed in the recorded history. Do not repeat old requests to verify HU's refresh-token copy or delete `refresh_token.inventory.expanded.out`; HU explicitly said not to revisit that file.
- DigitalOcean staging/deployment remains parked until the necessary HU+DI decisions and explicit spend/provisioning authorization. No live provider writes, production credentials, deployment, DNS or cutover are authorized by this plan.

### 2.4 Decision conflicts that must not be silently resolved

Stop and report for HU+DI decision where the frozen SPEC conflicts with recorded capability NO decisions or later directions. Especially: GST arithmetic/display (G-04); customer cancellation (ORD-064 versus SPEC §16 and the built `/track/` flow); the amount filter (ORD-019); returned-package inspection (ORD-076 versus plan NO, although SPEC §14.10 requires inspection); interim Admin fulfilment/tracking (ORD-080/081 recorded YES); production Zoho write/customer/item mapping; invoice delivery; paid-but-unconfirmed orders; disputes/chargebacks; enquiry-address validation defaults; editable order fields and guest cancellation authentication. Do not make business decisions in code or treat this plan as approval for those decisions.

## 3. Global Definition of Done and governance

Every task below has a task-specific DoD. In addition, apply these rules wherever relevant:

1. Evidence must identify command, exit code, test names/results, file/line or provider record, and environment (static/code read, local, mock, sandbox, staging, or production). A recorded historical pass is not a newly executed pass.
2. Tests run against PostgreSQL 17, not SQLite. Targeted tests after a narrow change; full suite only at agreed gates, not after every small fix. Do not weaken, skip, xfail or delete tests to get a green run. Review any guard-list or query-budget changes against their prior intent.
3. Keep the frozen SPEC/ARCHITECTURE unchanged unless HU+DI approve a controlled change request. Preserve NO PAYMENT → NO DISPATCH, no stale catalogue, idempotency, 3 total attempts (not 3 retries), secret hygiene, Zoho as inventory authority, and the agreed business pricing rules.
4. Use explicit paths for Git operations; never `git add -A`. No co-author trailers. Preserve Hu's uncommitted changes. Do not delegate to a coding agent unless HU explicitly authorizes delegation.
5. No production deployment, live credentials/writes, live customer payments, DNS/cutover, paid resource creation, real email, content publication, provider-record deletion or history rewrite without the specific separate HU approval.
6. At each authorized implementation task, report DONE/PARTIAL/NOT DONE/DEFERRED against every plan item and cite evidence. Update the private project records (PROJECT_LOG.md, CLAUDE.md, README/status register and AC index as applicable) only within the authorized task; then update the public mirror only when that publication is authorized.
7. Never print secrets or place them in logs, URLs, reports or commits. No claiming a test or provider operation passed unless its result was actually observed.
8. Before a task is closed, check its task-specific DoD, dependencies, regression risk, migration pairing, documentation/handoff and exact outstanding work. One task at a time; stop after its report and wait for HU's next authorization.

## 4. Implementation already completed (retain; do not redo without a specific reason)

These are implementation scopes already established in the project history or directly recorded by HU. They are labelled **IMPLEMENTATION COMPLETED** because the described implementation exists; that label does not falsely claim production readiness or a fresh test run. Evidence level is stated per item.

**C-01 — Django/PostgreSQL foundation and fail-closed settings.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** foundation scaffold, Python/Django/PostgreSQL/uv/pytest/Ruff setup and fail-closed production settings exist; assessment ran Ruff check/format and Django check successfully. Remaining: current-tree database-backed test/CI evidence is separate under P0-05.

**C-02 — Local B2C storefront-to-payment-to-order journey with stubs.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** catalogue/cart/checkout, server-side price review, payment attempt, provider-confirmed payment reconciliation, idempotent order placement and outbox enqueue exist; tests cover failure/replay/amount mismatch and NO PAYMENT → NO DISPATCH. Evidence: code/test-body reading plus historical test runs; assessment did not rerun tests. Production shipment lifecycle remains incomplete under Phase 2.

**C-03 — Zoho Payments adapter and sandbox session creation.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** adapter, token cache, hosted-session creation, signed-return/webhook processing logic and mock tests exist; HU confirms Payments sandbox works. The adapter implementation and sandbox readiness are completed at this scope. Webhook registration/webhook-first end-to-end proof, settlement/charge retrieval and production remain separately incomplete under P3/P8/P10.

**C-04 — Zoho Inventory adapter, stock-read path and guarded Sales Order/outbox foundations.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** Inventory adapter, stock reads, mapping/sync task infrastructure, guarded Sales Order flow, idempotency, retries and mock tests exist; recorded history includes sandbox reads and selected authorized test writes. HU says Zoho Inventory sandbox is integrated with Shiprocket sandbox. This does not mean production mapping/write policy or the EffyKlean delivery-status lifecycle is complete.

**C-05 — Zoho Inventory sandbox ↔ Shiprocket sandbox integration on the Zoho side.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** HU explicitly confirmed this integration as completed/known. Preserve that as HU-reported sandbox completion; do not repeat setup as though it were unstarted. Independent provider-console verification was not available to the assessment, and production evidence is not claimed. The EffyKlean application's inbound status sync and real-adapter lifecycle remain Phase 2 gaps.

**C-06 — Transactional outbox and bounded retry infrastructure.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** outbox/worker command, idempotency/correlation and three-total-attempt patterns exist with tests. Remaining scheduler deployment and non-retryable-error correction are P6-04 and P2-07, not a reason to rebuild the existing outbox.

**C-07 — Core Admin, audit, MFA and role-authorized capability foundations.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** Admin orders/products/customers/revisions/content/collections/coupons/staff/reports/system areas, MFA, audit events and role checks exist in the assessed code. Specific capability gaps, unresolved RBAC defaults, security issues and the 25 partial activity rows remain open elsewhere in this plan.

**C-08 — Distributor/Bulk application, negotiated pricing and quotation flows.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** application/review, Director-approved business pricing, Bulk enquiry/quote/acceptance and customer-role workflows exist with test coverage read by the assessor. GST display/arithmetic, business-account identity verification, bank/UPI and assisted orders remain separate gaps.

**C-09 — Catalogue revision/publishing framework and SEO baseline.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** revision workflow, publication gates, canonical/OG/JSON-LD/sitemap/robots and product availability vocabulary exist. Product-data verification, Zoho item mapping, five dilution-text conflicts, unpublished SEO/blog drafts and content approval remain open.

**C-10 — Signed-in customer saved-shipping implementation and retention logic.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** saved address model/code, optional feature flag, customer removal, retention/purge logic and tests were recorded in the 16-Oct history; migration 0005 was applied to the local `effyklean` database by HU-authorized work at that time. The assessment could not access the database or rerun tests. Confirm the current private-repository migration state before any later migration task; do not rebuild this feature. Provider-reported delivery is still needed to renew retention correctly.

**C-11 — Core storefront policy pages and contact-information content scaffolding.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** policy-page code/content scaffolding and canonical contact-detail tests exist. This is implementation completion of the scaffolding only; approved privacy/terms/retention, replacement wording correction, publication prerequisites and HU content sign-off remain incomplete under Phase 4/7.

**C-12 — Scheduler definitions, backup/restore documentation and media-storage adapter.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** scheduler definitions/advisory-lock logic, a backup/restore procedure with a reported local drill, and S3-compatible media adapter/migration tooling exist. Hosted scheduling, managed-database backup/restore, approved RPO/RTO, Spaces provisioning and checksum-verified migration remain incomplete under Phase 6.

**C-13 — Public/private decision, instruction and status-history records.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** Delta plan, status register, 122-capability master, SSD audit requirement, hosting instructions and gap assessment exist. Their existence is complete; the assessment identified stale/conflicting content, and this new plan is a reconciliation layer—not proof that every local/public copy is synchronized.

**C-14 — No-COD / prepaid rule and core price/order safeguards.**  
**Status: IMPLEMENTATION COMPLETED.**  
**DoD/evidence:** the current code and tests enforce prepaid payment gating, no COD, price snapshots/idempotency and historical order pricing. Do not implement COD as a “gap”; the exclusion is recorded in Section 6. The GST conflict and the cancellation decision conflict are not covered by this completion label.

---

## 5. Priority and task status plan

Priority order follows dependencies, not a promise of calendar dates. “Decision first” tasks are not coding authorizations. The task IDs retain the assessment's identifiers so each gap can be traced.

### Phase 0 — Governance, reproducible baseline and evidence integrity

**P0-01 — Review and reconcile the private working tree; commit/push only with approval.**  
**Status: INCOMPLETE — DEFERRED.** The assessment reports 113 changed paths, three commits ahead, and migrations 0025–0027 untracked. This task is not permission to change them.  
**DoD:** produce a complete explicit-path manifest grouping every changed/untracked path; inspect diffs and pair migrations with their models; exclude ignored test-password scripts and private logs; HU approves each group; only then commit/push approved paths. Verify `git status`, commit contents, migration pairing, trailer-free messages and CI on the exact resulting SHA. Stop before any unauthorized mutation.

**P0-02 — Resolve the eight historical co-author trailers.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU+DI record either a documented exception or explicit approval for history rewrite. If rewrite is approved, use a separate clone, retain a recoverable backup, prove each old/new tree hash matches, verify no trailers remain and force-push only after separate explicit approval. No rewrite is implied.

**P0-03 — Reconcile current-state records and public mirror.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** The records exist, but the assessment found stacked contradictory state paragraphs and stale public copies.  
**DoD:** after an authorized fresh baseline, publish one dated current-state block in PROJECT_LOG.md, CLAUDE.md, README and status register; retain history under clearly marked superseded entries; correct the CI history (12 runs, 7 success/5 failure at the assessment snapshot; none on its assessed current tree); reconcile local/public copies and record source SHAs. No unsupported claim that the public mirror is the private application repository.

**P0-04 — Fix acceptance-criterion evidence integrity.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** An AC index exists; AC-9.9 has a spurious parser-fixture credit, 20 ACs have structural-only evidence, and widened guard lists need historical review.  
**DoD:** AC-9.9 has a real behaviour test for no combos, no COD and full advance payment; each structural-only AC is labelled honestly; index regeneration and `--check` pass; guard allow-list/query-budget diffs are justified or reverted; no test weakening is hidden.

**P0-05 — Independent database-backed baseline validation.**  
**Status: INCOMPLETE — NOT STARTED.** The assessment collected 2,491 tests but did not run them; Docker/PostgreSQL was unavailable to the assessor.  
**DoD:** on an approved clean environment with PostgreSQL 17, record exact command, SHA, exit code, pass/fail/skip counts and duration for full suite, migration drift, Django checks and `check --deploy`; reconcile differences with the historical 2,491-pass report. Do not create or mutate a shared database without approval.

**P0-06 — Make tests independent of ignored workstation files.**  
**Status: INCOMPLETE — NOT STARTED.** The assessment found a structural test reading ignored `media/catalogue_source/source.json`; media is untracked.  
**DoD:** a clean clone of the approved tree runs the affected tests successfully; the AC-29.3 check remains non-vacuous; no test depends on ignored media or a workstation-only file; add a guard or tracked fixture only after HU approves the fixture; CI passes on that exact SHA.

### Phase 1 — Decisions and controlled specification changes (decision papers only)

**P1-01 — Decide the Zoho-managed shipment/delivery model and state semantics.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU+DI choose how EffyKlean learns handover, tracking, delivery and unsuccessful delivery; define Shipment sub-states, cancellation cutoff, same-day/staff-hold interaction, stale-status handling and customer-safe labels; cite actual Zoho package/status fields using an authorized read-only sandbox sample; approve the necessary architecture/spec CR before implementation.

**P1-02 — Decide GST arithmetic, display and authority.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** a written decision includes worked examples (including ₹100 and ₹10 discount), taxable amount, CGST/SGST/IGST, payable total, B2C/business display and the respective EffyKlean/Zoho responsibilities; reconcile SPEC §7.9/7.10/9.18/10.17/13.14 and obtain accountant sign-off where required. STOP → REPORT → HU+DI DECIDE.

**P1-03 — Reconcile acceptance criteria that conflict with agreed provider/business rules.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU+DI decide the exact changes for AC-12.7/12.8/15.1 (Zoho Payments settlement), AC-16.5 (manual versus API refund), AC-13.8 (invoice number/status), AC-13.6 (local HSN fields), and AC-23.1 (copy-as-is content); only after approval prepare controlled CRs, update SPEC/index and preserve traceability. No code in this decision task.

**P1-04 — Decide bank/UPI verification, assisted orders, combo rules and coupon precedence.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** explicitly choose BUILD or SPEC-defer for bank-transfer/UPI and assisted orders; decide the combo qualification/consumption model and fixed bundles; state combo-versus-coupon precedence. Any BUILD decision defines states, actors, audit events, fields and the exact point an order can be created/synced to Zoho.

**P1-05 — Resolve the small decision bundle.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** record decisions on Director-only versus Admin deletion (does current Director-only delete satisfy item 18?), related-product links, Admin URL, RBAC matrix, enquiry form call hours/window/band wording/address data source/contact phone and spelling, T41 scheduled publication, T38 slug handling, analytics/Search Console timing, CSP enforcement, distributor monthly-budget qualification, nearest-warehouse selection, paid-but-unconfirmed order fulfil/refund rule, and chargeback/dispute/post-placement-change process. Each decision cites its source and owner; no agent-invented business defaults.

**P1-06 — Resolve the NO-versus-SPEC/build conflict and order-edit/authentication rules.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU+DI decision paper quotes both sides for ORD-064, ORD-019 and ORD-076, lists options and consequences, then records the decision before changing code/spec. Also decide whether editable fields are limited to DC-08 (name/address/phone versus e-mail/GST) and how a guest proves authority to cancel. No silent override.

**P1-07 — Decide production Zoho writes, customer mapping and item mapping.**  
**Status: INCOMPLETE — DEFERRED.** Sandbox sync code and test-org work exist; production policy remains unsanctioned.  
**DoD:** approved rule for explicit write enablement and organization allow-list; match/create/shared-contact policy for new customers including GST-registered buyers; confirm Zoho owns item master; define safe production item-ID mapping that replaces SKU-code placeholders without using a sandbox-only command; document price discrepancies for sandbox items and failure behaviour. Use fake transport for policy tests before any approved sandbox test.

**P1-08 — Decide catalogue availability/cache/reconciliation model.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** define freshness and API budget against the actual Zoho plan; approve cache duration for list/detail, live stock checks at cart/checkout, reconciliation interval and outage behaviour; never invent stock; specify and test the request budget under concurrent traffic.

**P1-09 — Decide MRP verification and publication gate.**  
**Status: INCOMPLETE — DEFERRED.** Fifteen product MRPs were reported imported from Shopify compare-at prices using an assume flag.  
**DoD:** HU supplies or approves each MRP with source/date/approver; decide provisional marking and publication blocking; test that unverified MRP cannot silently appear as verified or drive misleading savings.

**P1-10 — Decide customer identity verification and password recovery.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** specify e-mail verification before business-role grants/order linking; treatment of pre-existing unverified accounts; single-use hashed password-reset token, expiry, throttle, generic unknown-account response and session invalidation. Depends on the approved e-mail channel; decision first, implementation later.

### Phase 2 — Shipment and delivery lifecycle

**P2-01 — Retire the incorrect direct shipment-creation path for Zoho-managed fulfilment.**  
**Status: INCOMPLETE — DEFERRED.** The real adapter's fulfilment method raises; HU says the Zoho Inventory sandbox is integrated with Shiprocket sandbox, but this does not supply the missing EffyKlean lifecycle.  
**DoD:** after P1-01 approval, each dispatch/retry/outbox/Admin trigger is tested with fake real-adapter transport: it does not attempt a second shipment writer, create a false local shipment, or mark the order failed merely because shipment creation is Zoho-owned; stub journey remains explicitly local-only; NO PAYMENT → NO DISPATCH tests remain intact.

**P2-02 — Implement approved Shipment fields and append-only event model.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** approved migration adds only the decided fields/substates/event history; migration applies and reverses on empty/populated test databases; unique provider-event identity prevents duplicates; tests cover duplicate/out-of-order events and migration drift.

**P2-03 — Implement inbound Zoho shipment/delivery status synchronization.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** scheduled read-only sync applies Zoho package/status data through one idempotent writer; tests cover created, in-transit, out-for-delivery, delivered, unsuccessful, duplicate/out-of-order, 429/5xx/timeouts; only provider-reported delivery sets delivered_at; stale statuses create an Admin exception; three total attempts and correlation IDs are evidenced; no secrets or customer addresses in logs.

**P2-04 — Use real handover/delivery signals for cancellation, replacement, returned-package and saved-address rules.**  
**Status: INCOMPLETE — DEFERRED.** Depends on the P1-01 decision and P2-02/03; customer cancellation itself also depends on P1-06.  
**DoD:** tests prove pre/post-handover cancellation rule for the approved customer roles, 24h/24h+1s/72h/72h+1s replacement boundaries, return eligibility only for handed-over undelivered parcels, and saved-address renewal only on a reported delivery. No behaviour depends on a stub flag.

**P2-05 — Align lifecycle tests and Admin/customer tracking pages.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** every stub-only lifecycle assertion has a real-adapter-faithful counterpart; Admin shows Zoho source, last sync and actionable errors; customer labels never overstate carrier confirmation; the existing E2E prototype/local acceptance intent remains covered.

**P2-06 — Build approved Admin fulfilment/tracking/local-pickup recording.**  
**Status: INCOMPLETE — DEFERRED.** HU's recorded ORD-080/081 YES conflicts with the older plan NO labels; resolve states under P1-01 before coding.  
**DoD:** paid order only; Admin action records carrier/tracking or pickup reason; delivered-by-Admin is labelled as reported, not carrier-confirmed; audit event records actor and details; idempotent; fake provider calls prove no shipment creation; unpaid/failed-payment path is rejected.

**P2-07 — Stop retrying non-retryable Zoho errors.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** validation/mapping/auth/not-supported errors terminate at first attempt with safe reason; transient failures receive at most three total attempts; targeted tests prove one-call versus three-call paths and Admin reconciliation displays the reason.

### Phase 3 — Money, tax and commercial completeness

**P3-01 — Implement the approved GST arithmetic and display rule.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Local tax code and tests exist, but the assessment found conflict with frozen SPEC.  
**DoD:** after P1-02, table-driven tests cover Karnataka/interstate, discounted/undiscounted, B2C/Distributor/Bulk, rounding and Zoho totals; tax-unavailable path never guesses; business-price display fails visibly rather than silently falling back; sandbox read-only comparison is attached.

**P3-02 — Retrieve and display Zoho Payments settlement/charges data.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** after P1-03 and scope check, read-only API data (where provided) is stored and displayed without locally inventing fees; absent/unavailable values are explicitly labelled; tests cover present/absent/error; sandbox evidence is distinct from production evidence.

**P3-03 — Display Zoho invoice number/status in Admin, if HU retains AC-13.8.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** after decision and approved read scope, Admin displays invoice number/status or “not yet invoiced”, plus a safe provider-error state; no invoice creation logic is added to EffyKlean; fake-response tests cover each state.

**P3-04 — Bank-transfer/UPI payment verification and assisted orders, if approved.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** implement only if P1-04 chooses BUILD; unverified payments cannot fulfil; reference deduplication, Admin verification, audit events and shared pricing/GST rules are tested; assisted-order overrides are explicit and Director-governed.

**P3-05 — Rule-based combos and fixed bundles, if approved.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** only if P1-04 chooses BUILD; qualifying quantities are consumed once, rules use the approved order, fixed bundles have explicit components, discounts do not go below zero, and SPEC examples including remove/re-add behaviour pass.

**P3-06 — Reconcile refund recording versus execution.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Refund amount/state can be recorded, but execution is manual and customer-facing wording may imply automatic payment.  
**DoD:** after P1-03 choose either a manual workflow with Admin checklist, cancelled-but-unrefunded report and honest customer wording, or an explicitly authorized idempotent provider refund path with audit/failure handling and sandbox proof. Duplicate-payment refunds are included in reconciliation. No real refund without specific approval.

**P3-07 — Sanctioned production Zoho writes and first-time customer mapping.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Adapter/sync infrastructure and sandbox activity exist; production write policy and customer/item mapping are unresolved.  
**DoD:** fake-transport tests prove explicit flag + organization allow-list, no writes without permission, one contact/Sales Order per reference, first-time customer succeeds, GST buyers are not collapsed into a shared contact, and errors remain visible. Only after explicit authorization, observe the approved behaviour in sandbox; never test live writes under this task.

### Phase 4 — Customer communications, privacy and legal

**P4-01 — Approve notification ownership and message matrix.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU approves a matrix for customer/staff messages (confirmation, payment issue, shipping/delivery, cancellation/refund, replacement, quotes, roles, Subscribe and GST invoice delivery), naming owner/system/channel/trigger/failure behaviour and exact wording. Website e-mail direction uses GoDaddy Support@EffyKlean.com as previously stated; do not invent credentials or legal wording.

**P4-02 — Implement asynchronous transactional e-mail for website-owned messages.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** SMTP configuration/check helper exists, but no complete transactional sender is implemented.  
**DoD:** approved messages enter the outbox transactionally, send asynchronously, retry no more than three total attempts, and are audited; failures never alter payment/order state; real backend and HTTPS public base URL are required by production settings; only after HU approves, send one test message to an approved test address and record delivery/authentication evidence. Keep marketing separate.

**P4-03 — Privacy, terms, cookie/analytics consent and retention.**  
**Status: INCOMPLETE — DEFERRED.** No approved legal text/retention decision is available.  
**DoD:** publish only HU-approved text; implement consent only where applicable analytics is actually present; decide and implement retention/deletion for contact messages, enquiries, subscribers and saved shipping; scheduled purge is tested; production contact-form gate can be satisfied. No legal text written by an agent.

**P4-04 — Align replacement/policy wording and production page prerequisites.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Policy pages exist, but assessment found wording conflicting with CR-008 and possible unpublished policy slugs.  
**DoD:** replacement page, FAQ and form consistently require video evidence (photos may support) and describe both website and Customer Care routes; tests fail on old wording; all footer policy links resolve on staging or remain hidden until published; deployment checklist includes policy/video loading; privacy contradictions are presented to HU/counsel, not silently edited.

### Phase 5 — Security and configuration

**P5-01 — Throttle guest tracking/cancellation and use shared customer throttling.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** limits documented per order reference/source; shared database/cache counters persist across workers/restarts; N+1 failure has a generic response, valid requests under limit succeed, and tests cover windows and proxy headers; no order-existence oracle is introduced.

**P5-02 — Tighten production settings guards.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Production settings already fail closed for several unsafe configurations, but gaps remain.  
**DoD:** production refuses payment sandbox flags; requires HTTPS PUBLIC_BASE_URL, real From address and required CSRF trusted origins; each invalid setting has a test; approved staging exceptions remain isolated in a separate settings module.

**P5-03 — Add CI deployment/dependency/security checks.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** CI exists and historically ran; it has not run on the assessment's current private tree and lacks several scans.  
**DoD:** CI runs `check --deploy`, dependency audit against lockfile and approved security lint rules; warnings are explicitly triaged; stale `noqa` references are reconciled; no test is weakened; a green run is linked to the exact approved commit.

**P5-04 — Security/hygiene review.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Existing MFA, CSRF/origin and header protections exist; further findings remain.  
**DoD:** document CSRF/origin, CSP, Admin path and proxy decisions; every broad exception has a reason or narrower handling; Razorpay residue is labelled historical; ignored seed-password script is excluded from build context and checked; findings have explicit disposition and owner.

**P5-05 — Verify customer identity and implement password reset.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** unverified e-mail cannot receive business pricing; provisioning re-verifies/refuses unverified accounts; hashed single-use reset token expires, is throttled, gives generic unknown-account response and invalidates sessions; Admin wording is corrected; e-mail tests use the approved backend.

**P5-06 — Trusted client IP and public form abuse controls.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Contact/subscribe controls exist, but Bulk/Distributor forms and proxy-aware client IP remain gaps.  
**DoD:** one trusted-proxy-aware helper ignores forged forwarded headers by default; use it for sign-in, contact and audit; throttle Bulk/Distributor applications per-source and globally; alert staff about new enquiries; tests cover caps and spoofing.

**P5-07 — Database TLS and connection policy.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** DB_SSLMODE is configurable; production rejects `prefer` and `disable`; CONN_MAX_AGE is decided against connection limits; advisory-lock jobs use a supported direct connection; on staging, observe TLS via `pg_stat_ssl` and record evidence.

**P5-08 — Keep single-use tokens out of URL logs and Referer headers.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** mask/drop query strings in access logs for setup/subscribe links or move tokens to a safe POST/fragment design; set and test `Referrer-Policy: no-referrer`; prove the approved link still works end to end without exposing the token.

### Phase 6 — Hosting and operations

**P6-01 — Create separate staging settings and restricted access gate.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** staging module requires sandbox flags, allows TESTCODE, forces noindex and non-delivering e-mail, is visibly distinct from production, and restricts every route (including health endpoint as designed) to approved people; production guards remain unchanged and tested.

**P6-02 — Provision DigitalOcean App Platform and Managed PostgreSQL (staging first).**  
**Status: INCOMPLETE — DEFERRED.** Hosting remains parked pending decision and spend authorization.  
**DoD:** after explicit approval, repository app spec contains no secrets; pre-deploy migration succeeds on clean DB; dedicated DB role and TLS used; health checks, HTTPS/proxy headers, egress/IP allow-lists and webhook reachability are observed; Tuesday Customer Care closure is reconciled with the 24-hour replacement window; resources and cost are recorded.

**P6-03 — Provision Spaces and verify media migration.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** S3-compatible storage code exists; no verified Spaces migration is established.  
**DoD:** after paid provisioning approval, bucket credentials exist only as platform secrets; every object copies with checksum verification, every DB media reference resolves, dry-run reports zero unresolved items, staging serves images/videos; do not delete local source files without separate approval.

**P6-04 — Run the scheduler/worker on a host.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Scheduler definitions/advisory-lock logic exist; no host is running the required jobs.  
**DoD:** chosen worker/cron design meets the required intervals (outbox, payment reconciliation, business-role suspension, archive/purge and shipment sync); concurrent-run guard is observed; a due task is processed on staging; failures alert; database connection mode is compatible with advisory locks.

**P6-05 — Monitoring, alerting, backups, RPO/RTO and restore drill.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Local backup/restore procedure and local drill were reported; managed database backup/restore and approved RPO/RTO are not established.  
**DoD:** HU approves availability, RPO, RTO and retention targets (99.5% is not approved by default); health/error/queue-age alerts reach a named recipient; managed DB backups are verified in provider console; restore to scratch DB succeeds with row-count reconciliation and measured restore time meets approved RTO.

**P6-06 — Extend TESTCODE coverage and safe cleanup runbook.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** TESTCODE traceability exists for payment attempts/orders, not all created records.  
**DoD:** approved nullable marker covers customers, saved addresses, enquiries, subscriptions and Zoho sync rows; report enumerates marked records; cleanup runbook is marker-only, dependency-aware and tested on a throwaway DB; external sandbox records are reconciled manually. Migration requires approval.

**P6-07 — Implement approved availability caching and reconciliation.**  
**Status: INCOMPLETE — DEFERRED.** Depends on P1-08 and a running scheduler.  
**DoD:** list/detail requests make zero provider calls within the approved cache lifetime; cart/checkout still check live stock; outage behaviour matches the decision; reconciliation reports drift; concurrent-view provider-call count stays within the approved budget.

### Phase 7 — Catalogue, content and product data

**P7-01 — Reconcile the 15-product catalogue with HU-approved data.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Fifteen products were reported in the dev database; five SKUs have conflicting dilution text and product logistics/HSN values remain incomplete.  
**DoD:** HU approves all conflicting dilution wording and the “Tools Required” decision; Admin records actual HSN/weight/dimensions/barcodes for each relevant product; Zoho comparison has no unexplained mismatch; agents do not invent values; confirm source data before any re-import to avoid duplicate products.

**P7-02 — Review and publish SEO and blog drafts.**  
**Status: INCOMPLETE — DEFERRED.** Fifteen SEO drafts and three blog drafts were reported unpublished.  
**DoD:** HU reviews and publishes through the approved revision workflow; different authorized people perform proposal/approval/publishing where required; sitemap and production canonical URLs are verified; agent does not approve/publish its own content.

**P7-03 — Approve storefront policy/content parity.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** HU signs off shipping/cancellation/replacement wording, contact details and FAQ; CR for copy-as-is is resolved; all claims match actual workflow and no unsupported policy is published.

**P7-04 — Verify MRP values and prevent unverified publication.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** each of 15 MRPs has HU-approved source/date; publication/review gate distinguishes verified from assumed values; import path preserves the marker; report identifies any published value differing from approved MRP.

### Phase 8 — Provider acceptance (sandbox evidence only)

**P8-01 — Complete Zoho Payments webhook-first sandbox proof.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** HU reports the Payments sandbox is working, but the assessment says the webhook was not registered and webhook-first end-to-end proof is absent.  
**DoD:** HU registers webhook on stable staging HTTPS URL; a TESTCODE sandbox payment places the order from the webhook while browser return is ignored; replay creates no duplicate; mismatched/failed payment creates no order; evidence includes attempt/event/order IDs and timestamps; settlement data handled per P3-02. No production payment.

**P8-02 — Complete Zoho Inventory scopes, Flow, stock, invoice and mapping evidence.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Sandbox reads and selected authorized test writes are recorded; HU reports Zoho Inventory–Shiprocket sandbox integration completed. Remaining assessment gaps include scope/read-back evidence, Flow/invoice/stock observation, item mapping and production policy.  
**DoD:** verify authorized scopes using the current token without repeating prohibited token-file checks; inspect Flow read-only; observe non-zero stock before/after an authorized sandbox order; read invoice number/status; record real item IDs and price discrepancies; confirm Zoho-side shipment integration with evidence where accessible. Clearly label HU-reported completion versus independently observed evidence. Never delete sandbox records or write without explicit authorization.

**P8-03 — Full two-product sandbox end-to-end acceptance.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Payments and Inventory sandbox components have prior working evidence/HU confirmation, but the assessment does not establish a complete EffyKlean payment→Zoho order→shipment→delivery→replacement journey.  
**DoD:** on approved staging, two-product TESTCODE order passes payment, one Zoho Sales Order, Zoho-managed shipment sync, delivery, and replacement request; separately prove failed payment/no dispatch, webhook replay, Zoho outage preservation, pre/post-handover cancellation per final decision and unsuccessful delivery/no refund entitlement. Each step cites environment, provider, evidence and TESTCODE; cleanup is planned and authorized; status register records observed—not inferred—results.

### Phase 9 — Remaining Shopify-parity inventory

**P9-01 — Reconcile every unresolved row in the 597-activity inventory into a four-disposition register.**  
**Status: INCOMPLETE — DEFERRED.** The assessment reports 597 rows as 259 DONE, 25 PARTIAL, 3 NOT DONE and 310 DEFERRED, including 148 explicit exclusions; 124 rows await naming/decision. The source CSV is now published at `docs/ImplementationPlan/RECONCILED_597_STATUS_2026-10-18.csv`. The [310-row disposition triage draft](../../AgntGapAnalysis/Deferred310_Disposition_Triage_DRAFT_2026-10-22.csv) remains provisional and does not replace the source register or the authoritative decision ledger. It uses the 310 Appendix A.4 rows and preserves their recorded IDs/status text. Provisional triage counts are 51 `EXCLUDE`, 3 `LATER`, 256 `INVESTIGATE / HU+DI DECISION REQUIRED`, and 0 `BUILD`; these are draft classifications, not HU+DI decisions. No row was promoted to `BUILD` from the assessment's combined status wording alone. The 51 exclusions are keyword/source-summary candidates and must be checked against authoritative decisions; the 256 investigate rows include many source statuses that collapse exclusion, lack of authorization and deferral into the same wording. The full source register is now available in `docs/ImplementationPlan/`; the earlier absence was a historical condition at assessment time, and the new 597-row working register should be used for current disposition reconciliation.  
**Required dispositions:** `BUILD` (authoritatively approved for implementation); `EXCLUDE` (explicit authoritative NO / NotToBeIMPLEMENTED-inEffyklean decision); `LATER` (approved/intentional future phase, with dependency/reason); `INVESTIGATE / HU+DI DECISION REQUIRED` (ambiguous, conflicting, blocked, evidence-only, proposal-only, or no authoritative disposition). Identify possible duplicates in a separate `duplicate_of`/evidence field; do not delete or merge records solely on similar wording.  
**DoD:** recover and verify the authoritative 597-row source and decision ledger; reconcile all 597 IDs, not just the 310 deferred subset; retain each source ID, full description, original status, source decision/citation, final disposition, reason, duplicate relationship if evidenced, owner/dependency and evidence; have HU+DI decide unresolved rows; update the row-level register and counts without deleting history; totals reconcile exactly to 597 and four dispositions; no proposal-only row becomes a commitment by inference. Do not treat this provisional triage as approval to implement.

**P9-02 — Implement only the named BUILD subset and close every PARTIAL row.**  
**Status: INCOMPLETE — DEFERRED.** Depends on P9-01 and HU+DI approval.  
**DoD:** each approved row has a requirement trace, task-specific DoD, behaviour tests, migration and audit/security checks as relevant; each of the 25 partial rows is closed by implementation, accepted-as-is with rationale, or explicit exclusion; no code starts for unapproved or ambiguous rows.

**P9-03 — Add a small browser regression suite if approved.**  
**Status: INCOMPLETE — DEFERRED.** Prior browser runs were manual agent reports and are not in CI.  
**DoD:** approved headless-browser suite covers home, product, cart, stub checkout, tracking, public enquiry forms and Admin sign-in; runs in CI on an approved commit; fails on broken navigation/flows and contains no secrets. Approval required for new dependencies.

**P9-04 — Close or explicitly accept minor findings.**  
**Status: INCOMPLETE — PARTIALLY COMPLETE.** Many Admin and storefront capabilities exist, but assessment minor findings m1–m21 and G-65/G-66 remain open or require decision.  
**DoD:** each minor item has a linked test/fix or written HU+DI acceptance; review business-cart limits, Zoho-owned dispatch counts, staff lockout, subscription consent version, exception handling, media proxy/cache, report semantics, password recovery runbook and stale documentation. Nothing is silently dropped.

### Phase 10 — Release readiness and cutover

**P10-01 — Production readiness gate.**  
**Status: INCOMPLETE — NOT STARTED.**  
**DoD:** every Critical/High gap is closed with evidence or formally deferred by an approved CR; HU UAT passes; numeric performance/availability/accessibility targets are approved and measured on staging; keyboard/accessibility and Core Web Vitals evidence recorded; no unsupported DONE claims; full suite/CI green on the release candidate.

**P10-02 — Production configuration and first live payment.**  
**Status: INCOMPLETE — DEFERRED.** Production configuration/live payment are not authorized.  
**DoD:** after separate HU+DI approval, production Zoho organization/item/tax IDs are accountant-verified; credentials are platform secrets; sandbox flags are absent and guards pass; one minimal live payment and its approved refund/reconciliation are observed; every external write is explicitly authorized. This task cannot begin from this plan alone.

**P10-03 — Clear temporary arrangements and execute cutover only when authorized.**  
**Status: INCOMPLETE — DEFERRED.**  
**DoD:** every temporary-arrangement row has evidence of clearance; domain redirect/rollback is agreed; Shopify is retained as Hu directed until transition approval; monitoring and backups work; observation period and rollback owner are recorded; separate HU+DI authorization exists for deployment, credentials, DNS and cutover.

## 6. NotToBeIMPLEMENTED-inEffyklean — explicit exclusions and architectural boundaries

These are exclusions from the EffyKlean build, not gaps to “finish”. If a future source row uses a conflicting label, apply the latest explicit HU decision and report the inconsistency; do not revive an excluded feature from Shopify screenshots or a parity inventory.

- **No cash on delivery, partial payment on delivery, COD collection/settlement/reconciliation, or post-delivery payment.** All orders must be fully paid before fulfilment: NO PAYMENT → NO DISPATCH.
- **No active Razorpay payment integration.** Zoho Payments is the selected provider. Razorpay-named ACs/docs must be reconciled as historical or changed by controlled CR; do not re-enable Razorpay as fallback.
- **No Shopify runtime dependency, Shopify theme/Liquid editor, Shopify Online Store theme administration, or unapproved Shopify app/Flow replication.** EffyKlean owns its Django storefront; Shopify remains the existing site until a separately authorized cutover.
- **No AWS hosting.** Hosting direction is DigitalOcean App Platform + Managed PostgreSQL; Droplets only if justified and approved; GoDaddy remains fallback. No paid provisioning without explicit approval.
- **No Django-owned authoritative inventory ledger, local stock adjustment/reservation as a competing source, or independent stock/location/purchase-order system where Zoho owns that function.** Zoho remains inventory authority; EffyKlean may display a safe projection and read/record approved operational metadata.
- **No separate Household Combo or Bulk Combo collection.** Combo pricing is not the same as separate combo collections. Rule-based combo packs/fixed bundles remain DEFERRED until the explicit model decision; do not mislabel that undecided work as excluded.
- **No loyalty/rewards, gift cards, wishlist/save-for-later, recently viewed, product reviews/ratings, unapproved recommendation/boosting features, international markets/duties/multi-currency, POS, marketplace/sales channels, Shopify theme customization, or AI/Sidekick features** unless a new explicit HU decision adds them.
- **No normal customer return/exchange/store-credit/return-label or general refund workflow under the current no-returns/no-refunds baseline.** This does not erase the existing pre-handover B2C cancellation rule or its refund amount: the cancellation/refund conflict and whether provider execution is manual/API must be resolved by P1-03/P1-06 before changing behaviour.
- **No mandatory SMS channel.** Prefer approved e-mail/WhatsApp workflows; WhatsApp is optional and its ownership/message behaviour must be decided. Do not collect SMS marketing consent by substitution.
- **No automatic customer-facing publication of unverified MRP/product data, no fabricated product values, and no agent-invented legal or policy text.**
- **No feature based on the unobserved MA-ORD-145 fulfilment-card menu.** It remains evidence-only; never invent menu actions.
- **No automated or manual feature solely because an inventory row says “authorized? NO – proposal only”.** It is not BUILD until HU+DI explicitly names it.

The 597-row inventory contains many more explicit exclusions. For each row, retain its exact ID, source decision and disposition in the row-level register. The list above is a guardrail summary, not permission to overwrite the source IDs or treat every deferred row as NO.

## 7. Not to be mistaken for completed work

- **Zoho Payments sandbox working** = HU-reported sandbox readiness; it does not prove a webhook registered, webhook-first order placement, settlement retrieval or production.
- **Zoho Inventory sandbox integrated with Shiprocket sandbox** = HU-reported sandbox integration; it does not prove the EffyKlean application can create/track production shipments or receive delivery status.
- **Zoho Inventory sandbox reads/test writes** = completed only for the operations recorded in the existing evidence; do not generalize them to production.
- **2,491 tests collected** is not a test pass. Historical full-suite pass counts are reports from earlier runs; the assessment itself did not execute the suite.
- **CI exists / historically ran** is not CI validation of the assessment's current private working tree.
- **Scheduler definitions exist** is not a deployed scheduler.
- **S3-compatible media code exists** is not a provisioned Spaces bucket or a checksum-verified migration.
- **Production settings fail closed in several cases** is not a staging environment, production deployment or full security sign-off.
- **A task's implementation completed** is not automatically HU acceptance of the batch or permission to commit/push/deploy.

## 8. Current gate order

1. HU+DI decide the blocking conflicts in P1-01, P1-02 and P1-06 first; do not implement around them.
2. Reconcile the current private tree and establish an approved reproducible baseline (P0), without losing Hu's uncommitted work.
3. Decide production Zoho write/customer/item mapping and stock/cache policy (P1-07/08); then implement the EffyKlean shipment lifecycle (P2) and commercial work (P3) only in the scope approved.
4. Approve communications/legal text before enabling customer-facing sends/forms (P4); complete security and identity controls (P5).
5. Provision staging only after explicit spend/access approval (P6); complete HU-supplied catalogue/content data (P7); run approved sandbox acceptance (P8).
6. Triage the remaining 597 rows (P9); only after all critical launch gaps, approved decisions, evidence and UAT are complete may HU+DI consider release (P10).

## 9. Known assessment limitations and handoff

The source assessment's local application snapshot is dated 22 October and cannot be assumed to equal a fresh private-repository state. Its static checks were Ruff check/format and Django check; it collected 2,491 tests but did not run them, migration checks, browser tests, penetration tests, provider consoles, database reads or DigitalOcean checks. Several prior test/provider results are class-3 agent reports. The status register public mirror lags later records. This plan therefore records implementation status at the strongest supportable level and deliberately leaves external/runtime verification incomplete where evidence is absent.

**Next authorized action:** HU+DI review the decision-first tasks; no implementation agent should start a task merely because it appears here. For each task, HU authorizes one bounded work package, the agent completes and verifies it, updates authorized project records, reports evidence and stops for the next HU decision.


Latest disposition reconciliation: MF-089 is BUILD after HU approved the proposed operational privacy/retention baseline; implement the approved notice and controls and do not claim legal sufficiency without review. MF-093 remains LATER with optional tracking consent-gated. MF-105 remains BUILD and must be decomposed into customer sign-in assistance and customer data-request export while preserving the source ID. These dispositions do not authorize implementation.

## Row-level DoD quality verification — 22 October 2026

Post-update verification of the companion working register confirms 597 rows and 597 unique IDs, with no blank DoD or evidence-method cells. After this decision reconciliation, 22-Oct baseline dispositions were 256 Implemented, 245 BUILD, 10 LATER, 10 INVESTIGATE and 76 EXCLUDE. Of the original 243 BUILD rows, 183 previously used one of three generic templates; each was rewritten with row-specific acceptance outcomes and evidence checks, and the remaining 60 already had bespoke DoDs. MF-089, MF-093 and MF-105 now have decision-aligned row-specific DoDs/evidence methods. The 18-Oct historical source CSV remains unchanged. These are planning/acceptance criteria only—not proof of implementation or test completion, nor authorization to implement or deploy.


## BUILD-245 ledger correction — 23 October 2026

The per-item source [BUILD245_LEDGER_2026-10-22.csv](./BUILD245_LEDGER_2026-10-22.csv) has been verified: 245 unique IDs, comprising 83 `DONE (verified)`, 62 `PARTIAL`, 100 `DEFERRED`, and 0 `NOT DONE`. Total: 245. This supersedes any note claiming the ledger was absent or reporting 64 PARTIAL / 247 total. Use the row-level status, evidence, limitations and next-action fields for each BUILD item. The 22-Oct disposition total (340 Implemented + 160 BUILD + 10 LATER + 9 INVESTIGATE + 78 EXCLUDE) is historical and superseded by the 23-Oct row-level correction below; do not conflate disposition with implementation status.

## Superseding disposition reconciliation — 23-Oct-2026

The 22-Oct aggregate in §2.4 and the implementation summary is historical and must not be treated as the latest verified row-level result. A 23-Oct source-to-record reconciliation corrected MA-GFT-001, MA-GFT-002 and MA-SET-032 from stale BUILD to EXCLUDE, retaining implementation status DEFERRED; the earlier MA-ORD-103/105 corrections remain. The current 245-row slice now has **83 Implemented, 157 BUILD and 5 EXCLUDE** dispositions, while implementation status remains **83 DONE (verified), 62 PARTIAL and 100 DEFERRED**.

Across the 597 IDs, row-level classifications currently verify 511: 340 Implemented, 157 BUILD, 5 EXCLUDE and 9 INVESTIGATE. **86 remain UNRECONCILED — DO NOT GUESS.** Aggregate arithmetic implies 10 LATER and 76 EXCLUDE among those 86, giving 340 Implemented + 157 BUILD + 10 LATER + 9 INVESTIGATE + 81 EXCLUDE = 597, but this is not a reconstructed 597-row register: the working CSV still fetches as zero bytes, and the 86 individual IDs are not mapped to authoritative row-level evidence. Do not infer or assign their dispositions from aggregate counts. Continue source-by-source reconciliation before asking Hu any remaining genuine decision. No coding agent was delegated.

## Latest superseding disposition reconciliation — 23-Oct-2026

The current 245-row disposition counts are **83 Implemented, 143 BUILD, 13 LATER and 6 EXCLUDE**. The separate implementation-status counts remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. The current reconciliation has changed the disposition, reason category or next action on 95 unique rows of the 245-row ledger. See `BUILD245_HUDI_DECISIONS_RECONCILIATION_2026-10-23.md`, `HU_RESPONSES_RECOVERED_REGISTER_2026-10-23.md`, and `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv`.

Across the 597 IDs, row-level classifications currently verify 511: 340 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE and 9 INVESTIGATE. **86 remain UNRECONCILED — DO NOT GUESS.** Aggregate arithmetic implies 10 additional LATER and 76 additional EXCLUDE among those 86, giving 340 Implemented + 143 BUILD + 23 LATER + 9 INVESTIGATE + 82 EXCLUDE = 597, but this is not a reconstructed 597-row register: the working CSV still fetches as zero bytes, and the 86 individual IDs are not mapped to authoritative row-level evidence. Do not infer or assign their dispositions from aggregate counts. Continue source-by-source reconciliation before asking Hu any remaining genuine decision. No coding agent was delegated.

## Latest correction — 23-Oct-2026: 597-row working register re-fetched and synchronized

This update supersedes earlier statements in this document that the 597-row working-disposition CSV was zero-byte. The current GitHub fetch returns **597 rows and 597 unique IDs**. In this pass, all 245 IDs in the current BUILD ledger were synchronized to the corrected 245-row ledger and response crosswalk; a direct ID join found **zero disposition mismatches** between those three records. The 597-row working register now reflects the corrected dispositions and later HU refinements.

Current 597-row register counts: **340 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE, 9 INVESTIGATE and 86 UNRECONCILED — DO NOT GUESS** (597 total). Thus 511 rows have a row-level classification; the 86 unreconciled rows remain unassigned. Aggregate arithmetic implies 10 further LATER and 76 further EXCLUDE among those 86, but those individual IDs are not mapped to authoritative evidence. Do not assign them from the aggregate.

Current 245-row ledger dispositions: **83 Implemented, 143 BUILD, 13 LATER and 6 EXCLUDE**. Its implementation-status counts remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. The 597-ID response crosswalk has 597 unique IDs; the decision overlay has 151 rows; the correction overlay has 19 unique row-specific corrections. Original HU answers remain historical evidence, and later specific refinements control current disposition. No coding agent was delegated and no implementation/deployment/provider action was performed by this reconciliation.
