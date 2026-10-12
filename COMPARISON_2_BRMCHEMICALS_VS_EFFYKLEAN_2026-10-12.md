# Comparison 2: BRMChemicals.com vs EffyKlean (functional and business workflows; look-and-feel excluded)

**Date:** 2026-10-12 · **Repository state:** HEAD `4af12e0`, 28 uncommitted paths (none staged); nothing was changed in the repository except new documents.
**Status:** ASSESSMENT ONLY. Not a requirement and not an implementation authorization. Every priority is a **recommendation**; HU+DI decide. `SPEC.md` v0.8, `ARCHITECTURE.md` and AD-01..AD-17 are not reopened.


## 1. Method and evidence limits

| Item | Statement |
|---|---|
| Source | `https://brmchemicals.com` (Shopify storefront). Inspected directly this session: homepage (rendered text via fetch), `sitemap.xml` and all child sitemaps (**853 URLs**), all 14 `/pages/` URLs, a sample collection (`/collections/chemicals`), two product pages, `/cart`, `/account/login`, `/search?q=soap`, and the public `products.json` feed (**695 products, 2,960 variants**). HTTP fetch only; no browser, no JavaScript execution. |
| What this cannot show | Behaviour that needs JavaScript or a real cart/checkout (add-to-cart result, shipping-rate calculation, pincode checks, payment methods offered at checkout, discount behaviour, stock messages, order e-mails). **No order, payment or account was created.** Those items are marked UNVERIFIED. |
| EffyKlean side | The local build at 127.0.0.1:8000 (empty catalogue in the running instance), the URLconf, templates and tests. effyklean.in is not live (see Comparison 3). |
| Authority | BRM is **external evidence only**, not a requirement (see `BRM_CHEMICALS_DEEP_INVESTIGATION_AND_EFFYKLEAN_ROADMAP.md`, RM-01..RM-10). Differences are recorded, not judged as defects. |
| Look-and-feel | Excluded as instructed. |

Status codes: SAME equivalent present; PART partial; MISS absent in EffyKlean; DIFF intentionally different (SPEC/decision); N/A BRM-specific (raw-materials business); UNV not verified.

## 2. Pages (BR-P)

