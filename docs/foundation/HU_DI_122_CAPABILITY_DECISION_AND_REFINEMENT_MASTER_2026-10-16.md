# HU+DI Canonical Record — Original 122 Capability Decisions and Approved Refinements

**Record date:** 2026-10-16; canonical consolidation amended to preserve source records  
**Authority:** HU's original YES/NO decisions from the joint HU+DI capability review  
**Purpose:** Preserve the 122 capability decisions, the business-intent explanations and conflict analysis, and the published row-level comparison in one durable record.

## Governing authority — mandatory

HU has explicitly confirmed that all 122 capabilities were worked through jointly with Di and that the original YES/NO answers are HU's decisions. Treat those answers as authoritative. They must not be overridden, downgraded, reopened, or questioned merely because a later file has incomplete citations or a reconstructed ledger does not reproduce every discussion verbatim.

- The original HU YES/NO answer remains the historical decision for each capability.
- The recorded business intent and explanations in the source ledger and reconciliation analysis must be preserved alongside the row-level map.
- Later explicit HU+DI-approved refinements must be recorded as subsequent refinements. They do not silently replace or erase the original answer.
- If an implementation plan, agent recommendation, code, test, provider configuration, or frozen specification appears inconsistent with a recorded answer, STOP → REPORT → HU+DI DECIDE. No agent or document may independently change the answer.
- A missing citation, truncated description, or mismatch in a generated map is a record-reconstruction defect, not evidence that HU did not decide or that the decision lacks authority.
- YES indicates desired capability/scope, not automatic implementation authorization. NO excludes the capability unless HU explicitly changes that decision later. Implementation and provider readiness remain separate questions.
- Do not invent missing wording or answers. Where sources differ, preserve the original records and expose the discrepancy for source reconciliation without asking HU to repeat the decision.

## How this master is assembled

This file consolidates (1) the existing 122-row master/map, (2) the original capability decision ledger dated 2026-10-12, (3) the business-intent-first conflict reconciliation dated 2026-10-12, and (4) the published ROW122 decision/evidence map dated 2026-10-16. The three source documents are reproduced in full in the appendices below so their explanations, qualifications, IDs, and historical wording remain available together.

The row map is a comparison/index view; its generic source labels, truncated descriptions, and implementation references must not be used to override the source decision ledger or conflict-analysis record. The source records below are retained as evidence. This is a consolidated decision record, not a claim that the underlying chat transcript has been reproduced word-for-word.

## Source integrity at consolidation

- Original decision ledger: `ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md` — source blob `ada612a7c469d7e407c546ad03df03572b85ad26`
- Business-intent-first conflict reconciliation: `CONFLICT_RECONCILIATION_ANALYSIS_2026-10-12.md` — source blob `cc70bd3cb2f78c104af2bd57fa82d0574efbf7fd`
- ROW122 decision/evidence map: `docs/foundation/ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md` — source blob `a26c967e8c91a8c1887d989a5c434c8b21aeafc3`
- Previously published master: `docs/foundation/HU_DI_122_CAPABILITY_DECISION_AND_REFINEMENT_MASTER_2026-10-16.md` — source blob `5121091935fb3c3ae30d8ff9798b8e42357aa514`

The three source documents below are included verbatim as fetched for this consolidation. Keep them unchanged as historical source appendices; corrections to the canonical interpretation belong in a separately dated amendment/refinement section, not by rewriting historical source text.

## Canonical row-level working register and refinement notes

## 1. Read this before using the record

This document is a durable working baseline created from the public analysis repository's current decision/evidence map and the linked HU+DI records. It is **not** proof that every original answer has been recovered.

The current map contains 122 unique Plan 2.3 capability IDs and working dispositions. Its own header states that only PRD-005 and PRD-042 have original answers explicitly recovered in the plan; other dispositions are working reconciliation. Therefore:

- Treat the YES/NO values in the imported map below as **current working dispositions**, not automatically as source-verified historical answers.
- Do not infer an original answer from a later refinement, code reference, test, or implementation plan.
- Keep the original answer and later refinement in separate fields.
- Where a source is missing, mark it `NOT RECOVERED`; do not guess.
- A code/test reference indicates a possible implementation/evidence link, not acceptance or completion.
- This document does not authorize implementation, staging, committing, pushing to the private project repository, deployment, DNS changes, production credentials/writes, or provider cutover.
- Any conflict with frozen specifications, architecture, ADRs, privacy/security requirements, or previously approved business rules must STOP → REPORT → HU+DI DECIDE.

## 2. Source records used

1. [ROW122 Decision/Evidence Map — 16 Oct 2026](ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md) — source for the imported 122-row working map below.
2. [Admin Capability Decision Ledger — 12 Oct 2026](../../ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md) — decision-question protocol and decisions recovered from the earlier discussion.
3. [Conflict Reconciliation Analysis — 12 Oct 2026](../../CONFLICT_RECONCILIATION_ANALYSIS_2026-10-12.md) — business-intent analysis and proposed reconciliations; distinguish analysis/recommendation from an HU-approved decision.
4. [HU+DI Decisions and Resume Checkpoint — 13 Oct 2026](../../HU_DI_DECISIONS_AND_RESUME_CHECKPOINT_2026-10-13.md) — continuity and later direction.
5. [Delta Implementation Plan reference copy](../../AgentImplementationRecords/EffyKlean_Delta_Implementation_Plan_13Oct2026.md) and [Status Register](../../AgentImplementationRecords/EffyKlean_Delta_Implementation_Status_Register.md) — implementation-plan working dispositions and status, not substitutes for original HU answers.

The private implementation repository was not independently byte-compared when this record was created. The coding agent must verify private-repository source documents and local working tree before storing the corresponding private/local copy.

## 3. Required reconciliation schema for every capability

For each of the 122 IDs, the final verified register must preserve:

- **Capability ID**
- **Full original capability description** (recover truncated labels from the original plan/source)
- **Original HU answer:** YES / NO / EVIDENCE ONLY / NOT RECOVERED
- **Original answer evidence:** exact conversation/date/source path or line/section; quote only the minimal necessary text
- **Suggestion(s) made at decision time:** preserve the alternative(s), if any
- **Di's later analysis/recommendation:** identify as Di's view, not Hu's answer
- **Conflict/ambiguity:** what clashed and with which source/rule
- **Later HU+DI-agreed refinement:** exact outcome and source/date; never overwrite original answer
- **Business rule / architectural constraint**
- **Agent's current disposition and evidence:** code/test/document references, clearly separated from business approval
- **Reconciliation status:** `SOURCE-VERIFIED`, `PARTIAL EVIDENCE`, `NOT RECOVERED`, `HU+DI DECISION NEEDED`, or `VERIFIED NO CONFLICT`
- **Open action / owner**

A row is `SOURCE-VERIFIED` only when the original answer is supported by its source and the later refinement trail is accurately represented. Do not mark the entire record complete merely because all 122 IDs exist.

## 4. Current reconciliation findings

- The existing map contains **122 unique IDs** and its working dispositions were matched against Delta Plan §2.3.
- Its summary reports 104 YES, 17 NO, and 1 EVIDENCE ONLY; this is the map's current working disposition, **not a verified count of original historical answers**.
- The map explicitly says only PRD-005 and PRD-042 have original answers recovered in the plan; all other decisions are working reconciliation. Recover the remaining answers from chat/source records where possible.
- Nine capability descriptions are truncated in the current map and must be restored from the original Plan 2.3 source: ORD-131, ORD-132, ORD-142, INV-024, INT-020, USR-020, USR-030, USR-031, USR-032.
- The map has generic evidence wording for most rows (“plan 2.3 working reconciliation”), so a later audit must link each original answer to a real source, not repeat the generic label.
- No capability is accepted simply because it is listed or referenced by code/tests. Batch acceptance remains a separate gate.
- A historical NO must remain visible even if a later proposal would change scope; any change requires a traceable later HU+DI decision rather than rewriting history.

## 5. Known later HU+DI refinements to track separately from original answers

These are later interpretations/refinements available to this working record. For each, the coding agent must locate and record the exact source reference/date in the final reconciliation. They do not retroactively change an original YES/NO answer.

### 5.1 Inventory and fulfilment
- Zoho Inventory remains the stock authority; do not create a competing Django stock ledger.
- Stock-changing actions must be Zoho-mediated.
- Admin-reported delivery must not be presented as carrier-confirmed delivery without supporting carrier evidence.
- Existing Zoho-managed fulfilment/Shiprocket behaviour must not be changed without evidence and review.

### 5.2 Catalogue and selling rules
- Do not create separate Household/Bulk combo collections.
- Distributor pricing uses quantity slabs. Bulk pricing is negotiated based on quantity, supply duration, payment and related factors.
- Shopify taxonomy is not the authority for GST calculation.
- Template choices are limited to approved templates; no arbitrary theme-code editing.
- Product content/revision workflow and publication constraints remain governed by the frozen specification and approved revision rules.

