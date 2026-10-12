# Comparison 1: Shopify Admin vs Django EffyKlean Admin

**Date:** 2026-10-12 · **Repository state:** HEAD `4af12e0`, 28 uncommitted paths (none staged); nothing was changed in the repository except new documents.
**Status:** ASSESSMENT ONLY. Not a requirement and not an implementation authorization. Every priority is a **recommendation**; HU+DI decide. `SPEC.md` v0.8, `ARCHITECTURE.md` and AD-01..AD-17 are not reopened.


## 1. Method and evidence limits (read first)

| Item | Statement |
|---|---|
| Shopify side | **NOT re-observed in this session.** The Shopify Admin is behind HU's signed-in browser; this session has no browser or Admin session that can be attached, and `WebFetch` cannot authenticate. Shopify facts are therefore **carried forward** from the read-only live walks of 2026-10-05 and 2026-10-10 (`SHOPIFY_ADMIN_LIVE_WALK_2026_10_10.md`, `SHOPIFY_ADMIN_UI_FIELD_PAGE_FLOW_MAP.md`, `SHOPIFY_ADMIN_FUNCTION_INVENTORY.md`, 2026-07 API restamp). Tier codes OBS, OBS-L, API, DOC, UNK are those files' codes. DOC and UNK rows are **not verified**. |
| Django side | **Re-verified this session** by static inspection: `modules/backoffice/urls.py` (128 route patterns), `modules/backoffice/shell.py` sidebar, view modules, `git status`. Evidence class `S` (see `PRODUCTION_READINESS_REGISTER.md` §0). No test run, no browser run, no provider contact. |
| What changed vs 2026-10-10 | Section 3 lists every inventory row whose status differs now, with the route evidence. All other rows keep the carried status and are labelled so. |
| Not done | No Shopify setting read or changed; no draft, order, payment or shipment created; no code changed. |
| Local Admin instance | A dev server is running (127.0.0.1:8000) with an **empty catalogue**; the Admin sign-in is protected by MFA and was not entered. Admin behaviour is therefore evidenced by code and prior tests, not by a fresh run. |

Status codes are those of the inventory: IMPL implemented, SIM labelled simulation, PART partial, MISS not implemented, BLK blocked by a named decision, N/A excluded or Shopify-only, UNV not verified.

## 2. Area-level comparison (SA-A, one row per Shopify Admin area)

| ID | Shopify Admin area | Shopify location | Observed Shopify behaviour (carried, OBS-L 2026-10-10) | Django EffyKlean Admin counterpart (verified at HEAD) | Status | Inventory rows |
|---|---|---|---|---|---|---|
| SA-A01 | Home (dashboard) | `/admin (Home)` | Sessions, sales, orders, conversion cards; to-do; alerts feed; recent activity | `/EKIAdmin2026` Home (`home.py`), attention list | PART | SYS-006..008, SYS-020, SYS-022 |
| SA-A02 | Orders > list | `/admin/orders` | Columns, status/payment/fulfilment filters, tabs, sort, saved views, export, print | `orders` (ops_views.order_list) | PART | ORD-001..023 |
| SA-A03 | Orders > detail | `/admin/orders/<id>` | Customer card, timeline, tags, risk, fulfilment, Shiprocket tracking, edit, refund, cancel | `orders/<reference>` + cancel, edit, refund, delivery, return, replacement, retry-zoho, retry-shipment | PART | ORD-024..099 |
| SA-A04 | Drafts | `/admin/draft_orders` | Create/send/complete draft orders, PO number, tax-exempt | none | MISS (BLK: DC-22) | DRF-001..021 |
| SA-A05 | Products > list/form | `/admin/products` | List filters, bulk bar, export/import, form (title, media, price, SEO, variants) | `products`, `products/new`, `<id>`, `commercial`, `revisions/*`, `export`, `bulk`, `review-queue` | PART | PRD-001..101 |
| SA-A06 | Collections | `/admin/collections` | Manual/automated collections, sort, SEO | none (category/product_type are product attributes) | MISS (N/A: no approved requirement) | COL-001..010 |
| SA-A07 | Inventory | `/admin/inventory` | On hand, committed, available, incoming, bin | none (Zoho is stock authority, SPEC §14) | N/A by SPEC | INV-001..018 |
| SA-A08 | Purchase orders / Transfers | `/admin/purchase_orders, /transfers` | Empty on store; create buttons | none | N/A by SPEC | INV-* |
| SA-A09 | Customers | `/admin/customers` | List, columns, notes, tags, export, merge, delete | `customers`, `customers/<key>`, notes, tags, export | PART | CUS-001..054 |
| SA-A10 | Segments | `/admin/customers/segments` | Saved filters | none | MISS (DEFER) | CUS-021, 022, 054 |
| SA-A11 | Companies (B2B) | `/admin/companies` | Empty on store | `business-accounts`, `distributor-applications`, `bulk-enquiries`, `bulk-quotes` | DIFFERENT MODEL | CUS-030..039 |
| SA-A12 | Discounts | `/admin/discounts` | Code/automatic discounts, eligibility, combinations | `discounts`, `coupons/*`, `distributor-pricing/*` | PART | DSC-001..041 |
| SA-A13 | Content > Files | `/admin/content/files` | File library, alt text, references | none (media managed with products/content pages) | MISS | CNT-* |
| SA-A14 | Content > Menus | `/admin/content/menus` | Navigation menus | `content/nav/*` | IMPL | CNT-* |
| SA-A15 | Content > Blog posts | `/admin/articles` | Blog posts, author, tags | `content/pages/*` (pages); blog posts read from `media/blog_source`; no blog editor route | PART | CNT-007 |
| SA-A16 | Content > Metaobjects | `/admin/content/metaobjects` | Custom structured content | none | N/A | CNT-* |
| SA-A17 | Markets / Catalogs / Rollouts | `/admin/markets` | Regions, price lists, rollouts | `distributor-pricing/*` (CR-006) covers B2B price only | N/A (single market, INR) | MKT-* |
| SA-A18 | Analytics > Reports | `/admin/reports` | Report library, explorations | `reports` (baseline sales reports) | PART | ANA-001..027 |
| SA-A19 | Analytics > Live View | `/admin/live` | Live visitors | none | MISS (DEFER) | ANA-* |
| SA-A20 | Growth (Attribution, Autopilot, Campaigns) | `/admin/marketing` | Channel attribution, campaigns | none | N/A (no campaign engine, SPEC) | MKT-*, CHN-* |
| SA-A21 | Settings > General | `/admin/settings/general` | Store profile, currency INR, order ID format, auto-archive | `settings` (read-mostly), order ID EKI-MMYY-DDxxxxx | PART | SET-001.. |
| SA-A22 | Settings > Plan / Billing | `/admin/settings/plan` | Plan and bills | not applicable (self-hosted) | N/A | SET-* |
| SA-A23 | Settings > Users and permissions | `/admin/settings/account` | Users, roles, secure sign-in | `staff`, `staff/<pk>/role`, `toggle`, `signins`, `mfa`, `account*` | PART (no invite/create: D-F2) | USR-001..032 |
| SA-A24 | Settings > Payments | `/admin/settings/payments` | Razorpay, PayPal, capture method | `payments` views, `unresolved-payments`, `reconciliation`, `integrations` (Zoho Payments selected, CR-007) | PART (no provider proof) | SET-*, INT-002/003 |
| SA-A25 | Settings > Checkout | `/admin/settings/checkout` | Unavailable on plan | none | N/A | SET-011 |
| SA-A26 | Settings > Customer accounts | `/admin/settings/customer_accounts` | Sign-in, self-serve returns | none (account rules in code) | MISS (DEFER) | SET-013 |
| SA-A27 | Settings > Shipping and delivery | `/admin/settings/shipping` | Profiles, split shipping, labels, routing | none (Zoho -> Shiprocket; SPEC §18) | N/A / BLK | SET-* |
| SA-A28 | Settings > Taxes | `/admin/settings/taxes` | India manual tax, prices include 18% | none in Admin (GST in code; Zoho mapping open B-07) | BLK | SET-* |
| SA-A29 | Settings > Locations | `/admin/settings/locations` | 3 locations | none (HU settled) | N/A | SET-* |
| SA-A30 | Settings > Notifications | `/admin/settings/notifications` | Customer and staff e-mail templates | none (no provider, SPEC §20 open D-09) | BLK | SET-021, 022 |
| SA-A31 | Settings > Customer privacy / Policies | `/admin/settings/privacy` | Privacy, cookie banner, policies | policy pages in code (`policy_pages.py`); Privacy/Terms unpublished pending HU legal text | PART | SET-* |
| SA-A32 | Settings > Apps and sales channels | `/admin/settings/apps` | Flow, WhatsApp, Zoho Inventory, Tidio, Weglot, Search & Discovery | `integrations` (readiness/health) | DIFFERENT MODEL | INT-001..023 |
| SA-A33 | Settings > Domains / Customer events / Brand / Languages / Metafields | `/admin/settings/domains` | Domain, pixels, brand assets, translations, custom fields | none | MISS / N/A | SET-* |
| SA-A34 | Search, audit, notifications, help | `global` | Global search, activity log, notification centre | `search`, `audit`, `audit/export`, `records` (Director deletion) | PART | SYS-001..011 |