| ID | BRM URL | Page | Observed behaviour | EffyKlean counterpart | Status | Related |
|---|---|---|---|---|---|---|
| BR-P01 | `/` | Home | Announcement bar (free shipping across India), promo banners, use-case icons, client logos, best sellers carousel, 10 recent launches, brand story, "BRM Promise", essentials guides, newsletter | Home `/`: hero, benefits, three collection cards, newsletter | PART | BR-F12 |
| BR-P02 | `/pages/contact-us` | Contact Us | Form: Name, Phone number, Email (Shopify contact form) | `/contact-us/` form: name, email, phone, fail-closed, Admin inbox `contact-messages` | SAME | BR-F09 |
| BR-P03 | `/pages/about-us` | About Us | Company story since 1987 | `/about-us/` | SAME | - |
| BR-P04 | `/pages/terms-of-user-agreement` | Terms | Terms page | Terms link goes to effyklean.com; page unpublished pending HU legal text | PART (BLK: HU text) | - |
| BR-P05 | `/pages/privacy-security` | Privacy & Security | Privacy page | Privacy link goes to effyklean.com; unpublished pending HU legal text | PART (BLK: HU text) | - |
| BR-P06 | `/pages/payment-shipping-returns` | Payment, Shipping & Returns | Combined policy | `/shipping-and-delivery/`, `/cancellation/`, `/replacement/` (separate, SPEC-driven) | DIFF | - |
| BR-P07 | `/pages/cancellation-policy` | Cancellation Policy | Cancellation policy | `/cancellation/` (SPEC §16) | SAME | - |
| BR-P08 | `/pages/refund-policy` | Return & Refund Policy | Refund policy, plus a contact form | Refund policy on effyklean.com; EffyKlean has no normal returns/refunds (SPEC §3.5); `/replacement/` | DIFF | - |
| BR-P09 | `/pages/faq` | FAQ | FAQ | `/faq/` (approved FAQ items, Admin `content/faq/*`) | SAME | - |
| BR-P10 | `/pages/rapid-search-results` | Search Results (app page) | Search app results page | `/products/?q=` search | SAME | BR-F01 |
| BR-P11 | `/pages/pclanding` | PC_Landing (ad landing page) | Marketing landing page with contact form | none | MISS (marketing) | - |
| BR-P12 | `/pages/fb-essential-ad-1` | FB Essential AD 1 (ad landing page) | Marketing landing page with contact form | none | MISS (marketing) | - |
| BR-P13 | `/pages/knowledge-hub` | Knowledge Hub | Educational content hub | Blog/`videos` exist but no hub; blog is empty in the running instance | PART | BR-F15 |
| BR-P14 | `/pages/buy-raw-materials-in-bulk-chemicals-oils-more-brm-chemicals` | Bulk requirement page | "CONTACT FOR BULK REQUIREMENT" form (Name, Phone, Email) | `/bulk-enquiry/` (organisation, contact, email, phone), Admin `bulk-enquiries`, negotiated `bulk-quotes` | SAME (stronger) | BR-W04 |
| BR-P15 | `/pages/thank-you` | Thank you (post-submit) | Confirmation after bulk requirement form | `/contact-us/received/`, `/distributor-application/received/` | SAME | BR-W04 |
| BR-P16 | `/cart` | Cart | Cart page, line items, checkout | `/cart/` (server totals, coupon, combo) | SAME | BR-F05 |
| BR-P17 | `/account/login` | Account login | Sign in (email/password), recover password | `/account/sign-in/`, `register/`, `setup/`, `account/` (orders, reorder, details, password) | SAME | BR-F07 |
| BR-P18 | `/search?q=soap` | Search results | 533 results for "soap"; filters product_type, availability, size, weight, price | `/products/?q=` with category, type, use case, size, price filters | SAME | BR-F01 |

Pages in sitemap: 14 (all listed or covered above; sitemap also lists `agents.md`).


## 3. Navigation and footer links (BR-L)

| ID | BRM link | Target | EffyKlean counterpart | Status |
|---|---|---|---|---|
| BR-L01 | Header SHOP > Chemicals | `/collections/chemicals` | category filters (`/products/?category=`, `product_type`, `use_case`) | N/A (different catalogue) |
| BR-L02 | Header SHOP > Herbal Extracts (Oil Soluble, Water Soluble) | `/collections/liquid-extract-oil-soluble, /collections/liquid-herbal-extract-water-soluble` | same | N/A (different catalogue) |
| BR-L03 | Header SHOP > Essential Oils | `/collections/essential-oil` | same | N/A (different catalogue) |
| BR-L04 | Header SHOP > Colourants | `/collections/colors` | same | N/A (different catalogue) |
| BR-L05 | Header SHOP > Butters & Waxes | `/collections/butters-waxes` | same | N/A (different catalogue) |
| BR-L06 | Header SHOP > Soap Bases | `/collections/soap-bases` | same | N/A (different catalogue) |
| BR-L07 | Header SHOP > Fragrances (5 sub-links) | `/collections/fragrance-oil-*, /collections/fine-fragrance` | same | N/A (different catalogue) |
| BR-L08 | Header SHOP > Clay Powders | `/collections/clay-powders` | same | N/A (different catalogue) |
| BR-L09 | Header SHOP > All Products | `/collections/all` | `/products/` | N/A (different catalogue) |
| BR-L10 | Header FORMULATIONS > Shampoo, Soap, Body, Face | `/blogs/shampoo, /blogs/soap, /blogs/body, /blogs/face` | `/videos/` (How-to); blog empty | PART |
| BR-L11 | Header Candle Making Kits | `/collections/candle-making-kit` | none (not applicable) | N/A |
| BR-L12 | Header About Us / Contact Us | `/pages/about-us, /pages/contact-us` | `/about-us/`, `/contact-us/` | SAME |
| BR-L13 | Header Log in | `/account/login` | `/account/sign-in/` | SAME |
| BR-L14 | Header Cart | `/cart` | `/cart/` | SAME |
| BR-L15 | Header search icon with suggestions | `/search?q=oils|chemicals|soap` | search box in header `/products/?q=` (no suggestions) | PART |
| BR-L16 | Footer Track Your Order | `https://www.shiprocket.in/shipment-tracking/ (external)` | `/track/` (EKI reference + contact; internal, own tracking) | DIFF |
| BR-L17 | Footer policy links (Payment/Shipping/Returns, Privacy, Cancellation, Terms, Refund) | `/pages/*` | shipping, cancellation, replacement pages; Privacy/Terms/Refund on effyklean.com | PART |
| BR-L18 | Footer Blogs | `/blogs/news` | blog route exists, 404 in running instance | PART |
| BR-L19 | Footer e-mail | `mailto:brmchemicals@gmail.com` | Support@EffyKlean.com, tel link | SAME |
| BR-L20 | Social: Facebook, Instagram | `external` | Facebook, Instagram, YouTube | SAME |
| BR-L21 | Footer newsletter form | `/contact#ContactFooter (tag form)` | `/subscribe/` verified opt-in | SAME |