### 5.3 Payments and integrations
- INT-002 should be interpreted as a provider-neutral integration/payment event log capability, not as a permanent requirement to use Razorpay.
- Current desired direction is Zoho Payments for EffyKlean.in in place of Razorpay, but this is not authorization to delete the existing Razorpay implementation or to perform a production cutover.
- No live provider writes, production payment, DNS/cutover, or deployment is authorized by this record.
- Provider integration behaviour must be evidence-backed; sandbox validation is distinct from production readiness.

### 5.4 Refunds, returns, and replacements
- No refunds/returns is the baseline business rule.
- Replacement for damaged or incorrect goods is a separate issue and must not be silently treated as a refund/return feature.
- Do not implement refund/return buttons or flows against the current NO disposition unless HU+DI explicitly changes the decision.

### 5.5 Users and roles
- Preserve the approved role model.
- No custom role builder and no arbitrary per-permission editing (including the NO dispositions for USR-030 and USR-031).
- Any conflict between the approved role model and a capability description must be reported rather than resolved by silently expanding permissions.

### 5.6 Hosting and retention
- DigitalOcean is the selected hosting platform for planning purposes as of 2026-10-16. This does not authorize deployment, DNS changes, production configuration, or cutover.
- Saved-address retention refinement: expire an address three months after its last successful delivery to that same address; a successful delivery renews the period. Order placement, payment, payment failure, dispatch, or other non-delivery events do not renew it. An active order temporarily protects the address but does not renew the expiry date. Any implementation is optional/off by default and requires persistent server-side expiry, robust scheduling, and safe idempotent purge. If this conflicts with frozen specifications/data model/deletion rules, stop the affected work and report for HU+DI decision.

## 6. Original decisions vs later refinements — known examples

The existing map identifies PRD-005 (vendor filter) and PRD-042 (vendor field) as NO with original answers recovered in the 12-Oct batch. The source ledger and conversation must be consulted for exact wording/evidence before declaring the entries fully verified.

A partial list of earlier answers mentioned in continuity records includes YES for INT-010, INT-011, INT-022, USR-003, USR-004, USR-013, SYS-005, SYS-020, SYS-011, SYS-021, SYS-022, and NO for SYS-004. This is **not a complete list** and must not be used to infer unlisted answers. The agent must recover and source each row independently.

## 7. Immediate work queue

1. Recover the full original Plan 2.3 source text and descriptions, especially the nine truncated labels.
2. For all 122 IDs, recover Hu's original answer and any suggestions from the actual decision conversations/ledger; cite the source for each.
3. Compare original answers to the current working map and flag every difference without overwriting the historical answer.
4. For each conflict, distinguish (a) Di's recommendation, (b) Hu's later explicit decision, and (c) the resulting HU+DI refinement.
5. Validate every refinement against the frozen SPEC, architecture, ADRs, current status register, and relevant code/tests.
6. Ask HU+DI to decide any unresolved contradiction or scope change. Do not invent answers or silently settle business ambiguity.
7. Store the verified document in the public analysis repository, local `EffyKleanProject` Git working tree, and private project GitHub repository using explicit paths only. Preserve unrelated changes. Do not use `git add -A`.
8. Report exact paths, commit IDs, source gaps, and any unresolved decisions. Do not claim complete until the per-row evidence audit is complete.

## Appendix A — Imported current 122-row working map

The following is copied from the 16-Oct map to make this record useful without having to reopen another file. It is included as a **working map**, not as a verified original-answer transcript. The map's capability descriptions and evidence labels retain the limitations noted above.

# Plan 2.3 decision/evidence map — the 122 rows (2026-10-16)

Scope: the 122 rows of Delta Plan section 2.3 (NOT the 122 SPEC acceptance criteria in `AC_CATEGORISATION_2026-10-15.md`). Generated by matching each Source ID against
`modules/`, `integrations/`, `tests/` and the status register. A match shows the ID is *referenced*, not that the capability is complete or accepted. No row is
marked accepted: Batch 1 is not accepted, and the Plan 2.3 label for each row (explicit answer recovered / agreed rule / evidence not recovered) is still the
HU+DI review item. Only PRD-005 and PRD-042 state a recovered original answer in the plan; every other decision is a working reconciliation.

Summary: {'decision recorded; implementation and tests NOT traced by ID': 84, 'mapped (ID referenced in code or register); no test names the ID': 7, 'excluded by decision (NO); do not build': 17, 'evidence-only placeholder; nothing to implement': 1, 'mapped + tests reference the ID (not independently verified)': 13}

