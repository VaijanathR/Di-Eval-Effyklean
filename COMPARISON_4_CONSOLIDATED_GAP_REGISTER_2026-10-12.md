# Comparison 4: Consolidated gap register and coverage summary

**Date:** 2026-10-12 · **Repository state:** HEAD `4af12e0`, 28 uncommitted paths (none staged); nothing was changed in the repository except new documents.
**Status:** ASSESSMENT ONLY. Not a requirement and not an implementation authorization. Every priority is a **recommendation**; HU+DI decide. `SPEC.md` v0.8, `ARCHITECTURE.md` and AD-01..AD-17 are not reopened.


**Priorities are recommendations, not approved decisions.** P1 = needed before a public launch or before other work can be judged; P2 = important after the P1 set; P3 = optional or needs a decision first. "Existing register" links point to `docs/foundation/PRODUCTION_READINESS_REGISTER.md` rows (not duplicated; the gaps below add only what the three comparisons newly show or re-rank). Comparison IDs: SA/ORD/CUS/... = Comparison 1 (and inventory IDs), BR = Comparison 2, EC = Comparison 3.

Files: `COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md`, `COMPARISON_2_BRMCHEMICALS_VS_EFFYKLEAN_2026-10-12.md`, `COMPARISON_3_EFFYKLEAN_COM_VS_IN_2026-10-12.md` (all in `docs/discovery/`).

## 1. Gap register (one row per distinct gap)


### Release path

| ID | Gap | Linked findings | Existing register | Nature | Recommended priority |
|---|---|---|---|---|---|
| CG-001 | effyklean.in is not hosted or reachable (DNS only, TLS fails); every `.in` finding is about the local build | EC §1, EC-V* | J-01, J-02, J-04 | MISSING | P1 (blocker) |
| CG-002 | Running/demo instance has an empty catalogue, so product pages, search, cart and journey parity cannot be shown; the 15-product source feed matches the live prices 15/15 but is not loaded | EC-P03..P17, EC-F01 | E-01, E-02 | MISSING (data) | P1 (small, needed for any visual review) |
| CG-003 | No visual, responsive or accessibility comparison has been done (no browser in this assessment); earlier browser evidence is historical | EC-V01..V06 | E-07 | UNVERIFIED | P1 (assessment, no build) |
| CG-004 | Provider proof is absent: Zoho Payments, Zoho Inventory and Shiprocket results are stubs or mocked HTTP | SA-A24, EC-F05, BR-F06 | B-01, B-02, B-05, B-06, B-11 | INSUFF | P1 (blocker) |
| CG-005 | Zoho tax/GST and invoice mapping undecided; printable GST invoice and packing slip not available in Admin | SA-A28, ORD-038, ORD-039, ORD-104 | B-07, D-06 | BLOCKED | P1 |
| CG-006 | Shipment status/tracking does not return into orders; `.in` track page has no carrier status (BRM uses Shiprocket externally, `.com` shows it in Admin) | BR-F08, BR-W05, EC-F08, EC-W04, SA-A02 | C-01, C-02, C-05 | MISSING | P1 |
| CG-007 | Transactional and staff e-mail (confirmation, shipping, contact alert, subscribe, resend) not built; no provider chosen | SET-021, SET-022, ORD-089, BR-W06, BR-W07, EC-W08, EC-W09 | D-09, H-05, H-06 | BLOCKED | P1 |
| CG-008 | Privacy, Terms, Refund and Contact-information pages are not on `.in`; footer sends customers to effyklean.com (HU legal text pending) | EC-P policy rows, EC-L06, BR-P04, BR-P05, BR-P08 | Phase 1 exit gate | BLOCKED (HU) | P1 (cut-over) |
| CG-009 | URL parity and redirects from effyklean.com paths (`/products/<handle>`, `/collections/*`, `/pages/*`, `/blogs/*`, `/policies/*`) to `.in` routes are not defined | EC-P* (all .com paths) | E-06 | MISSING | P2 (cut-over; SEO) |

### Admin operations

