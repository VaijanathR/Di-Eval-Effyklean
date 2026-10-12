# Comparison 3: effyklean.com vs effyklean.in (visual, functional and workflow)

**Date:** 2026-10-12 · **Repository state:** HEAD `4af12e0`, 28 uncommitted paths (none staged); nothing was changed in the repository except new documents.
**Status:** ASSESSMENT ONLY. Not a requirement and not an implementation authorization. Every priority is a **recommendation**; HU+DI decide. `SPEC.md` v0.8, `ARCHITECTURE.md` and AD-01..AD-17 are not reopened.


## 1. Method and evidence limits (read first)

| Item | Statement |
|---|---|
| effyklean.com | Inspected directly this session over HTTP: `sitemap.xml` and child sitemaps (**30 URLs**), all 30 pages fetched, `products.json` (15 products), `collections.json`, plus `/cart`, `/search`, `/account`, 5 policy pages, homepage rendered text. No JavaScript executed; no order, payment or login. |
| **effyklean.in is not publicly reachable.** | `effyklean.in` resolves in DNS (3.173.21.164) but the TLS handshake fails and `www.effyklean.in` does not resolve; nothing is served. This matches the recorded state (nothing pushed or deployed; Phase 2 hosting not authorized). The `.in` side is therefore the **local build** (`127.0.0.1:8000`, `manage.py runserver`, `config.settings.local`, stub providers). |
| Empty catalogue | The running local instance has **zero products** ("No products are currently available."). Product presentation on `.in` is evidenced by code (`modules/storefront/pages.py`), tests and the 15-product source feed (`media/catalogue_source/source.json`), **not by a rendered product page**. |
| Visual comparison | **NOT performed.** No browser or screenshot tool is available; rendered look-and-feel, spacing, imagery and responsive layout are UNVERIFIED. Only structural facts (HTML landmarks, viewport meta, text, link sets) were compared. Earlier browser/E2E evidence (register E-07, `E2E_PROTOTYPE_EVIDENCE.md`, 2026-10-10/11) is historical. |
| Not done | No order, payment, shipment, e-mail or subscription; no changes to either site. |

Status: SAME, PART, MISS (on .in), EXTRA (only on .in), DIFF (intentionally different), UNV (not verifiable here).

## 2. Pages (EC-P)

