## Authoritative row-level status correction — 23 October 2026

This note supersedes any conflicting aggregate totals or “unreconciled” claims elsewhere in this file. The current fetched source files have been compared by unique ID.

- **597-ID register:** 597 rows / 597 unique IDs. Current dispositions: **340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER, 14 INVESTIGATE** (597 total).
- **245-ID implementation ledger:** 245 rows / 245 unique IDs. Implementation outcomes: **83 DONE (verified), 62 PARTIAL, 100 DEFERRED** (245 total). Current dispositions within those 245 IDs: **83 Implemented, 141 BUILD, 13 LATER, 8 EXCLUDE** (245 total).
- All 83 verified DONE rows remain promoted to Implemented. Exact-ID comparison: every one of the 245 ledger IDs exists in the 597 register; **zero disposition mismatches**. The 597 response crosswalk also matches the 597 register by ID and current disposition.
- The earlier “163 pending” figure is not current: 62 PARTIAL + 100 DEFERRED = **162**. Of these, **141 are current BUILD** (61 PARTIAL + 80 DEFERRED); **21 are not BUILD** (1 PARTIAL and 12 DEFERRED are LATER; 8 DEFERRED are EXCLUDE).
- **Coverage gap before implementation handoff:** 11 additional IDs are marked BUILD in the 597 register but are not in the 245-row implementation ledger: MF-070, MF-071, MF-074, MF-078, MF-092, MF-107, MF-109, MF-114, MA-ORD-068, MA-DSC-023 and MA-SET-061. They need explicit ledger coverage; do not assume implementation status or evidence.
- MF-055 policy is approved and recorded; it remains PARTIAL / BUILD pending implementation and scoped sandbox validation. MF-084 legal wording still needs Hu/legal confirmation; MF-094 needs source/spec parity investigation before any narrow question; MF-115 is a release evidence gate, not a new policy question. These are distinct from the 83 already implemented.

Historical totals below are retained only as historical record and must not be used as current status.

---

# HU response recovery register — 23 October 2026

## Purpose and rule

This file is a recovery/index record for Hu's prior answers and decisions so they are not lost when preparing the next EffyKlean coding-agent instruction set. It is a working reconciliation record, not a claim that every historical chat utterance has already been audited exhaustively.

**Do not ask Hu to repeat a response already recorded in this file or its linked source records.** If an answer is absent, search the relevant conversation history and existing public project records before asking anything. Never infer a missing decision. Preserve the exact scope/conditions of an answer; keep scope disposition, implementation status, technical evidence, provider readiness, legal review, and authorization distinct.

## Primary source records recovered and checked

1. `HUDI Discussion/HuDI Conversation 17-part2.md` — read from beginning to end and reconciled response-by-response in the source-specific audit below. This source is now covered; that does not imply all earlier chat threads have been audited.
2. `HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md` — consolidated decisions 1–13 and prior answers.
3. `BUILD245_HUDI_DECISIONS_RECONCILIATION_2026-10-23.md` — reconciled settled rules, dependencies, exclusions and safeguards.
4. `BUILD245_DECISIONS_RECONCILED_LEDGER_2026-10-23.csv` — row-level BUILD245 reconciliation.
5. `HUDI_DISPOSITION_DECISIONS_2026-10-22.md` — 22-Oct decision-batch annotations and recovered prior answers; the 76 annotated rows are not 76 new decisions.
6. `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md` — historical generated question list only; superseded for generating new questions by the reconciliation overlay.
7. `BUILD245_IMPLEMENTATION_RECORD_2026-10-22.md` and `BUILD245_LEDGER_2026-10-22.csv` — implementation evidence/status, separate from Hu's decisions.
8. `AgntGapAnalysis/GAP_ASSESSMENT_211020261727.md` and the original gap-analysis/implementation-plan records — scope/gap/task background, not substitutes for direct Hu answers.

## Recovered, binding decisions and clarifications

