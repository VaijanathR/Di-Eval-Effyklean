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

**Precedence rules for this plan**
- HU's explicit instruction is to implement every pending task from the agent response; each such task is marked **YES**. Phases establish sequence and priority, not whether the business wants the capability.
- For capability decisions, preserve the recorded YES/NO in the decision ledger, interpreted through the functional resolutions in Section 4 below. A prior recommendation in the Shopify comparison is not a substitute for Hu's recorded decision.
- A recorded **NO** remains excluded unless Hu explicitly changes it.
- The most recent explicit HU+DI decision takes precedence over older provider notes: **Zoho Payments is the intended provider for EffyKlean.in, replacing Razorpay as the direction of travel.** This does not mean credentials, sandbox proof, production configuration, or live cutover are complete or authorised.
- Existing frozen specifications, architecture, privacy/security controls and operational invariants remain binding. A task can be YES while implementation is constrained by those rules.
- If new evidence reveals a true contradiction that cannot be reconciled by applying the agreed functional rules, **STOP → REPORT → HU+DI DECIDE**. Continue independent safe work.
- Do not treat this review draft as permission to deploy, cut over live payments, perform live provider writes, or make unauthorised commits.

## 2. Decision count — what can and cannot be counted reliably

The current Decision Ledger says the source comparison contains **494 capability rows**, but also explicitly warns that its own recovered decisions are incomplete/ambiguous for some rows. Therefore, a definitive YES/NO count across all 494 rows **cannot be responsibly claimed from the current ledger alone**.

A mechanical audit of the unique capability IDs explicitly named in the ledger yields the following provisional count after applying the ledger's explicit NO exceptions where a range accidentally overlaps them:

- **YES: 350 explicitly enumerated capability IDs**
- **NO: 29 explicitly enumerated capability IDs**
- **Total explicitly enumerated IDs: 379**
- **Not safely classifiable from the current ledger: 115 of the 494 source rows**, because the ledger summarises some categories as previously answered, leaves gaps, and identifies ambiguities that require the original source/conversation evidence.

These are counts of explicitly enumerated **capability IDs**, not counts of completed code tasks. They are **not a final count for all 494 source rows**. The original ledger itself notes the malformed Orders range and other ambiguities. In particular, interpret the explicitly stated exceptions as controlling: ORD-019, ORD-103, ORD-105, ORD-112 and ORD-116 are NO despite being accidentally included in adjacent ranges; PRD-060 is NO. Do not count any ID twice.

The agent-reported pending implementation tasks are a separate implementation backlog; the user explicitly directed that **every pending task in that response be YES**. This does not convert capability NOs into YES or override the functional rules below. The four items the agent labelled “out of scope without a decision” remain excluded and are not included in the YES task inventory: wishlist, reviews/recommendations, server-side cart, and related-product links.

**Required follow-up for a true 494-row final count:** reconcile the 115 unclassified rows against the full comparison and original recorded answers, then update the count. Do not guess or infer a missing YES/NO answer from a Shopify recommendation.

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

## 6. Recorded NO capability IDs

The ledger's explicit NO list must remain excluded, subject only to a later explicit HU decision. It includes:

- **Orders:** ORD-019, ORD-064, ORD-067, ORD-069, ORD-070, ORD-071, ORD-073, ORD-086, ORD-087, ORD-092, ORD-103, ORD-105, ORD-112, ORD-116, ORD-121, ORD-136, ORD-138, ORD-139.
- **Draft orders:** DRF-008.
- **Products:** PRD-060 (video/3D product media; separate old-site/how-to media migration tasks E-08/DC-22/DC-25/D-08 remain YES and are not this product-media feature).
- **Settings:** SET-008 (COD), SET-050 (transfer/move store to organisation/external owner), SET-058 (Shopify Network Intelligence), SET-070 (COD customisation), SET-071 (Razorpay Magic Checkout).
- **System shell:** SYS-004 (command palette/keyboard shortcuts), SYS-009 (setup guide/promotions), SYS-010 (Shopify AI assistant/Sidekick), SYS-013 (multi-store switcher).
- **ORD-145 is not a settled NO:** the ledger says its fulfilment-card menu was not observed and the capability is not assessed. Inspect read-only only if it may reveal a unique capability. Other explicit NOs and platform-specific exclusions documented in the ledger remain in force. The ledger's full NO rows should be checked against the source catalogue when producing the audited 494-row count.

**Counting note:** The provisional 29 explicit NO count above is an ID count after resolving accidental range overlap, not a count of every potential feature recommendation in the comparison. Do not interpret the source comparison's older REJECT/DEFER recommendation column as a user's NO response.

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
- A phase is complete only when its exit evidence is recorded and validated by the local agent. The plan is complete when all YES tasks have been implemented/tested, all explicitly NO capabilities remain excluded, the 494-row decision count has been reconciled without guessed answers, and release-gate evidence is complete.

## 9. HU review items

1. Confirm that this is the single consolidated review document to use for phase-wise planning, with the capability ledger and conflict analysis retained as source records rather than competing implementation roadmaps.
2. Review the provisional capability count: **350 YES and 29 NO among 379 explicitly enumerated IDs; 115 of the 494 source rows still need evidence-based classification** before a genuinely final all-row count can be stated.
3. Confirm the proposed priority order: baseline/evidence → Admin/integration foundations → local E2E → Zoho sandbox → mappings/shipping → storefront/customer experience → communications → infrastructure/release → remaining YES capabilities/beautification.
4. Confirm that the refund-handling agent task is treated as **YES to implement and enforce the agreed no-refunds/no-returns policy**, not as authorisation to build a refund execution workflow.
