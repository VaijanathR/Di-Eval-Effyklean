# HU response recovery register — 23 October 2026

## Purpose and rule

This file is a recovery/index record for Hu's prior answers and decisions so they are not lost when preparing the next EffyKlean coding-agent instruction set. It is a working reconciliation record, not a claim that every historical chat utterance has already been audited exhaustively.

**Do not ask Hu to repeat a response already recorded in this file or its linked source records.** If an answer is absent, search the relevant conversation history and existing public project records before asking anything. Never infer a missing decision. Preserve the exact scope/conditions of an answer; keep scope disposition, implementation status, technical evidence, provider readiness, legal review, and authorization distinct.

## Primary source records recovered and checked

1. `HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md` — consolidated decisions 1–13 and prior answers.
2. `BUILD245_HUDI_DECISIONS_RECONCILIATION_2026-10-23.md` — reconciled settled rules, dependencies, exclusions and safeguards.
3. `BUILD245_DECISIONS_RECONCILED_LEDGER_2026-10-23.csv` — row-level BUILD245 reconciliation.
4. `HUDI_DISPOSITION_DECISIONS_2026-10-22.md` — 22-Oct decision-batch annotations and recovered prior answers; the 76 annotated rows are not 76 new decisions.
5. `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md` — historical generated question list only; superseded for generating new questions by the reconciliation overlay.
6. `BUILD245_IMPLEMENTATION_RECORD_2026-10-22.md` and `BUILD245_LEDGER_2026-10-22.csv` — implementation evidence/status, separate from Hu's decisions.
7. `AgntGapAnalysis/GAP_ASSESSMENT_211020261727.md` and the original gap-analysis/implementation-plan records — scope/gap/task background, not substitutes for direct Hu answers.

## Recovered, binding decisions and clarifications

### Product lifecycle, publishing and URLs
- Product lifecycle approved: Draft, Active, Unlisted (direct-link only), Archived. Do not add Suspended absent a concrete evidenced need. Preserve order/history; authorised staff action required.
- Scheduled time never publishes automatically. A product may be published only after required approval is complete and an authorised Admin or Director manually publishes. If approval is incomplete or staff forget, it stays unpublished after the scheduled time. Do not bypass authorisation, approval or verified-commercial-data gates.
- Product IDs are the fixed URL identity: `/products/<id>/`. Editable slugs, slug-editing UI and slug-change redirects are out of scope.
- No bulk product deletion; archive/unpublish is safer. Product lifecycle decision does not authorise implementation by itself.

### Commercial data and catalogue integrity
- MA-PRD-047: unverified/provisional MRP, concentrate information, or Zoho data/mapping must not be published or used to calculate/display savings. Fail closed until verified; a warning-only marker is insufficient.
- Exact verified source/field for concentrate remains a technical/spec follow-up; do not invent the source or re-ask the settled no-provisional-data rule.
- Products are physical shipped products; do not add non-shipping products without an evidenced use case.
- No platform-to-platform imports; do not silently expand existing CSV import scope.

### Gift cards, customer records and tax
- Gift cards excluded/deferred; only reconsider with explicit HU+DI reopening and accountant-approved written terms.
- Customer/order-history deletion approved for authenticated Admin/Director only. Anonymisation not approved for implementation. Customer-record merging remains unapproved/out of scope.
- Deletion must define the exact data affected and preserve legally required tax/accounting records, active-order integrity and audit evidence; privileged actions must be logged. MF-089 contact-form retention (180 days) is separate.
- Tax-exemption controls approved for authenticated Admin/Director only, with role-based access and audit evidence (who/when and reason/evidence as applicable); no non-compliant exemptions.
- GST is inclusive. GST Number + Name leads to a Zoho GST invoice only if the pair is valid; otherwise consumer treatment. Do not invent exemptions; accountant-approved rules are required for exceptions.
- Customer address decision already recorded: one saved address, three-month retention and active-order protection; multiple saved addresses are parked.

### Marketing, channels, analytics and communication
- Marketing/channel capabilities are in scope, not blanket future features. WhatsApp marketing is through Meta, not directly through EffyKlean Admin. EffyKlean should provide secure configuration/credential settings for supported integrations.
- Scope approval does not itself authorise live provider connections, credentials, campaigns, messages or privacy-sensitive tracking. Secrets must not be exposed in UI/logs/responses; respect consent, data flows, customer-data sharing, wording, ownership and cost. Transactional WhatsApp is distinct from WhatsApp marketing.
- AD-15 analytics/reporting approved; operational reports use authoritative PostgreSQL/application data. Previously approved CUS groups CUS-001–033, 040–045, 050–056 remain YES, including segmentation filters, counts, marketing use, natural-language builder, actions and CSV import.
- MF-093 optional visitor/session/conversion/behaviour analytics and tracking-dependent events remain LATER until consent, privacy notice, retention and access controls are approved and implemented. No pixels just to reproduce Shopify dashboards.
- English-first until verified translations are supplied; do not ask again about language. SMS excluded; email/WhatsApp are preferred. This is channel preference only, not approval of providers, campaign wording, credentials or sends. Marketing consent must be explicit.
- Notifications/marketing must not create a second notification engine; specific wording/provider/credential/consent approvals remain separate dependencies.
- MA-ORD-111 scope is abandoned-checkout recovery through a Zoho-managed notification approach, not a separate website email engine.