### MF-055 — website-to-Zoho customer synchronization (HU approval, 23-Oct-2026)

**HU decision (23-Oct-2026): APPROVED.** The website is the source of truth for customer identity and details; Zoho is the synchronized downstream contact record in this workflow.

- When the first order is created, send the website customer's details to the corresponding Zoho contact, creating or updating the contact as required.
- When an authorised/manual customer-detail change is made on the website, synchronize the changed details to that customer's mapped Zoho contact.
- Maintain a reliable website-customer-to-Zoho-contact identity mapping. Prevent duplicate creation and never associate unrelated customers with one another or a shared generic contact.
- If synchronization fails or the mapping is missing/ambiguous, record the failure and resolve it safely; never guess or silently link the wrong contact.
- The approval settles the business policy only. MF-055 remains PARTIAL / BUILD until the implementation and appropriately scoped sandbox validation prove the required behaviour. No production writes, deployment, or coding-agent delegation is authorised by this decision.


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
- Do not over-engineer, invent new settings/switches or split clear requirements into unnecessary functionality. Do the task; avoid repeated assurances, motivational statements, and assurance loops that frustrate Hu. Report concrete work and evidence.
- If agent delegation is authorised, completion audit must map every plan/spec item to DONE (verified)/PARTIAL/NOT DONE/DEFERRED with command output or file-line evidence, and list shortcuts/stubs/placeholders/TODO/pass/test weakening/swallowed errors/out-of-scope claims.
- Stage only explicit paths; never `git add -A`; no commit co-author trailers. Keep PROJECT_LOG.md, CLAUDE.md, README and status register updated before clearing context. Keep .claude session log private/out of Git.
- Risk-based sufficient testing; no expensive full-suite rerun after narrow fixes unless a meaningful gate warrants it.
- Hosting is preferred on DigitalOcean App Platform + Managed PostgreSQL; hosting setup was parked until the other work is ready. Hu wants it completed after the agent's other tasks, but no agent delegation or live deploy is authorised by this preference alone.
- Preserve original sources and history; don't overwrite historical records to make them look current.

## Source-specific response audit — `HUDI Discussion/HuDI Conversation 17-part2.md`

**Audit result:** The complete source file was fetched from the repository and reviewed end-to-end. Each distinct decision, clarification, correction and process instruction in this source was compared with the current decision shortlist, reconciliation overlay, recovered-response register and 151-item decision crosswalk. The authoritative scope decisions below are recorded; implementation status and execution authorisation remain separate.