Area rows: 34. Django Admin sidebar (shell.py NAV): Home; Sales (Orders, Customers, Subscribers, Replacements, Unresolved payments, Reconciliation, Returned packages, Contact messages, Bulk enquiries, Distributor applications, Bulk quotes, Business accounts); Catalogue (Products, Catalogue review, Discounts, Distributor pricing, Content); Insights (Reports); Settings (Integrations, Settings, Staff, Delete records).

## 3. Re-verified differences since the 2026-10-10 inventory (SA-D)

| ID | Inventory row | Carried status | Status now | Evidence (class S, static) |
|---|---|---|---|---|
| SA-D01 | ORD-021 Export orders (CSV) | MISS | MISS (unchanged (confirmed)) | CONFIRMED: no `orders/export` route |
| SA-D02 | ORD-034 Staff comments on the order timeline (add, with attribution) | MISS | MISS (unchanged (confirmed)) | CONFIRMED: no order comment route |
| SA-D03 | ORD-036 Archive / unarchive order | MISS | MISS (unchanged (confirmed)) | CONFIRMED: no archive route |
| SA-D04 | DRF-001 Draft order list | BLK | BLK (unchanged (confirmed)) | CONFIRMED: no draft-order routes |
| SA-D05 | PRD-014 Export products (CSV) | MISS | IMPL (CHANGED) | route `products/export` |
| SA-D06 | PRD-073 Bulk edit (spreadsheet-style editor) | MISS | PART (CHANGED) | route `products/bulk` exists; spreadsheet-style editor not verified |
| SA-D07 | PRD-074 Bulk change status, tags, category | MISS | PART (CHANGED) | route `products/bulk` exists; scope (status/tags/category) not verified |
| SA-D08 | CUS-010 Customer notes (private) | MISS | IMPL (CHANGED) | route `customers/<key>/notes` |
| SA-D09 | CUS-011 Customer tags | MISS | IMPL (CHANGED) | route `customers/<key>/tags`, `tags/remove` |
| SA-D10 | CUS-026 Customer export | MISS | IMPL (CHANGED) | route `customers/export`; capability CUSTOMER_EXPORT (insight_views.py) |
| SA-D11 | DSC-015 Duplicate discount | MISS | IMPL (CHANGED) | route `coupons/<code>/duplicate` |
| SA-D12 | DSC-017 Bulk-generate unique codes | MISS | IMPL (CHANGED) | route `coupons/bulk` |
| SA-D13 | INT-004 Outbox / worker view | BLK | PART (CHANGED) | AD-07 outbox and `run_outbox` built 2026-10-11; order actions `retry-zoho`, `retry-shipment` exist; no dedicated outbox list page found in URLconf |
| SA-D14 | USR-011 Staff activity / sign-in history | MISS | IMPL (CHANGED) | route `staff/<pk>/signins` |
| SA-D15 | SYS-002 Audit export | MISS | IMPL (CHANGED) | route `audit/export` (urls.py `audit/export`) |
| SA-D16 | PRD-097 Export products dialog | MISS | IMPL (CHANGED) | route `products/export` |

Rows re-verified: 16. Everything else in Appendix A carries its 2026-10-10 status and is **not** re-verified one by one (see §5).

## 4. Counts

| Status | Carried 2026-10-10 | Now |
|---|---|---|
| IMPL* | 63 | 63 |
| IMPL | 18 | 27 |
| SIM | 9 | 9 |
| PART | 41 | 44 |
| MISS | 157 | 146 |
| BLK | 52 | 51 |
| N/A | 145 | 145 |
| UNV | 9 | 9 |
| **Total rows** | 494 | 494 |

By evidence tier of the Shopify side: OBS 287, OBS-L 129, DOC 36, — 23, UNK 14, API 5.

By family: Orders 119, Draft orders 13, Products 87, Collections 10, Inventory, purchasing, transfers 18, Gift cards 2, Customers, segments, B2B 45, Discounts 29, Content 23, Marketing, markets 11, Sales channels 8, Analytics and reports 27, Settings 51, Integrations, apps, automation 15, Staff, roles, security 20, System, search, home 16.

## 5. Coverage statement and unverified items

* **Covered:** every Shopify Admin area recorded in the 2026-10-10 live walk (34 area rows above), and all 494 function rows of the inventory (Appendix A), each mapped to a Django counterpart, an explicit difference, or a recorded exclusion.
* **Not covered / unverified:** (1) the live Shopify Admin was **not re-opened today**, so any Shopify change after 2026-10-10 is unknown; (2) DOC rows (standard Shopify capabilities not seen on this store) and UNK rows (app iframes, Flow contents, Growth, billing) are leads only; (3) the inventory lists lazily loaded Analytics reports only partly (about 49 visible of more); (4) Django behaviour was not re-run: statuses marked IMPL rest on static route evidence plus earlier tests; (5) statuses of 478 rows are carried, not re-derived.
* **To close (needs HU):** a signed-in browser session attached for a read-only re-walk; until then this comparison is as current as 2026-10-10 for Shopify.

## 6. Key findings

1. The Django Admin covers the **operational core** (orders with cancel/edit/refund record/replacement/returns, reconciliation, customers with notes/tags/export, coupons and distributor pricing, catalogue revisions with approval, content, staff with MFA, audit with export). It deliberately omits Shopify surfaces with no EffyKlean requirement (inventory authority, purchasing, markets, channels, apps, billing).
2. Largest genuine gaps (recommendations): **order export** (ORD-021), **order comments/timeline completeness** (ORD-033/034), **draft/quote orders** (DRF, blocked on DC-22), **transactional e-mail templates and resend** (SET-021/022, ORD-089, blocked on DC-21), **outbox list page** (INT-004), **staff invite/create** (USR-003, D-F2), **low-stock view** (blocked on Zoho stock read), **segments/filters** (CUS-003/021).
3. Twelve carried statuses were stale (now more implemented than recorded): audit export, staff sign-in history, customer notes, tags and export, product export (two rows), discount duplicate and bulk code generation, product bulk route (two rows, partial) and the outbox view (partial because AD-07 now exists).
4. Every Zoho, Shiprocket and Zoho Payments result in the Admin is a **labelled simulation or mocked HTTP**; none is provider-proven (register §0).


## Appendix A. All inventory rows (SA, IDs as in `SHOPIFY_ADMIN_FUNCTION_INVENTORY.md`)

Columns: ID, Shopify capability (truncated), Shopify evidence tier, status carried, status now, carried recommendation (a recommendation, not a decision). `Δ` marks the §3 re-verified rows.