## 4. Collections (BR-C, all 43 in the sitemap)

EffyKlean has **3 collections on effyklean.com / category and product_type filters on effyklean.in** (Household single, Household combo, Bulk). BRM collections are raw-material taxonomy and merchandising lists; none map to an EffyKlean collection. The comparable *capability* is category/use-case browsing (BR-F02).

| ID | Collection handle | Counterpart |
|---|---|---|
| BR-C01 | `/collections/chemicals` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C02 | `/collections/colors` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C03 | `/collections/essential-oil` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C04 | `/collections/herbal-extracts` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C05 | `/collections/butters-waxes` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C06 | `/collections/soap-bases` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C07 | `/collections/fragrances` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C08 | `/collections/clay-powders` | N/A (raw-material category; no EffyKlean equivalent) |
| BR-C09 | `/collections/featured-products` | N/A (BRM merchandising collection) |
| BR-C10 | `/collections/products-for-candle-making` | N/A (BRM merchandising collection) |
| BR-C11 | `/collections/waxes-for-candle` | N/A (BRM merchandising collection) |
| BR-C12 | `/collections/fragrance-oils-for-personal-care` | N/A (BRM merchandising collection) |
| BR-C13 | `/collections/essential-oils-for-personal-care` | N/A (BRM merchandising collection) |
| BR-C14 | `/collections/herbal-extracts-for-personal-care` | N/A (BRM merchandising collection) |
| BR-C15 | `/collections/butters-waxes-1` | N/A (BRM merchandising collection) |
| BR-C16 | `/collections/fragrance-oils-for-soap` | N/A (BRM merchandising collection) |
| BR-C17 | `/collections/essential-oils-for-soap` | N/A (BRM merchandising collection) |
| BR-C18 | `/collections/soap-bases-for-soap` | N/A (BRM merchandising collection) |
| BR-C19 | `/collections/liquid-extract-oil-soluble` | N/A (BRM merchandising collection) |
| BR-C20 | `/collections/liquid-herbal-extract-water-soluble` | N/A (BRM merchandising collection) |
| BR-C21 | `/collections/col-landing-frag-fb-1100` | N/A (BRM merchandising collection) |
| BR-C22 | `/collections/fragrance-oil-soluble` | N/A (BRM merchandising collection) |
| BR-C23 | `/collections/candles-diffuser` | N/A (BRM merchandising collection) |
| BR-C24 | `/collections/newly-launched-chemicals` | N/A (BRM merchandising collection) |
| BR-C25 | `/collections/natural-oils` | N/A (BRM merchandising collection) |
| BR-C26 | `/collections/fragrance-oil-personal-care` | N/A (BRM merchandising collection) |
| BR-C27 | `/collections/fragrance-oil-for-hair-care` | N/A (BRM merchandising collection) |
| BR-C28 | `/collections/fragrance-oil-for-soaps` | N/A (BRM merchandising collection) |
| BR-C29 | `/collections/bulk-products` | N/A (BRM merchandising collection) |
| BR-C30 | `/collections/lemon-shampoo-formulation-combo-kit` | N/A (BRM merchandising collection) |
| BR-C31 | `/collections/sulphate-free-lemon-shampoo-collection` | N/A (BRM merchandising collection) |
| BR-C32 | `/collections/fragrance-oil-for-candle` | N/A (BRM merchandising collection) |
| BR-C33 | `/collections/fragrance-water-soluble` | N/A (BRM merchandising collection) |
| BR-C34 | `/collections/fragrance-water-soluble-1` | N/A (BRM merchandising collection) |
| BR-C35 | `/collections/fine-fragrance` | N/A (BRM merchandising collection) |
| BR-C36 | `/collections/carrier-oil` | N/A (BRM merchandising collection) |
| BR-C37 | `/collections/homecare-fragrance-oil` | N/A (BRM merchandising collection) |
| BR-C38 | `/collections/recent-launches` | N/A (BRM merchandising collection) |
| BR-C39 | `/collections/fixed-oils` | N/A (BRM merchandising collection) |
| BR-C40 | `/collections/carrier-fixed-oils` | N/A (BRM merchandising collection) |
| BR-C41 | `/collections/candle-making-kit` | N/A (BRM merchandising collection) |
| BR-C42 | `/collections/candle-moulds` | N/A (BRM merchandising collection) |
| BR-C43 | `/collections/herbal-extract-collection-manual` | N/A (BRM merchandising collection) |