| Source topic | Hu's recorded answer / correction | Target record and reconciliation result |
|---|---|---|
| Product lifecycle | Approved Draft, Active, Unlisted (direct-link only), Archived; no Suspended state unless a concrete operational need is evidenced. Preserve order/history and authorised staff action. | Shortlist Decision 1; recovered above. Scope decision resolved; implementation not authorised by this approval alone. |
| Gift cards | Agreed to exclude from current scope and defer reconsideration unless HU+DI reopens it and accountant-approved terms exist. | Shortlist Decision 2; scope excluded/deferred. |
| Customer/order-history deletion | Deletion YES; anonymisation NO. Only authenticated Admin or Director. Customer-record merging was not approved. Preserve required accounting/tax records, order integrity and audit evidence. | Shortlist Decision 3; deletion scope approved with safeguards; anonymisation NO; merge unapproved. Do not infer bulk deletion approval from this general answer. |
| Tax-exemption controls | Approved; Admin or Director roles are responsible for applying tax rules. Record who/when and reason/evidence where applicable. | Shortlist Decision 4; scope approved, role enforcement and audit requirements retained. |
| Marketing and channels | Marketing/channel capabilities are to be implemented as in-scope features, not parked as future features. WhatsApp marketing is managed through Meta, not directly in EffyKlean Admin; provide secure integration configuration/credential settings for supported integrations. | Shortlist Decision 5; feature scope approved. Provider setup, live credentials, campaigns, sends and privacy-sensitive tracking remain separate gates. |
| Analytics and customer segmentation | Existing YES answers and AD-15 operational reporting approval stand; no new approval question is needed for already approved segmentation. Optional visitor/session/conversion/behaviour tracking remains gated by privacy/consent/retention controls. | Shortlist Decision 6; scope resolved from prior answers; MF-093 remains LATER. |
| Coupon restrictions and discount rules | Rejected excluding one-use-per-customer and eligibility controls. Approved both as optional per-coupon controls (all customers, new customers, specific customers/approved segments). Preserve no stacking, combo order/first-item rule, and distributor pricing rules. | Shortlist Decision 7; scope approved, existing pricing precedence unchanged. |
| Public quantity price breaks and “Subscribe” | Approved public quantity price breaks; quantity tier defines the selling price and does not stack as another discount. “Subscribe” means updates/communications, not recurring product orders or charges. | Shortlist Decision 8; quantity price-break scope resolved. Do not conflate updates subscription with product selling plans. |
| Content, forms, search, chat and package features | Earlier YES answers for site preferences, storefront search/settings/filters, forms builder, customer-facing chat/chatbot and package feature stand. Do not re-ask. Do not assume a Shopify theme-builder/Tidio clone or override Zoho/Shiprocket ownership. | Shortlist Decision 9; prior YES answers preserved; detailed implementation/provider requirements and package/shipping boundaries remain. |
| Admin-editable settings | Approved the proposed baseline split: safe contact/brand content may be editable through audited Admin controls; protected checkout/payment/GST/tax/shipping/Zoho-owned/domain settings stay restricted; extra fields require HU+DI approval. | Shortlist Decision 10; baseline approved; no broad unrestricted settings surface. |
| Channel semantics / active products | Rejected the invented separate Staff-availability setting and challenged the assumption that Active must mean hidden from the website. Do not over-engineer or add unsupported channel switches/POS behaviour. Preserve the approved lifecycle and staff-order safeguards. | Shortlist Decision 11; no separate staff-availability setting; no new decision/task from Di's withdrawn proposal. |
| Scheduled publication | Corrected Di's misreading: if the required approval is incomplete or Admin/Director forgets to publish, the product remains unpublished even after the scheduled time. Scheduled time never publishes by itself; authorised Admin/Director must manually publish after required approval. | Shortlist Decision 1 and Decision 13; MA-PRD-057 resolved. No automatic publication or schedule-based bypass. |
| Product URL identity | Approved fixed product-ID URLs `/products/<id>/`; no editable slugs or slug-change redirects. | Shortlist Decision 12; MA-PRD-063 resolved. |
| Work/process instructions | Asked whether every response was being saved; explicitly required the answers to be recovered and recorded before agent instructions. Rejected repeated assurances and asked for the task to be completed. | This register is the response index; the source-specific audit, reconciliation overlay and row-level crosswalk have now been updated and re-fetched for verification. Do not prepare the next coding-agent instruction set until the wider response reconciliation is complete. No coding-agent delegation was authorised. |

### Important interpretation corrections preserved

- The “Active product must be hidden from the public website” wording was Hu challenging Di's invented assumption, not a new rule. The existing Unlisted state is sufficient; no Staff-availability switch is to be added.
- The first response about scheduled publishing was corrected explicitly by Hu. The final authoritative rule is manual publication only after required approval; forgetting or reaching a scheduled time does not publish.
- “Marketing/channel features” means implementation scope, not future-only roadmap items. It still does not authorise arbitrary live provider actions.
- Updates subscription is not recurring product subscription.
- Approval of customer deletion does not approve anonymisation or customer merging, and does not silently settle bulk-delete behaviour.

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