| ID | Capability | Decision | Code reference | Test reference | Status | Decision evidence |
|---|---|---|---|---|---|---|
| ORD-130 | Order list "All locations" filter | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-131 | Order list stats strip: orders, items ordered, sales reversa | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-132 | Export orders: scope choices (current page, all orders, sele | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-133 | Export format choice (CSV for spreadsheets, plain CSV) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-135 | Bulk "Print packing slips" for selected orders | YES | modules/backoffice/order_tools_views.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| ORD-137 | "Mark as delivered" on a single fulfilment | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-140 | Bulk "Change fulfillment location" | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| ORD-142 | Order "More actions": Edit, Duplicate, Archive/Unarchive, Vi | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-143 | Link from Admin order to the customer's order status page | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-144 | Order header "Refund" and "Return" buttons | NO | - | tests/test_refund_guard.py | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| ORD-145 | Fulfilment card "..." menu (not opened; contents unobserved) | EVIDENCE ONLY | - | - | evidence-only placeholder; nothing to implement | decision source: plan 2.3 working reconciliation |
| PRD-001 | Product list with pagination, thumbnails, status badges | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-002 | Search products (ID, Zoho item, name) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-003 | Filter by status | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-004 | Filter by category / product type / use case | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-005 | Filter by vendor | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation (original answer recovered, 12-Oct batch) |
| PRD-006 | Filter by tag | YES | - | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-007 | Filter by collection / sales channel | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-008 | Filter by stock level (low, out) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-009 | Sort the list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-010 | Column: inventory ("N in stock") | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-011 | Column: category, product type | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-012 | Column: channels | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-013 | Saved product views | YES | modules/backoffice/listkit.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-014 | Export products (CSV) | YES | modules/backoffice/catalogue_views.py | tests/test_product_admin.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| PRD-015 | Product count by status summary | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-020 | Create product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-021 | Edit product content as a revision | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-022 | Duplicate product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-023 | Title | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-024 | Description (rich text) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-025 | Short description / benefits / usage / safety | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-026 | Price (MRP) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-027 | Compare-at price | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-029 | Charge-tax flag | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-031 | SKU | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-033 | Zoho item link / mapping | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-034 | Track quantity / sell when out of stock | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-035 | Quantity per location | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-038 | Country of origin | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-040 | Physical product / requires shipping | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-041 | Product type / category / tags | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-042 | Vendor | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation (original answer recovered, 12-Oct batch) |
| PRD-043 | Shopify taxonomy category | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-044 | Metafields (pinned custom data) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-046 | Theme template selector | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-048 | Concentrate quantity / dilution data | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-050 | Product status: draft, in review, approved, published | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-051 | Submit / return / approve / publish workflow | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-052 | Archive / unpublish a published product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-053 | "Unlisted" (reachable by link only) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-054 | Delete product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-055 | Product history / timeline | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-056 | Preview an unpublished revision | YES | modules/backoffice/catalogue_views.py, modules/catalogue/customer_view.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-058 | Upload, reorder and set primary image | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-059 | Image alt text | YES | modules/catalogue/customer_view.py, modules/catalogue/models.py | tests/test_catalogue_boundaries.py, tests/test_product_admin.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| PRD-062 | SEO title and meta description | YES | modules/catalogue/customer_view.py, modules/catalogue/models.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-063 | URL handle (slug) edit | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-001 | Collections list | YES | modules/backoffice/collection_views.py, modules/catalogue/collections.py | tests/test_catalogue_boundaries.py, tests/test_collections.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| COL-002 | Create manual collection | YES | modules/backoffice/forms.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| COL-003 | Create automated collection by rules | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-004 | Collection image, description, SEO | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-005 | Collection sort order | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-006 | Add / remove products in collection | YES | - | tests/test_migrations.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| COL-007 | Separate combo collections | NO | modules/catalogue/models.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| COL-008 | Collection channel availability | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-009 | Catalogs / price lists (B2B, markets) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-010 | Price override / adjustment per catalog | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-001 | Inventory page (per location counts) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-002 | States: available, committed, unavailable, on hand, incoming | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-003 | Adjust quantity | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-004 | Adjustment history | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-005 | Reserve / commit stock | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-006 | Low-stock alert | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-007 | Locations list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-008 | Add / edit / deactivate location | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-009 | Inventory-by-location report | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-010 | Purchase orders | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-011 | Transfers between locations | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-012 | Suppliers | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-013 | Inventory CSV import / export | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-020 | Inventory column "Bin name" | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-021 | Inventory quick-transfer popover | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-022 | Export inventory (from all locations) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-023 | Incoming popover with "Create transfer" | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-024 | Purchase order list: statuses Draft, Ordered, Archived; supp | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-001 | Integration readiness checks | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-002 | Razorpay webhook log | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-003 | Reconciliation queue | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-004 | Outbox / worker view | YES | - | tests/test_integration_visibility.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| INT-005 | Zoho mapping health and sync status | YES | - | tests/test_integration_visibility.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| INT-006 | Shiprocket status | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-007 | App store / marketplace | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-008 | Custom/private apps and API tokens | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-009 | Shopify Flow | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-020 | Flow workflows: eight Shopify-template marketing workflows ( | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-021 | Flow: workflow tags, last run, version history | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-023 | App row menu: open, view details, get support, uninstall | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-001 | Staff list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-002 | Deactivate / reactivate staff | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-005 | Roles (Admin, Director) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-006 | Granular per-area permissions | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-007 | Permission matrix confirm | YES | modules/backoffice/permissions_views.py, modules/identity/authority.py | tests/test_permissions.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-008 | Staff sign-in with MFA, lockout | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-009 | Recovery codes | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-010 | Own account: profile, password, sessions | YES | modules/backoffice/account_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-011 | Staff activity / sign-in history | YES | modules/backoffice/staff_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-012 | Collaborator accounts (agencies) | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-020 | Users: tabs Active, Pending, POS app-only, Requests; roles S | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-021 | Per-user "secure sign-in method required" flag | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-022 | Permission "Requests" tab (staff asking for access) | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-023 | POS app-only users | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-030 | Roles page: 17 roles in three categories (store, organizatio | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-031 | Role permission catalogue (e.g. orders: edit, apply discount | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-032 | Users: "Security" page (monitor user activity, collaborator  | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| SYS-001 | Audit trail viewer | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| SYS-002 | Audit export | YES | modules/backoffice/ops_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-003 | Global search | YES | - | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| SYS-006 | Home to-do overview | YES | modules/backoffice/home.py | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-007 | Home recent activity | YES | - | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-008 | Home business metrics | YES | - | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-012 | Responsive accessible shell | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |


## Appendix B — Decision ledger source snapshot

The ledger remains the detailed record of the original question/answer process and conflict-resolution protocol. Use its contents to recover the original choices and source trail; do not treat the imported map as a substitute for that ledger.

Source ledger SHA at time of retrieval: `ada612a7c469d7e407c546ad03df03572b85ad26`.

## Appendix C — Conflict analysis source snapshot

The conflict analysis contains recommendations and reasoning that must be distinguished from decisions actually approved by Hu. Do not elevate a Di recommendation into a business decision without evidence of Hu's agreement.

Source analysis SHA at time of retrieval: `cc70bd3cb2f78c104af2bd57fa82d0574efbf7fd`.

## Appendix D — Continuity checkpoint source snapshot

The 13-Oct checkpoint records later project direction and continuity notes. Confirm exact source context for each refinement before promoting the register to fully source-verified.

Source checkpoint SHA at time of retrieval: `69d831785343dd9e2963363831e7aa00ff3d88e2`.

---

**Governance reminder:** This document is a comparison baseline, not an implementation authorization. Preserve the historical answer, record later changes as later changes, and use STOP → REPORT → HU+DI DECIDE for material conflicts.


---

# Appendix A — Original HU+DI Capability Decision Ledger (2026-10-12)

**Source path:** `ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md`  
**Source blob SHA at consolidation:** `ada612a7c469d7e407c546ad03df03572b85ad26`  
**Preservation:** Full source text reproduced verbatim below.

# Shopify Admin vs EffyKlean Admin — HU+DI Decision Ledger

**Date:** 2026-10-12  
**Status:** Question phase believed complete based on decisions recovered from the conversation; conflict-resolution phase not yet complete.  
**Source comparison:** [COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md](COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md)  
**Purpose:** Persistent reference so future work does not depend on searching chat history.

## Decision protocol

- Ask about **unique capabilities only**. Group duplicate/overlapping source rows and retain all original IDs.
- A recorded decision is final for the question phase; do not ask it again merely because the same capability appears under another ID/category.
- YES means intended future capability/scope, not permission to implement immediately.
- NO excludes the capability unless the conflict-resolution phase explicitly reopens it and HU+DI records a new resolution.
- Finish the question phase before reviewing conflicts. Di should propose concrete reconciliation solutions and ask Hu only when a genuine business decision is unavoidable.
- No implementation is authorised by this ledger alone.
- Preserve source ID gaps; never invent IDs.
- The comparison file contains 494 actual feature entries. This ledger records decisions recoverable from the discussion summary and is a continuation aid; where a specific row decision is not explicitly transcribed below, verify the original conversation/source before treating it as a new undecided question.

## Project constraints that apply during conflict resolution

- Target: `www.effyklean.in`; Shopify reference: `effyklean.com`.
- Django 5.2, Python 3.14, PostgreSQL 17; modular monolith. Zoho is the authority for stock, accounting and tax records; Shiprocket handles fulfilment; Razorpay is the approved payment gateway.
- **NO PAYMENT → NO DISPATCH.**
- GST-inclusive prices. Checkout collects GST Number + GST Name; valid pair goes to Zoho GST invoice, otherwise consumer invoice.
- Product is SKU-centric; product title, concentrate quantity and final diluted volume are required commercial concepts. MRP and sale price after the current discount.
- One extra discount only. Combo discount is amount-based per product: first selected item receives no combo discount; later selected items receive the configured discount; if the first item is removed, the next becomes first.
- No separate Household/Bulk combo collections. Distributor quantity slabs only; Bulk is negotiated using quantity/monthly supply/payment factors.
- COD excluded from baseline. No returns/refunds baseline; replacements for damaged/incorrect goods are a separately defined case. Shipping charges are not added at checkout under SPEC §3.8.
- Existing Zoho workflow: Shopify order-created webhook updates Zoho order details. Do not replace or modify this workflow without inspection and HU+DI review. Shiprocket WhatsApp notifications remain enabled. Zoho and EKI order references are both used.
- Existing operations include two Karnataka POS locations and one Maharashtra delivery centre. Zoho–Shiprocket integration appears active but has not been proven through recent shipment activity.
- Customer Care: Wednesday–Monday, 10 AM–6 PM; Tuesday closed. Support email: Support@EffyKlean.com. Email/WhatsApp preferred; SMS is not the default.
- Marketing role is MARKETING; ADMIN/DIRECTOR may manage budgets.
- Do not infer that a provider setting is configured just because its capability was answered YES. Validate the current value before changing it.

## Recorded feature decisions

### Orders (ORD)

Recorded decisions:
- **YES:** ORD-001–018 except ORD-019; ORD-020–018? See correction below.
- **NO:** ORD-019 amount-range filter; ORD-064 customer-initiated cancellation; ORD-067 order line-item edits; ORD-069 refunds; ORD-070 refund execution; ORD-071 returns; ORD-073 exchanges; ORD-086 moving fulfilment to another location; ORD-087 splitting fulfilment across locations; ORD-092 merging/splitting orders; ORD-103 bulk fulfil/create labels; ORD-105 bulk cancellation; ORD-112 payment reminders; ORD-116 order routing rules; ORD-121 return-status list column; ORD-136 bulk manual status changes; ORD-138 bulk payment capture; ORD-139 bulk fulfilment requests.
- **YES:** ORD-020–049; ORD-060–063; ORD-065–066; ORD-068; ORD-072; ORD-074–085; ORD-088–091; ORD-093–095; ORD-100–111 except ORD-112; ORD-113–116 except ORD-116; ORD-120, ORD-122–126, ORD-134, ORD-141.
- ORD-107 order ID prefix/format was discussed as a capability; the source file marks its older recommendation as unapproved. Treat the user's later explicit YES in the conversation as scope intent, but retain the need to resolve implementation details.
- ORD-140 was considered covered by the prior location decisions; ORD-142 is a grouping of existing actions; ORD-143 overlaps customer order tracking (ORD-109); ORD-144 is covered by the NO decisions for refunds/returns. ORD-145 is **not assessed**: the fulfilment-card menu was not opened and its contents were not observed. Inspect the menu read-only before deciding whether any genuinely new capability exists.

### Draft orders (DRF)

- **YES:** DRF-001–007, DRF-009–011, DRF-020–021.
- **NO:** DRF-008 (complete draft as paid/payment pending).
- Conflict review needed for draft shipping lines, tax-exempt handling, discounts, payment semantics and the submitted-for-review approval step.

### Products (PRD)

Previously answered; do not re-ask. Explicitly recovered decisions include:
- **YES:** PRD-028, PRD-030, PRD-032, PRD-036–037, PRD-039, PRD-045, PRD-047, PRD-057, PRD-061, PRD-064–075 (with PRD-060 exception below), PRD-083–084 as reported in conversation, PRD-090–097, PRD-098, PRD-100–105.
- **NO:** PRD-060 (video and 3D product media).
- Explicitly recovered later **YES** decisions: PRD-066–074; PRD-072, PRD-073, PRD-074, PRD-075; PRD-083, PRD-084, PRD-090–097, PRD-098, PRD-100–105. (Overlapping IDs are listed once for the decision ledger.)
- The discussion recovered PRD-084 as YES even though the source row describes Shopify taxonomy-driven tax rates and the source file's old status says REJECT. This is a direct conflict requiring resolution; do not silently reinterpret the answer or ask the same capability again.
- Other previously covered product rows should be taken from the recorded chat decisions/source matrix; do not infer missing individual answers from a range alone.

### Collections (COL) and Inventory (INV)

- The user has already completed the questions in these categories; **do not restart the question batches**.
- Frozen constraints remain: Zoho is stock authority. Inventory adjustments, transfers, purchase orders, supplier management and inventory imports/exports in Django Admin were previously excluded. Read-only stock visibility and low-stock alerts had earlier conditional acceptance. Separate combo collections remain NO. Reconcile any later YES against these decisions during conflict review rather than asking duplicate questions.

### Gift cards (GFT)

- **YES:** GFT-001 create/sell/redeem gift cards; GFT-002 gift-card liability reporting.
- This reopens a previous explicit exclusion of gift cards/loyalty. Keep as a conflict for solution review.

### Customers (CUS)

- **YES:** CUS-001–033, CUS-040–045, CUS-050–056, as answered in the discussion.
- Conflict review must reconcile these YES choices with prior exclusions for customer import, Shopify Companies/B2B company records, customer segments/segment builder and customer merge where applicable. Do not re-ask the individual questions.

### Discounts (DSC)

- **YES:** DSC-001–027, DSC-040–041, as answered in the discussion.
- Conflict review: DSC-018 (combining discounts) versus the frozen “one extra discount only” rule; DSC-023 free shipping versus SPEC §3.8 and earlier shipping decision; DSC-026 combo-pack pricing versus the established combo selection/discount rule.

### Content (CNT)

- **YES:** CNT-001–020 and CNT-040–042, as answered in the discussion.
- Conflict review: theme/theme-code editing (CNT-014/CNT-041), forms builder (CNT-019), chat/chatbot (CNT-020), structured metaobjects (CNT-011), how-to videos (CNT-017), and Files library (CNT-009) had earlier rejection/defer constraints. Reconcile later YES decisions explicitly.

### Marketing (MKT)

- **YES:** MKT-001–007 and MKT-010–013, as answered in the discussion.
- Conflict review: Shopify Email/messaging campaigns, marketing automation/Autopilot and social posting/audiences were previously rejected/deferred. SMS remains excluded unless explicitly resolved otherwise.

### Channels (CHN)

- **YES:** CHN-001–008.
- Conflict review: social, Agentic/AI and marketplace/Shop app channel scope had previously been rejected/deferred.

### Analytics (ANA)

- **YES:** ANA-001–027.
- Conflict review: ANA-026 AI-agent session/conversation reporting reopens an earlier rejection of AI session/conversation reporting.

### Settings (SET)

- **YES:** SET-001–007, SET-009–027, SET-028–035, SET-052, SET-055–057, SET-059–061, SET-072–076.
- **NO:** SET-008 COD; SET-050 transfer/move store to organisation/external owner; SET-058 Shopify Network Intelligence; SET-070 COD payment customisation; SET-071 Razorpay Magic Checkout.
- Conflict review includes: SET-009 PayPal/alternative gateways; SET-013 self-service returns/store credit; SET-014/016 shipping profiles/local delivery; SET-019 duties; SET-025 apps/channels; SET-026 domains; SET-028/074 metafields; SET-034 feature previews/labs; SET-052 billing; SET-059 SMS marketing; SET-060 policy defaults; SET-061 fulfilment-service notifications; SET-072 social sign-in; SET-073 editable packing-slip template; SET-075 languages.
- SET-005/006/076 payment settings being in scope does not prove the current Razorpay account/domain or capture configuration is correct; verify read-only before changes. SET-024 notification templates was answered YES, but SMS conflicts with the current no-SMS preference and must be reconciled.

### Integrations (INT)

- **YES:** INT-010 webhook subscription configuration; INT-011 read-only Zoho Flow workflow visibility; INT-022 Zoho integration inventory/connection details.
- Earlier decisions: INT-001 readiness checks, INT-002 Razorpay webhook log, INT-003 reconciliation queue, INT-004 outbox/worker view, INT-005 Zoho mapping/sync health and INT-006 real Shiprocket status were covered/accepted; INT-007 app store and INT-008 custom/private apps/API tokens rejected; INT-009 Shopify Flow rejected; INT-020 Shopify-template marketing Flow builder rejected; INT-021 Flow tags/run/version history rejected; INT-023 app row menu rejected.
- ORD-141 YES for running Flow automation on orders conflicts with the earlier rejection of Shopify Flow capabilities. Resolve narrowly without assuming that the existing Zoho Flow workflow may be replaced.

### Staff users (USR)

- **YES:** USR-003 create/invite staff; USR-004 reset staff MFA; USR-013 restrict access to cost/reports/exports.
- Previously covered/accepted: USR-001 staff list, USR-002 deactivate/reactivate, USR-005 Admin/Director roles, USR-008 staff sign-in MFA/lockout, USR-009 recovery codes, USR-010 own profile/password/sessions, USR-011 staff activity/sign-in history, USR-021 secure sign-in, USR-032 activity monitoring.
- Previously rejected: USR-006 granular per-area permissions, USR-012 collaborator accounts, USR-022 requests tab, USR-023 POS app-only users, USR-030 custom role builder, USR-031 per-permission editing. USR-007 permission-matrix confirmation was flagged for D-F1; USR-020/022/023 details should be checked against source before any new question.

### System shell (SYS)

- **YES:** SYS-005/SYS-020 combined notification centre/home alerts feed; SYS-011 help/support link; SYS-021 recent items in global search; SYS-022 home traffic/conversion metrics.
- Previously covered: SYS-001 audit trail viewer, SYS-002 audit export, SYS-003 global search, SYS-006 home to-do overview, SYS-007 home recent activity, SYS-008 home business metrics, SYS-012 responsive/accessibility shell.
- **NO:** SYS-004 command palette/keyboard shortcuts; SYS-009 setup guide/promotions; SYS-010 AI assistant/Sidekick; SYS-013 multi-store switcher.

## Conflict-resolution backlog (do not re-ask the original feature questions)

Use this list as the starting point for phase-wise analysis. Di should propose a concrete solution for each, retaining all recorded YES intent where feasible and respecting frozen rules unless HU+DI explicitly revises them.

1. Stock authority vs product/inventory UI, package/weight and inventory indicators.
2. Order cancellation/restocking, post-order price edits, store credit, return labels/inspection, fulfilment actions, hold/release, bulk actions and delivery marking.
3. Customer-initiated changes, order routing and fulfilment ownership versus Zoho/Shiprocket workflow.
4. Draft order shipping/tax/discount/payment semantics.
5. Gift cards and liability reporting versus prior gift-card exclusion.
6. Customer import, company/B2B records, segments and merge versus earlier exclusions.
7. Discount stacking, free shipping and combo-pack pricing versus frozen discount/shipping/combo rules.
8. Content/theme/code/forms/chat/metaobjects/media/files versus prior exclusions/deferred decisions.
9. Marketing automation, campaigns, social posting/audiences and SMS versus prior exclusions and no-SMS preference.
10. Social/AI/marketplace channels versus prior exclusions.
11. AI session/conversation analytics versus prior rejection.
12. Alternative gateways, self-service returns/store credit, shipping profiles/local delivery, duties, apps/channels, domains, metafields, labs, billing, policy defaults, fulfilment notifications, social sign-in, packing slips and languages.
13. Flow automation versus earlier Shopify Flow rejection; protect existing Zoho Flow.
14. Product taxonomy/tax behaviour (especially PRD-084) versus EffyKlean's own category and tax rules.
15. Security permissions/MFA reset and cost/report/export restrictions versus the existing Admin/Director/Marketing role model.
16. ORD-145: read-only observation of the fulfilment card menu before deciding whether it contains any new unique capability.

## Next steps

1. Treat this ledger and the source comparison as the persistent working references; do not repeat the completed unique-question batches.
2. Inspect the exact source/earlier decision evidence for any ledger ambiguity before relying on it.
3. Complete the conflict-resolution phase with proposed solutions and HU+DI resolutions.
4. After conflicts are settled, update this ledger with final decisions, implementation interpretations, explicit supersessions, and any remaining open items.
5. Only then prepare an implementation-ready scope baseline. This ledger does **not** itself authorise implementation.


---

# Appendix B — Business-Intent-First Conflict Reconciliation (2026-10-12)

**Source path:** `CONFLICT_RECONCILIATION_ANALYSIS_2026-10-12.md`  
**Source blob SHA at consolidation:** `cc70bd3cb2f78c104af2bd57fa82d0574efbf7fd`  
**Preservation:** Full source text reproduced verbatim below.

# EffyKlean Admin Capability Reconciliation — Business Intent First

**Date:** 2026-10-12  
**Status:** HU+DI analysis record; assessment and reconciliation recommendations, not implementation authorisation.  
**Source comparison:** [COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md](COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md)  
**Decision ledger:** [ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md](ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md)  
**Purpose:** Reassess the recorded Shopify-vs-Django differences using HU's governing test: **Is this a genuine conflict where two decisions cannot coexist?** If not, retain the desired capability and combine it with the existing business rules where useful.

## 1. Governing principle

The earlier conflict backlog over-classified differences as conflicts. HU clarified that the YES/NO capability review was intentionally conducted first so that EffyKlean's desired future Admin experience could be established before resolving genuine contradictions. A YES often means “this capability is desirable for a better customer/management experience, now or in the future,” not “replace our current business model” and not “implement immediately.”

Apply this sequence to every capability:

1. **Identify the business intent** behind the capability and preserve the original comparison ID(s).
2. **Check coexistence:** can the capability and the existing rule both be true?
3. If yes, **combine them** into a coherent feature; do not label a conflict.
4. If the capability is useful but not needed immediately, preserve it as a **future enhancement** rather than rejecting it.
5. If a literal Shopify implementation is unsuitable, adapt the underlying value to EffyKlean's business model rather than cloning Shopify's workflow.
6. Raise a decision to HU only if two explicit decisions cannot coexist and there is no reasonable adaptation that preserves the intent.
7. Keep implementation status, provider verification, priority and implementation authorisation separate from business intent.

Shopify's implementation is evidence that a capability exists in a real commerce platform and can be worth investigating. It is not, by itself, proof that the same workflow, permissions or provider setup is appropriate for EffyKlean.

## 2. Evidence and limitations

- The source comparison covers **494 capability rows** across 34 Shopify Admin areas and maps them to Django Admin.
- The comparison says Shopify observations were carried forward from read-only walks on 2026-10-05 and 2026-10-10, not re-observed on 2026-10-12. Some rows are DOC/UNK and are not verified for this store.
- The Django side in the source comparison was statically inspected; no fresh test/browser run or provider contact was performed for that comparison. Provider integrations are explicitly described as simulations/mocked HTTP rather than provider-proven.
- The decision ledger is a continuity aid recovered from prior discussion, and it contains known errors/ambiguities (including the malformed Orders range and some over-broad “conflict” labels). The row-level comparison is the capability catalogue; the ledger and conversation decisions supply business intent.
- This document reconciles the known groups and corrects the decision approach. It does **not** claim that all provider integrations or implementation behaviour have been verified, nor does it authorise code changes.

## 3. Existing business rules that remain in force

These rules are constraints to design around, not reasons to discard additional Admin capabilities:

- Zoho remains the stock/inventory authority; storefront stock is a synchronised representation.
- HU's desired stock-sync model: sync Zoho items/products with the storefront on stock change, with hourly synchronisation/reconciliation as a fallback; support low-stock alerts in Zoho and on EffyKlean.in. Verify trigger support, retries, failure alerts and actual sync health before describing it as live.
- Product additions in Zoho or the storefront should include the required dimensions. Do not create duplicate Shiprocket dimension-management merely to repeat the same data; verify the data mapping at integration boundaries.
- HSN comes from the previously documented EffyKlean default and must be retrieved rather than guessed. HU's intended GST treatment: Karnataka intra-state supply uses 9% CGST + 9% SGST; other-state inter-state supply uses 18% IGST. Implement subject to correct place-of-supply and applicable product classification rules; the product category is not the tax engine.
- Product catalogue remains SKU-centric. A combo has no separate SKU; checkout computes combo pricing and the resulting Zoho order carries actual item SKUs, quantities, line prices and discounts.
- Combo pricing: first selected item receives no combo discount; subsequent selected items receive the configured amount-based discount; removing the first makes the next selected item first.
- One additional discount only, in line with the existing pricing rule. Distributor quantity slabs and negotiated Bulk pricing remain distinct from public promotions.
- No separate Household/Bulk combo collections. Distributor pricing uses quantity slabs; Bulk terms are negotiated using quantity, supply duration and payment factors.
- COD is excluded. **No refunds and no returns.** Replacements for damaged/incorrect goods remain a distinct existing process.
- **NO PAYMENT → NO DISPATCH.**
- No customer cancellation or editing after order placement. Admin may cancel an order based on the case.
- Admin may mark an order fulfilled and may add tracking or leave tracking blank (for example, a known customer collecting an online order from a location).
- Overrides require Director approval. Record the reason, actor and approver in the audit trail.
- Management may establish storefront/POS arrangements based on distributor discussions. A capability to support multiple sales contexts should not be dismissed merely because today's operation has one main web storefront.
- Zoho → Shiprocket remains the fulfilment/integration context. Existing Zoho Flow order-created workflow must be inspected and protected; do not replace or modify it without HU+DI review. Shiprocket WhatsApp notifications remain enabled.
- Email/WhatsApp are preferred; SMS is not the default channel. A non-default channel may be considered as a future configurable option where consent, compliance and business value are addressed.
- Existing role model includes ADMIN/DIRECTOR and MARKETING; ADMIN/DIRECTOR may manage marketing budgets. Director approval is required for overrides.
- Additional Admin powers are management capabilities used in the interest of the organisation. They are not automatically customer self-service features.

## 4. Outcome summary

**Assessment result:** the earlier backlog contains many apparent conflicts that are actually future capabilities, implementation differences, or opportunities to combine capability with a guardrail. After applying the coexistence test and the business rules above, **no additional HU decision is currently necessary merely to settle those false conflicts**.

Two areas need explicit implementation interpretation, but their business outcome is already clear:
- A self-service returns/refunds feature cannot be enabled because HU explicitly confirmed no refunds/returns. Admin order management can still be flexible.
- Shopify taxonomy-driven tax rates cannot be adopted literally because EffyKlean's GST rule and HSN handling are already defined. The useful product-tax/HSN data capability can still be supported without allowing a Shopify taxonomy to determine GST.

Other risks (provider proof, exact integration mechanics, data mapping, legal consent, security controls) are implementation/readiness checks—not reasons to ask HU to repeat business decisions.

## 5. Reconciliation by capability group

### 5.1 Orders and fulfilment — ORD-001..145

**Business intent:** a capable Admin order workspace with useful filtering, history, notes, exports, reconciliation, operational actions and management flexibility.

**Reconciliation:**
- Keep order list/detail, status/payment/fulfilment filters, customer and line-item detail, payment/provider references, EKI/Zoho/Shiprocket references, audit/timeline, customer history, attention flags, order exports, print/export options, destination/PO details, tracking links and other useful operational views as capability candidates. Missing in Django means an enhancement, not a conflict.
- Admin cancellation (ORD-060/061) coexists with the rule that customers cannot cancel after placement (ORD-064 is not to be exposed as customer self-service). Cancellation does not itself authorise an inventory adjustment; Zoho remains stock authority.
- Delivery contact/address corrections before handover can coexist with prohibiting post-order line-item, quantity, price or discount edits. Customer change requests can be handled by Customer Care/management without providing a self-service edit control.
- No refunds, returns, exchanges, store credit or return labels in the baseline (ORD-069..075, ORD-144 and related settings). Replacement for damaged/incorrect items remains separate (ORD-072).
- Admin fulfilment and tracking (ORD-080/081) are desired operational powers in HU's clarified model. Admin may mark fulfilled, add tracking, or leave it blank for local pickup. Keep this action auditable and ensure it cannot bypass payment verification. A manual delivery/fulfilment entry is an Admin record, not a claim that carrier data was received.
- Director approval is required for overrides; record approver/reason. The UI should make the distinction between ordinary Admin action and override explicit.
- Hold/release, exception resolution, retries, bulk selection/export, bulk status conveniences, order notes/comments, archive, duplication and related utilities should be evaluated as useful Admin capabilities with guardrails. Do not automatically reject bulk features merely because a previous recommendation called them unsafe. For destructive/high-impact bulk actions, use confirmation, preview, permission checks and audit; Director approval where the action is an override.
- Do not automatically reassign/split fulfilment locations or change routing in a way that contradicts the agreed operations model. The capability may be designed for future authorised management/distributor/POS needs; do not build an independent inventory or carrier system.
- Customer-facing tracking (ORD-109/143) can coexist with Admin fulfilment operations. The actual status source should be clear: provider/carrier status where verified, otherwise an explicitly recorded Admin update.
- ORD-141 “Run Flow automation” can be interpreted as a future Admin automation capability, not an instruction to implement Shopify Flow. It must coexist with and not silently replace the existing Zoho Flow. Define allowed triggers/actions, permissions and audit before implementation.
- ORD-145 remains unknown in the source comparison because the menu was not observed; this is a read-only evidence gap, not a business conflict. Inspect it only if it adds a unique capability not already represented.

**Disposition:** mostly desired capability/enhancement; no new business question. Preserve no refunds/returns, customer self-service restrictions, Zoho stock authority, payment gate and Director override approval.

### 5.2 Draft orders, distributor and Bulk workflow — DRF-001..021; CUS-029..033; relevant ORD rows

**Business intent:** help management serve distributors and Bulk customers with enquiries, quotations, negotiated pricing, approvals and convenient order creation.

**Reconciliation:**
- Shopify-style Draft Orders, custom line items, PO numbers, notes/timelines, review statuses and payment links are potential tools, not a requirement to copy Shopify wholesale.
- Build around EffyKlean's distributor application, distributor pricing, Bulk enquiry and Bulk quote/business-account model.
- Default to catalogue SKUs. Non-catalogue custom lines can be an explicitly controlled future capability if the business needs them; they must not bypass product/tax rules or create ambiguous Zoho order lines.
- Draft shipping lines are not required by default under the current shipping rule. This does not block draft/quotation workflows.
- Tax-exempt controls must not override the established GST/place-of-supply and HSN logic without a valid tax basis.
- Draft statuses, “submitted for review,” approval and payment links can improve the management workflow. Creating/sending a payment link is not payment confirmation. Do not dispatch until payment is verified unless HU+DI later approves a documented alternative.
- A quotation may be converted to a proper order with agreed SKU lines, quantities, prices and discounts; Zoho does not need a combo SKU.

**Disposition:** opportunity/addendum, not a conflict. Exact workflow is a future design/implementation detail; no repeat question needed.

### 5.3 Products, catalogue, collections and inventory — PRD-001..105; COL-001..010; INV-001..024

**Business intent:** richer product administration, efficient catalogue maintenance, better customer discovery, accurate logistics data and stock visibility without creating a second inventory system.

**Reconciliation:**
- Preserve product create/edit/revision/approval/publish, product history, preview, SEO, media, image alt text, tags, sorting/filtering, product export, safe bulk edits, and other catalogue conveniences as desired capabilities.
- Product import, bulk edits and archive operations can coexist with SKU-centric controls when designed with validation, preview, duplicate detection, approval, audit and rollback. Do not confuse “CSV import capability desired” with permission for unvalidated imports or platform-to-platform migration. No bulk product deletion; archive/unpublish is safer.
- Inventory adjustment, inventory import/export, purchase orders, supplier management, stock reservations and transfers remain outside EffyKlean Admin's independent authority. This does not exclude read-only Zoho-sourced stock, inventory indicators, low-stock filters/alerts or reports after integration is verified.
- Product weight/dimensions belong in the product-creation workflow as HU described. Ensure the same canonical values map to Zoho/Shiprocket as required; do not create a separate duplicate package database without need.
- HSN should use the previously documented default and the established GST logic. Shopify taxonomy must not determine GST (PRD-084); a useful tax/HSN data field or classification view may still exist independently of Shopify taxonomy.
- Product status, category, tags, bulk edits, collections and product filters are business tools. Do not introduce separate Household/Bulk combo collections. A future collection/catalog capability may support discovery, campaigns or distributor-specific storefronts if it does not violate that explicit exclusion.
- Combo products/bundles should not be implemented as separate SKU inventory when HU's combo model is a storefront calculation. Keep line-item details in the resulting order.
- Video/3D media, product translations, metafields, channel-specific product settings and other catalogue extras should be treated as future opportunities or lower-priority enhancements where useful; not automatically “conflicts.” Raw theme/code editing is different from safe content/layout controls and should be scoped with security/release controls.

**Disposition:** most rows are enhancements. The two explicit limits are no independent stock authority and no Shopify-taxonomy-driven GST. Neither requires rejecting useful adjacent capabilities.

### 5.4 Customers, distributor accounts, segments, data import/merge — CUS-001..056

**Business intent:** stronger customer history, follow-up, segmentation, account management and growth/retention tools.

**Reconciliation:**
- Customer list/search/details/order history/notes/tags/export, filters, segments, customer timelines and safe account-management tools can coexist with EffyKlean's customer and business-account model.
- Shopify “Companies” is a data model, not the only way to support B2B. EffyKlean can continue using distributor applications, business accounts, Bulk enquiries/quotes and distributor pricing, while adding useful account/contacts/locations/terms capability if business needs justify it.
- Customer import/merge is not inherently a business contradiction; it is a data-quality/privacy risk. If retained as future capability, require duplicate detection, mapping preview, validation, audit, backup/rollback and controlled permissions. Do not perform an unreviewed bulk import or merge. Customer deletion/anonymisation and data-request handling need legal/privacy rules and audit.
- Customer segments and filtered lists can support marketing and follow-up. They do not require copying ShopifyQL or Shopify's exact UI.
- Consent display can coexist with future consent updates and marketing tools; honour actual consent and channel-specific requirements. SMS is not the default and must not be sent without appropriate consent.
- Customer account invitations/sign-in assistance can be considered if customer accounts become part of the approved storefront experience; do not confuse Admin staff MFA reset with customer account recovery.

**Disposition:** enhancement opportunities with data/privacy controls; no need to reopen YES answers.

### 5.5 Discounts, promotions, combos and commercial pricing — DSC-001..041

**Business intent:** flexible commercial campaigns while preserving clear and predictable pricing.

**Reconciliation:**
- Discount lists, fixed/percentage discounts, eligibility, minimums, usage limits, date ranges, duplicate/code generation, reports and management comments can coexist with the existing pricing model.
- DSC-018 “combinations with other discounts” should be implemented as a configurable capability whose valid configuration is constrained by the existing “one additional discount only” rule. It must not silently permit unlimited stacking. If a requested future promotion would exceed the rule, treat it as a deliberate business-rule revision, not a hidden side effect.
- DSC-023 free-shipping discount is not needed in the current baseline. That does not block other discount types or a future shipping-promotion decision if the shipping model changes.
- DSC-026 combo pricing must implement the existing per-item selection rule. Do not create a combo SKU or a separate combo inventory ledger.
- Distributor quantity slabs and negotiated Bulk pricing remain separate from public promotional discounts; distributor/Bulk exclusion from public promotions is retained.
- Admin powers may include creating, scheduling, deactivating, duplicating and analysing discounts, subject to permissions and audit.

**Disposition:** combine the discount-combination UI with the one-extra-discount guardrail; preserve the established combo calculation. No new question needed.

### 5.6 Gift cards — GFT-001..002; SET-032

**Business intent:** possible future customer acquisition, gifting, retention and liability reporting.

**Reconciliation:**
- The ledger records GFT-001/002 as later YES answers while the comparison's older recommendation says REJECT. Under HU's stated method, a later YES is evidence of desired future capability, not a contradiction to be discarded.
- Gift cards are not the same as refunds, returns or store credit. They can be evaluated as a separate future commercial instrument with expiry/terms, liability accounting, fraud prevention, redemption controls and Zoho/accounting mapping.
- Do not conflate a gift card with issuing store credit on cancellation or refund; the latter remains excluded.

**Disposition:** future business enhancement; prior recommendation to reject is superseded as a recommendation by the later YES intent. Not implementation-authorised.

### 5.7 Content, Files, navigation, themes, forms, chat and structured content — CNT-001..042; related PRD/SET rows

**Business intent:** management should be able to improve storefront content, customer education, navigation, lead capture and engagement without depending on a developer for every routine update.

**Reconciliation:**
- Page creation/edit/publish, SEO, navigation, blog content, FAQ, redirect management, Files/media library, how-to content, forms and chat can be evaluated as capabilities supporting customer engagement and conversion.
- A previous “no theme editor/code” recommendation does not imply “no storefront customisation.” Prefer safe, versioned settings/layout controls and controlled publish/preview. Arbitrary raw theme-code editing should not be exposed casually; if ever required, it belongs in a separately controlled developer/release workflow.
- Forms and chat can coexist with existing distributor enquiry/Bulk intake and customer-care channels; integrate rather than duplicate data capture.
- Metaobjects/structured content can be represented by approved domain models where needed; copying Shopify's object model is unnecessary.
- Files library and media references can improve content management; enforce size/type, alt text, reference checks and safe deletion.
- Video/translation/localisation features are future enhancements, not conflicts. Implement only when content and support operations are ready.

**Disposition:** treat as growth/customer-experience opportunities; adapt the implementation to Django architecture and safe publishing rather than cloning Shopify internals.

### 5.8 Marketing, channels, messaging, POS and distributor storefronts — MKT-001..013; CHN-001..008; SET-024/059; relevant SET rows

**Business intent:** reach customers through useful channels, support distributor/POS operations and expand the business over time.

**Reconciliation:**
- Marketing campaigns, attribution, email, audience tools, social posting, Meta/Google/YouTube, WhatsApp and marketplace connections can be future capabilities where business value and provider setup support them. Earlier recommendations to reject these as “not in scope” should not override later YES intent by themselves.
- Keep the MARKETING role and ADMIN/DIRECTOR budget authority. Provide permissions, budget limits, approval and audit where needed.
- Existing email/WhatsApp preference and Shiprocket WhatsApp notifications remain. SMS is not the default; channel capability is not permission to send messages without valid consent or required compliance.
- POS and distributor storefronts are opportunities. HU confirmed management may create storefront/POS arrangements based on distributor discussions. The previous “single channel” rationale is not a permanent business prohibition.
- Multi-store or multi-channel architecture should be designed deliberately; do not add a Shopify-specific store switcher unless it maps to an actual EffyKlean operating model.
- International markets, languages, duties and local pricing can remain future capabilities; current India/INR operation is not a contradiction to future expansion.

**Disposition:** future growth capabilities; retain explicit NOs only where HU clearly said NO (e.g., COD, Razorpay Magic Checkout, or a specific unwanted Shopify-only mechanism).

### 5.9 Analytics and reports — ANA-001..027; SYS-008/022; CNT-042

**Business intent:** improve operational decisions, conversion, customer retention, financial control and growth planning.

**Reconciliation:**
- Sales/order/payment/discount/state reports, GST summaries, customer cohorts, average order value, inventory visibility, exports, scheduled reports, traffic/conversion and acquisition metrics can coexist with the business model when their data sources are available and trustworthy.
- Reports that depend on cost, payout, stock, traffic or carrier data must identify data source, freshness and coverage; do not manufacture unavailable metrics.
- ANA-026 AI-agent sessions/conversations was marked REJECT in the comparison while the ledger records a later YES for ANA-001..027. Treat the later YES as desired future scope to assess, not as a requirement to build a specific AI agent. It is only useful if EffyKlean actually deploys such a customer-facing agent and has appropriate privacy/retention controls.
- Home alerts/notifications and traffic/conversion cards can be added as management convenience when underlying data exists.

**Disposition:** reporting enhancements; no conflict merely because Django lacks the report today.

### 5.10 Settings, payment providers, tax, shipping, privacy and domains — SET-001..076

**Business intent:** management needs enough configuration visibility and control to run the business and expand capabilities without bypassing approved rules.

**Reconciliation:**
- Read-only settings/health views, store profile, brand assets, domains, languages, policies, customer privacy, notifications, payment capture configuration and provider readiness can improve operations.
- A YES for alternative gateways/settings means the capability may be desired in future; it does not mean a new gateway is already approved/configured or should be activated without testing. Razorpay remains the approved gateway in the current baseline; verify the current domain/account and capture mode before live use.
- COD remains an explicit NO and must not become available merely because a payment-settings screen exists.
- Self-service returns/store credit must not be enabled because HU explicitly confirmed no refunds and no returns. This is a feature-level constraint, not a reason to remove the rest of the customer-account/settings capability.
- Shipping profiles, local delivery/pickup and packing-slip templates may support future operations; Admin fulfilment without tracking is already accepted. Do not add an independent carrier or inventory authority.
- Tax settings must preserve the intended GST/place-of-supply logic and HSN mapping. Do not make Shopify taxonomy or an arbitrary Admin override the tax engine.
- Billing/plan screens specific to Shopify are not applicable to a self-hosted Django app. That is a platform-specific non-equivalence, not a business conflict; implement useful cost/usage/operational reporting only if there is a real requirement.
- Domains and sales-channel settings can support future storefront/POS expansion but do not prove DNS, Razorpay domain approval or provider configuration is complete.
- SMS and social sign-in may be future optional capabilities; consent, security and explicit channel choice remain required.
- Editable packing-slip templates can be useful, but the fulfilment source and actual output must be defined.
- Privacy/policy controls need HU-approved legal text and appropriate review; a capability does not authorise inventing legal policy.

**Disposition:** capability/configuration opportunities, with explicit exclusions and provider verification retained.

### 5.11 Integrations, automation and Zoho Flow — INT-001..023; ORD-141; SET-023

**Business intent:** transparent integration health, recovery, automation and fewer manual operations.

**Reconciliation:**
- Integration readiness, webhook logs, reconciliation queues, outbox/worker views, Zoho mapping/sync health, Shiprocket status, webhook subscription configuration and read-only workflow visibility are useful Admin capabilities.
- INT-009 “Shopify Flow” and INT-020/021 Shopify Flow-specific builder/history are platform-specific. Their prior rejection does not rule out EffyKlean-owned automation capabilities or Admin actions that run approved workflows.
- ORD-141 “Run Flow automation” can coexist with protecting Zoho Flow if interpreted as a future controlled automation action, not as permission to replace the existing Zoho order-created workflow or install Shopify Flow.
- HU's stock-sync intent is change-triggered Zoho-to-storefront sync plus hourly reconciliation/fallback, with low-stock alerts in both systems. Implementation must verify Zoho capabilities, event delivery, retries, idempotency, monitoring and recovery. Do not claim this is live until provider-proven.
- The existing Zoho order-created workflow that updates Zoho order details must be inspected read-only before any changes. Keep Shiprocket WhatsApp notifications enabled.
- Provider integrations currently shown as simulations/mocked HTTP in the comparison are not proof of live connectivity. Provider verification is a release/readiness task, not a business conflict.

**Disposition:** build toward reliable, observable integration operations while protecting existing workflows; no repeated business question.

### 5.12 Staff, roles, security, system shell and admin experience — USR-001..032; SYS-001..022

**Business intent:** empower management and staff while ensuring sensitive actions and information are controlled.

**Reconciliation:**
- Staff invite/create, deactivate/reactivate, MFA reset, sign-in history, audit export, permission visibility, cost/report/export access restrictions, global search, recent items, notification centre, home metrics and help/support links can improve the Admin experience.
- A prior rejection of a custom granular role builder does not contradict the need to control access. Implement the approved role model (including ADMIN/DIRECTOR/MARKETING) and clear capability permissions; do not assume a full Shopify-style role editor is required.
- MFA reset and account recovery should be restricted, audited and use appropriate re-verification. Staff invite/create needs secure activation and MFA onboarding.
- Cost, sensitive reports and exports should be limited to authorised roles. Director approval for overrides must be enforceable and auditable.
- Customer notification centre and staff operational alerts can coexist; do not send messages to customers without consent and configured providers.
- Home analytics should only show metrics backed by available, reliable data. A multi-store switcher is unnecessary until EffyKlean has a genuine multi-store operating model, but management's future distributor storefront/POS intent should inform the architecture.

**Disposition:** desired management flexibility with least privilege, audit and explicit Director override controls.

## 6. Explicit decisions versus future implementation details

Do not ask HU again about these unless new evidence demonstrates a real contradiction:

- Admin-only order cancellation; no customer cancellation/editing after placement.
- No refunds or returns; replacements remain separate.
- Admin can fulfil an order with or without tracking, including local pickup.
- Director approval for overrides.
- Distributor-driven storefront/POS arrangements are possible.
- Zoho stock authority and desired stock sync on change plus hourly reconciliation/fallback; low-stock alerts in Zoho and storefront after verification.
- Product dimensions are entered during product creation; map them consistently to relevant systems.
- EffyKlean products use one common, previously documented HSN code; retrieve and apply it consistently with the established GST treatment. Do not let Shopify taxonomy determine GST.
- Combo pricing is calculated on the storefront; Zoho receives individual SKU lines, not a combo SKU.
- Additional Admin capabilities are opportunities for business growth, not conflicts merely because they are absent from the current Django implementation.

## 7. Remaining items that are not business conflicts

These items require evidence or implementation planning, not another business-intent questionnaire:

1. Verify Zoho change-triggered sync, hourly reconciliation, retry/idempotency, stale-data visibility and alert thresholds.
2. Retrieve the exact, previously documented common HSN code used for EffyKlean products; do not ask HU to repeat the business decision.
3. Inspect existing Zoho/Shiprocket mapping and dimension fields; avoid duplicate data ownership.
4. Verify Razorpay domain/account approval and capture configuration before live use.
5. Verify actual Zoho/Shiprocket/provider connectivity; comparison currently records simulated/mocked outcomes.
6. Confirm the precise Director-approval mechanism and audit schema during implementation design.
7. Inspect ORD-145's menu read-only if its contents could add a unique capability.
8. Prioritise and sequence accepted capabilities into controlled implementation phases; the YES answers do not imply all features should be built at once.

## 8. Decision on whether any genuine conflicts remain

Using HU's test—**“Can these decisions coexist?”**—the current evidence does not identify a remaining business contradiction that requires HU to choose between two otherwise desired capabilities.

Where an exact Shopify feature would violate an explicit EffyKlean rule, preserve the rule and adapt or exclude only the incompatible behaviour:
- Do not enable customer self-service returns/refunds.
- Do not let Shopify taxonomy determine GST.
- Do not enable COD.
- Do not let storefront Admin independently change Zoho stock.
- Do not replace the existing Zoho Flow without inspection and HU+DI review.
- Do not dispatch without verified payment under the current rule.

These are design boundaries, not reasons to discard adjacent Admin capabilities. If later evidence exposes a truly irreconcilable pair of explicit decisions, record the exact source IDs, the two statements, why they cannot coexist, and the smallest decision needed from HU. Do not manufacture a conflict to keep a review checklist populated.

## 9. Recommended next step

Use this reconciliation record to update the decision ledger, correcting the false-conflict backlog and preserving the original YES/NO intent. Then produce an implementation-planning view with:
- capability/source IDs;
- business purpose;
- current implementation status;
- dependencies/provider evidence;
- security/audit guardrails;
- priority/phase;
- explicit implementation authorisation state.

This analysis is not implementation authorisation. It is the reconciled statement of desired business capability and the rules those capabilities must respect.


---

# Appendix C — Published ROW122 Decision/Evidence Map (2026-10-16)

**Source path:** `docs/foundation/ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md`  
**Source blob SHA at consolidation:** `a26c967e8c91a8c1887d989a5c434c8b21aeafc3`  
**Preservation:** Full source text reproduced verbatim below. This map is an index/comparison artifact; it does not supersede HU's original decisions or the explanations in Appendices A and B.

# Plan 2.3 decision/evidence map — the 122 rows (2026-10-16)

Scope: the 122 rows of Delta Plan section 2.3 (NOT the 122 SPEC acceptance criteria in `AC_CATEGORISATION_2026-10-15.md`). Generated by matching each Source ID against
`modules/`, `integrations/`, `tests/` and the status register. A match shows the ID is *referenced*, not that the capability is complete or accepted. No row is
marked accepted: Batch 1 is not accepted, and the Plan 2.3 label for each row (explicit answer recovered / agreed rule / evidence not recovered) is still the
HU+DI review item. Only PRD-005 and PRD-042 state a recovered original answer in the plan; every other decision is a working reconciliation.

Summary: {'decision recorded; implementation and tests NOT traced by ID': 84, 'mapped (ID referenced in code or register); no test names the ID': 7, 'excluded by decision (NO); do not build': 17, 'evidence-only placeholder; nothing to implement': 1, 'mapped + tests reference the ID (not independently verified)': 13}

| ID | Capability | Decision | Code reference | Test reference | Status | Decision evidence |
|---|---|---|---|---|---|---|
| ORD-130 | Order list "All locations" filter | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-131 | Order list stats strip: orders, items ordered, sales reversa | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-132 | Export orders: scope choices (current page, all orders, sele | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-133 | Export format choice (CSV for spreadsheets, plain CSV) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-135 | Bulk "Print packing slips" for selected orders | YES | modules/backoffice/order_tools_views.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| ORD-137 | "Mark as delivered" on a single fulfilment | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-140 | Bulk "Change fulfillment location" | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| ORD-142 | Order "More actions": Edit, Duplicate, Archive/Unarchive, Vi | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-143 | Link from Admin order to the customer's order status page | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| ORD-144 | Order header "Refund" and "Return" buttons | NO | - | tests/test_refund_guard.py | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| ORD-145 | Fulfilment card "..." menu (not opened; contents unobserved) | EVIDENCE ONLY | - | - | evidence-only placeholder; nothing to implement | decision source: plan 2.3 working reconciliation |
| PRD-001 | Product list with pagination, thumbnails, status badges | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-002 | Search products (ID, Zoho item, name) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-003 | Filter by status | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-004 | Filter by category / product type / use case | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-005 | Filter by vendor | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation (original answer recovered, 12-Oct batch) |
| PRD-006 | Filter by tag | YES | - | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-007 | Filter by collection / sales channel | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-008 | Filter by stock level (low, out) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-009 | Sort the list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-010 | Column: inventory ("N in stock") | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-011 | Column: category, product type | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-012 | Column: channels | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-013 | Saved product views | YES | modules/backoffice/listkit.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-014 | Export products (CSV) | YES | modules/backoffice/catalogue_views.py | tests/test_product_admin.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| PRD-015 | Product count by status summary | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-020 | Create product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-021 | Edit product content as a revision | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-022 | Duplicate product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-023 | Title | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-024 | Description (rich text) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-025 | Short description / benefits / usage / safety | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-026 | Price (MRP) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-027 | Compare-at price | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-029 | Charge-tax flag | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-031 | SKU | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-033 | Zoho item link / mapping | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-034 | Track quantity / sell when out of stock | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-035 | Quantity per location | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-038 | Country of origin | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-040 | Physical product / requires shipping | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-041 | Product type / category / tags | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-042 | Vendor | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation (original answer recovered, 12-Oct batch) |
| PRD-043 | Shopify taxonomy category | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-044 | Metafields (pinned custom data) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-046 | Theme template selector | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-048 | Concentrate quantity / dilution data | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-050 | Product status: draft, in review, approved, published | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-051 | Submit / return / approve / publish workflow | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-052 | Archive / unpublish a published product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-053 | "Unlisted" (reachable by link only) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-054 | Delete product | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-055 | Product history / timeline | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-056 | Preview an unpublished revision | YES | modules/backoffice/catalogue_views.py, modules/catalogue/customer_view.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-058 | Upload, reorder and set primary image | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| PRD-059 | Image alt text | YES | modules/catalogue/customer_view.py, modules/catalogue/models.py | tests/test_catalogue_boundaries.py, tests/test_product_admin.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| PRD-062 | SEO title and meta description | YES | modules/catalogue/customer_view.py, modules/catalogue/models.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| PRD-063 | URL handle (slug) edit | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-001 | Collections list | YES | modules/backoffice/collection_views.py, modules/catalogue/collections.py | tests/test_catalogue_boundaries.py, tests/test_collections.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| COL-002 | Create manual collection | YES | modules/backoffice/forms.py | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| COL-003 | Create automated collection by rules | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-004 | Collection image, description, SEO | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-005 | Collection sort order | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-006 | Add / remove products in collection | YES | - | tests/test_migrations.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| COL-007 | Separate combo collections | NO | modules/catalogue/models.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| COL-008 | Collection channel availability | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-009 | Catalogs / price lists (B2B, markets) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| COL-010 | Price override / adjustment per catalog | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-001 | Inventory page (per location counts) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-002 | States: available, committed, unavailable, on hand, incoming | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-003 | Adjust quantity | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-004 | Adjustment history | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-005 | Reserve / commit stock | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-006 | Low-stock alert | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-007 | Locations list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-008 | Add / edit / deactivate location | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-009 | Inventory-by-location report | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-010 | Purchase orders | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-011 | Transfers between locations | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-012 | Suppliers | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-013 | Inventory CSV import / export | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-020 | Inventory column "Bin name" | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-021 | Inventory quick-transfer popover | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-022 | Export inventory (from all locations) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-023 | Incoming popover with "Create transfer" | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INV-024 | Purchase order list: statuses Draft, Ordered, Archived; supp | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-001 | Integration readiness checks | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-002 | Razorpay webhook log | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-003 | Reconciliation queue | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-004 | Outbox / worker view | YES | - | tests/test_integration_visibility.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| INT-005 | Zoho mapping health and sync status | YES | - | tests/test_integration_visibility.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| INT-006 | Shiprocket status | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| INT-007 | App store / marketplace | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-008 | Custom/private apps and API tokens | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-009 | Shopify Flow | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-020 | Flow workflows: eight Shopify-template marketing workflows ( | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-021 | Flow: workflow tags, last run, version history | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| INT-023 | App row menu: open, view details, get support, uninstall | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-001 | Staff list | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-002 | Deactivate / reactivate staff | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-005 | Roles (Admin, Director) | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-006 | Granular per-area permissions | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-007 | Permission matrix confirm | YES | modules/backoffice/permissions_views.py, modules/identity/authority.py | tests/test_permissions.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-008 | Staff sign-in with MFA, lockout | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-009 | Recovery codes | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-010 | Own account: profile, password, sessions | YES | modules/backoffice/account_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-011 | Staff activity / sign-in history | YES | modules/backoffice/staff_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| USR-012 | Collaborator accounts (agencies) | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-020 | Users: tabs Active, Pending, POS app-only, Requests; roles S | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-021 | Per-user "secure sign-in method required" flag | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| USR-022 | Permission "Requests" tab (staff asking for access) | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-023 | POS app-only users | NO | - | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-030 | Roles page: 17 roles in three categories (store, organizatio | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-031 | Role permission catalogue (e.g. orders: edit, apply discount | NO | modules/backoffice/permissions_views.py | - | excluded by decision (NO); do not build | decision source: plan 2.3 working reconciliation |
| USR-032 | Users: "Security" page (monitor user activity, collaborator  | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| SYS-001 | Audit trail viewer | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |
| SYS-002 | Audit export | YES | modules/backoffice/ops_views.py | tests/test_staff_account.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-003 | Global search | YES | - | - | mapped (ID referenced in code or register); no test names the ID | decision source: plan 2.3 working reconciliation |
| SYS-006 | Home to-do overview | YES | modules/backoffice/home.py | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-007 | Home recent activity | YES | - | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-008 | Home business metrics | YES | - | tests/test_admin_home.py | mapped + tests reference the ID (not independently verified) | decision source: plan 2.3 working reconciliation |
| SYS-012 | Responsive accessible shell | YES | - | - | decision recorded; implementation and tests NOT traced by ID | decision source: plan 2.3 working reconciliation |


---

## Amendment and refinement register

- **2026-10-16 — HU authority clarification:** HU confirmed that the original YES/NO decisions for all 122 capabilities were reached through joint HU+DI work and must be treated as HU's authoritative original answers. No agent or later artifact may override or question them solely due to missing evidence citations.
- Subsequent refinements must be appended here with the approval date, affected capability IDs, original answer preserved, new approved interpretation, rationale, and source reference. Do not rewrite the historical appendices.