## 5. Blogs (BR-B, 99 blog URLs = 12 blog index pages + 87 articles)

| ID | Blog | Articles | EffyKlean counterpart |
|---|---|---|---|
| BR-B01 | `/blogs/news` | 68 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B02 | `/blogs/face` | 5 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B03 | `/blogs/shampoo` | 4 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B04 | `/blogs/candle` | 4 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B05 | `/blogs/body` | 3 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B06 | `/blogs/essential-oils` | 2 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B07 | `/blogs/soap` | 1 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B08 | `/blogs/dfgdfg` | 0 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B09 | `/blogs/abcd` | 0 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B10 | `/blogs/formulations` | 0 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B11 | `/blogs/essential-oils-1` | 0 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |
| BR-B12 | `/blogs/essential-oils-2` | 0 | Blog route `/blog/`, `/blog/<slug>/` exists (3 posts in `media/blog_source`); 404 in running instance; no blog editor in Admin (PART) |

Blog URLs in the sitemap: 99 (12 blog indexes + 87 articles; the Articles column excludes the index page).


## 6. Products (BR-PR)

Direct feed analysis (`/products.json`, 695 products, read this session): option sets Size 428 + SIZE 20, Weight 242, Title (single-variant) 5; **2,960 variants (max 6 per product)**; price range ₹115 to ₹42,000; compare-at price set on 2,405 variants; SKU set on 2,288 variants; product types: 538 blank, Liquid Extracts 73, Chemicals and Excipients 39, Essential Oils 28, Butters & Waxes 10, Fragrance Oils 4, Extracts 3; vendor labels inconsistent ("BRM Chemicals", "BRM CHEMICALS", "BRM HERBALS", "BRM herbals").