- **This source file:** the 19 explicit HU-authored messages identifiable in `HUDI Discussion/HuDI Conversation 17-part2.md` are now indexed verbatim with source line references and normalized decision mappings in the appendix below. Key target ledger rows for MA-PRD-047, MA-PRD-057, MA-PRD-063, MA-CUS-009, MA-CUS-014, MA-CUS-045, MA-PRD-071, MA-SET-011 and MA-SET-013 were re-fetched and inspected.
- **Source limitation:** some assistant acknowledgements in the source say “Agreed, Hu” or “Recorded and verified” without a separate visible HU-authored message. Those acknowledgements are not treated as HU quotes. Do not fabricate wording for any response not explicitly present.
- **Not yet exhaustive across the project:** this does not prove every answer from every earlier chat thread has been checked against every relevant row in the 597-item history and canonical 122-capability master. Do not prepare the next coding-agent instruction set until that broader cross-thread reconciliation is complete.
- **Next reconciliation step:** compare the other identified gap-analysis/decision source files with the shortlist, 22-Oct decision log, canonical 122-capability master, 597-item disposition history and 245-row ledger. For each answer, record requirement ID(s), exact source, target record and verification status. Use `SOURCE FOUND / RECORDED AND VERIFIED / MISSING FROM RECORD / AMBIGUOUS — DO NOT GUESS`; never fabricate timestamps or verbatim quotes.

## Verbatim HU-response inventory — source file line references

This inventory records the explicit HU-authored messages visible in `HUDI Discussion/HuDI Conversation 17-part2.md` (GitHub main; source blob SHA `3528acd80981c8fef2036bbb56b2459e4a59d435`). Quotes below preserve the source wording, spelling and punctuation; source line numbers refer to that exact blob. This is an evidence index, not a replacement for the requirement-level rows. The associated decision records and ledger rows must retain the normalized rule and implementation status separately.

