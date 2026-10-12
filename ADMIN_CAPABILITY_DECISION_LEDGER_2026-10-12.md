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