| ID | effyklean.com path | Page | Observed on .com | effyklean.in counterpart (local build) | Status | Evidence |
|---|---|---|---|---|---|---|
| EC-P01 | `/` | Home | Hero "Welcome", benefits (cost, eco, less plastic, performance), 3 collection cards, newsletter, footer with payment icons and policies; announcement "Make 1 or 5 liter final product..." | `/` hero, benefits, collection cards, search, footer with info links; meta description present | SAME (structure); look UNV | home HTML both |
| EC-P02 | `/products/room-freshener-concentrate-air-freshener-concentrate-brute` | Product: room-freshener-concentrate-air-freshener | Single variant, price ₹320.00 (compare-at ₹850.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P03 | `/products/laundry-wash-concentrate` | Product: laundry-wash-concentrate | Single variant, price ₹290.00 (compare-at ₹640.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P04 | `/products/soft-soap-concentrate-transparent` | Product: soft-soap-concentrate-transparent | Single variant, price ₹290.00 (compare-at ₹620.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P05 | `/products/glass-cleaner-concentrate-glass-cleaners-green-gel` | Product: glass-cleaner-concentrate-glass-cleaners | Single variant, price ₹190.00 (compare-at ₹560.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P06 | `/products/floor-cleaner-concentrate-floor-phenyl-compounds` | Product: floor-cleaner-concentrate-floor-phenyl-c | Single variant, price ₹220.00 (compare-at ₹460.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P07 | `/products/toilet-cleaner-concentrate-toilet-phenyl-compounds` | Product: toilet-cleaner-concentrate-toilet-phenyl | Single variant, price ₹295.00 (compare-at ₹730.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P08 | `/products/dish-wash-concentrate-paste-copy` | Product: dish-wash-concentrate-paste-copy | Single variant, price ₹290.00 (compare-at ₹670.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P09 | `/products/floor-cleaner-concentrate-pine-oil-based` | Product: floor-cleaner-concentrate-pine-oil-based | Single variant, price ₹195.00 (compare-at ₹470.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P10 | `/products/floor-cleaner-concentrate` | Product: floor-cleaner-concentrate | Single variant, price ₹160.00 (compare-at ₹290.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P11 | `/products/floor-cleaner-concentrate-pine` | Product: floor-cleaner-concentrate-pine | Single variant, price ₹130.00 (compare-at ₹180.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P12 | `/products/toilet-cleaner-concentrate-toilet` | Product: toilet-cleaner-concentrate-toilet | Single variant, price ₹160.00 (compare-at ₹185.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P13 | `/products/room-freshener-concentrate-air-freshener` | Product: room-freshener-concentrate-air-freshener | Single variant, price ₹180.00 (compare-at ₹190.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P14 | `/products/glass-cleaner-concentrate` | Product: glass-cleaner-concentrate | Single variant, price ₹135.00 (compare-at ₹180.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P15 | `/products/laundry-wash-concentrate-gel` | Product: laundry-wash-concentrate-gel | Single variant, price ₹150.00 (compare-at ₹290.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P16 | `/products/dish-wash-concentrate-gel` | Product: dish-wash-concentrate-gel | Single variant, price ₹150.00 (compare-at ₹197.00), 2 images, /cart/add form | `/products/<id>/` quantity + add to cart, facts, classification, related; price/compare-at taken from the same source feed | PART: data identical (price and compare-at match 15/15 on the live feed); rendered page UNV (empty catalogue) | products.json vs source.json |
| EC-P17 | `/pages/contact-us` | Contact us | Form: Name, Phone number, Email | `/contact-us/` name, email, phone, message; Admin inbox; no notification e-mail (H-05) | SAME |  |
| EC-P18 | `/pages/about-us` | About us | Static page | `/about-us/` | SAME |  |
| EC-P19 | `/pages/faq` | FAQ | FAQ with video-linked questions (AirFreshner 1 L / 5 L headings seen) | `/faq/` approved items, Admin-managed | SAME |  |
| EC-P20 | `/pages/our-values` | Our values | Static page | `/our-values/` | SAME |  |
| EC-P21 | `/pages/distributor-enquiry-page` | Distributor enquiry | Page present; form fields not found in the fetched HTML (only footer/search forms): UNV whether it is a form or text | `/distributor-application/` with submit, received page, Admin review and provisioning (CR-006) | EXTRA/PART: .in stronger |  |
| EC-P22 | `/pages/videos-how-to` | Videos - How to | Videos list (AirFreshner 1 L/5 L, handwash 5 L...) | `/videos/` same headings (VIDEOS - HOW TO) | SAME |  |
| EC-P23 | `/collections/household-users-single-items` | Household single items | 8 products per collections.json; filter (availability, price), sort | `/products/?product_type=Household+format` filters category, type, use case, size, price | PART |  |
| EC-P24 | `/collections/household-users-combo-packs` | Household combo packs | **Page shows "0 products"** (collections.json says 50; `/products.json` for the collection returns an empty list): live combo collection is empty | Combo discount is a cart rule (SPEC §7), not a collection; no combo packs page | DIFF: combo is a rule on .in; empty on .com | collection products.json [] |
| EC-P25 | `/collections/bulk-user-products` | Bulk user products | 8 products; filter and sort | `/products/?product_type=Bulk+format`; `/bulk-enquiry/` | PART |  |
| EC-P26 | `/blogs/news` | Blog index | 4 blog URLs | `/blog/` returns **404 in the running instance** (3 posts exist under `media/blog_source`; publication state not verified) | MISS (UNV cause) |  |
| EC-P27 | `/blogs/news/eco-friendly-cleaning-why-it-matters-and-how-you-c` | Blog post 1 | Article page | `/blog/<slug>/` route exists; source JSON present; 404 in running instance | UNV |  |
| EC-P28 | `/blogs/news/how-to-remove-stubborn-stains-with-our-specialty-p` | Blog post 2 | Article page | `/blog/<slug>/` route exists; source JSON present; 404 in running instance | UNV |  |
| EC-P29 | `/blogs/news/holiday-cleaning-checklist-make-your-home-guest-re` | Blog post 3 | Article page | `/blog/<slug>/` route exists; source JSON present; 404 in running instance | UNV |  |
| EC-P30 | `/policies/privacy-policy` | Policy: privacy-policy | Shopify policy page (200) | Footer link goes to **effyklean.com/policies/privacy-policy**; `.in` own pages exist only for shipping, cancellation, replacement (no own Privacy/Terms/Refund; HU legal text pending) | PART (BLK: HU text) |  |
| EC-P31 | `/policies/refund-policy` | Policy: refund-policy | Shopify policy page (200) | Footer link goes to **effyklean.com/policies/refund-policy**; `.in` own pages exist only for shipping, cancellation, replacement (no own Privacy/Terms/Refund; HU legal text pending) | PART (BLK: HU text) |  |
| EC-P32 | `/policies/terms-of-service` | Policy: terms-of-service | Shopify policy page (200) | Footer link goes to **effyklean.com/policies/terms-of-service**; `.in` own pages exist only for shipping, cancellation, replacement (no own Privacy/Terms/Refund; HU legal text pending) | PART (BLK: HU text) |  |
| EC-P33 | `/policies/shipping-policy` | Policy: shipping-policy | Shopify policy page (200) | Footer link goes to **effyklean.com/policies/shipping-policy**; `.in` own pages exist only for shipping, cancellation, replacement (no own Privacy/Terms/Refund; HU legal text pending) | PART (BLK: HU text) |  |
| EC-P34 | `/policies/contact-information` | Policy: contact-information | Shopify policy page (200) | Footer link goes to **effyklean.com/policies/contact-information**; `.in` own pages exist only for shipping, cancellation, replacement (no own Privacy/Terms/Refund; HU legal text pending) | PART (BLK: HU text) |  |
| EC-P35 | `/cart` | Cart | Cart page with quantity, GST/GSTIN fields (app), gift mention | `/cart/` coupon box, combo note, server totals | SAME |  |
| EC-P36 | `/search?q=floor` | Search | Predictive search form `/search` | `/products/?q=` form in header | SAME |  |
| EC-P37 | `/account` | Login / account | Redirects to Shopify customer authentication (returns 406 to plain HTTP) | `/account/` 303 to sign-in; register, setup, orders, reorder | SAME |  |
| EC-P38 | `/sitemap.xml, /robots.txt` | SEO files | Shopify sitemap (7 child sitemaps), robots | `/sitemap.xml` (9 URLs, no products because empty), `/robots.txt` | SAME |  |

### 2a. Routes that exist only on effyklean.in (EC-X)

| ID | Route | Description | Behaviour | Status |
|---|---|---|---|---|
| EC-X01 | `/products/ (list)` | .in only | Product list with filters category, type, use case, size, price; empty message | EXTRA |
| EC-X02 | `/cart/add, update, remove, coupon, coupon/remove, coupon/use` | .in cart operations | Server cart with coupon / combo choice | EXTRA |
| EC-X03 | `/checkout/, /checkout/review, /checkout/pay, /checkout/payment/return` | .in own checkout | Guest checkout, signed review, GST fields, Zoho Payments (stub) | DIFF (.com uses Shopify/Razorpay checkout: not entered) |
| EC-X04 | `/orders/<reference>/confirmation` | .in confirmation | Order confirmation after verified payment | DIFF |
| EC-X05 | `/track/, /track/cancel` | .in tracking and cancellation review | EKI id + contact; cancellation per SPEC §16 | EXTRA (.com has Shopify order status pages: UNV) |
| EC-X06 | `/bulk-enquiry/ (+submit, received, quotes)` | .in bulk | Bulk institutional enquiry | EXTRA |
| EC-X07 | `/subscribe/, confirm, unsubscribe` | .in verified subscribe | Mailbox verification; no provider | EXTRA/PART |
| EC-X08 | `/account/register, setup, reorder, details, password, sign-out` | .in account | Customer account functions | SAME (.com Shopify accounts) |
| EC-X09 | `/contact-us/received/, /distributor-application/received/` | .in confirmations | Post-submit pages | SAME |
| EC-X10 | `/replacement/, /cancellation/, /shipping-and-delivery/` | .in policies | Own policy pages (SPEC §23) | EXTRA |
| EC-X11 | `/api/v1/ ...` | .in API | Storefront API (modules.storefront.urls) | EXTRA |
| EC-X12 | `/EKIAdmin2026/` | .in staff Admin | Staff Admin (not public navigation) | N/A |

## 3. Navigation and links (EC-L)

| ID | effyklean.com | effyklean.in | Status |
|---|---|---|---|
| EC-L01 | Header HOME / VIDEOS / SHOP / PRODUCTS / FAQ / ABOUT / CONTACT / VALUES / BLOGS / DISTRIBUTOR ENQUIRY | Header on .in: Home, Products (Household / Bulk format filters), About Us, Our Values, Contact Us, FAQ, Videos, Bulk enquiry, Distributor application, Track, Account, Cart, Subscribe | PART: .in has no Blogs dropdown, no Shop dropdown (filters instead); adds Track and Bulk |
| EC-L02 | Header Log in | Account link `/account/` | SAME |
| EC-L03 | Header Cart | `/cart/` | SAME |
| EC-L04 | Header search | Header search form | SAME |
| EC-L05 | Social: Facebook, Instagram, YouTube | Same three URLs in footer | SAME |
| EC-L06 | Footer policies: privacy, refund, terms, shipping, contact information | Links to effyklean.com/policies/* for privacy, refund, terms, contact; own pages for shipping, cancellation, replacement | PART (own pages pending HU text) |
| EC-L07 | Footer "Powered by Shopify" | none | DIFF |
| EC-L08 | Footer payment methods | none observed in .in footer text | UNV |
| EC-L09 | Footer newsletter | `/subscribe/` verified opt-in | SAME (stronger) |
| EC-L10 | Floating WhatsApp button (app, 72 mentions in markup) | none; footer has `tel:+919422618051` and mailto | MISS |
| EC-L11 | Language app (Weglot script present) | none (English only) | MISS (UNV usage) |
| EC-L12 | Support mailbox | mailto:Support@EffyKlean.com | SAME |

## 4. Functions (EC-F)

| ID | Function | effyklean.com | effyklean.in | Status |
|---|---|---|---|---|
| EC-F01 | Product catalogue | 15 products, 3 collections | 15 products in source; categories via filters; running instance empty | UNV |
| EC-F02 | Pricing and compare-at | ₹130 to ₹320; MRP-style compare-at | Identical price and compare-at for 15/15 (feed vs source); rendered UNV | SAME (data) |
| EC-F03 | Variants | Single "Default Title" variant per product, "Makes 1 or 5 liters" in title | Pack size as separate product/SKU (same pattern) | SAME |
| EC-F04 | Cart and coupons | Shopify cart, discount codes (admin DC list) | Server cart, coupon, combo OR coupon, ₹500 minimum, one discount only | DIFF (SPEC §7) |
| EC-F05 | Checkout and payment | Shopify checkout with Razorpay (Admin walk) incl. COD/Magic Checkout app | Own checkout, Zoho Payments (stub), **no COD** (SPEC §3.9) | DIFF |
| EC-F06 | GST/GSTIN capture | App-driven (GSTIN text on cart page) | Structured GST number/name at checkout (D-01) | SAME |
| EC-F07 | Shipping charge | Shopify shipping profiles (Admin walk) | No shipping charge (SPEC §3.8) | DIFF |
| EC-F08 | Delivery and tracking | Shiprocket tracking on order (Admin walk) | Internal tracking page; status feed from Shiprocket MISSING (C-02) | PART |
| EC-F09 | Customer accounts | Shopify new customer accounts | Own accounts: orders, reorder, details | SAME |
| EC-F10 | Order cancellation / returns | Self-serve cancellation/returns configurable in Shopify (Admin walk) | Cancellation per SPEC §16, replacement with video evidence (CR-008) | DIFF |
| EC-F11 | Bulk / distributor | Distributor enquiry page (form UNV) | Bulk enquiry + quotes + distributor application + business accounts | .in stronger |
| EC-F12 | Newsletter | Footer form (Shopify tag) | Verified opt-in; no provider decided | PART (BLK) |
| EC-F13 | Contact | Form Name/Phone/Email | Form name/email/phone, fail-closed | SAME |
| EC-F14 | Search | Shopify search form | Query + filters | SAME |
| EC-F15 | Analytics | gtag script present | none (consent first) | MISS (deliberate) |
| EC-F16 | SEO | Meta description, canonical, og:title, JSON-LD (2) | Meta description, sitemap, robots; E-06 VERIFIED (T) | SAME (structure) |
| EC-F17 | Responsive | viewport meta present on all fetched pages | viewport meta present on all HTML pages checked; layout UNV | UNV |
| EC-F18 | Languages / currency | Weglot present; INR | INR; English only | PART |
| EC-F19 | Live chat | WhatsApp floating button | none | MISS |

## 5. Customer journeys and workflows (EC-W)

| ID | Journey | effyklean.com | effyklean.in | Status |
|---|---|---|---|---|
| EC-W01 | Guest purchase: home > product > cart > checkout > pay > confirmation | Shopify path (not executed) | Implemented and browser-tested locally against stubs; no provider proof (B-01) | UNV / PART |
| EC-W02 | Signed-in purchase and reorder | Shopify accounts | Implemented (D-04, F-05) | SAME |
| EC-W03 | Apply coupon / combo discount | Discount codes | One discount only; combo OR coupon; ₹500 minimum | DIFF |
| EC-W04 | Track order | Shopify order status + Shiprocket link | `/track/` by EKI id and contact | PART (status feed MISSING) |
| EC-W05 | Cancel order | Shopify self-serve cancellation (settings seen) | `/track/cancel` review per SPEC §16 (80% refund rule, simulated provider) | DIFF |
| EC-W06 | Replacement (damaged/incorrect) | Not observed | Video evidence flow (CR-008), Admin decision | EXTRA |
| EC-W07 | Bulk / distributor enquiry | Distributor page (form UNV) | Full application, review, role provisioning | .in stronger |
| EC-W08 | Contact / support | Contact form | Contact form + Admin inbox (no e-mail alert) | PART |
| EC-W09 | Newsletter subscription | Footer form | Verified opt-in (stub mail backend) | PART |
| EC-W10 | Read policies | Shopify policy pages | Own pages for 3; others link back to .com | PART |
| EC-W11 | Watch how-to videos | Videos page | Videos page | SAME |

## 6. Look-and-feel and responsiveness (EC-V, structural evidence only)

| ID | Aspect | effyklean.com | effyklean.in | Status |
|---|---|---|---|---|
| EC-V01 | Viewport meta | present on all fetched pages | present on all HTML pages checked (home, about, faq, policies, cart, bulk, account) | SAME |
| EC-V02 | Header/footer landmarks | Shopify theme markup | `header.site-header`, `nav[aria-label=Main]`, `footer.site-footer` | UNV (visual) |
| EC-V03 | Colours and typography | not measured | theme-color `#1c1e6b` on .in; not compared | UNV |
| EC-V04 | Imagery | 2 images per product (feed) | local `media/products` (31 files) and logo asset | UNV (rendering) |
| EC-V05 | Mobile layout | not rendered | Admin drawer layout browser-tested earlier (E-07); storefront historical | UNV |
| EC-V06 | Accessibility | not assessed | skip/landmarks only by inspection | UNV |

## 7. Coverage counts and unverified items

* effyklean.com sitemap URLs: **30**, all fetched (1 home, 15 products, 6 pages, 3 collections, 4 blog URLs, `agents.md`); plus cart, search, account and 5 policy pages (9). Rows: EC-P 38, EC-X 12, EC-L 12, EC-F 19, EC-W 11, EC-V 6.
* effyklean.in: **0 pages publicly reachable**; 25 local routes probed (home, 9 sitemap pages, cart, checkout, track, bulk, videos, blog, contact, sign-in, subscribe, account, register, policies, robots) and the full URLconf read.
* **Unverified:** all rendered visuals; checkout/payment on `.com`; `.com` order-status and account pages; the distributor form on `.com`; why `/blog/` is 404 locally; product pages on `.in` (empty catalogue); live behaviour after any HU home-page change in the working tree.

## 8. Key findings

1. **`.in` is not yet a site anyone can open**; any statement of parity is about the local build only (matches the register's Phase 2 status).
2. **Catalogue data matches the live site exactly** (15/15 prices and compare-at prices), but the running local instance shows an empty catalogue: first thing to load (via `import_catalogue_source`, which creates draft revisions awaiting Director approval) before any visual or journey comparison is possible.
3. **The live `Household combo packs` collection is empty** (0 products), so the combo concept exists on `.com` only as discount rules; `.in` implements it as a cart rule.
4. `.in` footer sends Privacy, Terms, Refund and Contact information back to **effyklean.com** pages (HU legal text pending); this is a cut-over blocker for a standalone `.in`.
5. `.in` is ahead on bulk/distributor, verified subscribe, replacement and tracking by EKI id; behind on blog availability (404), WhatsApp contact button, language option, and shipment tracking status.
6. No visual or responsive claim is made; a browser pass is required.