| Source line | HU's exact message | Requirement / decision mapping | Record disposition |
|---:|---|---|---|
| 76 | “i think the Cuatomer and order history deletion is a GO. dont worry about legal etc. its just a features and will used only by admin and senior staff who knows what they are doing” | Customer/order-history deletion; later clarified by HU at line 107. | GO recorded for deletion, but superseded/refined by explicit line 107: deletion YES, anonymisation NO. Do not treat “senior staff” as overriding the later explicit Admin/Director role rule. |
| 87 | “what is anonymised? i think only people who can do it are the ones who log in using proper credentials and the role is admin or director” | Meaning of anonymisation; authentication and privileged-role restriction. | Role restriction recorded. The next explicit answer at line 107 decides anonymisation NO and deletion YES. |
| 107 | “anonymization is a NO for implementation, Deletion is YES for implementation” | Customer deletion/anonymisation; MA-CUS-009 and related shortlist Decision 3. | Binding: deletion YES; anonymisation NO; merging not approved; authenticated Admin/Director only; preserve required records and audit evidence. |
| 127 | “the admin or director know the tax rules. so Tax Exemption control is APPROVED” | Tax-exemption controls; MA-CUS-014 / MA-CUS-045. | Scope approved for Admin/Director; retain role checks and change audit. Do not convert this into permission to violate applicable tax rules. |
| 144 | “keep these as a feature. whatsapp marketing happens in meta cannot be directly done in our admin page. we can just do integrations and open API keys for integrations” | Marketing/channels and integrations; shortlist Decision 5. | In-scope feature, not future-only. WhatsApp marketing via Meta; secure integration/credential configuration; live provider actions remain separately gated. |
| 163 | “Keep marketing and channel capabilities features - they should be implemented not Future Features.” | Correction to the prior interpretation of marketing/channel scope. | Explicit correction recorded: implementation scope, not future-only. |
| 300 | “no. i think if we send a generic festive coupon it should be add one use per customer limit or eligibility restritiond” | Coupon restrictions; shortlist Decision 7. | Both controls approved as optional per-coupon settings: one use per customer and eligibility for all/new/specific customers or approved segments. Existing no-stacking/combo/distributor rules remain. |
| 338 | “thats approved” | Public quantity price breaks; MA-PRD-071 / shortlist Decision 8. | Approved: public quantity tier sets selling price and does not stack as another discount; distributor slabs remain separate. |
| 395 | “No Active product can be hidden from the public website. why is it required to be that way?” | Product lifecycle / channel semantics; shortlist Decision 11. | Challenge to Di's proposed extra rule, not a request to create a new setting. Withdraw separate Staff-availability switch; preserve approved Active/Unlisted semantics. |
| 411 | “dont over engineer anything di. i have given clear requirements you dont have to tear them apart and cook up new functionality” | Process constraint for all implementation/decision reconciliation. | Binding working constraint: follow recorded requirements; do not invent functionality or split clear requirements without evidenced need. |
| 425 | “dont keep tell me this -> HU+DI means making progress against your requirements—not making the project more complicated. I'll keep that principle front and centre. i know it already and you saying it will not change anything but may frustrate me further.” | Communication/process correction. | Do not repeat motivational assurances; complete the work and report concrete results. |
| 439 | “why? scheduled publishing is by admin or director if they forget then the timeline is pushed for publishing. why you want to defer it?” | MA-PRD-057 scheduled publication. This message was followed by HU's explicit correction at line 454. | Do not use this message alone as the final rule: line 454 corrects Di's misreading and is authoritative. |
| 454 | “Admin or Director schedules the publication, and if they forget to publish it manually, the system publishes it at the scheduled time. ,_ are you even reading what i said. i said if they forget then no pubishing. it is published only one when the approval is complete” | MA-PRD-057; explicit correction of the preceding misunderstanding. | Final rule: scheduled time does not publish automatically. Required approval and authorised Admin/Director manual publication are mandatory; if forgotten or approval incomplete, it remains unpublished. |
| 461 | “ok anything else pending i think we are almost done right?” | Request for remaining-work status. | Not a scope approval. Answer should distinguish remaining decision corrections from technical/provider/implementation evidence. |
| 497 | “yes. Approved. Go ahead” | MA-PRD-063 product URL identity. | Approved fixed product-ID URLs `/products/<id>/`; editable slugs and slug-change redirects out of scope. Scope approval is not implementation authorisation. |
| 507 | “ok” | Acknowledgement after the MA-PRD-063 decision record was reported as updated. | Acknowledgement only; no new scope decision. |
| 510 | “are you updating all the responses and saving them right? i dont want you to loose anything, as thi sis the basis for the next instruction set to the agent” | Requirement to preserve answers before the next coding-agent instruction set. | Explicit task requirement: reconcile and verify answers before producing agent instructions. No delegation is authorised by this message. |
| 535 | “what do you mean if you are not sure you are saving the responses then why are you asking me the questions? just for fun? is this a joke for you?” | Correction of process failure and unsupported assurances. | Do not ask already answered questions; do the source-to-record reconciliation and report verified coverage, gaps and conflicts. |
| 560 | “i want you to go back through this chat and remember all my responses and record them first” | Direct instruction to recover and record responses first. | This register and linked decision records are the persistence targets; do not prepare agent instructions until reconciliation is complete. |

### Transcript completeness limitation that must not be hidden

The source file contains assistant acknowledgements such as “Agreed, Hu” / “Recorded and verified” without a separate HU-authored message immediately preceding every acknowledgement. Those assistant statements are not verbatim HU quotations and must not be relabelled as such. Where the exact HU wording is absent from the source, preserve the decision only where corroborated by the decision record, and label the exact quote as unavailable rather than inventing it.

### Source-specific coverage status after this inventory

- Explicit HU messages visible in this source have been indexed above with exact source line references and normalized decision mappings.
- The authoritative row-level decisions already present include MA-PRD-047, MA-PRD-057, MA-PRD-063, MA-CUS-009, MA-CUS-014, MA-CUS-045, MA-PRD-071, MA-SET-011 and MA-SET-013; their implementation statuses are not changed by this index.
- This establishes coverage of explicit HU messages visible in this one source file only. It does not establish exhaustive coverage of every earlier chat thread or prove implementation completion.