| ID | Item | BRM observed | EffyKlean | Status |
|---|---|---|---|---|
| BR-PR01 | Variant model | Size/Weight variants, up to 6 | SKU-per-pack model (RM-03 `INSUFF`: variant-ready, 1 variant per product today) | PART |
| BR-PR02 | Product page `/products/sodium-hydroxide-flakes` | Size selector, quantity, add to cart, share, mentions COA, GST, bulk, WhatsApp | `/products/<id>/`: quantity, add to cart, facts, classification, related (RM-01) | PART |
| BR-PR03 | Product page `/products/camphor-essential-oil` | same pattern | same | PART |
| BR-PR04 | Catalogue size | 695 products | 15 products (source feed); running instance 0 | N/A (different business) |
| BR-PR05 | Data quality | blank type 538/695, inconsistent vendor | EffyKlean: catalogue revision workflow with approval (H-01) | EffyKlean stronger |


## 7. Functions (BR-F)

| ID | Function | BRM observed behaviour | EffyKlean implementation | Status |
|---|---|---|---|---|
| BR-F01 | Search with suggestions and result page | Search panel with suggestions (`/search?q=oils\|chemicals\|soap`), popular categories; results page 533 for "soap"; filters product_type, availability, size, weight, price (observed) | `/products/?q=`; filters category, type, use case, size, price (E-02 VERIFIED T). No type-ahead suggestions | PART |
| BR-F02 | Category browsing | 43 collections, mega-menu with 3 levels | Filters + 3 collections on .com; flat on .in | PART |
| BR-F03 | Product variants and size selector | Size/Weight options, price per variant | One SKU per pack size; no selector (E-03) | PART |
| BR-F04 | Add to cart with confirmation notice | "Item added to your cart", Check out / Continue shopping (observed in markup) | `/cart/add`, redirect to cart (UNV: no notice text) | PART |
| BR-F05 | Cart | Cart page, line items (observed `/cart`) | `/cart/` with coupon, combo note, server totals | SAME |
| BR-F06 | Checkout and payment methods | Shopify checkout (not entered; payment methods UNVERIFIED) | Own checkout: signed review, GST fields, Zoho Payments (stub), no COD (SPEC §3.9) | UNV / DIFF |
| BR-F07 | Customer account | Login, recover password (observed) | Account: register, sign in, setup, orders, reorder, details, password | SAME |
| BR-F08 | Order tracking | Footer link to Shiprocket public tracking (external) | `/track/` EKI id + contact (own page); shipment status return path MISSING (register C-02) | PART |
| BR-F09 | Contact form | Name, Phone, Email | `/contact-us/` name, email, phone, fail-closed | SAME |
| BR-F10 | Newsletter | Footer form (Shopify customer tag form), no verification observed | `/subscribe/` with mailbox verification and unsubscribe (H-06 BLOCKED on provider) | SAME (stronger) |
| BR-F11 | Bulk / B2B requirement | Form on the bulk page; **no quote or B2B account** (page says bulk ordering is text/email only) | Bulk enquiry, negotiated quotes, distributor application, business accounts, distributor pricing (CR-006) | EffyKlean stronger |
| BR-F12 | Merchandising on home | Best sellers, recent launches, collections, use-case icons, client logos | Collections cards, benefits; no best-seller/recent-launch module | PART |
| BR-F13 | Free shipping announcement | Announcement bar: free shipping across India | No shipping charge (SPEC §3.8) but no announcement bar | PART |
| BR-F14 | Wishlist / reviews / recommendations | Markup contains the words "wishlist" (1) and "review" (10); app or feature not confirmed | Not in scope (register F-04) | UNV |
| BR-F15 | Knowledge hub / formulations | Knowledge Hub page, Formulations blogs (shampoo 4, soap 1, body 3, face 5, candle 4) | Videos page; blog (3 posts) | PART |
| BR-F16 | Technical documents (COA/SDS) | COA mentioned once on product page; downloads UNVERIFIED | Product facts; no document downloads | UNV |
| BR-F17 | Analytics and tag manager | Google Tag Manager, third-party script `cdn.codeblackbelt.com` (purpose UNVERIFIED) | No analytics (register I-04, consent first) | MISS |
| BR-F18 | Social links | Facebook, Instagram | Facebook, Instagram, YouTube | SAME |
| BR-F19 | Live chat / WhatsApp | No chat; WhatsApp mentioned in product text | n/a (effyklean.com has a floating WhatsApp widget; .in none) | N/A |
| BR-F20 | Currency/language | None observed | INR only | SAME |

