# EffyKlean Delta Implementation Plan — Final Review Draft
**File:** `plan/first/EffykleanDeltaImplemenationPlanFinal13oct2026.md`  
**Prepared:** 13 October 2026  
**Status:** **HU review draft — not yet approved as the controlling implementation plan**  
**Purpose:** Consolidate the Admin capability YES/NO decisions, the agreed conflict reconciliations, and the pending implementation tasks reported by the EffyKlean coding agent into one prioritised, phase-wise plan.

## 1. Source of truth and precedence

This plan consolidates these records:

1. [Admin Capability Decision Ledger (12 Oct 2026)](../../ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md) — original capability decisions and source IDs.
2. [Phase-Wise Implementation Plan Draft (13 Oct 2026)](../../EFFYKLEAN_PHASE_WISE_IMPLEMENTATION_PLAN_DRAFT_2026-10-13.md) — pending implementation tasks reported by the local coding agent.
3. [Conflict Reconciliation Analysis (12 Oct 2026)](../../CONFLICT_RECONCILIATION_ANALYSIS_2026-10-12.md) — the detailed business-intent-first reconciliation and functional resolutions.
4. [HU+DI Decisions and Resume Checkpoint (13 Oct 2026)](../../HU_DI_DECISIONS_AND_RESUME_CHECKPOINT_2026-10-13.md) — later decisions, including payment-provider direction and implementation priority.
5. [Master Functionality Comparison and Evidence Consolidation (12 Oct 2026, 18:00)](EffyKlean_Master_Functionality_Comparison_Evidence_Consolidation12102026-1800Hr.md) — 597-row cross-cutting and capability evidence register. It informs evidence, implementation state, and validation gaps; it does not replace HU's YES/NO decisions.

**Precedence rules for this plan**
- HU's explicit instruction is to implement every pending task from the agent response; each such task is marked **YES**. Phases establish sequence and priority, not whether the business wants the capability.
- For capability decisions, preserve the recorded YES/NO in the decision ledger, interpreted through the functional resolutions in Section 4 below. A prior recommendation in the Shopify comparison is not a substitute for Hu's recorded decision.
- A recorded **NO** remains excluded unless Hu explicitly changes it.
- The most recent explicit HU+DI decision takes precedence over older provider notes: **Zoho Payments is the intended provider for EffyKlean.in, replacing Razorpay as the direction of travel.** This does not mean credentials, sandbox proof, production configuration, or live cutover are complete or authorised.
- Existing frozen specifications, architecture, privacy/security controls and operational invariants remain binding. A task can be YES while implementation is constrained by those rules.
- If new evidence reveals a true contradiction that cannot be reconciled by applying the agreed functional rules, **STOP → REPORT → HU+DI DECIDE**. Continue independent safe work.
- Do not treat this review draft as permission to deploy, cut over live payments, perform live provider writes, or make unauthorised commits.

## 2. Source inventory, master-evidence reconciliation, and decision-count status

### 2.1 Keep the two kinds of records separate

The [Master Functionality Comparison and Evidence Consolidation (12 Oct 2026, 18:00)](EffyKlean_Master_Functionality_Comparison_Evidence_Consolidation12102026-1800Hr.md) is an **evidence and implementation-state register**, not a substitute for HU's YES/NO decisions.

Its accounting is:
- **597 master rows total:** 103 cross-cutting/platform rows (MF-*) plus 494 Shopify Admin capability rows (MA-*).
- The 494 MA-* rows map one-to-one to the 494 capability IDs in Comparison 1. The 12 Orders batch-1 decision-log rows are folded into ORD-001–ORD-012; they are not 12 extra capability rows.
- The master's dispositions (NO ACTION, VALIDATE, BLOCKED-DEC, REJECT/OOS, IMPLEMENT, FIX) describe what the evidence suggests needs to happen next. They are **not** HU's YES/NO answers. In particular, NO ACTION does not mean business decision NO, and BLOCKED-DEC does not automatically mean Hu has not decided.
- The master reports 365 MA rows with no validation in that session (V0), 75 carried from an earlier browser walk (V0B), 8 simulation-only (V0S), 36 static checks (V1) and 10 HU+DI batch-1 acceptance rows (V2H). It also says Shopify was not re-observed and no provider row had sandbox/production proof. These are evidence maturity notes, not feature-decision counts.

### 2.2 Correct the earlier “115” and the provisional YES/NO totals

The earlier “115 remaining rows” came from an invalid subtraction and was not a list of 115 known unanswered decisions. The follow-up audit found 122 rows that were not individually represented in the ledger's explicit ID/range transcription. We then assigned working dispositions to those rows using the ledger, conflict analysis and functional rules.

**Important correction before review:** the previously displayed **443 YES / 50 NO / 1 evidence-only** split must be treated as a *working disposition tally*, not a fully source-verified final count. Some of the 122 rows were adapted using category-level reasoning, and the master's implementation/evidence labels cannot validate a HU YES/NO answer. I will not present that arithmetic as an audited final answer count until each working disposition is traced to either (a) an explicit recovered HU answer, or (b) a clearly cited functional rule that necessarily determines the disposition. This prevents us from replacing one unverified count with another.

Current accounting:
- **494 source capability rows** are in scope for the decision audit.
- **122 rows** needed a row-level reconciliation beyond the ledger's explicit ID/range transcription; their working dispositions are recorded in the audit table below.
- **ORD-145** remains an evidence-only placeholder: its menu contents were not observed and no feature should be invented.
- The authoritative original answers remain the decision ledger and recoverable HU+DI conversation records; the conflict analysis supplies functional interpretation; the master supplies implementation evidence/state.
- Before final approval, the audit must label each of the 122 rows as **explicit answer recovered**, **determined by an agreed functional rule**, or **decision evidence not yet recovered**. A row in the last group must not be silently converted to YES or NO.