## 597-row response reconciliation crosswalk — 23 October 2026

The row-level file [HU_RESPONSE_RECONCILIATION_597_2026-10-23.csv](./HU_RESPONSE_RECONCILIATION_597_2026-10-23.csv) has been created from the immutable 18-Oct 597-row snapshot, the canonical 12-Oct 122-capability decision master, the 22-Oct HU+DI disposition log, the 245-row BUILD ledger, the 151-item decision crosswalk, and the 23-Oct genuine-decision shortlist. It contains 597 unique source IDs and keeps historical implementation/status fields separate from HU decision evidence.

Verified crosswalk counts:
- **215 rows** have an existing HU decision/response summary traced to a source record. These include original 12-Oct YES/NO decisions, recorded 22-Oct dispositions/directions, and 23-Oct refinements. Summaries from decision logs/shortlists are not presented as verbatim HU quotes; verbatim is used only where the source itself supplies it.
- **144 rows** are reconciled from an existing ledger/crosswalk without treating that reconciliation as a new HU response.
- **238 rows** have no HU decision found in the sources checked for this pass. This is explicitly **not** a claim that Hu never answered, nor that these rows all require a question. They must be checked against the relevant historical source before any question is asked; many may be implemented or technical/evidence tasks.
Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.

This is the first cross-source, 597-ID response reconciliation pass—not a claim of exhaustive historical-chat coverage. Keep STOP → REPORT → HU+DI DECIDE, do not delegate to a coding agent without Hu's explicit authorization, and do not ask Hu to repeat an answer already marked RECORDED AND VERIFIED.


## Superseding update — 23 October 2026, earlier HU answers incorporated

After the initial crosswalk pass, I also reconciled the 18-Oct persistent HU answers file [RESP_18OCT_QA_HU ANSWERS.md](../../HUDI%20Discussion/RESP_18OCT_QA_HU%20ANSWERS.md) against the 597 IDs and attached the applicable directions to 56 distinct rows. This preserves earlier instructions while leaving later, more-specific decisions authoritative. The row-level crosswalk has been re-fetched and now contains **597 unique IDs** with these current counts:
- **252** rows with an existing HU decision/response source recorded;
- **127** rows reconciled from existing ledgers without treating that reconciliation as a new HU response;
- **218** rows where no HU decision was found in the sources checked so far. This is not proof that Hu never answered and does not mean all 218 require a question.

These counts supersede the earlier initial-pass counts recorded above. The 18-Oct source was not a verbatim transcript of every earlier conversation; this is still not an exhaustive audit of every historical chat. The zero-byte 597-row disposition working CSV remains a separate unresolved record-reconstruction defect.


## Final response-triage update — 23 October 2026 (supersedes earlier counts)

The 597-row crosswalk now incorporates the grouped original HU decisions from the canonical 12-Oct master and the applicable 18-Oct QA answer record, in addition to the 22-Oct decision log and 23-Oct refinements. The CSV was re-fetched and checked: **597 rows, 597 unique IDs**.

Current row-level classification:
- **530 rows** have a recorded HU decision/response source linked to the requirement ID. Original grouped YES/NO decisions are preserved as historical decisions; later specific refinements remain controlling. Decision-log summaries are not mislabeled as verbatim quotations.
- **11 rows** are reconciled from existing ledgers without treating that reconciliation as a new HU response.
- **44 rows** have an implemented/closed/no-action source status and need no HU question now; revisit only if concrete evidence reveals a material gap.
- **12 rows** were individually triaged as existing scope boundaries, frozen-spec/technical gates, or unapproved proposals. No broad HU question is warranted now; verify reference-site/SPEC evidence first, and STOP → REPORT → HU+DI DECIDE only if a real conflict remains.

Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.