### ORD: Orders (119)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| ORD-001 | List of orders with pagination | OBS | IMPL* | IMPL* | COVERED |
| ORD-002 | Status tabs (All, open, cancelled, etc.) | OBS | IMPL* | IMPL* | COVERED |
| ORD-003 | Free-text search (EKI ID, name, email, phone, GST, reference) | OBS | IMPL* | IMPL* | COVERED |
| ORD-004 | Filter by payment status | OBS | IMPL | IMPL | COVERED |
| ORD-005 | Filter by shipment status | OBS | IMPL | IMPL | COVERED |
| ORD-006 | Filter by date range | OBS | IMPL | IMPL | COVERED |
| ORD-007 | Sort by any column (date, total, customer) | OBS | MISS | MISS | ACCEPT: cheap, no rule needed |
| ORD-008 | Column: items count | OBS | MISS | MISS | ACCEPT: orders spanning several products are hard to scan wi |
| ORD-009 | Column: "Fulfil by" date (dispatch due) | OBS | MISS | MISS | ACCEPT: supports the dispatch rule; derive from the order da |
| ORD-010 | Column: sales channel | OBS | N/A | N/A | REJECT: single channel; revisit with I4 |
| ORD-011 | Column: delivery method | OBS | N/A | N/A | REJECT: one method only |
| ORD-012 | Column: delivery status (carrier) | OBS | SIM | SIM | DEFER: until DC-18 gives real status |
| ORD-013 | Column and filter: tags | OBS | MISS | MISS | DEFER: with ORD-035 |
| ORD-014 | Column: flags (risk, payment issues, edited, cancel requested) | OBS | MISS | MISS | ACCEPT: show reconciliation, edited, cancelled flags that al |
| ORD-015 | Saved views / custom list tabs | OBS | PART | PART | DEFER: little value at current volume |
| ORD-016 | Choose visible columns | OBS-L | MISS | MISS | DEFER: not needed at current volume |
| ORD-017 | Filter by customer / customer type (B2C, Distributor, Bulk) | DOC | PART | PART | ACCEPT: after Distributor/Bulk orders exist |
| ORD-018 | Filter by product / SKU | DOC | MISS | MISS | ACCEPT: finding every order for one product is a routine ope |
| ORD-019 | Filter by amount range | DOC | MISS | MISS | DEFER |
| ORD-020 | Filter by tags, channel, risk level, delivery method, return status, location | OBS | MISS | MISS | DEFER: revisit after the underlying data exists |
| ORD-021 | Export orders (CSV) | OBS | MISS | MISS Δ | ACCEPT: Part 1 M2 recommendation stands |
| ORD-022 | Print selected orders (from list) | OBS-L | MISS | MISS | DEFER: with ORD-038 |
| ORD-023 | Order count / stats strip (orders, items ordered, returns, fulfilled) | OBS-L | MISS | MISS | DEFER: Reports covers the need |
| ORD-030 | View customer, contact, addresses | OBS | IMPL* | IMPL* | COVERED |
| ORD-031 | View line items (title, SKU, price, quantity, line total) | OBS | IMPL* | IMPL* | COVERED |
| ORD-032 | View payment summary (subtotal, discount, GST, total, paid) | OBS | IMPL* | IMPL* | COVERED |
| ORD-033 | View timeline of events | OBS | PART | PART | ACCEPT: Part 1 B4 |
| ORD-034 | Staff comments on the order timeline (add, with attribution) | OBS | MISS | MISS Δ | ACCEPT: Part 1 B5 |
| ORD-035 | Order tags (add, remove) | OBS | MISS | MISS | DEFER |
| ORD-036 | Archive / unarchive order | OBS | MISS | MISS Δ | DEFER: lists are filterable by state; no case for hiding ord |
| ORD-037 | Fraud / risk level display and analysis | OBS-L | MISS | MISS | FLAG: no source of risk data is identified (Razorpay risk fi |
| ORD-038 | Print order / packing slip | OBS | MISS | MISS | DEFER: dispatch is Zoho/Shiprocket-driven; revisit when DC-1 |
| ORD-039 | Print invoice / GST tax invoice | OBS | PART | PART | FLAG: confirm whether the customer-facing invoice is Zoho's  |
| ORD-040 | Source / attribution (first session, referral) | OBS | MISS | MISS | DEFER: with H2 |
| ORD-041 | Customer order count shown on the order | OBS | PART | PART | ACCEPT: small, derived data |
| ORD-042 | Payment reference (confirmation #, gateway, checkout reference) | OBS | IMPL* | IMPL* | COVERED |
| ORD-043 | Order references (EKI ID, checkout ref, Zoho ref, Shiprocket ref) | OBS | IMPL* | IMPL* | COVERED |
| ORD-044 | Integration activity panel (Zoho, Shiprocket, Razorpay) | OBS | SIM | SIM | COVERED (stub level) |
| ORD-045 | Link to customer record | OBS | IMPL* | IMPL* | COVERED |
| ORD-046 | Next / previous order navigation | OBS-L | MISS | MISS | DEFER |
| ORD-047 | Order notes from the customer (checkout notes) | DOC | UNV | UNV | FLAG: confirm whether checkout carries a customer note; if s |
| ORD-048 | Additional order details / custom attributes (company name, GST number from cart) | OBS | IMPL* | IMPL* | COVERED |
| ORD-049 | Residential-address flag on the delivery address | — | MISS | MISS | ACCEPT: Part 1 B3 |
| ORD-060 | Cancel order (Admin) | OBS | IMPL* | IMPL* | COVERED |
| ORD-061 | Cancel with reason | OBS | IMPL* | IMPL* | COVERED |
| ORD-062 | Cancel and restock inventory toggle | OBS | N/A | N/A | REJECT: Zoho owns stock |
| ORD-063 | Cancel and notify customer toggle | OBS | BLK | BLK | DEFER: until DC-21 |
| ORD-064 | Customer-initiated cancellation | OBS | IMPL* | IMPL* | FLAG: D-C2 (Part 1 §11) |
| ORD-065 | Edit delivery name, address, phone before handover | OBS | IMPL* | IMPL* | COVERED |
| ORD-066 | Edit customer e-mail, GST number, GST name | OBS | IMPL* | IMPL* | FLAG: D-C1 (Part 1 §11) |
| ORD-067 | Edit line items (add, remove, change quantity) | OBS | N/A | N/A | REJECT: Part 1 B8 |
| ORD-068 | Edit prices or apply a discount to a placed order | OBS | N/A | N/A | REJECT: same reason |
| ORD-069 | Refund (money back) | OBS | N/A | N/A | REJECT: frozen rule |
| ORD-070 | Refund execution after an approved cancellation | OBS | BLK | BLK | ACCEPT: after DC-15 (Part 1 B10) |
| ORD-071 | Return items / create return | OBS | N/A | N/A | REJECT: frozen rule |
| ORD-072 | Replacement (damaged / wrong item), with evidence | OBS | IMPL* | IMPL* | COVERED |
| ORD-073 | Exchange | OBS | N/A | N/A | REJECT: covered by replacement |
| ORD-074 | Store credit issue | OBS | N/A | N/A | REJECT: not in SPEC; no loyalty or credit |
| ORD-075 | Return label / return shipping | DOC | N/A | N/A | REJECT: with ORD-071 |
| ORD-076 | Inspect returned package before restock | OBS | BLK | BLK | ACCEPT: after DC-17 |
| ORD-077 | Mark as paid (manual payment) | OBS | BLK | BLK | ACCEPT: after DC-22 |
| ORD-078 | Capture authorized payment | OBS-L | N/A | N/A | FLAG: Razorpay capture mode (auto vs manual) is not recorded |
| ORD-079 | Request payment / send payment link | DOC | MISS | MISS | DEFER: with ORD-110 |
| ORD-080 | Fulfil items (create fulfilment) | OBS | N/A | N/A | REJECT: Part 1 B18 |
| ORD-081 | Add tracking number manually | OBS | N/A | N/A | REJECT: Part 1 B18 |
| ORD-082 | Retry failed Zoho submission / Shiprocket shipment request | OBS | SIM | SIM | COVERED (stub level) |
| ORD-083 | Resolve a fulfilment exception | OBS | SIM | SIM | COVERED (stub level) |
| ORD-084 | Mark delivered (record delivery) | OBS | SIM | SIM | COVERED (stub level) |
| ORD-085 | Hold / release fulfilment hold | OBS-L | MISS | MISS | DEFER: no case recorded; Admin can already hold via cancel/e |
| ORD-086 | Move fulfilment to another location | OBS-L | MISS | MISS | REJECT: HU settled the locations; Zoho chooses |
| ORD-087 | Split fulfilment across locations | OBS | N/A | N/A | FLAG: confirm whether multi-package/multi-location shipments |
| ORD-088 | Create shipping label | OBS-L | N/A | N/A | DEFER: with DC-18 |
| ORD-089 | Resend order confirmation / invoice / shipping e-mail | OBS | BLK | BLK | DEFER: until DC-21 |
| ORD-090 | Send invoice to customer (draft order invoice) | OBS | BLK | BLK | DEFER: with drafts |
| ORD-091 | Duplicate order | OBS-L | MISS | MISS | DEFER: with drafts |
| ORD-092 | Merge / split orders | DOC | N/A | N/A | REJECT: financial record integrity |
| ORD-093 | Unarchive order | OBS-L | MISS | MISS | DEFER: with ORD-036 |
| ORD-094 | Mark order as "needs attention" / resolve reconciliation item | OBS | IMPL* | IMPL* | COVERED |
| ORD-095 | Cancel a Distributor/Bulk order as an Admin case | OBS | BLK | BLK | ACCEPT: when D/B orders exist (Part 1 B20) |
| ORD-100 | Bulk select orders on the list | OBS | MISS | MISS | DEFER |
| ORD-101 | Bulk tag / untag | OBS | MISS | MISS | DEFER |
| ORD-102 | Bulk archive | OBS | MISS | MISS | DEFER |
| ORD-103 | Bulk fulfil / create labels | DOC | N/A | N/A | REJECT |
| ORD-104 | Bulk print packing slips / invoices | OBS-L | MISS | MISS | DEFER |
| ORD-105 | Bulk cancel | OBS-L | N/A | N/A | REJECT: unsafe at volume; single action keeps the audit clea |
| ORD-106 | Bulk export selected | OBS-L | MISS | MISS | ACCEPT: with ORD-021 |
| ORD-107 | Order ID prefix and format setting | OBS | IMPL | IMPL | [UNAPPROVED historical recommendation — NOT A HU+DI DECISION |
| ORD-108 | Auto-archive when paid and fulfilled | OBS | MISS | MISS | DEFER: with ORD-036 |
| ORD-109 | Order status page / customer order tracking | OBS | IMPL* | IMPL* | COVERED |
| ORD-110 | Abandoned checkouts list | OBS | MISS | MISS | FLAG: an abandoned checkout holds no Order and may hold pers |
| ORD-111 | Abandoned checkout recovery e-mail | OBS | BLK | BLK | DEFER |
| ORD-112 | Payment reminder | OBS | BLK | BLK | DEFER |
| ORD-113 | Order-edit request from customer ("change request") | OBS | MISS | MISS | DEFER: Customer Care handles it |
| ORD-114 | Disputes / chargebacks | OBS | MISS | MISS | DEFER: DC-16 |
| ORD-115 | Delivery estimate (manual dates) | OBS | MISS | MISS | DEFER |
| ORD-116 | Order routing rules to locations | OBS | N/A | N/A | REJECT |
| ORD-120 | Order list column "Destination" (ship-to) | OBS-L | MISS | MISS | ACCEPT: helps GST reporting and dispatch checks |
| ORD-121 | Order list column "Return status" | OBS-L | N/A | N/A | REJECT: frozen rule |
| ORD-122 | Order list column "PO number" | OBS-L | MISS | MISS | DEFER: with DRF-009 |
| ORD-123 | Order list column "Label status" | OBS-L | SIM | SIM | DEFER: DC-18 |
| ORD-124 | Order detail: "View map" of the delivery address | OBS-L | MISS | MISS | DEFER |
| ORD-125 | Order detail: source session ("1st session from Google, 3 sessions"), "View conversion details" | OBS-L | MISS | MISS | DEFER: with ANA-012 |
| ORD-126 | Order detail: "This is their 1st order" customer-history line | OBS-L | MISS | MISS | ACCEPT: derived data (see ORD-041) |
| ORD-130 | Order list "All locations" filter | OBS-L | N/A | N/A | DEFER: no use while one dispatch source is configured |
| ORD-131 | Order list stats strip: orders, items ordered, sales reversals, orders fulfilled, delivered, or | OBS-L | MISS | MISS | DEFER: Reports covers part; fulfilment-time is useful once r |
| ORD-132 | Export orders: scope choices (current page, all orders, selected, matching search, by date) | OBS-L | MISS | MISS | ACCEPT: with ORD-021; keep scope choices |
| ORD-133 | Export format choice (CSV for spreadsheets, plain CSV) | OBS-L | MISS | MISS | ACCEPT: with ORD-021 |
| ORD-134 | Export transaction histories (payment transactions) | OBS-L | MISS | MISS | DEFER: until DC-15 |
| ORD-135 | Bulk "Print packing slips" for selected orders | OBS-L | MISS | MISS | DEFER: with ORD-038 |
| ORD-136 | Bulk "Mark as": Unfulfilled, In progress, Fulfilled, On hold, Delivered | OBS-L | N/A | N/A | REJECT: state is system-derived |
| ORD-137 | "Mark as delivered" on a single fulfilment | OBS-L | SIM | SIM | FLAG: should Admin be able to record delivery by hand when c |
| ORD-138 | Bulk "Capture payments" | OBS-L | N/A | N/A | REJECT: capture is a gateway-flow matter, not a bulk Admin a |
| ORD-139 | Bulk "Request fulfillment" and "Cancel fulfillment requests" | OBS-L | N/A | N/A | REJECT |
| ORD-140 | Bulk "Change fulfillment location" | OBS-L | N/A | N/A | REJECT: locations are HU-settled |
| ORD-141 | Bulk "Run Flow automation" on orders | OBS-L | N/A | N/A | REJECT |
| ORD-142 | Order "More actions": Edit, Duplicate, Archive/Unarchive, View order status page, Print order p | OBS-L | PART | PART | COVERED for the status page (customer tracking exists); othe |
| ORD-143 | Link from Admin order to the customer's order status page | OBS-L | MISS | MISS | DEFER |
| ORD-144 | Order header "Refund" and "Return" buttons | OBS-L | N/A | N/A | REJECT (as ORD-069, ORD-071) |
| ORD-145 | Fulfilment card "..." menu (not opened; contents unobserved) | UNK | UNV | UNV | FLAG: contents not observed; cannot assess |

### DRF: Draft orders (13)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| DRF-001 | Draft order list | OBS | BLK | BLK Δ | ACCEPT: after DC-22 |
| DRF-002 | Create draft order for a customer | OBS | BLK | BLK | ACCEPT: after DC-22 |
| DRF-003 | Add products / custom items | OBS | BLK | BLK | FLAG: are non-catalogue custom line items allowed? |
| DRF-004 | Apply named order discount to a draft | OBS-L | N/A | N/A | FLAG: existing practice versus SPEC §3.7. Confirm whether ne |
| DRF-005 | Tax-exempt flag on a draft | OBS | BLK | BLK | FLAG: how GST on B2B orders works is an open decision (GST m |
| DRF-006 | Draft shipping / delivery line | OBS | N/A | N/A | REJECT |
| DRF-007 | Send draft invoice / payment link | OBS | BLK | BLK | DEFER |
| DRF-008 | Complete draft as paid / payment pending | OBS | BLK | BLK | ACCEPT: after DC-22 |
| DRF-009 | PO number on a draft | OBS | BLK | BLK | ACCEPT: after DC-22; useful for B2B |
| DRF-010 | Draft order timeline and notes | OBS | BLK | BLK | ACCEPT: after DC-22 |
| DRF-011 | Delete / duplicate draft | DOC | BLK | BLK | ACCEPT: after DC-22 |
| DRF-020 | Draft statuses: Open, Invoice sent, Completed, Submitted for review | OBS-L | BLK | BLK | DEFER: with drafts |
| DRF-021 | Draft "Submitted for review" (approval step before an order) | OBS-L | BLK | BLK | ACCEPT: after DC-22; relevant to SPEC §27.3 |

### PRD: Products (87)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| PRD-001 | Product list with pagination, thumbnails, status badges | OBS | IMPL | IMPL | COVERED |
| PRD-002 | Search products (ID, Zoho item, name) | OBS | IMPL | IMPL | COVERED |
| PRD-003 | Filter by status | OBS | IMPL | IMPL | COVERED |
| PRD-004 | Filter by category / product type / use case | OBS | IMPL | IMPL | COVERED |
| PRD-005 | Filter by vendor | OBS | N/A | N/A | REJECT |
| PRD-006 | Filter by tag | OBS | MISS | MISS | ACCEPT: tags exist and customers filter by them |
| PRD-007 | Filter by collection / sales channel | OBS | N/A | N/A | DEFER |
| PRD-008 | Filter by stock level (low, out) | OBS | BLK | BLK | ACCEPT: after DC-17 |
| PRD-009 | Sort the list | OBS | IMPL | IMPL | COVERED |
| PRD-010 | Column: inventory ("N in stock") | OBS | BLK | BLK | ACCEPT: after DC-17 |
| PRD-011 | Column: category, product type | OBS | IMPL | IMPL | COVERED |
| PRD-012 | Column: channels | OBS | N/A | N/A | REJECT |
| PRD-013 | Saved product views | OBS | MISS | MISS | DEFER |
| PRD-014 | Export products (CSV) | OBS | MISS | IMPL Δ | ACCEPT: export; see import PRD-072 |
| PRD-015 | Product count by status summary | DOC | IMPL | IMPL | COVERED |
| PRD-020 | Create product | OBS | IMPL* | IMPL* | COVERED |
| PRD-021 | Edit product content as a revision | OBS | IMPL* | IMPL* | COVERED |
| PRD-022 | Duplicate product | OBS | IMPL* | IMPL* | COVERED |
| PRD-023 | Title | OBS | IMPL* | IMPL* | COVERED |
| PRD-024 | Description (rich text) | OBS | IMPL* | IMPL* | COVERED |
| PRD-025 | Short description / benefits / usage / safety | OBS | IMPL* | IMPL* | COVERED |
| PRD-026 | Price (MRP) | OBS | IMPL* | IMPL* | COVERED |
| PRD-027 | Compare-at price | OBS | IMPL* | IMPL* | COVERED |
| PRD-028 | Unit price with measurement (price per litre) | OBS | UNV | UNV | FLAG: confirm whether a per-unit price display is required ( |
| PRD-029 | Charge-tax flag | OBS | IMPL* | IMPL* | COVERED |
| PRD-030 | Cost per item | OBS | MISS | MISS | DEFER: Part 1 C16; Zoho may hold cost |
| PRD-031 | SKU | OBS | IMPL* | IMPL* | COVERED |
| PRD-032 | Barcode | OBS | MISS | MISS | DEFER |
| PRD-033 | Zoho item link / mapping | — | IMPL* | IMPL* | COVERED |
| PRD-034 | Track quantity / sell when out of stock | OBS | N/A | N/A | REJECT |
| PRD-035 | Quantity per location | OBS | BLK | BLK | DEFER: see INV |
| PRD-036 | Weight | OBS | BLK | BLK | FLAG: DC-19 decides where weight lives |
| PRD-037 | Package / dimensions | OBS | BLK | BLK | FLAG: DC-19 |
| PRD-038 | Country of origin | OBS | MISS | MISS | DEFER: domestic only |
| PRD-039 | HS code | OBS | MISS | MISS | FLAG: GST invoices need an HSN code; confirm whether Zoho ho |
| PRD-040 | Physical product / requires shipping | OBS | N/A | N/A | REJECT |
| PRD-041 | Product type / category / tags | OBS | IMPL | IMPL | COVERED |
| PRD-042 | Vendor | OBS | N/A | N/A | REJECT |
| PRD-043 | Shopify taxonomy category | OBS | N/A | N/A | REJECT: EffyKlean has its own category set |
| PRD-044 | Metafields (pinned custom data) | OBS | N/A | N/A | REJECT: Part 1 L11 |
| PRD-045 | Google-feed fields (age group, condition, gender, MPN) | OBS | MISS | MISS | DEFER: with I2 |
| PRD-046 | Theme template selector | OBS | N/A | N/A | REJECT |
| PRD-047 | Verified commercial data marker (MRP, concentrate, Zoho) | — | MISS | MISS | FLAG: D-B1 |
| PRD-048 | Concentrate quantity / dilution data | — | IMPL* | IMPL* | COVERED |
| PRD-050 | Product status: draft, in review, approved, published | OBS | IMPL* | IMPL* | COVERED |
| PRD-051 | Submit / return / approve / publish workflow | OBS | IMPL* | IMPL* | COVERED |
| PRD-052 | Archive / unpublish a published product | OBS | BLK | BLK | ACCEPT: after DC-10 |
| PRD-053 | "Unlisted" (reachable by link only) | OBS | N/A | N/A | REJECT: Part 1 C4 |
| PRD-054 | Delete product | DOC | N/A | N/A | REJECT: archive instead |
| PRD-055 | Product history / timeline | OBS | IMPL | IMPL | COVERED |
| PRD-056 | Preview an unpublished revision | DOC | PART | PART | ACCEPT: Part 1 C14 |
| PRD-057 | Schedule publish date | OBS | MISS | MISS | DEFER |
| PRD-058 | Upload, reorder and set primary image | OBS | IMPL* | IMPL* | COVERED |
| PRD-059 | Image alt text | OBS | MISS | MISS | ACCEPT: Part 1 C9 |
| PRD-060 | Video and 3D media on a product | OBS | MISS | MISS | DEFER: DC-25 |
| PRD-061 | Media from the Files library | OBS | MISS | MISS | DEFER |
| PRD-062 | SEO title and meta description | OBS | PART | PART | ACCEPT: Part 1 C12 |
| PRD-063 | URL handle (slug) edit | OBS | PART | PART | ACCEPT: with DC-28 |
| PRD-064 | Variants and options (size, colour) | OBS | N/A | N/A | DEFER: Part 1 C19; single-variant pattern OBS/API |
| PRD-065 | Product family / pack-size grouping | — | MISS | MISS | DEFER |
| PRD-066 | Bundles / combo packs as products | OBS | PART | PART | FLAG: DC-33 |
| PRD-067 | Related / complementary products | OBS | MISS | MISS | DEFER |
| PRD-068 | Reviews and ratings | OBS | MISS | MISS | DEFER |
| PRD-069 | Product boosts / search ranking | OBS | N/A | N/A | REJECT |
| PRD-070 | Selling plans / subscriptions | DOC | N/A | N/A | DEFER: no requirement exists |
| PRD-071 | Product quantity rules and price breaks | API | N/A | N/A | DEFER: see E15 |
| PRD-072 | Import products (CSV) | OBS | PART | PART | DEFER: Part 1 M1 |
| PRD-073 | Bulk edit (spreadsheet-style editor) | OBS-L | MISS | PART Δ | DEFER |
| PRD-074 | Bulk change status, tags, category | OBS | MISS | PART Δ | DEFER |
| PRD-075 | Product translations | OBS | N/A | N/A | DEFER: with I5 |
| PRD-083 | Product/collection status "Suspended" (in addition to Active, Draft, Unlisted) | OBS-L | N/A | N/A | DEFER: meaning unconfirmed; ask whether the business uses it |
| PRD-084 | Product category determines tax rates (Shopify taxonomy) | OBS-L | N/A | N/A | REJECT: category does not drive tax here |
| PRD-090 | Bulk bar "Bulk edit" (spreadsheet editor) | OBS-L | MISS | MISS | DEFER: as PRD-073 |
| PRD-091 | Bulk archive / unlist products | OBS-L | BLK | BLK | DEFER: with PRD-052 |
| PRD-092 | Bulk delete products | OBS-L | N/A | N/A | REJECT |
| PRD-093 | Bulk include/exclude in sales channels and catalogs | OBS-L | N/A | N/A | REJECT |
| PRD-094 | Bulk add/remove tags | OBS-L | MISS | MISS | DEFER |
| PRD-095 | Bulk add to / remove from collections | OBS-L | BLK | BLK | DEFER |
| PRD-096 | "Create email campaign" from selected products | OBS-L | N/A | N/A | REJECT |
| PRD-097 | Export products dialog | OBS-L | MISS | IMPL Δ | ACCEPT: with PRD-014 |
| PRD-098 | Import products: CSV with downloadable sample, or "import from your platform" (Etsy, TikTok, Am | OBS-L | PART | PART | DEFER CSV (as PRD-072); REJECT platform imports |
| PRD-100 | Product list filters: vendor, tag, status, category, sales channel, catalogs, type, collection, | OBS-L | PART | PART | ACCEPT: tag filter (PRD-006); DEFER collection; REJECT vendo |
| PRD-101 | Product sort by created and updated date | OBS-L | UNV | UNV | ACCEPT: cheap; confirm existing sorts first |
| PRD-102 | Rich-text description editor tools (headings, colour, alignment, tables) | OBS-L | UNV | UNV | DEFER: confirm what the current editor supports |
| PRD-103 | Barcode type selector (GTIN, UPC, EAN, ISBN, ASIN, NS-PID, custom) | OBS-L | MISS | MISS | DEFER: with PRD-032 |
| PRD-104 | Inventory adjustment on the product page with a reason; unavailable breakdown (damaged, quality | OBS-L | N/A | N/A | REJECT |
| PRD-105 | Package picker and "Manage packages" (sample box 22×13.7×4.2 cm) | OBS-L | N/A | N/A | FLAG: DC-19 decides where weight and package data live |

### COL: Collections (10)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| COL-001 | Collections list | OBS | MISS | MISS | DEFER: DC-29 |
| COL-002 | Create manual collection | OBS | MISS | MISS | DEFER |
| COL-003 | Create automated collection by rules | OBS | MISS | MISS | DEFER |
| COL-004 | Collection image, description, SEO | OBS | MISS | MISS | DEFER |
| COL-005 | Collection sort order | OBS | MISS | MISS | DEFER |
| COL-006 | Add / remove products in collection | OBS | MISS | MISS | DEFER |
| COL-007 | Separate combo collections | OBS | N/A | N/A | REJECT: frozen rule |
| COL-008 | Collection channel availability | OBS | N/A | N/A | REJECT |
| COL-009 | Catalogs / price lists (B2B, markets) | OBS | MISS | MISS | DEFER: with E15 |
| COL-010 | Price override / adjustment per catalog | OBS | MISS | MISS | DEFER: with E15 |

### INV: Inventory, purchasing, transfers (18)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| INV-001 | Inventory page (per location counts) | OBS | BLK | BLK | ACCEPT: after DC-17 |
| INV-002 | States: available, committed, unavailable, on hand, incoming | OBS | BLK | BLK | ACCEPT: after DC-17 (read-only) |
| INV-003 | Adjust quantity | OBS | N/A | N/A | REJECT |
| INV-004 | Adjustment history | OBS | N/A | N/A | REJECT |
| INV-005 | Reserve / commit stock | OBS | N/A | N/A | REJECT |
| INV-006 | Low-stock alert | DOC | BLK | BLK | ACCEPT: after DC-17 |
| INV-007 | Locations list | OBS | BLK | BLK | DEFER |
| INV-008 | Add / edit / deactivate location | OBS | N/A | N/A | REJECT |
| INV-009 | Inventory-by-location report | DOC | BLK | BLK | DEFER |
| INV-010 | Purchase orders | OBS | N/A | N/A | REJECT: Part 1 F4 |
| INV-011 | Transfers between locations | OBS | N/A | N/A | REJECT |
| INV-012 | Suppliers | DOC | N/A | N/A | REJECT |
| INV-013 | Inventory CSV import / export | DOC | N/A | N/A | REJECT |
| INV-020 | Inventory column "Bin name" | OBS-L | N/A | N/A | REJECT |
| INV-021 | Inventory quick-transfer popover | OBS-L | N/A | N/A | REJECT |
| INV-022 | Export inventory (from all locations) | OBS-L | N/A | N/A | REJECT |
| INV-023 | Incoming popover with "Create transfer" | OBS-L | N/A | N/A | REJECT |
| INV-024 | Purchase order list: statuses Draft, Ordered, Archived; supplier, destination, received, expect | OBS-L | N/A | N/A | REJECT |

### GFT: Gift cards (2)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| GFT-001 | Create / sell / redeem gift cards | UNK | N/A | N/A | REJECT |
| GFT-002 | Gift card liability reporting | DOC | N/A | N/A | REJECT |

### CUS: Customers, segments, B2B (45)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| CUS-001 | Customer list (name, phone, orders, total spent, last order) | OBS | IMPL* | IMPL* | COVERED |
| CUS-002 | Search customers | OBS | IMPL* | IMPL* | COVERED |
| CUS-003 | Filter customers (location, orders, spend, consent) | OBS | MISS | MISS | DEFER |
| CUS-004 | Customer detail: contact, invoice details | OBS | IMPL* | IMPL* | COVERED |
| CUS-005 | Customer order history | OBS | IMPL* | IMPL* | COVERED |
| CUS-006 | Customer addresses (multiple, default) | OBS | UNV | UNV | FLAG: confirm what Admin should show |
| CUS-007 | Edit customer details (as Admin) | OBS | MISS | MISS | DEFER: DC-31 |
| CUS-008 | Create customer manually | OBS | MISS | MISS | DEFER: DC-31 |
| CUS-009 | Delete / anonymise customer | OBS | BLK | BLK | FLAG: D-D2 |
| CUS-010 | Customer notes (private) | OBS | MISS | IMPL Δ | ACCEPT: distributor/bulk follow-up needs notes; audit each n |
| CUS-011 | Customer tags | OBS | MISS | IMPL Δ | DEFER |
| CUS-012 | Marketing consent display (e-mail, SMS, WhatsApp) | API | PART | PART | COVERED (display); DEFER changes |
| CUS-013 | Edit marketing consent | OBS | MISS | MISS | DEFER |
| CUS-014 | Tax-exempt flag | API | N/A | N/A | FLAG: GST mapping decision |
| CUS-015 | Customer metafields (budget, state, PIN from enquiry form) | OBS | N/A | N/A | COVERED (intake) |
| CUS-016 | Customer account state (enabled, disabled, invited) | API | PART | PART | ACCEPT: after DC-31/32 |
| CUS-017 | Send account invite | DOC | N/A | N/A | DEFER: DC-21 |
| CUS-018 | Reset customer password / sign-in help | DOC | BLK | BLK | FLAG: D-D1 |
| CUS-019 | Customer timeline | OBS | MISS | MISS | DEFER |
| CUS-020 | Merge customers | OBS-L | N/A | N/A | REJECT: identity integrity |
| CUS-021 | Customer segments (list) | OBS | MISS | MISS | DEFER |
| CUS-022 | Create segment by filter (ShopifyQL-like) | OBS-L | MISS | MISS | DEFER |
| CUS-023 | Segment membership counts / use in marketing | OBS | N/A | N/A | REJECT |
| CUS-024 | Companies (B2B) | OBS | N/A | N/A | REJECT |
| CUS-025 | Company locations, contacts, payment terms | DOC | N/A | N/A | REJECT |
| CUS-026 | Customer export | OBS | MISS | IMPL Δ | ACCEPT: with M2 |
| CUS-027 | Customer import | OBS-L | N/A | N/A | REJECT |
| CUS-028 | Customer data request (export one customer) | DOC | BLK | BLK | FLAG: D-D2 |
| CUS-029 | Distributor application review and status | — | IMPL* | IMPL* | COVERED |
| CUS-030 | Distributor account created on approval | — | BLK | BLK | ACCEPT: after DC-31/32 |
| CUS-031 | Distributor pricing slabs and overrides | — | BLK | BLK | ACCEPT: after configuration is approved |
| CUS-032 | Bulk enquiry intake, status and notes | — | IMPL* | IMPL* | COVERED (intake); ACCEPT notes |
| CUS-033 | Bulk proposal and negotiated pricing record | — | BLK | BLK | ACCEPT: after configuration is approved |
| CUS-040 | Customer list optional columns: e-mail, phone, first/last name, postal code, language, ID, adde | OBS-L | PART | PART | DEFER |
| CUS-041 | Customer "deletable" flag (can this customer be deleted) | OBS-L | MISS | MISS | FLAG: D-D2 |
| CUS-043 | Customer notification language ("Will receive notifications in English") | OBS-L | MISS | MISS | DEFER |
| CUS-044 | "Create order" from the customer page | OBS-L | MISS | MISS | DEFER: with drafts |
| CUS-045 | Customer "Collect tax" setting | OBS-L | N/A | N/A | FLAG: GST mapping (see CUS-014) |
| CUS-050 | Bulk "Delete customer" | OBS-L | BLK | BLK | FLAG: D-D2 |
| CUS-051 | Bulk "Add to company" | OBS-L | N/A | N/A | REJECT |
| CUS-052 | Bulk "Remove tags" | OBS-L | MISS | MISS | DEFER |
| CUS-053 | "Select all in this store" (selection beyond the page) | OBS-L | MISS | MISS | DEFER |
| CUS-054 | Segment actions: use, duplicate, export, rename, delete | OBS-L | MISS | MISS | DEFER: with CUS-021 |
| CUS-055 | Describe-your-segment (natural-language segment builder) | OBS-L | N/A | N/A | REJECT |
| CUS-056 | Import customers by CSV dialog | OBS-L | N/A | N/A | REJECT (as CUS-027) |

### DSC: Discounts (29)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| DSC-001 | Discount list | OBS | IMPL* | IMPL* | COVERED |
| DSC-002 | Search and status tabs | OBS | PART | PART | DEFER |
| DSC-003 | Filter by date, type, method | OBS | MISS | MISS | DEFER |
| DSC-004 | Create a code discount | OBS | IMPL* | IMPL* | COVERED |
| DSC-005 | Percentage or fixed value | OBS | IMPL* | IMPL* | COVERED |
| DSC-006 | Applies to specific products | OBS | IMPL* | IMPL* | COVERED |
| DSC-007 | Applies to collections / categories | OBS | PART | PART | DEFER |
| DSC-008 | Minimum purchase amount | OBS | IMPL | IMPL | COVERED |
| DSC-009 | Minimum quantity | OBS | MISS | MISS | DEFER |
| DSC-010 | Total usage limit | OBS | IMPL* | IMPL* | COVERED |
| DSC-011 | One use per customer | OBS | BLK | BLK | ACCEPT: after DC-31 |
| DSC-012 | Customer eligibility (all, segment, specific) | OBS | BLK | BLK | ACCEPT: all/new customers after DC-31; DEFER segments |
| DSC-013 | Start and end dates | OBS | IMPL* | IMPL* | COVERED |
| DSC-014 | Edit / deactivate / delete a discount | OBS | IMPL* | IMPL* | COVERED |
| DSC-015 | Duplicate discount | DOC | MISS | IMPL Δ | DEFER |
| DSC-016 | Generate random code | OBS | MISS | MISS | DEFER |
| DSC-017 | Bulk-generate unique codes | DOC | MISS | IMPL Δ | DEFER |
| DSC-018 | Combinations with other discounts | OBS | IMPL* | IMPL* | FLAG: D-E1 |
| DSC-019 | Used count and sales total | OBS | PART | PART | ACCEPT: Part 1 E8 |
| DSC-020 | Automatic discount (no code) | API | MISS | MISS | DEFER |
| DSC-021 | Buy X get Y | OBS | MISS | MISS | DEFER |
| DSC-022 | Amount off order (distinct from product) | OBS | IMPL* | IMPL* | COVERED |
| DSC-023 | Free shipping discount | OBS | N/A | N/A | REJECT |
| DSC-024 | Sales-channel limitation of a discount | OBS | N/A | N/A | REJECT |
| DSC-025 | Discount timeline / comments | OBS | MISS | MISS | DEFER |
| DSC-026 | Combo pack pricing (rule set) | — | PART | PART | FLAG: DC-33 |
| DSC-027 | Distributor/Bulk exclusion from promotions | — | IMPL | IMPL | COVERED |
| DSC-040 | Discount list filters (status active/scheduled/expired, type, method, sales channel) and sort ( | OBS-L | PART | PART | DEFER |
| DSC-041 | Staff comments with @mention and links to records (orders, drafts, customers, products, variant | OBS-L | MISS | MISS | DEFER: with ORD-034 |

### CNT: Content (23)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| CNT-001 | Pages: list, create, edit, publish | OBS | PART | PART | ACCEPT: DC-24 |
| CNT-002 | Page SEO fields | OBS | PART | PART | ACCEPT: with DC-26 |
| CNT-003 | Page visibility / schedule | OBS | MISS | MISS | DEFER |
| CNT-004 | Page templates | OBS | N/A | N/A | REJECT |
| CNT-005 | Navigation menus: header, footer, account | OBS | MISS | MISS | DEFER |
| CNT-006 | Blog list / create / edit posts | OBS | MISS | MISS | DEFER |
| CNT-007 | Blog post author, tags, excerpt, image | OBS | MISS | MISS | DEFER |
| CNT-008 | Blog comments moderation | DOC | N/A | N/A | DEFER |
| CNT-009 | Files library: upload, alt text, delete | OBS | PART | PART | DEFER: DC-25 |
| CNT-010 | Files: references (where used) | OBS | MISS | MISS | DEFER |
| CNT-011 | Metaobjects (definitions, entries) | OBS | N/A | N/A | REJECT |
| CNT-012 | Redirects (URL redirects) | OBS | MISS | MISS | ACCEPT: Part 1 G5 |
| CNT-013 | Sitemap / robots | OBS | IMPL* | IMPL* | COVERED |
| CNT-014 | Themes: library, customise, edit code | OBS | N/A | N/A | REJECT |
| CNT-015 | Online Store preferences (title, meta, social image, password page) | DOC | MISS | MISS | DEFER |
| CNT-016 | Storefront search settings and filters (Search & Discovery) | OBS | N/A | N/A | DEFER |
| CNT-017 | How-to videos page | OBS | MISS | MISS | DEFER: DC-25 |
| CNT-018 | FAQ management | OBS | MISS | MISS | DEFER |
| CNT-019 | Forms (Shopify Forms) builder | OBS | N/A | N/A | REJECT |
| CNT-020 | Customer-facing chat / chatbot (Tidio) | OBS | N/A | N/A | DEFER |
| CNT-040 | Pages list: title, visibility, content excerpt, updated; 6 pages (videos, distributor enquiry,  | OBS-L | PART | PART | ACCEPT: as CNT-001 |
| CNT-041 | Themes: published theme, draft themes, update, edit theme, import, theme store | OBS-L | N/A | N/A | REJECT |
| CNT-042 | Online Store home: 30-day sessions by device (mobile, desktop, tablet) | OBS-L | MISS | MISS | DEFER: with ANA-012 |

### MKT: Marketing, markets (11)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| MKT-001 | Marketing campaigns | UNK | N/A | N/A | REJECT |
| MKT-002 | Attribution | UNK | N/A | N/A | DEFER: with H2 |
| MKT-003 | Automations / Autopilot | UNK | N/A | N/A | REJECT |
| MKT-004 | Shopify Email / Messaging campaigns | OBS | N/A | N/A | REJECT |
| MKT-005 | Newsletter sign-up and consent | OBS | PART | PART | DEFER |
| MKT-006 | Abandoned cart automations | OBS | MISS | MISS | DEFER |
| MKT-007 | Social posting / audiences | DOC | N/A | N/A | REJECT |
| MKT-010 | Markets: India (INR) | OBS | IMPL | IMPL | COVERED |
| MKT-011 | International markets, duties, local pricing | OBS | N/A | N/A | DEFER |
| MKT-012 | Languages and translations | OBS | MISS | MISS | DEFER |
| MKT-013 | Market-specific domains / rollouts | OBS | N/A | N/A | DEFER |

### CHN: Sales channels (8)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| CHN-001 | Online Store channel | OBS | IMPL | IMPL | COVERED |
| CHN-002 | Point of Sale | OBS | N/A | N/A | FLAG: should POS sales ever appear in EffyKlean? HU settled  |
| CHN-003 | Facebook & Instagram channel | OBS | MISS | MISS | DEFER |
| CHN-004 | Google & YouTube channel / product feed | OBS | MISS | MISS | DEFER |
| CHN-005 | WhatsApp channel | OBS | MISS | MISS | DEFER |
| CHN-006 | Agentic / AI channel | OBS | N/A | N/A | DEFER |
| CHN-007 | Marketplaces / Shop app | DOC | N/A | N/A | DEFER |
| CHN-008 | Pixels and customer events (Meta, Google) | OBS | MISS | MISS | DEFER |

### ANA: Analytics and reports (27)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| ANA-001 | Reports page: sales by day | OBS | IMPL* | IMPL* | COVERED |
| ANA-002 | Top products by sales | OBS | IMPL* | IMPL* | COVERED |
| ANA-003 | Orders by status | OBS | IMPL* | IMPL* | COVERED |
| ANA-004 | Payment attempts report | OBS | IMPL* | IMPL* | COVERED |
| ANA-005 | Date-range selection on reports | OBS | PART | PART | ACCEPT: Part 1 H1 |
| ANA-006 | Compare to previous period | OBS | MISS | MISS | DEFER |
| ANA-007 | Sales by customer / customer type | OBS | MISS | MISS | DEFER |
| ANA-008 | Sales by discount | OBS | PART | PART | ACCEPT: Part 1 E8 |
| ANA-009 | Sales by state / location (GST relevance) | DOC | MISS | MISS | ACCEPT: GST reporting is a real need |
| ANA-010 | Average order value | DOC | MISS | MISS | ACCEPT: derived |
| ANA-011 | Returning customer rate / cohorts | OBS-L | MISS | MISS | DEFER |
| ANA-012 | Sessions, conversion rate, traffic sources | OBS | MISS | MISS | DEFER |
| ANA-013 | Live view | OBS | MISS | MISS | DEFER |
| ANA-014 | Product analysis: ABC, sell-through, days of inventory | OBS | BLK | BLK | DEFER: DC-17 |
| ANA-015 | Finance: payments, taxes, payouts | OBS-L | MISS | MISS | DEFER |
| ANA-016 | Tax / GST summary report | OBS-L | MISS | MISS | FLAG: GST mapping |
| ANA-017 | Custom reports / saved reports | OBS-L | MISS | MISS | DEFER |
| ANA-018 | Report export and scheduling | OBS | MISS | MISS | ACCEPT: export; DEFER scheduling |
| ANA-019 | Bulk-customer savings report | — | BLK | BLK | DEFER |
| ANA-020 | Search-terms report | OBS-L | MISS | MISS | DEFER |
| ANA-021 | Behaviour reports: conversion, bounce, landing pages, device, search terms with no results, sea | OBS-L | MISS | MISS | DEFER: with ANA-012 |
| ANA-022 | Customer reports: RFM analysis and list, predicted spend tiers, one-time customers, returning c | OBS-L | MISS | MISS | DEFER |
| ANA-023 | Finance reports: finance summary, gross profit by order, cost of goods sold, net payments by ga | OBS-L | MISS | MISS | DEFER: needs cost and settlement data |
| ANA-024 | Acquisition reports: sessions by referrer/location, visitors | OBS-L | MISS | MISS | DEFER |
| ANA-025 | Inventory report: ABC product analysis | OBS-L | BLK | BLK | DEFER |
| ANA-026 | Storefront-agent (AI) session and conversation reports | OBS-L | N/A | N/A | REJECT |
| ANA-027 | Pin a report; report library by category | OBS-L | MISS | MISS | DEFER |

### SET: Settings (51)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| SET-001 | General: store name, contact e-mail and phone, address | OBS | BLK | BLK | ACCEPT: after DC-06 |
| SET-002 | General: currency, time zone, units | OBS | N/A | N/A | REJECT |
| SET-003 | Brand assets: logo, colours, slogan, social links | OBS | MISS | MISS | DEFER |
| SET-004 | Plan, billing, subscription | OBS | N/A | N/A | REJECT |
| SET-005 | Payments: Razorpay settings | OBS | PART | PART | ACCEPT: after DC-15 |
| SET-006 | Payments: capture mode | OBS | UNV | UNV | FLAG: see ORD-078 |
| SET-007 | Payments: manual payment methods | OBS | BLK | BLK | ACCEPT: after DC-22 |
| SET-008 | Payments: COD | OBS | N/A | N/A | REJECT: permanent exclusion |
| SET-009 | Payments: PayPal / alternative gateways | OBS | N/A | N/A | REJECT |
| SET-010 | Payment customizations (hide / reorder methods) | OBS | N/A | N/A | DEFER |
| SET-011 | Checkout settings: required fields, GST fields, order notes | OBS | MISS | MISS | DEFER |
| SET-012 | Checkout customisation | OBS | N/A | N/A | REJECT |
| SET-013 | Customer accounts settings (sign-in type, self-serve returns, store credit) | OBS | MISS | MISS | DEFER |
| SET-014 | Shipping profiles, zones, rates | OBS | N/A | N/A | REJECT |
| SET-015 | Packages and packing slip template | OBS | MISS | MISS | DEFER |
| SET-016 | Local delivery and pickup | OBS | N/A | N/A | REJECT |
| SET-017 | Carrier accounts / shipping labels | OBS | N/A | N/A | DEFER |
| SET-018 | Taxes: GST rates and state overrides | OBS | N/A | N/A | FLAG: GST mapping |
| SET-019 | Duties at checkout | OBS | N/A | N/A | REJECT |
| SET-020 | Locations | OBS | N/A | N/A | REJECT |
| SET-021 | Notifications: customer e-mail templates (confirmation, shipping, cancel, refund, payment error | OBS | BLK | BLK | ACCEPT: after DC-21 |
| SET-022 | Notifications: staff e-mails (new order, store summary, disputes) | OBS | BLK | BLK | ACCEPT: after DC-21 |
| SET-023 | Notifications: order-creation webhook | OBS | N/A | N/A | COVERED by design (AD-07 not yet built) |
| SET-024 | Notification SMS / WhatsApp templates | DOC | N/A | N/A | DEFER |
| SET-025 | Apps and sales channels settings | OBS | N/A | N/A | REJECT |
| SET-026 | Domains | OBS | N/A | N/A | REJECT |
| SET-027 | Customer events (pixels) | OBS | MISS | MISS | DEFER |
| SET-028 | Metafields and metaobjects definitions | OBS | N/A | N/A | REJECT |
| SET-029 | Languages | OBS | MISS | MISS | DEFER |
| SET-030 | Customer privacy: cookie banner, data requests, consent | OBS | PART | PART | FLAG: legal input |
| SET-031 | Policies: refund, privacy, terms, shipping, contact | OBS | PART | PART | ACCEPT: per DC-24; text is HU's |
| SET-032 | Gift cards settings | OBS | N/A | N/A | REJECT |
| SET-033 | Order ID prefix / auto-archive | OBS | PART | PART | COVERED |
| SET-034 | Feature previews / labs | DOC | N/A | N/A | REJECT |
| SET-035 | Store activity log | OBS-L | PART | PART | COVERED |
| SET-050 | Transfer or move the store to an organization / external owner | OBS-L | N/A | N/A | REJECT |
| SET-052 | Billing: list of bills (number, date, reason, total, status) | OBS-L | N/A | N/A | REJECT |
| SET-055 | Taxes: "Global collected tax report" | OBS-L | MISS | MISS | FLAG: GST mapping |
| SET-056 | Taxes: country of origin and HS codes recorded on 0 of 66 variants | OBS-L | MISS | MISS | FLAG: GST invoices need HSN; the source of HSN data is open  |
| SET-057 | Legal notice policy (not set) | OBS-L | MISS | MISS | DEFER |
| SET-058 | Privacy: "Shopify Network Intelligence" (enabled) | OBS-L | N/A | N/A | REJECT |
| SET-059 | Privacy: double opt-in for marketing; e-mail and SMS marketing in checkout | OBS-L | MISS | MISS | DEFER |
| SET-060 | Policies: "Default rules" for policy pages | OBS-L | N/A | N/A | REJECT |
| SET-061 | Staff notification: "Fulfillment request notification" to a fulfilment service | OBS-L | N/A | N/A | REJECT |
| SET-070 | Payment customization "Hides COD payment method for non-MagicX shipping methods" (active) | OBS-L | N/A | N/A | REJECT COD; evidence that COD rules exist in Shopify (inform |
| SET-071 | Razorpay Magic Checkout (one-click checkout) | OBS-L | MISS | MISS | DEFER: separate Razorpay product; SPEC is silent |
| SET-072 | Customer sign-in connections: Google, Facebook | OBS-L | MISS | MISS | DEFER: with the sign-in decision |
| SET-073 | Packing slip template (editable HTML/Liquid; ship-to, PO number, order name) | OBS-L | MISS | MISS | DEFER: with ORD-038 |
| SET-074 | Metafield definitions in use: product boosts, related and complementary products, Google custom | OBS-L | N/A | N/A | REJECT |
| SET-075 | Languages: English published (4 domains); Hindi, Kannada, Malayalam, Marathi, Tamil, Telugu pre | OBS-L | MISS | MISS | DEFER |
| SET-076 | Payment capture method (label only; value not readable) | OBS-L | UNV | UNV | FLAG: capture mode unverified; see ORD-078 |

### INT: Integrations, apps, automation (15)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| INT-001 | Integration readiness checks | — | IMPL* | IMPL* | COVERED |
| INT-002 | Razorpay webhook log | — | SIM | SIM | COVERED |
| INT-003 | Reconciliation queue | — | IMPL* | IMPL* | COVERED |
| INT-004 | Outbox / worker view | — | BLK | PART Δ | ACCEPT: when AD-07 is built |
| INT-005 | Zoho mapping health and sync status | — | PART | PART | ACCEPT: after DC-17 |
| INT-006 | Shiprocket status | — | SIM | SIM | ACCEPT: real status after DC-18 |
| INT-007 | App store / marketplace | OBS | N/A | N/A | REJECT |
| INT-008 | Custom/private apps and API tokens | OBS | N/A | N/A | REJECT |
| INT-009 | Shopify Flow | OBS | N/A | N/A | REJECT |
| INT-010 | Webhook subscriptions config | OBS | N/A | N/A | DEFER |
| INT-011 | Zoho Flow workflows | UNK | N/A | N/A | FLAG: contents unknown; inspect before any change |
| INT-020 | Flow workflows: eight Shopify-template marketing workflows (welcome discount e-mail, thank cust | OBS-L | N/A | N/A | REJECT the builder; abandoned-cart and welcome flows relate  |
| INT-021 | Flow: workflow tags, last run, version history | OBS-L | N/A | N/A | REJECT |
| INT-022 | "EffyZohoFlow" custom app and "Zoho Inventory" app (names only; configuration deliberately not  | OBS-L | UNV | UNV | FLAG: how Shopify talks to Zoho (app plus webhook) is unknow |
| INT-023 | App row menu: open, view details, get support, uninstall | OBS-L | N/A | N/A | REJECT |

### USR: Staff, roles, security (20)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| USR-001 | Staff list | UNK | IMPL* | IMPL* | COVERED |
| USR-002 | Deactivate / reactivate staff | UNK | IMPL* | IMPL* | COVERED |
| USR-003 | Create staff / invite | UNK | BLK | BLK | FLAG: D-F2 |
| USR-004 | Reset staff MFA | UNK | BLK | BLK | FLAG: D-F2 |
| USR-005 | Roles (Admin, Director) | UNK | IMPL* | IMPL* | COVERED |
| USR-006 | Granular per-area permissions | UNK | N/A | N/A | REJECT |
| USR-007 | Permission matrix confirm | UNK | IMPL* | IMPL* | FLAG: D-F1 |
| USR-008 | Staff sign-in with MFA, lockout | UNK | IMPL* | IMPL* | COVERED |
| USR-009 | Recovery codes | — | IMPL* | IMPL* | COVERED |
| USR-010 | Own account: profile, password, sessions | DOC | PART | PART | ACCEPT: Part 1 K2 |
| USR-011 | Staff activity / sign-in history | OBS-L | MISS | IMPL Δ | ACCEPT: Part 1 K3 |
| USR-012 | Collaborator accounts (agencies) | OBS-L | N/A | N/A | REJECT |
| USR-013 | Staff permission to see cost, reports, export | DOC | MISS | MISS | DEFER |
| USR-020 | Users: tabs Active, Pending, POS app-only, Requests; roles Store owner, Administrator and a cus | OBS-L | PART | PART | FLAG: WebAdmin is broader than EffyKlean Admin in refunds, p |
| USR-021 | Per-user "secure sign-in method required" flag | OBS-L | IMPL | IMPL | COVERED |
| USR-022 | Permission "Requests" tab (staff asking for access) | OBS-L | N/A | N/A | REJECT |
| USR-023 | POS app-only users | OBS-L | N/A | N/A | REJECT |
| USR-030 | Roles page: 17 roles in three categories (store, organization, point of sale), "Add role" for c | OBS-L | N/A | N/A | REJECT: custom role builder; see USR-031 |
| USR-031 | Role permission catalogue (e.g. orders: edit, apply discounts, set payment terms, charge card,  | OBS-L | N/A | N/A | REJECT per-permission editing; use as input to a role review |
| USR-032 | Users: "Security" page (monitor user activity, collaborator request code) | OBS-L | PART | PART | ACCEPT: activity monitoring as K3; REJECT collaborators |

### SYS: System, search, home (16)

| ID | Shopify capability | Tier | Carried | Now | Carried recommendation |
|---|---|---|---|---|---|
| SYS-001 | Audit trail viewer | — | IMPL* | IMPL* | COVERED |
| SYS-002 | Audit export | — | MISS | IMPL Δ | ACCEPT: Part 1 K3 |
| SYS-003 | Global search | OBS | PART | PART | ACCEPT: Part 1 M3 |
| SYS-004 | Command palette / keyboard shortcuts | OBS-L | MISS | MISS | DEFER |
| SYS-005 | Notification centre | OBS | MISS | MISS | DEFER |
| SYS-006 | Home to-do overview | OBS | PART | PART | ACCEPT: Part 1 A1 |
| SYS-007 | Home recent activity | OBS | MISS | MISS | ACCEPT: Part 1 A2 |
| SYS-008 | Home business metrics | OBS | PART | PART | ACCEPT: Part 1 A3 |
| SYS-009 | Setup guide / promotions | OBS | N/A | N/A | REJECT |
| SYS-010 | AI assistant (Sidekick) | OBS-L | N/A | N/A | REJECT |
| SYS-011 | Help centre / support link | DOC | MISS | MISS | DEFER |
| SYS-012 | Responsive accessible shell | — | IMPL* | IMPL* | COVERED |
| SYS-013 | Multi-store switcher | DOC | N/A | N/A | REJECT |
| SYS-020 | Home: Alerts feed (unread count, "view unread only") | OBS-L | MISS | MISS | DEFER: same as SYS-005 |
| SYS-021 | Recents list in search | OBS-L | MISS | MISS | DEFER |
| SYS-022 | Home: last-30-days sessions, sales, orders, conversion and live visitors cards | OBS-L | PART | PART | ACCEPT: sales and orders (as SYS-008); DEFER traffic |