### Discounts, prices and subscriptions
- Combo rule: first qualifying item has no combo discount; later qualifying items receive it; if first is removed, next becomes first. Evaluate oldest-created first; qualifying quantities cannot be reused.
- Coupon/promotion feature approved with optional one-use-per-customer limit and optional eligibility restrictions (all customers, new customers, specific customers/approved segments). Configurable per offer, not mandatory for every offer.
- B2C may use combo discount OR a valid company promotion/coupon, not both; only one additional discount on a sale price. Distributor pricing remains product-specific with optional quantity discounts and no combo offers.
- Public quantity price breaks are in scope. A price tier for the qualifying quantity is not an extra discount stacked with combo/coupon/another discount. Distributor slabs are separate.
- “Subscribe” means EffyKlean updates/communications, with applicable consent/preferences/unsubscribe; it does not mean recurring product orders or payments. MA-PRD-070 recurring product selling plans remain separate and are not approved by the updates-subscription answer.

### Content, forms, search, chat and package features
- Prior YES answers for site preferences, storefront search settings/filters, forms builder, customer-facing chat/chatbot and MA-PRD-105 package/shipping feature stand. Specifically the newer ledger records YES for MA-CNT-008/015/016/019/020 and MA-PRD-105. Do not ask scope again or silently convert to EXCLUDE.
- These do not authorise cloning Shopify theme builder or selecting Tidio by assumption. Blog comments need moderation/privacy; forms must preserve MF-089 privacy/retention fail-closed requirements; search must use grounded catalogue filters/settings without invented ranking; chat provider/escalation/hours/consent/data/promises need specific definition before connection/launch.
- MA-PRD-105 package feature does not override LATER MA-PRD-036/037, DC-19 or approve a competing carrier workflow. Zoho/Shiprocket remains the approved shipping workflow.
- Shopify plan/billing, theme editor/code/Liquid, app previews and other Shopify-only mechanics are not direct EffyKlean requirements unless an existing approved need maps to a native Django feature. DNS/domain changes are restricted hosting/security actions, not ordinary Admin settings.
- Safe business content (e.g. contact details/brand assets) may be editable through audited Admin controls. Do not expose frozen payment, checkout/GST/tax rules, checkout requirements, shipping rates/authority, Zoho-owned locations/data, or domains/DNS as ordinary editable settings. Customer-account settings must preserve approved access rules; no self-service returns/store credit. Any additional editable field needs individual HU+DI approval.

### Inventory, orders, payments, invoices and shipping
- Zoho Inventory remains stock/purchasing/supplier authority. Inventory adjustments/history, reservations, locations, purchase orders, transfers, suppliers, bins and related stock operations stay in Zoho; no competing local stock master. Inventory import authority remains Zoho. Do not repeat completed general sandbox/OAuth checks. Narrow per-location reads/exports are specific evidence tasks only if not yet evidenced.
- Zoho Inventory sandbox is working and Hu says it is integrated with Shiprocket sandbox. Treat as completed/known; do not revive old blocked assumptions.
- Zoho Payments sandbox is working per Hu. This is not production readiness or permission for live writes.
- Frozen payment rules: no COD, no partial payment, no Razorpay/alternative gateway fallback; website paid state only after Zoho verification; NO PAYMENT → NO DISPATCH.
- Manual mark-as-paid only after staff verifies payment in Zoho; full payment only. Payment links apply to manually entered orders only, not general website orders.
- Zoho owns invoicing and the existing Zoho-managed Shiprocket workflow. Do not add a second invoice writer, notification engine, carrier-label writer or fulfilment/location master.
- MA-ORD-103 and MA-ORD-105 are NO/EXCLUDE from current scope (bulk fulfil/create-labels and bulk cancellation) while implementation status remains DEFERRED/not implemented.
- MA-ORD-080/084 direction is status visibility/sync and constrained fallback for manually entered orders, not a parallel fulfilment system. MA-ORD-141 BUILD is limited to its approved single action and existing Flow safeguards; no unreviewed Flow writes.
- Existing operational facts: two Karnataka POS and one Maharashtra delivery centre; WhatsApp notifications enabled; Zoho order number and EKI website order number tracked; SHP-00011/00012 are junk. Do not introduce a competing carrier workflow. Razorpay is historical only.