## 8. Workflows (BR-W)

| ID | Workflow | BRM observed | EffyKlean | Status |
|---|---|---|---|---|
| BR-W01 | Browse > product > size > cart > checkout > pay | Observed up to the cart; checkout/payment not entered | Implemented locally with stubs (D-01, D-02); provider proof missing (B-01) | PART |
| BR-W02 | Search and filter to find a raw material | Observed (search, filters) | Implemented for 15 products; scale untested | SAME |
| BR-W03 | Customer sign-up/login/recover | Observed forms | Implemented | SAME |
| BR-W04 | Bulk requirement lead > thank-you > e-mail contact | Observed form and thank-you page; follow-up process unknown (UNV) | Bulk enquiry > Admin status/notes > quote > approve > provisioning (G-02) | EffyKlean stronger |
| BR-W05 | Track an order | External Shiprocket tracker | Internal track page; no shipment status feed yet (C-02) | PART |
| BR-W06 | Contact and support | Contact form, e-mail address | Contact form + Admin inbox; no notification e-mail (H-05 BLOCKED) | PART |
| BR-W07 | Newsletter sign-up | Footer form | Verified opt-in (blocked on mail provider) | PART |
| BR-W08 | Returns and refunds | Return & Refund policy page + form | No normal returns (SPEC); replacement with video evidence (CR-008) | DIFF |
| BR-W09 | Content-led acquisition (blogs, formulations, ad landing pages) | 68 news articles, 18 formulation/candle/essential articles, 2 ad landers (+3 stray test blogs) | 3 blog posts; no ad landers | MISS |

## 9. Coverage counts and unverified items

* BRM sitemap URLs: **853** (pages 14, collections 43, blog URLs 99 (12 indexes + 87 articles), products 695, home 1, `agents.md` 1). Rows created: BR-P 18, BR-L 21, BR-C 43, BR-B 12, BR-PR 5, BR-F 20, BR-W 9.
* **Inspected directly:** 14 of 14 pages, 1 of 43 collections plus the feed analysis of all 695 products, 2 of 695 product pages, cart, login, search. **Not individually opened:** 42 collection pages, 693 product pages, 87 blog articles (covered through the sitemap and feed, not read).
* **Unverified:** JavaScript behaviour; checkout, shipping calculation, payment methods; wishlist/review/COA features; purpose of `codeblackbelt` script; any behaviour behind login.
* Comparative findings are feeding the consolidated register (Comparison 4) as G-items; prior RM-01..RM-10 are not re-opened.

## 10. Key findings

1. BRM is a **catalogue-heavy raw-materials store** (695 products, 2,960 variants, 533 "soap" results). Its strengths are discovery (search suggestions, 43 collections, formulation content), not B2B workflow: it has **no quote, no B2B account, no distributor flow**, only a lead form. EffyKlean's bulk/distributor workflow is already stronger.
2. Gaps relative to BRM that fit EffyKlean's scale: **search suggestions**, **add-to-cart confirmation notice**, **best-seller/recent-launch modules**, **content hub depth**, **shipment tracking feed**, **technical document downloads** (all recommendations, none approved).
3. Items BRM has that EffyKlean should *not* copy without a decision: wishlist/reviews (no requirement, F-04), tag manager (consent first, I-04).
4. BRM catalogue data quality is weak (538 blank product types, inconsistent vendor names); EffyKlean's revision-and-approval workflow is an advantage.