| ID | Gap | Linked findings | Existing register | Nature | Recommended priority |
|---|---|---|---|---|---|
| CG-010 | No outbox/worker list page in Admin although AD-07 now exists (retry actions only) | INT-004 | B-09, H-07, J-05 | PARTIAL | P1 (operations) |
| CG-011 | No low-stock or inventory view | PRD-008, INV-* | I-03 | BLOCKED (Zoho stock read) | P1 once Zoho proof exists |
| CG-012 | No order export; no export scope/format choices; no bulk selection | ORD-021, ORD-106, ORD-132, ORD-133, ORD-100 | H-03 | MISSING | P2 |
| CG-013 | Order detail lacks staff comments and a complete timeline | ORD-033, ORD-034 | H-03 | PARTIAL | P2 |
| CG-014 | Order list lacks sort by column, filter by product/SKU, amount range, tags | ORD-007, ORD-017, ORD-018, ORD-019, ORD-013 | H-03 | PARTIAL | P2 |
| CG-015 | Staff cannot be invited, created or have MFA reset in Admin (decision D-F2) | USR-003, USR-004 | H-02 | BLOCKED (decision) | P2 |
| CG-016 | Customer sign-in help and customer data-request export undecided (D-D1, D-D2) | CUS-018, CUS-028, CUS-050 | D-04 | BLOCKED (decision) | P2 |
| CG-017 | Reports lack export/scheduling and search-term report | ANA-018, ANA-020 | I-01 | MISSING | P2 |
| CG-018 | Draft / quote orders for B2B (PO number, send invoice) not built | DRF-001..021, ORD-090, ORD-091 | G-01..G-04 | BLOCKED (DC-22) | P3 |
| CG-019 | Customer segments and rich customer filters not built | CUS-003, CUS-021, CUS-022, CUS-054 | I-02 | MISSING | P3 |
| CG-020 | Notification centre, home activity feed and alerts | SYS-005, SYS-007, SYS-020 | H-04 | MISSING | P3 |
| CG-021 | Product CSV import and spreadsheet bulk editor scope unclear (`products/bulk` exists; contents not verified) | PRD-072, PRD-073, PRD-074, PRD-090 | H-01 | UNVERIFIED | P3 (verify first) |
| CG-022 | Blog: `/blog/` is 404 in the running instance and Admin has no blog post editor | EC-P blog rows, BR-B*, CNT-007, BR-F15 | E-01 | PARTIAL | P2 |

### Storefront and content

| ID | Gap | Linked findings | Existing register | Nature | Recommended priority |
|---|---|---|---|---|---|
| CG-023 | Catalogue discovery: no search suggestions, no add-to-cart confirmation, no best-seller or new-arrival modules | BR-F01, BR-F04, BR-F12 | E-02 | MISSING | P3 |
| CG-024 | Product variant selector (several pack sizes on one product) vs one SKU per pack | BR-F03, BR-PR01, EC-F03 | E-03 | PARTIAL (decision) | P3 |
| CG-025 | Technical documents (COA/SDS) downloads; BRM presence unverified | BR-F16 | E-01 | UNVERIFIED | P3 (decision) |
| CG-026 | Content hub, formulation guides and ad landing pages (BRM has 87 articles and 2 landers; EffyKlean 3 posts) | BR-P11..P13, BR-W09, BR-F15 | E-01 | MISSING | P3 |
| CG-027 | Floating WhatsApp contact button and tel/mail prominence (`.com` has the app) | EC-L10 | H-05 | MISSING | P3 (decision) |
| CG-028 | Language option (Weglot on `.com`); no requirement on `.in` | EC-L11, EC-F18 | none | MISSING | P3 (decision, may be NOT IN SCOPE) |
| CG-029 | Analytics/tag manager with consent (`.com` and BRM load tag scripts; `.in` none) | BR-F17, EC-F15 | I-04 | MISSING (deliberate) | P2 (decision) |
| CG-030 | Free-shipping announcement (BRM) vs "no shipping charge" (SPEC §3.8): no announcement bar | BR-F13 | E-05 | MISSING | P3 |
| CG-031 | Combo concept: the live `.com` combo collection is empty; `.in` has the rule but no combo presentation page | EC-P combo row, EC-F03 | F-01 | DIFF (decision) | P3 |
| CG-032 | Wishlist, reviews, recommendations: present or hinted at BRM, no EffyKlean requirement | BR-F14 | F-04 | NOT IN SCOPE | Decision only |

### Assessment follow-ups