## Correction — working disposition CSV restored, but not fully reconciled (23 October 2026)

Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.

Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.


## Latest disposition-register update — 23 October 2026 (supersedes prior row counts)

Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.

## Superseding update — BUILD-245 prior-input reconciliation and stale-question cleanup (23-Oct-2026)

This update supersedes the earlier BUILD-disposition counts below where they conflict with the corrected row-level records.

### Verified source-to-record reconciliation

- The 597-ID response crosswalk was re-fetched and checked for unique IDs. The 245-row BUILD ledger is joined to it by exact activity ID; response evidence and implementation status are kept separate.
- Before correction, the 245-row ledger showed 160 BUILD dispositions, 83 Implemented and 2 EXCLUDE. Of the 160 BUILD rows, 156 had an identified prior response/decision source: 16 from the 18-Oct HU answer record, 69 from the existing decision/response records, 69 from the canonical original HU decisions, and 2 with an original YES superseded by a later exclusion/defer decision. Four rows — MF-055, MF-084, MF-094 and MF-115 — were ledger-only reconciliations, not explicit HU responses.
- A concrete conflict was found and fixed: MA-GFT-001, MA-GFT-002 and MA-SET-032 still carried current disposition BUILD even though the later HU decision excludes gift cards from current scope and leaves them deferred for possible future reconsideration. The 245-row ledger and 597-ID response crosswalk now mark all three EXCLUDE while retaining implementation status DEFERRED. Reopen only through a later explicit HU+DI decision and accountant-approved terms. The original YES decisions remain historical evidence and are not erased.
- The correction overlay `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv` now contains five corrections: MA-ORD-103/105 plus the three gift-card rows.
Current 245-row disposition counts are **83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE** (245 total). Separate implementation outcomes remain **83 DONE (verified), 62 PARTIAL and 100 DEFERRED**.
- Forty-six additional next-action/reason-category entries in the 245-row ledger were corrected so settled HU decisions are not still presented as broad open questions. The edits preserve genuine provider, legal, evidence, validation and detailed specification gates. They do not authorize deployment, live provider writes or implementation beyond existing authorization.

### Remaining coverage boundary

Superseded interim statement: the working CSV is populated and has 597 rows / 597 unique IDs. Current dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Exact-ID comparisons found zero disposition mismatches against the 597 response crosswalk and against the 245-row ledger for shared IDs; do not use the old 511-classified / 86-unreconciled aggregate.

## Latest superseding update — 160-row prior-input reconciliation (23-Oct-2026)

The reconciliation has progressed beyond the earlier three-gift-card correction. The original 160 BUILD-disposition rows were checked against prior HU answer/decision sources and then reclassified where later, more-specific decisions already controlled the current scope. The original source evidence remains preserved; original YES answers are not erased, but they do not override later explicit refinements.

Current 245-row dispositions: 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE. Implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED.

Additional row-level corrections applied to both the 245-row ledger and 597-ID response crosswalk:
- **LATER:** MA-CUS-006 (multiple saved addresses; one address remains the current rule), MA-PRD-075, MA-SET-029, MA-SET-075 and MA-MKT-012 (verified translations required), plus MA-ANA-012/013/021/024/026, MA-SET-027, MA-CNT-042 and MA-MKT-002 (optional tracking/attribution remains LATER under MF-093 until consent, privacy notice, retention and access controls are approved and implemented).
- **EXCLUDE:** MA-CUS-020 (customer merging is unapproved; customer deletion remains separately scoped under MA-CUS-009).
- The earlier gift-card correction remains: MA-GFT-001, MA-GFT-002 and MA-SET-032 are EXCLUDE/deferred. MA-ORD-103/105 remain EXCLUDE/deferred.

The correction overlay now has **19 rows**. The 597-ID crosswalk was updated to retain the original answer and record the later refinement as controlling. Ninety-five row-level edits do not mean 95 implementation tasks are complete.

