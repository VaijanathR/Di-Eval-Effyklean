# HU+DI Master Record — 122 Capability Decisions, Conflict Resolutions, and Refinements

**Record date:** 2026-10-16  
**Status:** WORKING BASELINE — NOT YET SOURCE-COMPLETE OR AUTHORITATIVE FOR ALL 122 ORIGINAL ANSWERS  
**Purpose:** Persistent, comparison-ready record for HU+DI and the coding agent. Preserve Hu's original YES/NO answers separately from Di's later recommendations and any subsequent HU+DI-agreed refinements. Do not silently rewrite historical answers.

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