| ID | Gap | Linked findings | Existing register | Nature | Recommended priority |
|---|---|---|---|---|---|
| CG-033 | Shopify Admin not re-observed since 2026-10-10; 478 of 494 inventory rows carry unrefreshed statuses | Comparison 1 §5 | none | UNVERIFIED | P2 (needs HU signed-in session) |
| CG-034 | `.com` distributor enquiry page: form existence not confirmed in fetched HTML | EC-P distributor row | G-01 | UNVERIFIED | P3 (browser check) |
| CG-035 | Checkout and payment flow on `.com` and BRM not entered (by instruction) | BR-F06, EC-W01 | D-01, B-01 | UNVERIFIED (not authorised) | n/a |
| CG-036 | Shopify Admin surfaces with no EffyKlean requirement (collections, files, metaobjects, markets, channels, apps, plan): recommended exclusions | SA-A06..A08, A15..A20 | none | NOT IN SCOPE | Reject (recommendation) |

Gaps: **36**. By recommended priority: Decision 1, P1 10, P2 10, P3 13, Reject 1, n/a 1.


## 2. Coverage counts

| Comparison | Source items found | Rows written | Directly inspected | Carried from earlier evidence | Not inspected / unverified |
|---|---|---|---|---|---|
| 1 Shopify Admin vs Django Admin | 34 Admin areas, 494 inventory capabilities | 34 area rows + 494 function rows + 16 re-verified deltas | Django side: 128 admin routes, sidebar, view modules | All Shopify observations (live walks 2026-10-05, 2026-10-10; API 2026-07); 478 function statuses | Shopify not re-opened today; 36 DOC and 14 UNK rows are leads only |
| 2 BRM vs EffyKlean | 853 sitemap URLs (14 pages, 43 collections, 99 blog URLs, 695 products, 2 other) | 18 pages + 21 links + 43 collections + 12 blogs + 5 product + 20 function + 9 workflow rows | 14/14 pages, 1/43 collections, 2/695 product pages, cart, login, search; feed of 695 products | prior BRM report (RM-01..10) | 42 collections, 693 product pages, 87 blog articles read only via sitemap/feed; checkout, JS behaviour |
| 3 effyklean.com vs effyklean.in | 30 `.com` URLs + 9 extra; 0 reachable `.in` pages | 38 page + 12 `.in`-only + 12 link + 19 function + 11 workflow + 6 visual rows | 30/30 `.com` URLs, 25 local routes, URLconf | register E-07 visual evidence (historical) | all rendered visuals; checkout; `.in` product pages (empty catalogue) |

## 3. Inaccessible or unverified items (explicit)

1. **Live Shopify Admin:** no authenticated session available to this assessment; not re-observed (CG-033).
2. **effyklean.in:** not deployed; DNS resolves but TLS fails (CG-001).
3. **Rendered look-and-feel and responsiveness** on any site (CG-003).
4. **Checkout and payment** on effyklean.com and brmchemicals.com: not entered, by instruction (CG-035).
5. **Behaviour that needs JavaScript:** search suggestions, add-to-cart notice, variant selection on BRM; widgets on `.com`.
6. **`.com` combo collection:** `collections.json` reports 50 products but the page and `products.json` report 0; cause unverified.
7. **Local Admin run:** not signed in (MFA); statuses are static-code evidence.

## 4. Key findings

1. EffyKlean's Admin and storefront are broad and cover the core of what the sources do, with **stronger bulk/distributor workflow than BRM** and **stronger verified-subscribe and replacement flows than `.com`**.
2. The decisive gaps are not new features; they are **launch prerequisites already in the readiness register**: hosting (CG-001), provider proof (CG-004), tax/invoice (CG-005), shipment status (CG-006), transactional e-mail (CG-007), legal pages (CG-008).
3. New findings from this assessment: the **empty catalogue** in the running instance (CG-002), **no URL redirect plan** from `.com` (CG-009), **blog 404** (CG-022), **no outbox view** though AD-07 exists (CG-010), and **12 stale statuses** in the Shopify inventory.
4. The 36 gaps reduce to **10 P1, 10 P2, 13 P3** recommendations plus decisions that only HU+DI can take.

## 5. Evidence limitations

* Evidence classes follow the register: `S` static inspection for Django; HTTP fetch of public pages for the external sources; **no `SB` or `P` evidence** of any provider.
* The assessment ran against HEAD `4af12e0` plus 28 uncommitted paths (home-page link rearrangement, TESTCODE B1, Zoho Inventory adapter, payment edits); these were not touched.
* No full test suite was run for this assessment.