Superseded interim statement: the working CSV is populated and has 597 rows / 597 unique IDs. Current dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Exact-ID comparisons found zero disposition mismatches against the 597 response crosswalk and against the 245-row ledger for shared IDs; do not use the old 511-classified / 86-unreconciled aggregate.

## Latest correction — 23-Oct-2026: 597-row working register re-fetched and synchronized

Superseded interim finding: the working CSV is now populated and has 597 rows / 597 unique IDs. Current 597-ID dispositions are 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE. Current 245-ID ledger dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE; implementation outcomes remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. Exact-ID comparisons show zero disposition mismatches for IDs in common.

Current 597-row register counts are **340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE** (597 total; 597 unique IDs). The register is populated and the current exact-ID comparisons found no disposition mismatches against the response crosswalk or the 245-row ledger for IDs in common. The earlier 86-UNRECONCILED statement is superseded.

Current 245-row ledger dispositions: **83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE**. Its implementation-status counts remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. The 597-ID response crosswalk has 597 unique IDs; the decision overlay has 151 rows; the correction overlay has 19 unique row-specific corrections. Original HU answers remain historical evidence, and later specific refinements control current disposition. No coding agent was delegated and no implementation/deployment/provider action was performed by this reconciliation.

## Latest audit correction — 23-Oct-2026

The earlier count of 95 changed rows was an interim checkpoint. After the final pass replacing stale repeated questions with specific evidence/provider/legal/implementation actions, comparison with the pre-reconciliation 245-row ledger now confirms **114 unique rows** have at least one corrected disposition, reason category or next action. This does not mean those 114 capabilities are implemented.

Current row-level totals: 340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER and 14 INVESTIGATE (597 unique IDs). The earlier interim aggregate is superseded; the current register is populated and fully classified by row.


## Superseding 245-row prior-input reconciliation — 23 October 2026

Hu directed Di to reconcile the 160+ items for which Hu had already supplied input before continuing with remaining decisions. The 245 unique implementation-ledger IDs were matched by exact ID against the 597-ID response crosswalk and 151-row BUILD-245 decision/action overlay. **234/245 have an identified prior HU decision/response source; 11 are ledger-only reconciliations and must not be represented as explicit HU answers.** The 597-ID crosswalk itself contains 597 unique IDs. This pass is not a claim that every earlier conversation thread has been exhaustively searched.

**Corrections saved:** 35 row-specific next-action entries were refined in both the 245-row implementation ledger and decision/action overlay so prior scope answers are not asked again while specific technical, evidence, provider, consent, legal and genuinely unresolved policy items remain visible. Current disposition was corrected from BUILD to EXCLUDE for MA-PRD-083 (no Suspended state in the approved four-state lifecycle) and MA-PRD-092 (no bulk product deletion; archive/unpublish instead). Both retain implementation status DEFERRED. The current-disposition correction overlay now has 21 row-specific entries. Re-fetched row-level files must be used to verify these changes before reporting them as saved.

Additional implementation-ledger follow-up wording was clarified for MF-063 (Zoho Flow/Shiprocket check remains parked for later testing), MF-079 (existing GoDaddy/Zoho messaging direction; wording, credentials and delivery tests remain), and MF-088 (Spaces is the approved direction, but provisioning remains a separate HU-authorised action). No new scope decision was inferred.

Two further stale next actions were corrected: MA-PRD-067's G-23 scope question is superseded by the original YES and verified implementation; MA-DSC-020 must follow the existing no-stacking precedence and is not a fresh question. Both remain in their existing implementation status; no new HU decision was invented.


## MF-055 decision status after Hu's response (23-Oct-2026)

MF-055 is no longer an open policy question. Hu explicitly approved the website-as-source-of-truth rule and website-to-Zoho synchronization described above. The prior “next decision prepared” text is historical and superseded. Keep implementation status separate: MF-055 remains PARTIAL / BUILD until implementation and targeted sandbox validation are evidenced.