### 2.3 Audit of the 122 rows missing from the ledger's explicit ID/range transcription

The table below is a working reconciliation aid, not a claim that the master itself supplied the user's decision. “YES by reconciliation” means retain the useful capability in an EffyKlean-compatible form only where that interpretation is supported by the agreed business rule; “NO” means exclude the literal capability; “EVIDENCE ONLY” means inspect without inventing functionality. Where the rationale is merely a broad category assumption rather than a recovered decision or necessary rule, it must be verified against the source conversation before the final YES/NO total is approved.

| Source ID | Capability | Final decision | Reconciliation / implementation constraint |
|---|---|---|---|
| ORD-130 | Order list "All locations" filter | **YES** | Location filter limited to configured EffyKlean locations; no independent inventory/routing authority. |
| ORD-131 | Order list stats strip: orders, items ordered, sales reversals, orders fulfilled, delivered, or | **YES** | Show reliable metrics only; omit or clearly label return/reversal measures excluded by the no-returns baseline. |
| ORD-132 | Export orders: scope choices (current page, all orders, selected, matching search, by date) | **YES** | Scoped order exports with permissions, audit and data minimisation. |
| ORD-133 | Export format choice (CSV for spreadsheets, plain CSV) | **YES** | CSV export formats with permissions and data minimisation. |
| ORD-135 | Bulk "Print packing slips" for selected orders | **YES** | Bulk packing slips only where operationally supported; do not bypass Zoho/Shiprocket ownership. |
| ORD-137 | "Mark as delivered" on a single fulfilment | **YES** | Audited Admin-reported delivery record allowed, but never label it carrier-confirmed without carrier evidence. |
| ORD-140 | Bulk "Change fulfillment location" | **NO** | No bulk fulfilment-location reassignment; preserve the agreed location model and Zoho/fulfilment ownership. |
| ORD-142 | Order "More actions": Edit, Duplicate, Archive/Unarchive, View order status page, Print order p | **YES** | Composite action menu allowed only for individually permitted actions; excluded actions remain absent. |
| ORD-143 | Link from Admin order to the customer's order status page | **YES** | Link to customer status/tracking page; carrier status only when verified. |
| ORD-144 | Order header "Refund" and "Return" buttons | **NO** | Refund/return buttons are excluded by the no-refunds/no-returns baseline. |
| ORD-145 | Fulfilment card "..." menu (not opened; contents unobserved) | **EVIDENCE ONLY** | Unobserved menu placeholder, not a defined capability; inspect read-only and do not invent actions. |
| PRD-001 | Product list with pagination, thumbnails, status badges | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-002 | Search products (ID, Zoho item, name) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-003 | Filter by status | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-004 | Filter by category / product type / use case | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-005 | Filter by vendor | **NO** | Original answer recovered from the 12-Oct question batch: Hu answered NO. |
| PRD-006 | Filter by tag | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-007 | Filter by collection / sales channel | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-008 | Filter by stock level (low, out) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-009 | Sort the list | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-010 | Column: inventory ("N in stock") | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-011 | Column: category, product type | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-012 | Column: channels | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-013 | Saved product views | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-014 | Export products (CSV) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-015 | Product count by status summary | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-020 | Create product | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-021 | Edit product content as a revision | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-022 | Duplicate product | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-023 | Title | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-024 | Description (rich text) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-025 | Short description / benefits / usage / safety | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-026 | Price (MRP) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-027 | Compare-at price | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-029 | Charge-tax flag | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-031 | SKU | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-033 | Zoho item link / mapping | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-034 | Track quantity / sell when out of stock | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-035 | Quantity per location | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-038 | Country of origin | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-040 | Physical product / requires shipping | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-041 | Product type / category / tags | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-042 | Vendor | **NO** | Original answer recovered from the 12-Oct question batch: Hu answered NO. |
| PRD-043 | Shopify taxonomy category | **YES** | Use EffyKlean product-category/tax mapping; Shopify taxonomy is not the GST engine. |
| PRD-044 | Metafields (pinned custom data) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-046 | Theme template selector | **YES** | Approved template choices only; no arbitrary theme-code editing. |
| PRD-048 | Concentrate quantity / dilution data | **YES** | Retain concentrate quantity and final diluted-volume product data. |
| PRD-050 | Product status: draft, in review, approved, published | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-051 | Submit / return / approve / publish workflow | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-052 | Archive / unpublish a published product | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-053 | "Unlisted" (reachable by link only) | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-054 | Delete product | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-055 | Product history / timeline | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-056 | Preview an unpublished revision | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-058 | Upload, reorder and set primary image | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-059 | Image alt text | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-062 | SEO title and meta description | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| PRD-063 | URL handle (slug) edit | **YES** | Retain the useful catalogue capability with SKU-centric data, safe publishing, and Zoho stock/tax authority. |
| COL-001 | Collections list | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-002 | Create manual collection | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-003 | Create automated collection by rules | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-004 | Collection image, description, SEO | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-005 | Collection sort order | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-006 | Add / remove products in collection | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-007 | Separate combo collections | **NO** | Conflict resolution: no separate combo collections; implement combo pricing/grouping without separate Household/Bulk combo collections. |
| COL-008 | Collection channel availability | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-009 | Catalogs / price lists (B2B, markets) | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| COL-010 | Price override / adjustment per catalog | **YES** | Retain collection/catalogue capability under SKU-centric products and distributor/Bulk pricing rules. |
| INV-001 | Inventory page (per location counts) | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-002 | States: available, committed, unavailable, on hand, incoming | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-003 | Adjust quantity | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-004 | Adjustment history | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-005 | Reserve / commit stock | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-006 | Low-stock alert | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-007 | Locations list | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-008 | Add / edit / deactivate location | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-009 | Inventory-by-location report | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-010 | Purchase orders | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-011 | Transfers between locations | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-012 | Suppliers | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-013 | Inventory CSV import / export | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-020 | Inventory column "Bin name" | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-021 | Inventory quick-transfer popover | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-022 | Export inventory (from all locations) | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-023 | Incoming popover with "Create transfer" | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INV-024 | Purchase order list: statuses Draft, Ordered, Archived; supplier, destination, received, expect | **YES** | Capability accepted; all stock-changing actions must be Zoho-mediated, with Zoho as authority and no competing Django ledger. |
| INT-001 | Integration readiness checks | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-002 | Razorpay webhook log | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-003 | Reconciliation queue | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-004 | Outbox / worker view | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-005 | Zoho mapping health and sync status | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-006 | Shiprocket status | **YES** | Keep provider-neutral, observable integration capability; use Zoho Payments direction and protect existing Zoho Flow. |
| INT-007 | App store / marketplace | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| INT-008 | Custom/private apps and API tokens | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| INT-009 | Shopify Flow | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| INT-020 | Flow workflows: eight Shopify-template marketing workflows (welcome discount e-mail, thank cust | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| INT-021 | Flow: workflow tags, last run, version history | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| INT-023 | App row menu: open, view details, get support, uninstall | **NO** | Exclude literal Shopify app-store/private-app/Shopify Flow mechanisms; preserve separately approved EffyKlean integrations. |
| USR-001 | Staff list | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-002 | Deactivate / reactivate staff | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-005 | Roles (Admin, Director) | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-006 | Granular per-area permissions | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-007 | Permission matrix confirm | **YES** | Provide a reviewable role/permission matrix within the approved fixed roles. |
| USR-008 | Staff sign-in with MFA, lockout | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-009 | Recovery codes | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-010 | Own account: profile, password, sessions | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-011 | Staff activity / sign-in history | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-012 | Collaborator accounts (agencies) | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-020 | Users: tabs Active, Pending, POS app-only, Requests; roles Store owner, Administrator and a cus | **YES** | Active/pending staff administration; omit POS-app-only users and rejected request-tab mechanism. |
| USR-021 | Per-user "secure sign-in method required" flag | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| USR-022 | Permission "Requests" tab (staff asking for access) | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-023 | POS app-only users | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-030 | Roles page: 17 roles in three categories (store, organization, point of sale), "Add role" for c | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-031 | Role permission catalogue (e.g. orders: edit, apply discounts, set payment terms, charge card, | **NO** | Explicit exclusion of custom role-builder/collaborator/POS-only/request-tab mechanisms; keep approved Admin/Director/Marketing role model. |
| USR-032 | Users: "Security" page (monitor user activity, collaborator request code) | **YES** | Accepted staff/security capability with MFA, least privilege, audit and Director override controls. |
| SYS-001 | Audit trail viewer | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-002 | Audit export | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-003 | Global search | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-006 | Home to-do overview | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-007 | Home recent activity | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-008 | Home business metrics | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |
| SYS-012 | Responsive accessible shell | **YES** | Accepted admin-shell/search/home capability with reliable data and accessibility/responsive controls. |

### Important resolution changes to otherwise YES-listed items

The following recorded YES intentions are constrained by later functional resolutions and are **NO for the literal feature**:
- **ORD-074:** issuing store credit on cancellation/refund — excluded; gift cards remain a separate accepted capability.
- **ORD-075:** return labels/return shipping — excluded because returns are not in the baseline.
- **ORD-076:** inspection of returned packages before restock — excluded because returns are not in the baseline.
- **SET-013:** customer self-service returns/store credit — excluded.
- **COL-007:** separate combo collections — excluded; combo pricing/grouping remains supported without separate Household/Bulk combo collections.

The stock-management rows INV-001–INV-024 present in the source are YES capabilities, but any stock write, adjustment, transfer, purchase-order or location operation must be performed through the authorised Zoho boundary. That preserves the user's later YES answers without making Django a competing inventory authority.


## 3. Functional decisions and conflict resolutions agreed by HU+DI

These are the functional resolutions to use while planning and implementing. They preserve desired capabilities wherever they can coexist with EffyKlean's established business model.

### 3.1 Orders, cancellation, changes, fulfilment and refunds
- Admin may cancel an order; **customers may not cancel or edit an order after placement**.
- Customer/address/delivery-contact corrections may be handled through controlled Customer Care/Admin processes where appropriate; this does not permit changing order lines, quantities, prices or discounts after placement.
- **No refunds and no returns** in the baseline. Store credit, exchanges, return labels and customer self-service returns/refunds are not to be enabled. Replacements for damaged/incorrect goods are a separate process.
- Admin may mark an order fulfilled, add tracking, or leave tracking blank for local pickup. An Admin fulfilment record must not be represented as carrier-confirmed status unless it actually came from the carrier.
- **NO PAYMENT → NO DISPATCH.** A payment link/session is not proof of payment. Dispatch requires verified payment.
- Director approval is required for overrides; record the reason, actor and approver in the audit trail. Destructive/high-impact actions require permission checks, confirmation/preview and audit.
- Admin fulfilment/cancellation does not independently change authoritative inventory; Zoho remains the stock authority.
- Customer-facing tracking can use verified carrier status or clearly identified Admin-entered status. Do not claim provider-confirmed delivery without evidence.

### 3.2 Zoho Inventory, stock sync and product data
- **Zoho Inventory is the stock authority.** Django Admin may show Zoho-sourced stock, inventory indicators, low-stock filters and alerts, but must not become a second independent inventory ledger or permit unauthorised stock adjustments/transfers.
- Desired sync model: Zoho change-triggered sync to the storefront plus hourly reconciliation/fallback, with low-stock alerts in Zoho and EffyKlean.in. Retry, idempotency, freshness, monitoring and actual trigger support must be verified before calling it operational.
- Product weight/dimensions belong in the product-creation workflow. Map canonical values to Zoho/Shiprocket; do not duplicate ownership in a second package/dimension master unless evidence shows it is required.
- Retrieve the previously documented common EffyKlean HSN code; do not guess it. Apply the agreed GST/place-of-supply logic: Karnataka intra-state supply uses 9% CGST + 9% SGST; other-state inter-state supply uses 18% IGST, subject to correct place-of-supply and applicable classification.
- **Shopify taxonomy must not determine GST.** A useful tax/HSN data field or classification view can exist without adopting Shopify's taxonomy-driven tax behaviour.
- No separate Household/Bulk combo collections. A combo is calculated at storefront/order-pricing level; Zoho receives the actual SKU lines, quantities, prices and discounts, not a combo SKU.

### 3.3 Discounts, combos, distributor and Bulk pricing
- One additional discount only; do not silently enable unlimited stacking. A discount-combination UI is acceptable only when its rules enforce this limit.
- Combo pricing is amount-based per product: the first selected item receives no combo discount; subsequent selected items receive the configured discount; if the first is removed, the next selected item becomes first.
- Distributor quantity slabs and negotiated Bulk pricing remain distinct from public promotional discounts. Distributor/Bulk orders are excluded from public promotions under the established rule.
- Free-shipping discounts are not in the current baseline because shipping charges are not added at checkout under the frozen rule; this does not block other discount types.
- Gift cards are a distinct future commercial instrument, not refunds or store credit. The later YES decisions for gift cards and liability reporting supersede the old recommendation to reject them; implement only with expiry/terms, fraud/redemption controls and Zoho/accounting mapping.

### 3.4 Draft orders and assisted selling
- Drafts, quotes, PO numbers, notes/timelines, review statuses and payment links can support distributor/Bulk workflows; do not clone Shopify wholesale blindly.
- Default to catalogue SKUs. Any future custom lines require validation and must not bypass product/tax rules or create ambiguous Zoho lines.
- Draft shipping lines are not required by default. Tax-exempt controls must not override the agreed GST/HSN/place-of-supply logic.
- A quotation/payment link is not payment confirmation; the payment gate remains binding.

### 3.5 Customer, distributor accounts, data and consent
- Customer history, search, tags, notes, filters, segments and exports can coexist with the EffyKlean distributor/business-account model.
- Shopify Companies is not mandatory as a data model. Support distributor applications, business accounts, Bulk enquiries/quotes, contacts, locations and terms in an EffyKlean-appropriate way.
- Customer import/merge can be considered as a controlled capability only with duplicate detection, mapping preview, validation, audit, backup/rollback and permissions. Do not run an unreviewed import/merge. Deletion/anonymisation and data requests need privacy rules.
- Honour actual channel-specific consent. SMS is not the default and must not be sent without appropriate consent and compliance. Email/WhatsApp are preferred; keep Shiprocket WhatsApp notifications enabled.
- Contact and Subscribe forms require approved privacy wording, retention behaviour and a configured provider. Do not invent legal policy text.

### 3.6 Content, media and storefront control
- Page editing, SEO, navigation, blog/FAQ, redirects, Files/media, how-to content, forms and chat are desired capabilities where useful; adapt them to Django rather than cloning Shopify internals.
- Prefer safe, versioned content/layout controls with preview and controlled publishing. Arbitrary theme-code editing must not be exposed casually; if ever required, use a separate controlled developer/release workflow.
- Files/media require type/size validation, alt text, reference checks and safe deletion.
- Videos hot-linked from the old site must be migrated to approved storage. Replacement-video uploads require storage and retention rules.
- Structured content may use approved EffyKlean domain models; it need not copy Shopify metaobjects.

### 3.7 Marketing, channels, POS and expansion
- Marketing campaigns, attribution, email, audiences, social posting, Meta/Google/YouTube, WhatsApp, marketplaces, and distributor/POS storefront arrangements are growth capabilities when provider configuration and business readiness support them.
- Keep the MARKETING role; ADMIN/DIRECTOR may manage budgets. Add permissions, budget limits, approval and audit where needed.
- SMS is not the default; channel capability is not permission to send without consent.
- Distributor/POS arrangements may be created based on management's discussions with distributors. Do not treat the current single main storefront as a permanent prohibition on future channels.
- Do not build a Shopify-specific multi-store switcher unless it maps to a real EffyKlean operating model. International markets, languages and local pricing may be future capabilities.

### 3.8 Analytics, settings and security
- Reports are valid only when backed by trustworthy data. Show data source, freshness and coverage for stock, payout, carrier, traffic and cost metrics; do not manufacture unavailable metrics.
- Shopify-specific billing/plan screens do not map directly to a self-hosted Django application. Implement only genuine EffyKlean cost/usage/operational needs.
- A YES for alternative payment-gateway/settings visibility does not itself authorise activation. The later provider direction is Zoho Payments; verify account/domain, credentials, webhook and capture behaviour in sandbox before any live cutover.
- COD is an explicit NO. Razorpay Magic Checkout is an explicit NO.
- Implement the approved ADMIN/DIRECTOR/MARKETING role model and clear capability permissions; a Shopify-style custom role builder is not required. Staff invites, MFA reset and recovery must be secure, re-verified and audited. Restrict cost, sensitive reports and exports to authorised roles.
- Home metrics/alerts and analytics must reflect available reliable data. Customer messages must not be sent until providers and consent are configured.

### 3.9 Integrations and automation
- Build integration readiness, webhook logs, reconciliation queue, outbox/worker visibility, Zoho mapping/sync health, real Shiprocket status and webhook-subscription configuration.
- EffyKlean-owned automation is distinct from Shopify Flow. A “run automation” capability does not authorise installing Shopify Flow or replacing existing Zoho Flow.
- Inspect the existing Zoho order-created workflow read-only before any change. Do not replace or modify it without the required HU+DI review.
- Provider mocks/simulations are not evidence of live connectivity. Keep Shiprocket WhatsApp notifications enabled and preserve both Zoho and EKI order references.

### 3.10 Platform-specific exclusions vs future capability
- A capability missing from Django is not itself a conflict. Adapt useful intent to the approved architecture.
- Do not implement wishlist, reviews/recommendations, server-side cart, or related-product links from this plan; the agent explicitly labelled them out of scope without a decision.
- Preserve explicit NOs in the ledger. In particular: COD, customer cancellation/editing after placement, refund/return/store-credit execution, inventory authority in Django, Shopify Flow-specific builder/history, Shopify AI assistant/Sidekick, command palette, setup-guide promotions, multi-store switcher, Shopify Network Intelligence, Razorpay Magic Checkout, and other specifically recorded NO rows.
- Where a feature was previously labelled REJECT/DEFER only as a recommendation but Hu later answered YES, preserve that later YES intent and implement an EffyKlean-appropriate version subject to the rules above.

### 3.11 Reconciliation against the master evidence register

The master register's 7.7 conflict list is useful evidence, but its “conflict flagged” status is not automatically a live business conflict after applying later HU+DI resolutions. The implementation plan adopts these reconciliations:

- **MA-ORD-010 and MA-ORD-011 (sales-channel and delivery-method columns): DEFER, not NO.** The master correctly records the 10-Oct HU+DI decision overriding the comparison's earlier REJECT recommendation. Keep these out of the first release unless they become necessary to a frozen acceptance criterion; do not mark them permanently rejected.
- **MA-ORD-067 and MA-ORD-068 (line-item / price edits): NO for post-placement line-item, quantity, price or discount edits.** The existence of the route orders/<ref>/edit is implementation evidence, not proof that these capabilities are authorised. Inspect the route read-only to determine whether it only supports allowed correction of delivery/contact details. Do not expand it into order commercial edits.
- **MF-026 / MA-PRD-067 (related-product links): NO for this plan.** The prior agent explicitly identified related-product links as out of scope without a decision; the existence of rendered code does not authorise new work. Preserve existing code only if removing it is not separately required; do not add/extend this capability.
- **MF-054 (GST calculation): the master correctly flags a SPEC-vs-arithmetic concern.** Apply the frozen SPEC and the agreed tax-inclusive pricing, HSN and intra-/inter-state rules; do not silently alter the tax base based on customary arithmetic. The agent must expose the exact formula, affected code/tests and a worked example as evidence. If the frozen SPEC's tax-base wording genuinely conflicts with the agreed business rule, stop that change and report the exact discrepancy for HU+DI decision; do not guess.
- **MF-070 (dispatch/tracking):** the accepted business rule is no dispatch before verified payment. Admin may record fulfilment/tracking; tracking may be blank for pickup, and a carrier status may be shown only when verified. Reconcile the dispatch code to these cases and the frozen ACs; do not require a fabricated tracking reference for pickup. If a frozen AC unambiguously requires tracking for every dispatch, report that exact contradiction before changing it.
- **MF-106 / MF-064 / MA-DRF-* (assisted/draft orders): YES in EffyKlean's business form.** Frozen SPEC §27.3 and §12.11 require admin-assisted orders and bank-transfer/UPI verification. Implement controlled distributor/Bulk enquiry, quote, approval and order creation; Shopify-style draft-order mechanics and custom non-catalogue lines are not automatically required.
- **MA-ANA-019 (customer-visible Bulk savings): YES.** Preserve transparent Bulk savings/customer-facing commercial information consistent with the agreed negotiated Bulk pricing model. Do not infer distributor quantity slabs or a separate Household/Bulk combo collection from this.
- **ORD-145 / MA-ORD-145:** evidence-only. The menu was not opened in the master evidence run. Read-only inspection is allowed; implementation of unknown actions is not.
- **Master statuses generally:** NO ACTION, VALIDATE, BLOCKED-DEC, REJECT/OOS, IMPLEMENT and FIX are work/evidence dispositions, not the HU capability vote. Validate implementation state before coding to avoid duplicating existing work, but do not use a master disposition to reverse an explicit HU YES/NO.


## 4. Prioritised implementation plan — phase by phase

The phases below combine the agent's pending tasks with the Admin capability areas. The capability ledger contains broad feature scope; the agent report identifies the immediate technical backlog. **All tasks listed in the agent's pending-task response are YES.** The task identifiers are retained as reported. Phase order is the implementation priority, aligned to HU's stated workstream priority: (1) Admin and integrations, (2) storefront functionality, (3) customer communication and updates, (4) beautification. Explicit release blockers must still be surfaced even when they occur in a later workstream.

### Phase 0 — Baseline, evidence and plan reconciliation (P0 — first)
**YES — implement/complete**
- **A-02:** Review and record current uncommitted-work baseline; preserve every existing change.
- **A-04:** Review the change set and commit the reviewed baseline only when commit authorisation is appropriate; then rerun the full suite on the committed tree. Never discard/overwrite work.
- **J-10:** Work through the release gate, record each unmet criterion and its evidence.
- Reconcile this plan to `docs/foundation/PRODUCTION_READINESS_REGISTER.md`, keeping exact agent IDs and mapping every task to a phase.
- Record current branch, HEAD, working-tree state, migration state and current test results from the agent's actual repository evidence. The previously reported 1,819-test pass was on an earlier tree and is not current evidence.
- Resolve count limitations for the 494-row capability catalogue by auditing every source row against recorded HU answers; do not invent answers.
**Exit evidence:** preserved baseline, fresh tests on a clearly identified tree, reconciled task register, exact row-count audit and release-blocker list.

### Phase 1 — Admin and integration foundations; credential-free engineering (P0)
**YES — implement**
- **B-14:** Shared Zoho Payments token cache.
- **J-03:** Scheduler definition for `run_outbox`, reconciliation and `dispatch_orders`.
- **J-02:** Storefront header/CSRF implementation aligned to approved security architecture.
- **A-05:** CI workflow calls `scripts/ci.sh`.
- **A-03:** Map acceptance criteria to tests.
- **F-01:** Combo-discount regression tests.
- **J-08:** Loading-time baseline.
- **E-07:** Responsive checks rerun and results recorded.
- **Development migration:** review and safely apply/validate the reported `orders.0022` migration against the development database.
- Implement relevant YES Admin capabilities in the order of operational value: audit trail/export; integration readiness, webhook log, reconciliation queue and outbox/worker visibility; Zoho mapping/sync health; read-only Zoho Flow visibility; staff security and permissions; order/customer/product administration; home alerts/search/recents; reports only when source data is reliable.
**Exit evidence:** automated tests, lint/framework checks, migration validation, responsive/load baselines, security/permission tests, and updated project log.

### Phase 2 — Local end-to-end order journey with stubs (P0)
**YES — implement and test before deployment**
Build one repeatable local journey using one or two products and provider stubs/mocks:
- Product/SKU selection, order lines, pricing and discount calculation.
- Checkout and order creation.
- Stub payment session; success, failure, interrupted/abandoned checkout.
- Webhook validation, amount/currency/order-reference checks, duplicate/replay idempotency and reconciliation.
- Enforce **NO PAYMENT → NO DISPATCH** in every relevant transition.
- Inventory read/order handoff boundary with Zoho stub where needed.
- Shipping handoff and tracking/status return boundary with Shiprocket stub.
- Customer-facing order/payment status and notification events.
- Failure paths and audit trail.
**Exit evidence:** repeatable automated E2E on the approved local PostgreSQL setup; success/failure tests; no real provider write or dispatch in stub tests; limitations recorded.

### Phase 3 — Zoho Payments and Zoho Inventory sandbox proof (P0)
**YES — implement and verify**
- **B-01:** Zoho Payments sandbox session flow.
- **B-02:** Payment webhook flow.
- **B-05:** Zoho Inventory stock-read flow.
- **B-06:** Zoho Inventory Sales Order creation.
- **B-11:** Verify Sales Order total equals the amount successfully paid.
- Use one TESTCODE order. Obtain the required Zoho test organisation and OAuth credentials through safe channels; missing access is a dependency, not a NO.
- Verify references, amount/currency, webhook validation, duplicate-event handling, payment state and reconciliation.
- Zoho Payments is the intended provider. Do not introduce new Razorpay dependencies or perform a live cutover during sandbox proof.
**Exit evidence:** sandbox result identifiers and outcomes, verified payment/Sales Order total consistency, no unapproved production writes.

### Phase 4 — Zoho tax/customer mappings and Shiprocket fulfilment (P0)
**YES — implement and verify**
- **B-07:** GST/tax/invoice mapping.
- **B-08:** Customer mapping to Zoho contacts.
- **B-16:** HSN/tax mapping and validation, retrieving the previously documented common HSN rather than guessing.
- **C-01:** Zoho → Shiprocket handoff; replace the current adapter refusal with approved tested behaviour.
- **C-02:** Shipment tracking/status return path.
- **C-04:** Establish weight/dimension master and data ownership. Reuse canonical product dimensions if sufficient; do not create duplicate ownership without evidence.
- **C-05:** Pickup mapping for the existing operating locations.
- Inspect the existing Zoho Flow and prove it does not conflict with EffyKlean writes; protect it and do not change it without HU+DI review.
- Verify stock sync on change plus hourly reconciliation/fallback, retries, idempotency, stale-data visibility and low-stock alerts before calling it live.
**Exit evidence:** documented mappings, sandbox tests, no duplicate/conflicting order writes, verified stock source, shipment/tracking proof.

### Phase 5 — Storefront and customer-facing functionality (P1)
**YES — implement**
- **D-06:** Correct customer-facing GST amounts.
- **D-07:** Invoice generation/delivery behaviour.
- **D-09:** Specified customer-facing order/payment experience.
- **B-13:** Associated customer-facing payment/order capability.
- **H-05:** Contact Form, including privacy wording, retention and email-provider requirements.
- **H-06:** Subscribe capability, including privacy wording, retention and email-provider requirements.
- **E-08 / DC-22 / DC-25:** Move old-site hot-linked videos to approved storage and complete associated media requirements.
- **D-08:** Replacement video-upload storage and retention.
- **G-03:** Bank-transfer/UPI assisted orders, with payment verification and audit guardrails.
- **G-04:** Distributor GST handling during Zoho outage without guessing tax data or bypassing approved controls.
- **I-03:** Low-stock view using real Zoho stock read.
- **I-04:** Analytics with cookie-consent behaviour.
- Implement relevant YES storefront capabilities: SKU-centric catalogue, agreed combo pricing, distributor/Bulk enquiry and quote flows, content/SEO/media, safe content publishing, customer account/history features, and consent-aware messaging. Preserve all NO decisions and existing business rules.
- **Refund-handling agent item — YES as a policy/guardrail task:** implement and test the agreed **no-refunds/no-returns** baseline, including blocking refund/return/store-credit execution and keeping replacement cases separate. The agent's generic “manual or automated refund” wording does not override the explicit HU+DI no-refunds/no-returns decision. Do not implement a refund execution workflow unless Hu explicitly changes that business decision.
**Exit evidence:** customer-visible values and invoices tested, privacy/retention and consent requirements documented, media migrated, order/payment safety preserved.

### Phase 6 — Customer communications and updates (P1)
**YES — implement**
- **N1–N11:** Implement transactional email requirements; choose/configure the provider, sender domain and approved wording as required.
- Implement agreed email/WhatsApp order/payment/dispatch updates where applicable; preserve Shiprocket WhatsApp notifications.
- Do not default to SMS or send to a channel without the appropriate consent.
- Add staff/customer notifications only when event source, provider, wording and delivery status are verified.
**Exit evidence:** provider/sender verification, tested message templates and event triggers, failure/retry behaviour, consent checks and no secrets in Git.

### Phase 7 — Hosting preparation, security and operational readiness (P1 release blockers)
**YES — prepare and verify; actual public deployment remains separately gated**
- **J-01 to J-07:** Complete the infrastructure requirements exactly as mapped in the readiness register, including hosting preparation, HTTPS/HSTS, scheduler operations, secrets management, monitoring/alerts, backups/restore drill and required migration readiness.
- **J-10:** Re-check release gate against evidence.
- Use approved architecture: DigitalOcean preferred, App Platform + Managed PostgreSQL preferred; no AWS. Keep production secrets out of the repository.
- Confirm operational scheduler behaviour for `run_outbox`, reconciliation and `dispatch_orders`; verify monitoring and alerts; perform a backup restore drill.
- Validate migrations safely. Confirm hosting, production cutover and public launch authorisation separately before acting.
**Exit evidence:** security/operations verified, scheduler proven, restore drill complete, migration validation, monitoring checks and evidence-based release-gate decision.

### Phase 8 — Remaining YES Admin capability catalogue, future growth and visual refinement (P2, after safety-critical paths)
**YES where the ledger records YES; do not turn recommendations into NOs**
- Complete remaining accepted Admin capabilities by category: Orders/fulfilment (ORD); Draft orders (DRF); Products/catalogue (PRD); Collections/stock visibility (COL/INV); Customers/distributor accounts (CUS); Discounts/combos (DSC); Gift cards/liability reporting (GFT); Content/media (CNT); Marketing (MKT); Channels/POS (CHN); Analytics (ANA); Settings (SET); Integrations/automation (INT); Staff/security (USR); System shell/search/notifications (SYS).
- Prioritise within each category using operational risk, customer impact, dependency readiness and implementation effort. Keep exact source IDs and statuses in the register.
- Treat campaigns, social/marketplace channels, gift cards, advanced segmentation, advanced reports, languages and other future growth features as accepted scope where YES was recorded, but sequence them after order/payment/stock/shipping safety and data-provider readiness.
- Implement visual polish/beautification only after the core journey, Admin controls, integrations and customer updates have evidence of working correctly.
**Exit evidence:** each YES capability has a phase, task owner/status, acceptance criteria, dependencies and validation evidence. No capability is silently dropped because it was recommended as DEFER/REJECT in an older comparison when the later HU decision was YES.

## 5. Agent tasks — complete checklist and status rule

All of the following are **YES**. Their phase is shown above; this checklist ensures none are lost during consolidation.

| Agent task / identifier | Decision | Phase |
|---|---|---|
| A-02 baseline review and preservation | YES | 0 |
| A-04 reviewed baseline commit + full suite on committed tree | YES | 0 |
| J-10 release gate | YES | 0, 7 |
| B-14 shared Zoho Payments token cache | YES | 1 |
| J-03 scheduler definition | YES | 1, 7 |
| J-02 storefront header/CSRF | YES | 1 |
| A-05 CI workflow calling scripts/ci.sh | YES | 1 |
| A-03 acceptance criteria mapped to tests | YES | 1 |
| F-01 combo discount regression test | YES | 1 |
| J-08 loading-time baseline | YES | 1 |
| E-07 responsive checks | YES | 1 |
| orders.0022 development migration validation | YES | 1, 7 |
| Local one/two-product E2E using provider stubs | YES | 2 |
| B-01 Zoho Payments sandbox session | YES | 3 |
| B-02 payment webhook proof | YES | 3 |
| B-05 Zoho stock read | YES | 3 |
| B-06 Zoho Sales Order create | YES | 3 |
| B-11 paid amount equals Sales Order total | YES | 3 |
| B-07 GST/tax/invoice mapping | YES | 4 |
| B-08 Zoho contact/customer mapping | YES | 4 |
| B-16 HSN/tax mapping | YES | 4 |
| C-01 Zoho-to-Shiprocket handoff | YES | 4 |
| C-02 tracking/status return path | YES | 4 |
| C-04 weight/dimension master | YES | 4 |
| C-05 pickup mapping | YES | 4 |
| D-06 customer-facing GST amounts | YES | 5 |
| D-07 invoice generation/delivery | YES | 5 |
| D-09 customer-facing order/payment experience | YES | 5 |
| B-13 related customer-facing payment/order capability | YES | 5 |
| Refund-handling item as no-refund policy/guardrail enforcement | YES | 5 |
| N1–N11 transactional email requirements | YES | 6 |
| H-05 Contact Form | YES | 5 |
| H-06 Subscribe | YES | 5 |
| E-08 old-site video migration | YES | 5 |
| DC-22/DC-25 related media requirements | YES | 5 |
| D-08 replacement-video storage/retention | YES | 5 |
| G-03 bank-transfer/UPI assisted orders | YES | 5 |
| G-04 distributor GST during Zoho outage | YES | 5 |
| I-03 low-stock view backed by real Zoho stock | YES | 5 |
| I-04 analytics with cookie consent | YES | 5 |
| J-01 to J-07 infrastructure requirements (exact mapping from register) | YES | 7 |
| Four agent-listed “out of scope without a decision” items: wishlist, reviews/recommendations, server-side cart, related-product links | NO / excluded from this plan | Excluded |

## 6. Final NO implementation decisions and explicit exclusions

The final NO implementation IDs after applying the recovered answers and conflict resolutions are listed below. These are final implementation dispositions, not merely the source comparison's older REJECT/DEFER recommendations.

- **Orders (23):** ORD-019, ORD-064, ORD-067, ORD-069, ORD-070, ORD-071, ORD-073, ORD-074, ORD-075, ORD-076, ORD-086, ORD-087, ORD-092, ORD-103, ORD-105, ORD-112, ORD-116, ORD-121, ORD-136, ORD-138, ORD-139, ORD-140, ORD-144.
- **Draft orders (1):** DRF-008.
- **Products (3):** PRD-005 (vendor filter), PRD-042 (vendor field), PRD-060 (video/3D product media). Separate old-site/how-to video migration tasks E-08/DC-22/DC-25/D-08 remain YES; they are not this product-media feature.
- **Collections (1):** COL-007 (separate combo collections). Combo pricing/grouping remains supported without separate Household/Bulk combo collections.
- **Settings (6):** SET-008 (COD), SET-013 (customer self-service returns/store credit), SET-050 (transfer/move store to organisation/external owner), SET-058 (Shopify Network Intelligence), SET-070 (COD customisation), SET-071 (Razorpay Magic Checkout).
- **Integrations (6):** INT-007 (Shopify app store/marketplace), INT-008 (Shopify custom/private apps and API tokens), INT-009 (Shopify Flow), INT-020 (Shopify-template marketing workflows), INT-021 (Shopify Flow tags/run/version history), INT-023 (Shopify app row menu). These NOs do not prohibit separate, approved EffyKlean integration and automation capabilities.
- **Staff/security (6):** USR-006 (granular custom per-area permission builder), USR-012 (collaborator accounts), USR-022 (staff access-request tab), USR-023 (POS app-only users), USR-030 (Shopify-style custom role builder), USR-031 (Shopify-style role permission catalogue).
- **System shell (4):** SYS-004 (command palette/keyboard shortcuts), SYS-009 (setup-guide promotions), SYS-010 (Shopify AI assistant/Sidekick), SYS-013 (multi-store switcher).

**Count:** 50 NO implementation decisions. ORD-145 is not included because its menu was not observed and it is an evidence-only placeholder, not a settled capability decision. Do not infer a decision from the source comparison's older recommendation column.

## 7. Dependencies, release gates and safeguards

- Zoho Payments and Zoho Inventory sandbox access/OAuth credentials are required for Phase 3; never commit credentials.
- Provider proof is mandatory before describing an integration as operational. Stubs prove local contract behaviour, not live provider connectivity.
- Existing Zoho Flow must be inspected before changes; existing Zoho–Shiprocket integration and pickup/location mapping must be verified.
- GST/HSN and customer mapping must be validated; do not guess the HSN or use taxonomy as tax engine.
- Contact/Subscribe privacy wording, retention, email provider and sender domain must be settled as part of those YES tasks; legal wording must be approved, not invented.
- Refund/return execution remains NO under the current rule; implement the guardrail unless Hu explicitly changes the policy.
- HTTPS/HSTS, secrets, monitoring, alerts, backups/restore, migrations, scheduler and the full release gate are launch blockers.
- Do not deploy or perform public launch as a side effect of this plan. Public deployment remains subject to separate authorisation.

## 8. Execution governance and definition of complete

- Update `PROJECT_LOG.md`, the readiness register and this plan at phase checkpoints, recording IDs, status, evidence, test command/result, dependencies and remaining blockers.
- Use exact IDs; do not omit a task while reorganising it. Mark statuses as NOT STARTED / IN PROGRESS / BLOCKED / VERIFIED only with evidence.
- Preserve all uncommitted work. Never use `git add -A`; do not reset, clean, stash or overwrite work to make the tree look clean.
- No commit/push, live provider writes, production cutover or deployment without the appropriate authorisation.
- Complete phases in priority order. Continue independent safe work while a specific dependency is blocked.
- A phase is complete only when its exit evidence is recorded and validated by the local agent. The plan is complete when all YES tasks have been implemented/tested, all explicitly NO capabilities remain excluded, every one of the 494 capability rows has a traceable decision basis without guessed answers, and release-gate evidence is complete.

## 9. HU review items

1. Confirm that this is the single consolidated review document to use for phase-wise planning, with the capability ledger and conflict analysis retained as source records rather than competing implementation roadmaps.
2. Review the 122-row reconciliation audit and the corrected count-status note. Do not treat 443 YES / 50 NO / 1 evidence-only as final until the row-level decision evidence has been traced as described in Section 2.
3. Confirm the proposed priority order: baseline/evidence → Admin/integration foundations → local E2E → Zoho sandbox → mappings/shipping → storefront/customer experience → communications → infrastructure/release → remaining YES capabilities/beautification.
4. Confirm that the refund-handling agent task is treated as **YES to implement and enforce the agreed no-refunds/no-returns policy**, not as authorisation to build a refund execution workflow.
