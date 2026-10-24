# BUILD-152 implementation report

**Created:** 2026-10-24 053435 IST (Asia/Kolkata). Ledger: `docs/ImplementationPlan/AgentReports/BUILD152_ITEM_LEDGER_2026-10-24_053255.csv` (one row per record, with criteria outcomes, implementation paths and lines, validation, evidence type, limitations, next action and owner). **Nothing was staged, committed or pushed. No live provider write, deployment, DNS change, e-mail or payment was made.**

## 1. Overall status
**Not complete, and this report does not call it complete.** 152 records: **57 DONE (verified), 51 PARTIAL, 44 DEFERRED, 0 NOT DONE.** Reason categories for the 95 unfinished records: DEFERRED / BLOCKED: 7; DEFERRED / DECISION REQUIRED: 23; DEFERRED / DEPENDENCY NOT MET: 14; PARTIAL / ACCOUNTANT VALIDATION PENDING: 2; PARTIAL / BLOCKED: 6; PARTIAL / DECISION REQUIRED: 21; PARTIAL / DEPENDENCY NOT MET: 12; PARTIAL / VALIDATION PENDING: 10.

Most unfinished records wait on something outside this repository: an HU+DI decision, legal or accountant text, a provider scope or credential (the Zoho sandbox token lacks purchase-order, adjustment, transfer, invoice, contact-update and item-update scopes), a paid resource (Spaces) or hosting. I list each one in section 8. I did not mark any record DONE on the strength of a test count alone; each DONE row names the criterion and the tests that exercise it.

Evidence type everywhere is local PostgreSQL 17 pytest, mock (real adapter over a fake transport), or SANDBOX-OBSERVED read-only. **No criterion is proven against a live production system.**