### Other recovered scope/disposition decisions
- Shopify Flow and Zoho logic are relevant; ignore Shopify Billing, Growth, Shopify Razorpay settings, Magic Checkout, Theme editor/code.
- Zoho Flow immediately transfers Shopify-created order details into Zoho Inventory Order/Sales Order so staff can view/act; exact mapping was deliberately parked for later rather than blocking other work.
- MF-008: Hu confirmed EffyKlean distributor enquiry is already implemented and is a form; independent runtime verification is separate.
- MF-009: evidence-only; competitor/reference observations alone do not create scope.
- MF-050: investigate signed-in cross-device cart persistence before disposition; not blanket BUILD approval.
- MA-ORD-037: continue INVESTIGATE; no BUILD authorization.
- MA-ORD-040: EXCLUDE source/referral attribution.
- MA-ORD-077: BUILD manual mark-as-paid only after Zoho verification; full payment only.
- MA-ORD-079: BUILD payment link for manually entered orders only; full payment only.
- MA-USR-020 is composite: active staff list covered; POS-app-only and Requests-tab functions were excluded. Preserve the source ID and separate components; do not ask a blanket question.
- MA-ORD-103/105 remain excluded despite deferred implementation status.
- Marketing/channels and customer-segmentation scope decisions must be read with the detailed shortlist and reconciliation overlay, not inferred from old Shopify comparison labels.

### Governance and process instructions from Hu
- Read existing EffyKlean context and public GitHub records before asking Hu to repeat anything.
- Do not delegate to a coding agent unless Hu explicitly authorises it.
- Use STOP → REPORT → HU+DI DECIDE for frozen architecture/spec conflicts, new decisions, business ambiguity or authorization/risk issues.
- Agent instructions should be concise and task-focused (task + constraints + expected report); don't offload instruction quality to agent.
- If agent delegation is authorised, completion audit must map every plan/spec item to DONE (verified)/PARTIAL/NOT DONE/DEFERRED with command output or file-line evidence, and list shortcuts/stubs/placeholders/TODO/pass/test weakening/swallowed errors/out-of-scope claims.
- Stage only explicit paths; never `git add -A`; no commit co-author trailers. Keep PROJECT_LOG.md, CLAUDE.md, README and status register updated before clearing context. Keep .claude session log private/out of Git.
- Risk-based sufficient testing; no expensive full-suite rerun after narrow fixes unless a meaningful gate warrants it.
- Hosting is preferred on DigitalOcean App Platform + Managed PostgreSQL; hosting setup was parked until the other work is ready. Hu wants it completed after the agent's other tasks, but no agent delegation or live deploy is authorised by this preference alone.
- Preserve original sources and history; don't overwrite historical records to make them look current.

## Current decision shortlist (source-of-truth pointers)

The 23-Oct shortlist contains the detailed approvals for:
1. product lifecycle/publishing;
2. gift cards;
3. customer/order-history deletion vs anonymisation/merging;
4. tax-exemption controls;
5. marketing/channels/pixels/social/AI commerce;
6. analytics and customer segmentation;
7. coupon/promotion restrictions and discount precedence;
8. public quantity price breaks and meaning of “Subscribe”;
9. content/forms/search/chat/package features;
10. safe Admin-editable settings;
11. channel semantics and staff-entered orders;
12. fixed product-ID URLs;
13. manual-only scheduled publication.

Use the linked shortlist for the full detailed decision wording; this recovery file does not replace the row-level ledgers or frozen specification.

## Coverage status — be honest

- **Recovered and indexed:** decisions above, the 22-Oct disposition log, the 23-Oct reconciliation overlay, the latest ledger changes, and prior context explicitly retained in conversation memory.
- **Not yet claimed exhaustive:** every individual message/answer across all prior chat threads has not been checked one-by-one against every relevant row in the 597-row register and canonical 122-capability master. This must be done before claiming complete response coverage or issuing the next coding-agent instruction set.
- **Next reconciliation step:** compare the actual prior HU replies in the gap-analysis/decision threads against the shortlist, the 22-Oct decision log, canonical 122-capability master, the row-level 597-item disposition history and the 245-row ledger. Record each distinct HU response with its requirement ID(s), answer/condition, source conversation/date when known, target public record, and verification status. Use `SOURCE FOUND / RECORDED AND VERIFIED / MISSING FROM RECORD / AMBIGUOUS — DO NOT GUESS` as statuses. Never fabricate exact timestamps or verbatim quotes.