## 2. Item ledger (summary; full detail in the CSV)
| ID | Status | Reason | What was concluded |
|---|---|---|---|
| MA-ANA-011 | DONE (verified) | - | Returning customer rate and first-order cohorts from authoritative order data |
| MA-ANA-017 | DONE (verified) | - | Native saved/custom reports within the approved reporting scope: smallest safe design, private, audited, authoritative data only |
| MA-ANA-027 | DONE (verified) | - | Pin a report; report library by category |
| MA-CNT-004 | DONE (verified) | - | Page-template need mapped to a minimal native Django layout model (no Shopify theme mechanics, no code editing); draft/review/publish flow kept |
| MA-CNT-014 | DONE (verified) | - | Theme library/customise/edit-code mechanics are not an EffyKlean requirement as-is; no arbitrary code editing in Admin; approved layout needs mapped to safe native Djang… |
| MA-CNT-015 | DONE (verified) | - | Native audited site preferences: home title, default description, default sharing image, storefront password page (Director only, off by default, hashed, throttled, exem… |
| MA-CNT-016 | DONE (verified) | - | Storefront search settings/filters: only grounded EffyKlean catalogue filters/settings; no invented ranking; audited |
| MA-CNT-019 | DONE (verified) | - | Admin-built public forms: field builder (6 types, max 12, no files) [MET]; draft -> Director approval -> publish lifecycle with live copy separate from draft [MET]; fail… |
| MA-COL-008 | DONE (verified) | - | Collection channel availability mapped to catalogue/publication lifecycle; no separate Staff-availability setting |
| MA-CUS-009 | DONE (verified) | - | Deletion YES for authenticated Admin/Director only; anonymisation NO; defined deleted/kept data; active-order integrity, tax/accounting/audit preservation; privileged ac… |
| MA-CUS-043 | DONE (verified) | - | English used for customer notifications; additional languages stay LATER until verified translations exist; field cannot be set to anything else |
| MA-CUS-050 | DONE (verified) | - | Bulk customer deletion follows the MA-CUS-009 boundary: Admin/Director only, protect active orders, preserve tax/accounting/audit records; confirmation; per-customer out… |
| MA-DSC-011 | DONE (verified) | - | Optional per-coupon one-use-per-customer limit; identity = checkout e-mail OR 10-digit mobile (option A); enforced authoritatively at pay; one additional discount rule p… |
| MA-DSC-012 | DONE (verified) | - | Optional coupon/promotion eligibility: all, new customers, specific customers, approved saved segment; auditable; no invented extras; automatic offers respect it |
| MA-DSC-026 | DONE (verified) | - | Approved combo rule: first qualifying item no discount, later items discounted, removing the first promotes the next; combo OR coupon, never both; qualifying quantities … |
| MA-INV-002 | DONE (verified) | - | Stock states: available, committed, on hand shown from verified Zoho data; incoming/unavailable shown only if Zoho supplies them (it does not) and never invented |
| MA-INV-003 | DONE (verified) | - | Adjust quantity stays Zoho Inventory-owned; no competing local stock write; verified supported workflow |
| MA-INV-005 | DONE (verified) | - | Reserve/commit stock stays Zoho-owned; verified Zoho-supported capability and safe sync; no competing local reservation |
| MA-INV-008 | DONE (verified) | - | Add/edit/deactivate location stays Zoho-owned; locations are read, with no local location master |
| MA-INV-012 | DONE (verified) | - | Suppliers stay Zoho-owned; verified Zoho-supported read path (vendor contacts); no competing supplier master |
| MA-INV-013 | DONE (verified) | - | Inventory CSV import/export: import authority stays in Zoho (no local import); export of the read-only copy exists and is audited |
| MA-ORD-078 | DONE (verified) | - | Capture authorised payment: check whether Zoho Payments has an authorise-then-capture step; if unsupported record 'not applicable' |
| MA-PRD-007 | DONE (verified) | - | Filter by collection / sales channel using recorded catalogue + approved channel semantics |
| MA-PRD-012 | DONE (verified) | - | Product list column showing where a product sells, under the HU-reconciled semantics (no separate Staff-availability switch) |
| MA-PRD-040 | DONE (verified) | - | Baseline: every product is a physical, shipped product; no non-shipping/digital product flag |
| MA-PRD-046 | DONE (verified) | - | Smallest native page/layout model instead of a theme-template selector: two layouts (Standard, Wide) chosen per page, under the draft/review/approve/publish flow; no tem… |
| MA-PRD-052 | DONE (verified) | - | HU 23-Oct four-state lifecycle (Draft/Active/Unlisted/Archived); authorised staff action; preserve order+revision history; no Suspended; manual only |
| MA-PRD-053 | DONE (verified) | - | Unlisted = reachable and orderable only by direct link; hidden from listing, search, sitemap, collections, feed; noindex |
| MA-PRD-057 | DONE (verified) | - | Scheduled time never publishes; publication only after approval + manual Admin/Director action; unpublished if forgotten; no bypass |
| MA-PRD-063 | DONE (verified) | - | Fixed /products/<id>/ URL identity; no editable slug UI or slug-change redirect behaviour |
| MA-PRD-066 | DONE (verified) | - | Combo packs via approved model: orders expand to component SKUs; no combo SKU; first item undiscounted, later discounted |
| MA-PRD-071 | DONE (verified) | - | Public quantity price breaks: tier = selling price for the quantity, not an extra discount; no stacking; distributor slabs separate; shown identically in cart/review/ord… |
| MA-PRD-091 | DONE (verified) | - | Bulk archive/unlist only after individual behaviour verified; preview then confirm; per-product audit; not bulk deletion |
| MA-PRD-093 | DONE (verified) | - | Bulk include/exclude in sales channels and catalogs mapped to the approved lifecycle and existing bulk collection add/remove |
| MA-PRD-098 | DONE (verified) | - | CSV product import with downloadable sample; platform-to-platform import excluded |
| MA-PRD-100 | DONE (verified) | - | Product list filters from recorded data (tag, status, category, type, collection, sale state); vendor is EXCLUDE; no invented catalogs/channels |
| MA-SET-001 | DONE (verified) | - | Store name/contact e-mail/phone/address editable through an audited Admin control; canonical identity + payment/GST/tax/checkout/shipping/Zoho-owned data/domains stay pr… |
| MA-SET-003 | DONE (verified) | - | Logo, colours, slogan and social links fall within the audited editable brand-content baseline; restricted settings stay protected |
| MA-SET-007 | DONE (verified) | - | Payments: manual payment methods stay out (frozen NO COD / manual / partial payment) |
| MA-SET-009 | DONE (verified) | - | Payments: PayPal / alternative gateways stay out; Zoho Payments is the only gateway, no fallback |
| MA-SET-010 | DONE (verified) | - | Payment customizations (hide / reorder methods) are not exposed |
| MA-SET-011 | DONE (verified) | - | Checkout settings (required fields, GST fields, order notes): mapped against the approved boundary; required-field toggles, GST/tax and checkout rules are not editable |
| MA-SET-012 | DONE (verified) | - | Checkout customisation cannot weaken required fields, GST/tax or the frozen payment rules |
| MA-SET-013 | DONE (verified) | - | Customer-account settings: password sign-in only; no self-service returns or store credit; explicit consent |
| MA-SET-014 | DONE (verified) | - | Shipping profiles/zones/rates: no competing shipping authority; shipping stays the Zoho-managed Shiprocket workflow with no checkout shipping charge |
| MA-SET-016 | DONE (verified) | - | Local delivery and pickup mapped to the evidenced use case (staff-recorded local pickup on the order), no competing shipping authority |
| MA-SET-017 | DONE (verified) | - | Carrier accounts / shipping labels stay in the Zoho-managed Shiprocket workflow; no competing carrier/label system |
| MA-SET-020 | DONE (verified) | - | Locations: Zoho remains the authority; location visibility mapped to verified Zoho data; no local location-master controls |
| MA-SET-026 | DONE (verified) | - | Domains: shown, never ordinary editable settings; DNS/domain changes remain a restricted action; current domains preserved |
| MA-SET-034 | DONE (verified) | - | Feature previews/labs: only a native feature-switch capability evidenced by the frozen design; documented flags shown read-only |
| MA-SET-056 | DONE (verified) | - | HSN and country of origin: Admin entry available, never guessed or hard-coded; website vs Zoho HSN comparison is report-only |
| MA-SET-059 | DONE (verified) | - | Marketing consent explicit and double opt-in; SMS excluded; optional tracking off until approved consent/privacy controls exist |
| MA-SET-073 | DONE (verified) | - | Packing slip fields (ship-to, PO number, order name) through a safe native template; no editable HTML/Liquid |
| MA-USR-003 | DONE (verified) | - | Staff invite: least-privilege, role-checked, audited, abuse-controlled; no credential passes through the page |
| MA-USR-004 | DONE (verified) | - | Staff MFA reset: role checks, audit, abuse controls, session safeguards; a stolen password cannot be used to re-enrol |
| MA-USR-032 | DONE (verified) | - | Security page: monitor user activity (audit-only view); collaborator request code has no EffyKlean equivalent |
| MF-092 | DONE (verified) | - | Redirect and URL-parity plan from effyklean.com paths to effyklean.in routes; preserve relevant URLs/redirect information; no DNS change, no Shopify closure |
| MA-ANA-014 | PARTIAL | BLOCKED | Product analysis (ABC, sell-through, days of inventory): ABC class and days-of-stock-left from the Zoho stock copy exist [MET, pre-existing]; sell-through needs received… |
| MA-ANA-015 | PARTIAL | BLOCKED | Finance: payments, taxes, payouts: payment and tax reports exist [pre-existing]; payouts and gateway fees [NOT available: the Zoho Payments sandbox returns 404 for settl… |
| MA-ANA-018 | PARTIAL | VALIDATION PENDING | Report export [MET, pre-existing CSV] and scheduling [IMPLEMENTED: owner-only e-mail of non-personal-data saved reports, off by default]; authentication/delivery verific… |
| MA-ANA-022 | PARTIAL | DECISION REQUIRED | Customer reports: RFM analysis and list [MET: 1-5 quintile R/F/M scores + rule-based segment], one-time and returning customers [MET], predicted spend tiers [NOT built] |
| MA-ANA-025 | PARTIAL | BLOCKED | Inventory report: ABC product analysis: ABC and days of stock left delivered [pre-existing MET]; sell-through blocked exactly as MA-ANA-014 |
| MA-CHN-004 | PARTIAL | VALIDATION PENDING | Google product feed prepared and validated locally [MET: required fields, price format, identifiers real or explicitly absent, escaping, unlisted products excluded]; Mer… |
| MA-CNT-041 | PARTIAL | DECISION REQUIRED | Themes (published/draft theme, update, edit, import, store): smallest native page/layout model [MET via MA-CNT-004 + Store profile brand settings]; separate draft/publis… |
| MA-CUS-014 | PARTIAL | ACCOUNTANT VALIDATION PENDING | Admin/Director-only tax-exemption control with who/when/reason/evidence + audit [MET]; applying an exemption to tax/orders requires an accountant-approved rule [NOT MET,… |
| MA-CUS-045 | PARTIAL | ACCOUNTANT VALIDATION PENDING | Customer 'Collect tax' setting: control + role checks + audit [MET as the same recorded decision, shown as Collect tax Yes/No]; effect on tax collection [NOT MET pending… |
| MA-DRF-003 | PARTIAL | DECISION REQUIRED | Draft orders: add products [MET: catalogue products only]; custom (non-catalogue) items [NOT built: they would bypass product/GST/Zoho item mapping] |
| MA-DRF-004 | PARTIAL | DECISION REQUIRED | Apply a named order discount to a draft: existing company coupons apply to staff-channel drafts [MET]; an ad-hoc named discount is a price override with no defined Direc… |
| MA-DRF-007 | PARTIAL | DEPENDENCY NOT MET | Send draft invoice / payment link: staff copy the signed payment link [MET]; the system does not SEND it (no approved e-mail/WhatsApp provider or wording; Zoho owns invo… |
| MA-INT-006 | PARTIAL | DECISION REQUIRED | Shiprocket status: no EffyKlean Shiprocket adapter by decision; Zoho package/shipment fields are read and shown [MET, shape only]; a live status needs the shipment-lifec… |
| MA-INV-001 | PARTIAL | VALIDATION PENDING | Inventory page with per-location counts: page shows Zoho's on hand / available / committed / reorder with read time [MET]; per-location split [NOT possible: the test org… |
| MA-INV-009 | PARTIAL | DEPENDENCY NOT MET | Inventory-by-location report: needs a per-location Zoho stock read [not available: single location, no per-location fields] |
| MA-INV-022 | PARTIAL | DEPENDENCY NOT MET | Export inventory from all locations: CSV of Zoho's per-item totals exists [MET]; per-location values [not available, see MA-INV-009] |
| MA-MKT-001 | PARTIAL | DEPENDENCY NOT MET | Marketing campaigns: requirements mapped and provider/consent/wording gates listed [MET: document]; drafts and consent-filtered audience count [MET]; credentials, approv… |
| MA-ORD-020 | PARTIAL | DEPENDENCY NOT MET | Order filters: tags, channel, delivery method and return status [MET, pre-existing, re-run green]; risk-level filter [NOT built: MA-ORD-037 fraud/risk is INVESTIGATE, no… |
| MA-ORD-039 | PARTIAL | BLOCKED | Print invoice / GST tax invoice: verify the Zoho invoice number/status fields [MET, observed: invoices[].invoice_number/status/total/date] and show them in Admin [MET]; … |
| MA-ORD-062 | PARTIAL | VALIDATION PENDING | Cancel and restock toggle: no restock toggle is needed because EffyKlean does not commit stock; whether Zoho RELEASES stock when a Sales Order is cancelled must be verif… |
| MA-ORD-080 | PARTIAL | DEPENDENCY NOT MET | Fulfil items: Admin reflects Zoho's statuses at a glance [MET: invoice, payment, package and carrier/tracking read on request and as list columns]; verify the Zoho-manag… |
| MA-ORD-084 | PARTIAL | DEPENDENCY NOT MET | Mark delivered: align with the Zoho/Shiprocket sync [read of Zoho's delivery date is available; NOT wired to change EffyKlean's delivery state: no authoritative state ma… |
| MA-ORD-088 | PARTIAL | BLOCKED | Create shipping label: ownership stays with Zoho/Shiprocket [honoured: no label creation in EffyKlean]; verify the supported label/status hand-off technically [package +… |
| MA-ORD-090 | PARTIAL | BLOCKED | Send invoice to customer: verify invoice number/status [MET] and the supported delivery trigger [NOT verified: sending is a Zoho action needing a write scope and an exte… |
| MA-ORD-123 | PARTIAL | VALIDATION PENDING | Order list column 'Label status': a Zoho packing/label column [MET: 'Zoho packing and label (last read)']; verification against real Shiprocket-populated values [NOT pos… |
| MA-ORD-131 | PARTIAL | DEPENDENCY NOT MET | Order list stats strip incl. fulfilled/delivered metrics: needs authoritative carrier timestamps |
| MA-PRD-047 | PARTIAL | DECISION REQUIRED | Verified-commercial-data marker: marker with verification note, snapshot and 'changed since verified' detection [MET, pre-existing]; authoritative SKU/pack-size source c… |
| MA-PRD-096 | PARTIAL | DEPENDENCY NOT MET | Create an e-mail campaign from selected products: bulk action on the Products page creates a plain-text draft featuring them; audience count under the single consent gat… |
| MA-SET-015 | PARTIAL | DECISION REQUIRED | Packing slip template [MET: native fixed template, see MA-SET-073]; packages / package presets [NOT built: package weights and dimensions are LATER by HU (DC-19, MA-PRD-… |
| MA-SET-021 | PARTIAL | DECISION REQUIRED | Notification e-mail templates (customer): event matrix and draft wording prepared for review [MET: document]; provider direction recorded (GoDaddy first); nothing sent, … |
| MA-SET-022 | PARTIAL | DECISION REQUIRED | Notification e-mail templates (staff): event matrix and draft wording prepared for review [MET: document]; provider direction recorded (GoDaddy first); nothing sent, wor… |
| MA-SET-025 | PARTIAL | DECISION REQUIRED | Apps and sales-channel settings: the needs that exist are exposed as read-only feature switches and credential presence on the Settings overview (server environment, nev… |
| MA-SET-055 | PARTIAL | DECISION REQUIRED | Global collected-tax report: GST report from EffyKlean orders and the included-GST split on the order page exist [pre-existing/MET]; the authoritative collected-tax sour… |
| MF-020 | PARTIAL | VALIDATION PENDING | 15 real products present in the running instance and equal to the old site: source<->live-site parity [MET: 15/15 handle, price, compare-at and SKU match, read from the … |
| MF-054 | PARTIAL | VALIDATION PENDING | Zoho tax/GST mapping [MET locally: modules/orders/tax.py rule with tests; report-only HSN comparison]; invoice trigger and numbering [PARTLY OBSERVED: the sandbox shows … |
| MF-055 | PARTIAL | DEPENDENCY NOT MET | Website-owned customer identity synchronised to the mapped Zoho contact: persistent mapping [MET, pre-existing], first-order create/reuse with duplicate prevention [MET,… |
| MF-070 | PARTIAL | DECISION REQUIRED | Shipment created only by Zoho -> Shiprocket (no second writer): real adapter refuses to create shipments and sends nothing [MET, test]; no Shiprocket endpoint, token or … |
| MF-071 | PARTIAL | VALIDATION PENDING | Shipment status/tracking return path into orders: read-only mirror of Zoho package/invoice state on the Order page and order list [MET]; carrier/tracking VALUES populate… |
| MF-074 | PARTIAL | DEPENDENCY NOT MET | Weight/dimension source [MET: one SKU source in grams/millimetres with database constraints, converted by a single mapping, never partial, never invented, empty until st… |
| MF-078 | PARTIAL | DECISION REQUIRED | GST amounts and invoice number/status visible in Admin [MET: website GST split on the order page, labelled as the website calculation; Zoho invoice number/status read]; … |
| MF-079 | PARTIAL | DECISION REQUIRED | Transactional e-mail events: event matrix and draft wording for review [MET: document]; sender/DNS finding [MET: read-only]; SMTP configuration and a no-send check comma… |
| MF-084 | PARTIAL | DECISION REQUIRED | EffyKlean's own Privacy, Terms, Refund and Contact-information pages: pages exist at /policies/<slug>/ [MET, pre-existing]; legal confirmation of the privacy wording [NO… |
| MF-086 | PARTIAL | DECISION REQUIRED | Blog index and three posts: importer creates the three posts as hidden, unpublished drafts [MET: run against a clean database with the real source folder: 3 BLOG pages, … |
| MF-094 | PARTIAL | DECISION REQUIRED | Customer-initiated WhatsApp link: footer link from the configured number [MET, pre-existing tests]; frozen SPEC compared: it defines WhatsApp only as an optional notific… |
| MF-105 | PARTIAL | DECISION REQUIRED | Customer sign-in help (staff-issued reset link) and data-request export: both built [pre-existing]; wording and link lifetime approval [PENDING: draft wording now in the… |
| MF-107 | PARTIAL | VALIDATION PENDING | Hosting/HTTPS/WSGI server/deployment recipe: WSGI entry, gunicorn dependency, /healthz and fail-closed production settings [pre-existing, tested]; recipe and illustrativ… |
| MF-109 | PARTIAL | DECISION REQUIRED | Process supervision for run_outbox, retry_integrations, reconciliation and dispatch_orders: the jobs table, restart/failure-signal plan and two new scheduled jobs (form … |
| MF-110 | PARTIAL | DECISION REQUIRED | Secrets management: inventory of every secret-like setting with presence-only state [MET: document; 70 variables, 13 secret-like, no value printed]; .env is git-ignored … |
| MF-114 | PARTIAL | VALIDATION PENDING | Performance and load baseline: in-process page and checkout latency measured with a regression test [MET]; Zoho sandbox read latency measured [MET]; provider calls per p… |
| MF-115 | PARTIAL | DEPENDENCY NOT MET | Release acceptance gate: evidence matrix of gate rows with their blockers prepared [MET: see the report's section 8 and the release-gate table]; gate rows 3, 5 and 11 [B… |
| MF-116 | PARTIAL | DECISION REQUIRED | Shopify themes/theme editor/Liquid/app store/billing: underlying EffyKlean needs mapped to native capabilities [MET: page layouts (MA-CNT-004, MA-PRD-046), store brand p… |
| MA-ANA-020 | DEFERRED | DECISION REQUIRED | Search-terms report: needs storing visitors' search text (may contain personal data); privacy and retention rules required first (MF-089 baseline) |
| MA-ANA-023 | DEFERRED | DEPENDENCY NOT MET | Finance reports (gross profit, cost of goods sold, net payments): need an authoritative cost basis (Zoho) and settlement data; neither is readable with the current access |
| MA-CHN-002 | DEFERRED | DECISION REQUIRED | Point of sale: hardware and an in-person payment method are not approved; staff-assisted orders already cover phone/in-person order entry without a terminal |
| MA-CHN-003 | DEFERRED | DECISION REQUIRED | Facebook & Instagram channel: no Meta integration or customer-data transfer authorised; catalogue data is available in the validated feed format |
| MA-CHN-005 | DEFERRED | DECISION REQUIRED | WhatsApp channel: the click-to-chat link exists; marketing through Meta needs a business account, templates and opt-in data flow; notifications remain Zoho's |
| MA-CHN-006 | DEFERRED | DECISION REQUIRED | Agentic/AI channel: no AI provider may receive customer data without a data-minimisation decision; machine-readable product data already exists in the feed |
| MA-CHN-007 | DEFERRED | DECISION REQUIRED | Marketplaces/Shop app: no marketplace is named in existing requirements |
| MA-CHN-008 | DEFERRED | DECISION REQUIRED | Pixels and customer events: optional tracking stays LATER until consent, privacy notice, retention, access control and CSP enforcement exist |
| MA-CNT-008 | DEFERRED | DECISION REQUIRED | Blog comments moderation: minimal moderation/privacy proposal prepared [MET: document]; comments stay disabled until HU approves the safeguards, wording and moderator [a… |
| MA-CNT-011 | DEFERRED | DECISION REQUIRED | Metaobjects: map only an approved structured-content need to a native model [SEARCHED: none found] |
| MA-CNT-020 | DEFERRED | DECISION REQUIRED | Customer chat: minimal use case, data flow and gates described [MET: document]; no provider selected or authorised (Tidio is not authorised) |
| MA-DSC-023 | DEFERRED | DECISION REQUIRED | Free shipping discount: the frozen SPEC allows no separate shipping charge at all (SPEC 3.8, 18.5; AC-7.3, AC-18.3), so there is no shipping amount a discount could remo… |
| MA-INT-011 | DEFERRED | BLOCKED | Zoho Flow workflows: read-only inspection by HU in the Zoho organisation; no Flow access/scope here and HU deferred it to the testing phase |
| MA-INT-022 | DEFERRED | BLOCKED | 'EffyZohoFlow' custom app and Zoho Inventory app: as MA-INT-011 |
| MA-INV-004 | DEFERRED | DEPENDENCY NOT MET | Adjustment history stays Zoho-owned; verify available Zoho history read capability [verified: NOT readable with the current token] |
| MA-INV-010 | DEFERRED | DEPENDENCY NOT MET | Purchase orders stay Zoho-owned; verify Zoho-supported read capability [verified: NOT readable with the current token] |
| MA-INV-011 | DEFERRED | DEPENDENCY NOT MET | Transfers between locations stay Zoho-owned; verify capability [verified: NOT readable/doable with the current token; one location only] |
| MA-INV-020 | DEFERRED | DEPENDENCY NOT MET | Inventory column 'Bin name' stays Zoho data; verify availability [verified: storage locations/bins are disabled in the test organisation, so no bin field is returned] |
| MA-INV-021 | DEFERRED | DEPENDENCY NOT MET | Quick-transfer popover must call only the approved Zoho-owned workflow if supported [not supported with the current token] |
| MA-INV-023 | DEFERRED | DEPENDENCY NOT MET | Incoming popover with 'Create transfer': Zoho returns no incoming figure and no transfer scope exists |
| MA-INV-024 | DEFERRED | DEPENDENCY NOT MET | Purchase-order list (Draft/Ordered/Archived; supplier, destination, received, expected): fields stay Zoho-owned; not readable with the current token |
| MA-MKT-003 | DEFERRED | DECISION REQUIRED | Automations: one supported automation proposed (welcome after verified subscribe); no automated send until wording and provider are approved |
| MA-MKT-004 | DEFERRED | DECISION REQUIRED | Messaging campaigns: WhatsApp-through-Meta direction recorded; templates, opt-in evidence and credentials required before any send |
| MA-MKT-006 | DEFERRED | DEPENDENCY NOT MET | Abandoned-cart automation: needs a customer identity on the cart (the cart is session-only), a consent rule, delay and wording; the proposal is recorded |
| MA-MKT-007 | DEFERRED | DECISION REQUIRED | Social posting/audiences: manual copy only proposed; no API posting and no customer-list transfer without a per-platform data-flow approval |
| MA-MKT-011 | DEFERRED | DECISION REQUIRED | International markets, duties and local pricing: HU's original YES conflicts with the current no-international-markets/duties baseline; both are preserved and the confli… |
| MA-MKT-013 | DEFERRED | BLOCKED | Market-specific domains/rollouts: need DNS/domain changes, which are a restricted action; scope recorded |
| MA-ORD-063 | DEFERRED | DEPENDENCY NOT MET | Cancel and notify customer toggle: notifications are Zoho-managed (email/WhatsApp); wording, consent, provider and credentials are not approved; sending from EffyKlean w… |
| MA-ORD-068 | DEFERRED | DECISION REQUIRED | Edit prices or apply a discount to a placed order: the frozen SPEC says historical orders must preserve the exact pricing and discount applied (SPEC 7.7, 15.8) [conflict… |
| MA-ORD-111 | DEFERRED | DEPENDENCY NOT MET | Abandoned-checkout recovery e-mail: recovery uses the Zoho-managed notification approach with no EffyKlean notification engine; how Zoho receives the abandoned list, plu… |
| MA-ORD-141 | DEFERRED | BLOCKED | Bulk 'Run Flow automation': allowed triggers/actions/permissions/audit must be defined before implementation and the existing Zoho Flow protected; HU deferred Zoho Flow … |
| MA-PRD-070 | DEFERRED | DEPENDENCY NOT MET | Selling plans/subscriptions: 'Subscribe' means update e-mails only (settled); recurring product charges need a payment-mandate capability from the payment provider that … |
| MA-PRD-104 | DEFERRED | BLOCKED | Inventory adjustment on the product page with a reason: Zoho owns stock; the sandbox token lacks the inventory-adjustments scope, so no adjustment can be created or read… |
| MA-PRD-105 | DEFERRED | DEPENDENCY NOT MET | Package picker / Manage packages: package weights and dimensions are LATER by HU (MA-PRD-036/037, DC-19) and a picker would add a competing carrier authority; the weight… |
| MA-SET-004 | DEFERRED | DECISION REQUIRED | Plan, billing, subscription: a Shopify mechanic with no EffyKlean business need evidenced in the SPEC or HU decisions |
| MA-SET-019 | DEFERRED | DECISION REQUIRED | Duties at checkout: conflicts with the no-international-duties baseline; both preserved |
| MA-SET-023 | DEFERRED | DECISION REQUIRED | Order-creation webhook: the equivalent hand-off is the direct EffyKlean -> Zoho Sales Order (sandbox-verified, flags off); no separate outbound webhook is defined or app… |
| MA-SET-024 | DEFERRED | DECISION REQUIRED | Notification SMS/WhatsApp templates: SMS excluded; customer WhatsApp/e-mail shipment notices belong to Zoho/Shiprocket; EffyKlean WhatsApp templates would be marketing t… |
| MA-SET-057 | DEFERRED | DECISION REQUIRED | Legal notice policy: needs HU-supplied legal text; none was written |
| MA-SET-060 | DEFERRED | DECISION REQUIRED | Default rules for policy pages: needs HU/legal-approved policy text; no wording was fabricated |
| MA-SET-061 | DEFERRED | DEPENDENCY NOT MET | Staff notification 'Fulfillment request notification' to a fulfilment service: fulfilment is the Zoho-managed Shiprocket workflow; EffyKlean sends no external notificati… |
| MA-SET-072 | DEFERRED | DECISION REQUIRED | Customer social sign-in (Google, Facebook): separate provider review, data flow, credentials, consent and security validation needed; not inferred from marketing scope |
| MF-063 | DEFERRED | BLOCKED | Existing Zoho Flow 'salesorder add' (Shopify to Zoho) does not conflict with the direct EffyKlean handoff: needs read-only inspection of the Flow in the Zoho organisatio… |
| MF-088 | DEFERRED | BLOCKED | Videos page and media on object storage: storage interface and copy-only verified migration command exist [pre-existing, in-memory bucket tests]; a real bucket [NOT prov… |

## 3. Completion-claim timeline
* I made **no completion claim** during this task: no message said or implied the work was finished. The harness repeatedly asked for a short status; each was answered with one line stating what I was doing.
* An earlier full-suite run mid-task had 6 failures (guard allow-lists, AC index) and I reported none as passing. The final full run had 3 failures (see section 5), fixed afterwards.
* This report is the first and only completion statement, and it says the task is not complete.

## 4. Shortcuts and integrity findings
Scan method: grep of every added line in modified files and every new file (about 11,700 lines) for TODO/FIXME/XXX/HACK, NotImplemented, bare `pass`, skip/xfail, broad `except`, mock/stub/fake, fallback, hard-coded; each match inspected.
* **TODO / FIXME / NotImplemented / `pass` / skip / xfail: none introduced.**
* **Broad `except Exception` (7, each with a reason comment):** the Storefront password gate reads its setting (2: fails **open** with a log line if the setting cannot be read, so a database hiccup could expose a store that the Director locked; HU+DI should decide open vs closed); the storefront profile read in `site.py` (1: falls back to the built-in defaults, so a database problem cannot blank a page); the Settings overview rendering without a database (1); robots.txt (1: a settings problem must not break it); the Inventory page showing a short, safe reason when the Zoho read fails (1); scheduled-report error recording, retried at the next run (1). None hides a business result; the gate's fail-open is a security trade-off to review.
* **Stubs/mocks in tests only**, labelled by evidence type. `LocalZohoStub` is used for simulated Zoho behaviour; the real adapter is tested over a fake transport. None of this proves behaviour against Zoho.
* **Not implemented on purpose (scope deferrals):** everything in section 8.
* **Tests changed (all disclosed):** (a) allow-list guard tests extended for each new field, file, migration, table, middleware, route, capability and import (test_catalogue_model, test_catalogue_boundaries, test_f05/f06/f07b boundaries, test_foundation_boundaries, test_i01/i03, test_identity_boundaries/model, test_sec_request_boundary, test_migrations, test_admin_workflow): each guard still checks the same protection and now names the new item. (b) `test_build_customers_pack`: the old MA-CUS-041 assertions ("Cannot be deleted", "Order history is never deleted") were replaced because HU's 23-Oct decision made deletion available; the protection "orders are always kept" is now asserted byte-for-byte in `test_build152_customer_deletion`. (c) Footer/header link tests (test_storefront_shell, test_policy_pages, test_storefront_policies, test_videos, test_distributor_applications) and one Zoho-unknown-item test (test_i02) were already modified in the working tree before this task (HU's 23-Oct footer decision and earlier work); I did not alter them. (d) `AC_TEST_INDEX.md` regenerated by `scripts/ac_index.py`. No test was removed to get green, and none was skipped.
* **New defaults/permissions (need HU+DI review):** new capabilities `CUSTOMER_DELETE` and `CUSTOMER_TAX_EXEMPTION` (Admin and Director), `STORE_CONTACT_MANAGE` and `STOREFRONT_GATE_MANAGE` (Director only); staff invitation / MFA-reset by one-time link (replaces the "command line only" wording; needs a security review); a global middleware for the storefront password page; price breaks take no coupon or combo on a tiered line (literal reading); what "delete a customer" deletes versus keeps; Zoho invoice/package state mirrored read-only; custom forms and campaign drafts use existing Admin capabilities (`REVISION_*`, `CONTACT_REVIEW`, `CUSTOMER_EXPORT`).

## 5. Validation (exact commands; evidence kept separate)
* Full suite: `scratchpad/runtests.sh -q -x --maxfail=50 --junitxml=final.xml tests` (loads the git-ignored `.env`, test settings, throwaway PostgreSQL 17 on 127.0.0.1:5432): **3011 passed, 3 failed in 2236 s (0:37:16).** The 3 failures were `test_f06_boundaries` allow-lists for the new `forms_pages.py` module and its three routes. I extended the allow-lists, changed the module's imports to the form the boundary test accepts, and re-ran: `pytest tests/test_f06_boundaries.py tests/test_build152_custom_forms.py tests/test_ac_structural_evidence.py` → **52 passed**.
* **The full suite was not re-run end to end after that last change**; only the files above were. The change touched `forms_pages.py` imports and one allow-list.
* `ruff check .` → exit 0 ("All checks passed!"); `ruff format --check .` → "450 files already formatted"; `manage.py makemigrations --check --dry-run` → "No changes detected"; `manage.py check` → no issues (1 silenced).
* Read-only Zoho sandbox probes: see `BUILD152_ZOHO_READONLY_EVIDENCE_*.md` (only GETs plus the standard OAuth refresh POST, disclosed there).
* **CI did not run** (nothing pushed). Browser/visual checks were **not** performed this run; storefront and Admin pages were exercised through Django's test client only.
* Environment limits: the Docker daemon (development database `effyklean`) was not running and needs sudo, so that database was never inspected or migrated.

## 6. Repository reconciliation
* Repository `EffyKleanProject`, branch `main`, HEAD `ad69d92` (same as at the start; `origin/main` is the same commit as at the start). Stashes: 0. Staged: 0.
* Working tree: 88 modified tracked files (3035 insertions, 192 deletions) and 83 untracked files (new modules, templates, migrations, tests, and the documents in `docs/ImplementationPlan/AgentReports/`). The 14 modified files and untracked documents that existed before this task are preserved (`config/settings/local.py`, `modules/backoffice/mfa.py`, storefront pages, several tests, `AgentReports/build245_reconciliation_20261023_152655_IST.csv`, the two "COMPLETE REPORT…22OCT2026" documents). They cannot be cleanly separated by Git alone because they sit in the same uncommitted tree.
* New migrations (all in the repo, **none applied to `effyklean`**): catalogue 0016–0019, orders 0035–0040, identity 0009, backoffice 0005.
* Nothing was committed, pushed, reset, discarded or rewritten. Commit authorship note: no commit was made, so no co-author trailer exists (project rule: never add one).

## 7. Assumptions and unverified behaviour
* Every new page was exercised through the Django test client, not a browser; layout and accessibility are unobserved.
* The Zoho contact update request (MF-055) has never been sent to Zoho (the token lacks the scope).
* Old-site URL redirects were built from the public sitemap; a live crawl was not possible.
* The 2.6 s product-list figure under the real Zoho adapter is an estimate (15 inline availability calls × about 175 ms).
* Draft e-mail wording, deployment spec and latency budget are proposals, not approved or validated.
* Migrations were exercised only on throwaway databases.

## 8. Blocker audit (every unfinished record is in the CSV with its exact next action)
Genuine external blockers (evidence in the Zoho evidence document): token scopes missing (MA-INV-004/010/011/020/021/023/024, MA-PRD-104, MA-ANA-014/025, MF-055 live update); Zoho Payments settlement 404 and payout 401 (MA-ANA-015/023); Spaces not provisioned (MF-088); Zoho Flow inspection deferred by HU (MF-063, MA-INT-011/022); legal text (MF-084, MA-SET-057/060); accountant rules (MA-CUS-014/045); e-mail credentials and approved wording (MF-079, MF-105, MA-SET-021–024); hosting (MF-107/109/114/115).
Decision conflicts needing HU+DI (nothing was decided here): P1-09 unverified MRP and Sale badge (MA-PRD-047); `dispatch_orders` versus Zoho-managed shipping (MF-070/109); international markets and duties (MA-MKT-011, MA-SET-019); inline Zoho availability calls on customer pages (MF-114); open versus closed behaviour of the storefront password gate.
Work I could have done and did not: none that I judge independently actionable and safe. Items I considered and declined as customer-visible business changes: fail-closed MRP display (MA-PRD-047).

## 9. Highest risks and discrepancies
1. Product list makes 15 sequential Zoho calls per page with the real adapter (slow page, and a Zoho outage turns the page into a 503).
2. Scheduling `dispatch` with the real adapter would push paid orders to "shipment failed".
3. New global middleware (storefront gate) fails open if its setting is unreadable.
4. Permission-matrix additions and the one-time-link staff enrolment need HU+DI security review.
5. 12 new migrations are unapplied to the development database; applying them needs a verified backup first.
6. The MRP shown for all 15 live products is still provisional (imported compare-at prices).
7. Customer deletion removes the sign-in account, notes and tags only; orders and consent history stay (HU 23-Oct), which should be confirmed against legal advice.

## 10. Deliverables and next step
Deliverables in `docs/ImplementationPlan/AgentReports/`: `BUILD152_DEPLOYMENT_PROCESSES_AND_SECRETS_2026-10-24_044318.md`, `BUILD152_ITEM_LEDGER_2026-10-24_053255.csv`, `BUILD152_MARKETING_CHANNEL_AND_CONTENT_PROPOSALS_2026-10-24_044448.md`, `BUILD152_NOTIFICATION_EVENT_MATRIX_AND_DRAFT_WORDING_2026-10-24_043549.md`, `BUILD152_PERFORMANCE_BASELINE_2026-10-24_044330.md`, `BUILD152_URL_PARITY_MAP_2026-10-24_043515.md`, `BUILD152_ZOHO_PROBES_2026-10-24_043502.py.txt`, `BUILD152_ZOHO_READONLY_EVIDENCE_2026-10-24_043502.md` (this report included).
Continuity documents updated: `PROJECT_LOG.md`, `CLAUDE.md` (state paragraph), `README.md`, and the Delta status register.
**Next actionable step without waiting for a decision:** HU starts the development database, takes a backup, and authorises applying the 12 new migrations; then the Director reviews drafts. Run `/clear` before the next task.

### Final self-audit
I re-read `EffykleanSSD_Audit_Requirement.md` and the 22-Oct mandate against this report. Challenges I tried: (a) a DONE row resting only on a test name — I checked each cited test exists and passed in the final run (the CSV tags each as passed or not matched; parametrised tests match by base name); (b) tests that ran only before the last code change — disclosed in section 5; (c) a blocker that was actually doable — none found; (d) premature completion claims — none made. Known gap: the full suite was not repeated after the final small fix.
