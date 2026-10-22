I found that ORD-007, ORD-008, ORD-009, and ORD-012 had stale statuses in Comparison 1, despite being implemented per the HU+DI decision log — I'll correct these in the reconciliation while continuing to build the inventory. · summary

  Ran 5 shell commands

Status: the Shopify-row engine is built; fixing a small bug, then I'll generate and check all sections.

  Ran 7 shell commands

EffyKlean Master Functionality Inventory — evidence consolidation only

I am building this from the four comparison documents, the production-readiness register, SPEC.md v0.8 and the decision
logs. No repository file has been written or modified in this task, and nothing was loaded, staged or committed.

0. Repository state and method

Repository safety report (read-only commands)

┌──────────────┬───────────────────────────────────────────────────────────────────────────────────────────────────┐
│     Item     │                                              Result                                               │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ HEAD         │ 4af12e05fb119c139b624f73f5f94c9e04190859 ("test, docs: combined retry-path regression tests and   │
│              │ worker runbook")                                                                                  │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Staged       │ none                                                                                              │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Unstaged     │ 17 paths: PROJECT_LOG.md, config settings (3), integrations/zoho.py, modules/orders (4),          │
│ modified     │ modules/storefront (3), and 4 test files                                                          │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Untracked    │ 15 paths: the 4 COMPARISON_* documents, PRODUCTION_READINESS_REGISTER.md, 2 foundation docs,      │
│              │ integrations/zoho_inventory.py, the TESTCODE command, model and migration files, and 3 test files │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Source       │ All four exist at the expected docs/discovery/COMPARISON_*_2026-10-12.md paths (61,151 / 22,655 / │
│ documents    │  24,208 / 11,242 bytes). They are untracked and were unchanged during this task.                  │
├──────────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Other        │ None. The working tree was preserved.                                                             │
│ changes      │                                                                                                   │
└──────────────┴───────────────────────────────────────────────────────────────────────────────────────────────────┘

Method and limits
- The four comparison documents are my own outputs from earlier today. I re-read them programmatically (row IDs,
  columns), not line by line by eye.
- I re-checked against SHOPIFY_ADMIN_FUNCTION_INVENTORY.md (including its decision log), PROJECT_LOG.md, the register
  (76 rows), SPEC §3, §12–§13, §20, §23, §26–§29 and §33, and the Admin URLconf, templates and view code.
- I did not re-read ARCHITECTURE.md or the individual decision records beyond the AD references already cited in the
  register. I did not run the test suite or any browser.
- Every Shopify observation is carried from your 2026-10-05 and 2026-10-10 walks. Nothing was re-observed.

Corrections to my earlier comparisons (found while consolidating)
1. Comparison 1 carried stale statuses for ORD-007, ORD-008, ORD-009 and ORD-012 (shown as MISS or SIM). The inventory
   decision log records them as HU+DI-accepted and implemented in Orders batch 1 (commit dd4478c). The code confirms
   it: sort parameters and a "Dispatch from" column exist.
2. As a result, Comparison 4 gap CG-014 ("order list lacks sort by column") is wrong for sorting. The remaining filters
   (product, amount, tags) are still open.
3. ORD-010 and ORD-011: the inventory recommendation said REJECT, but the HU+DI decision is DEFER. The decision
   prevails (flagged below).
4. The 494-row inventory excludes 12 decision-log rows, which are the Orders batch 1 decisions, and they are folded
   into the matching ORD rows.

Master ID scheme. MF-nnn rows are platform, storefront, integration, content, infrastructure and governance functions
(numbered with deliberate gaps, so they are stable labels and not dense). MA-<original id> rows are the Shopify Admin
capabilities, one per inventory row, with the original ID kept.

Legend (applies to all sections)
- Status: IVV implemented and adequately validated; IIV implemented but inadequately validated; PART partially
  implemented; MISS missing; BLK blocked by an external dependency or an HU+DI decision; EXC deliberately excluded or
  not applicable; UNV unverified.
- Disposition (preliminary, for HU+DI review; not a priority): IMPLEMENT; FIX; VALIDATE; REJECT/OOS (rejected or out of
  scope); BLOCKED-DEC (blocked, decision required); NO ACTION.
- Evidence type: S static code; T automated tests; B browser (earlier tree); M mocked provider HTTP; F public-site
  fetch 2026-10-12; O Shopify observation (carried); D document. The tier after O: is the inventory tier (OBS, OBS-L,
  API, DOC, UNK).
- Validation codes:
  - V0: none this session; status carried from the inventory.
  - V0B: V0, plus an agent-reported browser walk on an earlier tree, with no row-level test trace.
  - V0S: V0, a labelled local simulation with no provider contact.
  - V1: static route/code check on 2026-10-12 (existence only).
  - V2: automated tests on an earlier tree (stubs/mocks), not re-run now.
  - V2H: HU+DI batch-1 acceptance on 2026-10-10 with named tests, commit dd4478c, earlier tree.
  - V3: public HTTP fetch on 2026-10-12.
  - V4: local-build GET probe on 2026-10-12 (empty catalogue).
  - V5: not possible.
- Global caveats for all "implemented" rows: there is no AC-to-test index (register A-03), and no full-suite run on the
  current tree (A-04). No row has provider-sandbox or production proof. Unit tests and stubs are not counted as
  provider proof.
- Source ID prefixes: C1 = Comparison 1 (inventory IDs like ORD-001, areas SA-Axx, deltas SA-D), C2 = BR-…, C3 = EC-…,
  C4 = CG-…, REG = readiness register row. Every MA- row is also a row of Comparison 1 Appendix A.

Section plan: §1 MF-001–MF-121; §2 MA-ORD-001–MA-ORD-145; §3 MA-DRF-001–MA-GFT-002; §4 MA-CUS-001–MA-DSC-041; §5
MA-CNT-001–MA-ANA-027; §6 MA-SET-001–MA-SYS-022; §7 reconciliation.

  Ran 1 shell command

§1 Platform, storefront, integration, content, infrastructure and governance (MF-001 to MF-121, 103 rows)

Part 1a (MF-001 to MF-076)

Master ID: MF-001
Domain: Governance / baseline
Functionality: Frozen SPEC v0.8, ADs and ARCHITECTURE are the authority
Expected behaviour / AC: Competitor behaviour never overrides approved rules; AC-1.2
Status: IVV
Evidence: D: CLAUDE.md; SPEC revision history
Validation: V1: read this session
Dependency / blocker: -
SPEC / decision: SPEC §34; CLAUDE.md
Source IDs: REG A-01, A-06
Disposition: NO ACTION
Rationale: Governance baseline in force
Evidence gap: -
────────────────────────────────────────
Master ID: MF-002
Domain: Governance / baseline
Functionality: Reviewed and committed baseline for the 28 uncommitted paths (home-page links, TESTCODE B1, Zoho
Inventory adapter, payment edits)
Expected behaviour / AC: Change set reviewed by HU+DI before commit
Status: BLK
Evidence: S: git status (17 modified, 15 untracked incl. 5 assessment docs, 0 staged)
Validation: V1: git status 2026-10-12
Dependency / blocker: HU+DI review of change set
SPEC / decision: CLAUDE.md principle 6
Source IDs: REG A-02
Disposition: BLOCKED-DEC
Rationale: No commit without explicit HU+DI approval
Evidence gap: Contents of working tree not re-reviewed here
────────────────────────────────────────
Master ID: MF-003
Domain: Governance / validation
Functionality: Requirement-to-AC-to-test traceability index
Expected behaviour / AC: Each AC maps to named tests (SPEC §31)
Status: PART
Evidence: S: SPEC §31/§33; 77 test files, untagged
Validation: V1
Dependency / blocker: none
SPEC / decision: SPEC §31, §33
Source IDs: REG A-03
Disposition: VALIDATE
Rationale: Needed to support every "implemented" claim in this inventory (row-level traceability is absent)
Evidence gap: No AC-to-test index exists
────────────────────────────────────────
Master ID: MF-004
Domain: Governance / validation
Functionality: Full test suite proof on the current committed tree
Expected behaviour / AC: 0 failed; ruff, check, migration drift clean
Status: IIV
Evidence: T: PROJECT_LOG 1819 passed on an earlier tree; focused runs only since
Validation: V2: not re-run this session
Dependency / blocker: MF-002 (clean committed tree)
SPEC / decision: SPEC §30
Source IDs: REG A-04
Disposition: VALIDATE
Rationale: One suite run underpins all "implemented" rows
Evidence gap: Suite takes about 22 minutes
────────────────────────────────────────
Master ID: MF-005
Domain: Governance / delivery
Functionality: CI pipeline (scripts/ci.sh on every push)
Expected behaviour / AC: Green run per push
Status: BLK
Evidence: S: scripts/ci.sh exists; no .github workflow
Validation: V1
Dependency / blocker: Remote repository authorisation (HU+DI)
SPEC / decision: SPEC §30
Source IDs: REG A-05
Disposition: BLOCKED-DEC
Rationale: Needs an authorised remote
Evidence gap: -
────────────────────────────────────────
Master ID: MF-006
Domain: Governance / assessment
Functionality: Re-observation of the live Shopify Admin (statuses carried from 2026-10-10)
Expected behaviour / AC: Shopify rows reflect today's Admin
Status: UNV
Evidence: O: live walks 2026-10-05, 2026-10-10
Validation: V5: no authenticated session available
Dependency / blocker: HU signed-in browser session
SPEC / decision: SPEC §29 (reference only)
Source IDs: C4 CG-033; C1 §5
Disposition: BLOCKED-DEC
Rationale: Cannot be done without HU access
Evidence gap: Shopify changes after 2026-10-10 unknown
────────────────────────────────────────
Master ID: MF-007
Domain: Governance / assessment
Functionality: Rendered visual, responsive and accessibility parity of effyklean.in vs effyklean.com
Expected behaviour / AC: Responsive/mobile and Core Web Vitals baseline (SPEC §30.2)
Status: UNV
Evidence: D: E2E_PROTOTYPE_EVIDENCE (147+147 checks, earlier tree)
Validation: V5: no browser in the comparison; VB historical only
Dependency / blocker: Catalogue loaded (MF-020); browser pass
SPEC / decision: SPEC §30.2
Source IDs: C4 CG-003; C3 EC-V01..V06, EC-F17; REG E-07
Disposition: VALIDATE
Rationale: Historical browser evidence does not prove the current tree
Evidence gap: All visual claims unverified
────────────────────────────────────────
Master ID: MF-008
Domain: Governance / assessment
Functionality: effyklean.com Distributor enquiry page: whether it is a form
Expected behaviour / AC: Parity of distributor enquiry (SPEC §9)
Status: UNV
Evidence: F: fetched HTML shows only footer/search forms
Validation: V3
Dependency / blocker: Browser check
SPEC / decision: SPEC §9
Source IDs: C4 CG-034; C3 EC-P
Disposition: VALIDATE
Rationale: Needs rendered page
Evidence gap: Form may be app-injected (JS)
────────────────────────────────────────
Master ID: MF-009
Domain: Governance / assessment
Functionality: Competitor checkout and payment flows (effyklean.com, BRM)
Expected behaviour / AC: Not entered, by instruction
Status: UNV
Evidence: -
Validation: V5: not authorised (no orders/payments)
Dependency / blocker: -
SPEC / decision: -
Source IDs: C4 CG-035; C2 BR-F06; C3 EC-W01
Disposition: NO ACTION
Rationale: Deliberately not attempted
Evidence gap: Unverified by design
────────────────────────────────────────
Master ID: MF-020
Domain: Storefront / catalogue
Functionality: Catalogue data present in the running/demo instance (15 products from the source feed; prices and
compare-at match effyklean.com 15/15)
Expected behaviour / AC: Customer can browse products (SPEC §6; AC-6.x)
Status: MISS
Evidence: F+S: products.json vs media/catalogue_source/source.json; local GET /products/ shows "No products are
currently available"
Validation: V3 + V4
Dependency / blocker: Director approval of draft revisions (import_catalogue_source creates revisions for review)
SPEC / decision: SPEC §6; AC-6.1..6.10
Source IDs: C4 CG-002; C3 EC-F01, EC-F02, EC-P02..P16
Disposition: IMPLEMENT
Rationale: Operational data step, not new scope; prerequisite to judge any product journey
Evidence gap: Not loaded in this task (forbidden)
────────────────────────────────────────
Master ID: MF-021
Domain: Storefront / catalogue
Functionality: Product list: search, category, type, use-case, size, price filters, sort
Expected behaviour / AC: Search/browse/filter (RM-02)
Status: IVV
Evidence: T: test_rm_catalogue.py; S: pages.py filters
Validation: V2; V4 (form fields only, no data)
Dependency / blocker: MF-020 for data
SPEC / decision: SPEC §6; AC-6.x
Source IDs: REG E-02; C2 BR-F01, BR-F02, BR-W02, BR-P10, BR-P18, BR-L15; C3 EC-F14, EC-P36, EC-L04, EC-X01
Disposition: NO ACTION
Rationale: Implemented and test-backed
Evidence gap: Quality at real catalogue size untested; BRM scale 695
────────────────────────────────────────
Master ID: MF-022
Domain: Storefront / catalogue
Functionality: Search type-ahead suggestions
Expected behaviour / AC: No SPEC requirement
Status: MISS
Evidence: F: BRM search panel suggestions
Validation: V3
Dependency / blocker: -
SPEC / decision: SPEC silent
Source IDs: C2 BR-F01; C4 CG-023
Disposition: NO ACTION
Rationale: Enhancement, deferred; no requirement found in SPEC §6
Evidence gap: JS behaviour not observed
────────────────────────────────────────
Master ID: MF-023
Domain: Storefront / catalogue
Functionality: Product detail page: rich product information, quantity, add to cart, facts, classification
Expected behaviour / AC: Rich product information (RM-01)
Status: IIV
Evidence: T: test_catalogue_model.py; S: pages.py _add_to_cart_form, _facts
Validation: V2; V4 not possible (no product)
Dependency / blocker: MF-020
SPEC / decision: SPEC §6; AC-6.x
Source IDs: REG E-01; C2 BR-PR02, BR-PR03; C3 EC-P02..P16
Disposition: VALIDATE
Rationale: Rendered page never seen on current tree
Evidence gap: Content completeness/approval unconfirmed (register E-01)
────────────────────────────────────────
Master ID: MF-024
Domain: Storefront / catalogue
Functionality: Pack size: separate SKU per size vs one product with a size selector
Expected behaviour / AC: SPEC §6 SKU model; RM-03 "variant-ready" only
Status: PART
Evidence: S: one Sku per product id; no variant entity
Validation: V1
Dependency / blocker: HU+DI: is a multi-size selector wanted?
SPEC / decision: SPEC §6
Source IDs: REG E-03; C2 BR-F03, BR-PR01; C3 EC-F03; C4 CG-024
Disposition: BLOCKED-DEC
Rationale: Roadmap approved "ready", not built; decision needed before any change
Evidence gap: -
────────────────────────────────────────
Master ID: MF-025
Domain: Storefront / catalogue
Functionality: Separation of catalogue revision from live Zoho availability
Expected behaviour / AC: Catalogue content never decides stock (SPEC §14)
Status: IVV
Evidence: T: test_i02_catalogue_pages.py
Validation: V2
Dependency / blocker: Real stock source pending (MF-052)
SPEC / decision: SPEC §14; AC-14.x
Source IDs: REG E-04
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: Real source not proven
────────────────────────────────────────
Master ID: MF-026
Domain: Storefront / catalogue
Functionality: Related-product links on the product page
Expected behaviour / AC: SPEC silent
Status: IIV
Evidence: S: pages.py _related_html (line 431/508) renders related products
Validation: V1
Dependency / blocker: HU+DI: confirm scope
SPEC / decision: SPEC silent
Source IDs: REG E-09; (conflict)
Disposition: BLOCKED-DEC
Rationale: CONFLICT FLAGGED: register E-09 says NOT IN SCOPE, but code renders related products
Evidence gap: Reported, not resolved
────────────────────────────────────────
Master ID: MF-027
Domain: Storefront / catalogue
Functionality: Add-to-cart confirmation notice (BRM shows "Item added to your cart")
Expected behaviour / AC: No requirement
Status: UNV
Evidence: F: BRM markup
Validation: V3
Dependency / blocker: -
SPEC / decision: SPEC silent
Source IDs: C2 BR-F04; C4 CG-023
Disposition: NO ACTION
Rationale: Enhancement, deferred
Evidence gap: .in redirect behaviour not seen with data
────────────────────────────────────────
Master ID: MF-028
Domain: Storefront / home
Functionality: Home page: hero, benefits, collection cards, newsletter, search, footer (HU-approved link rearrangement
uncommitted)
Expected behaviour / AC: Home content per SPEC §23
Status: IIV
Evidence: S: pages.home; T: test_storefront_shell.py (modified); V4 GET / 200
Validation: V4; V2
Dependency / blocker: MF-002 (uncommitted change)
SPEC / decision: SPEC §23
Source IDs: C3 EC-P01; C2 BR-P01; C4 CG-023
Disposition: VALIDATE
Rationale: Rendering not compared
Evidence gap: Visual UNV
────────────────────────────────────────
Master ID: MF-029
Domain: Storefront / home
Functionality: Home merchandising modules (best sellers, recent launches, client logos)
Expected behaviour / AC: No requirement
Status: MISS
Evidence: F: BRM home sections
Validation: V3
Dependency / blocker: -
SPEC / decision: SPEC silent
Source IDs: C2 BR-F12; C4 CG-023
Disposition: NO ACTION
Rationale: Enhancement, deferred
Evidence gap: -
────────────────────────────────────────
Master ID: MF-030
Domain: Storefront / catalogue
Functionality: Separate Household Combo or Bulk Combo collection page
Expected behaviour / AC: Combo is a cart rule, not a collection
Status: EXC
Evidence: F: effyklean.com combo collection is empty (0 products); S: no combo page on .in
Validation: V3; V1
Dependency / blocker: -
SPEC / decision: SPEC §3.11
Source IDs: C3 EC-P24; C4 CG-031
Disposition: REJECT/OOS
Rationale: SPEC §3.11 excludes a separate combo collection
Evidence gap: collections.json says 50 products vs 0 on page: cause unverified
────────────────────────────────────────
Master ID: MF-031
Domain: Storefront / catalogue
Functionality: Format filter Household/Bulk (not a purchasing restriction)
Expected behaviour / AC: Formats are not restrictions (SPEC §3.21)
Status: IVV
Evidence: S: /products/?product_type=Household+format and Bulk+format links; V4 200
Validation: V4; V2
Dependency / blocker: -
SPEC / decision: SPEC §3.21; AC-6.x
Source IDs: C3 EC-P23, EC-P25
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: Behaviour with data unseen
────────────────────────────────────────
Master ID: MF-032
Domain: Storefront / catalogue
Functionality: BRM raw-material taxonomy: 43 collections, 695 products, 12 blogs
Expected behaviour / AC: Not an EffyKlean business
Status: EXC
Evidence: F: BRM sitemap and products.json
Validation: V3
Dependency / blocker: -
SPEC / decision: BRM report (reference only)
Source IDs: C2 BR-C01..BR-C43, BR-PR04, BR-B01..B12, BR-L01..BR-L09, BR-L11
Disposition: REJECT/OOS
Rationale: Competitor catalogue is not EffyKlean scope; BRM is evidence only per the approved BRM record
Evidence gap: -
────────────────────────────────────────
Master ID: MF-033
Domain: Storefront / catalogue
Functionality: Wishlist, save-for-later, recently viewed, reviews/ratings, recommendations
Expected behaviour / AC: SPEC silent; loyalty out (§3.2)
Status: MISS
Evidence: F: BRM markup hints only
Validation: V3
Dependency / blocker: HU+DI: scope ambiguity S-1
SPEC / decision: SPEC silent
Source IDs: REG F-04, S-1; C2 BR-F14; C4 CG-032
Disposition: BLOCKED-DEC
Rationale: Register lists scope ambiguity S-1 open; nothing approves or excludes it
Evidence gap: Existence at BRM unconfirmed
────────────────────────────────────────
Master ID: MF-034
Domain: Storefront / catalogue
Functionality: Technical documents (COA/SDS) download
Expected behaviour / AC: No requirement
Status: UNV
Evidence: F: BRM product page mentions COA once
Validation: V3
Dependency / blocker: -
SPEC / decision: SPEC silent
Source IDs: C2 BR-F16; C4 CG-025
Disposition: NO ACTION
Rationale: Enhancement, deferred; existence unverified
Evidence gap: -
────────────────────────────────────────
Master ID: MF-040
Domain: Storefront / cart
Functionality: Cart with server-authoritative totals and availability (cookie holds id+quantity only)
Expected behaviour / AC: Server authority (RM-04); AC-11.x
Status: IVV
Evidence: T: test_sec_f02_f03_checkout_integrity.py, test_i03_cart.py
Validation: V2; V4 GET /cart/ 200
Dependency / blocker: -
SPEC / decision: SPEC §11; AC-11.1..11.6
Source IDs: REG D-02; C2 BR-F05, BR-P16, BR-L14; C3 EC-P35, EC-X02, EC-L03
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: -
────────────────────────────────────────
Master ID: MF-041
Domain: Storefront / checkout
Functionality: Guest checkout: signed review, structured address, GST number/name capture
Expected behaviour / AC: AC-11.x; GST capture AC-13.x
Status: IIV
Evidence: T: test_i04_checkout.py, test_e2e_prototype.py; B: exit gate row 7
Validation: V2; VB historical
Dependency / blocker: Real payment (MF-043)
SPEC / decision: SPEC §11, §13.5; AC-11.x, AC-13.x
Source IDs: REG D-01; C3 EC-F06, EC-W01, EC-W02, EC-X03, EC-X04; C2 BR-W01
Disposition: VALIDATE
Rationale: Browser evidence is historical
Evidence gap: Not re-run on current tree
────────────────────────────────────────
Master ID: MF-042
Domain: Storefront / checkout
Functionality: No cash on delivery or partial payment on delivery
Expected behaviour / AC: COD not offered (AC-12.x)
Status: EXC
Evidence: S/T: absent; register D-03
Validation: V2; V1
Dependency / blocker: -
SPEC / decision: SPEC §3.9, §12.8
Source IDs: REG D-03; C3 EC-F05
Disposition: REJECT/OOS
Rationale: Preserved exclusion (SPEC §3.9, v0.7)
Evidence gap: Shopify .com has a COD/Magic Checkout app: not comparable
────────────────────────────────────────
Master ID: MF-043
Domain: Storefront / payment
Functionality: Prepaid online payment via Zoho Payments (selected provider, CR-007); order created only after verified
payment
Expected behaviour / AC: AC-12.x; AC-15.x
Status: IIV
Evidence: M/T: integrations/zoho_payments.py, test_zoho_payments.py (~50)
Validation: V2: mocked HTTP; never run against Zoho
Dependency / blocker: Zoho Payments sandbox credentials; B-01 acceptance
SPEC / decision: SPEC §12.1, §12.17; CR-007
Source IDs: REG B-01, B-02; C4 CG-004; C2 BR-F06; C3 EC-L08
Disposition: VALIDATE
Rationale: Mocked only; no SB/P evidence exists
Evidence gap: Webhook payload shape and signature encoding are assumptions
────────────────────────────────────────
Master ID: MF-044
Domain: Storefront / checkout
Functionality: No separate shipping charge
Expected behaviour / AC: No shipping line (AC-8.x/11.x)
Status: EXC
Evidence: S: no shipping-charge code; SPEC
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §3.8
Source IDs: C3 EC-F07; C2 BR-F13
Disposition: REJECT/OOS
Rationale: Preserved exclusion (SPEC §3.8)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-045
Domain: Storefront / content
Functionality: "Free shipping" announcement bar
Expected behaviour / AC: Content only; SPEC §3.8 says no shipping charge
Status: MISS
Evidence: F: BRM announcement bar
Validation: V3
Dependency / blocker: Wording decision
SPEC / decision: SPEC §3.8, §23
Source IDs: C2 BR-F13; C4 CG-030
Disposition: BLOCKED-DEC
Rationale: Whether to announce free shipping is a content/legal wording decision (§23.4)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-046
Domain: Storefront / promotions
Functionality: Combo discount: first eligible item none, later items configured amount
Expected behaviour / AC: AC-21.x
Status: IIV
Evidence: S: orders/pricing.py:54-69; T: test_i03_cart.py
Validation: V2
Dependency / blocker: Regression test for delete-first case
SPEC / decision: SPEC §21; AC-21.1..21.7
Source IDs: REG F-01; C3 EC-F04, EC-W03
Disposition: VALIDATE
Rationale: Code exists; named regression test missing
Evidence gap: -
────────────────────────────────────────
Master ID: MF-047
Domain: Storefront / promotions
Functionality: One additional discount only (combo OR coupon, never stacked); ₹500 minimum with an additional discount
Expected behaviour / AC: AC-21.x; AC-7.x
Status: IVV
Evidence: T: test_coupons.py:73,174; test_rm_commercial.py
Validation: V2
Dependency / blocker: HU+DI confirmation (implementation default)
SPEC / decision: SPEC §21, §7
Source IDs: REG F-02; C3 EC-F04
Disposition: BLOCKED-DEC
Rationale: Behaviour is a recorded implementation default awaiting HU+DI confirmation (mapping §11)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-048
Domain: Storefront / promotions
Functionality: Coupon rules and Admin coupon management (create, edit, duplicate, bulk codes, toggle)
Expected behaviour / AC: AC-21.x
Status: IVV
Evidence: T: test_coupons.py, test_discounts_admin.py; S: coupons/* routes
Validation: V2; V1
Dependency / blocker: -
SPEC / decision: SPEC §21, §27.1
Source IDs: REG F-03; C1 DSC-015, DSC-017
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: -
────────────────────────────────────────
Master ID: MF-049
Domain: Storefront / orders
Functionality: Same-day dispatch prohibited (next IST day)
Expected behaviour / AC: AC-18.x
Status: IVV
Evidence: T: DispatchNotPermittedError, test_f05_checkout
Validation: V2
Dependency / blocker: -
SPEC / decision: SPEC §18; PROJECT_LOG 2026-10-09
Source IDs: REG C-03; C1 ORD-009
Disposition: NO ACTION
Rationale: Implemented and approved
Evidence gap: SPEC itself carries no sentence (inventory ORD-009 note)
────────────────────────────────────────
Master ID: MF-050
Domain: Storefront / account
Functionality: Cart persistence across devices for signed-in users
Expected behaviour / AC: SPEC states no server cart (register)
Status: MISS
Evidence: S: signed first-party cookie by design
Validation: V1
Dependency / blocker: HU+DI: scope ambiguity S-3
SPEC / decision: SPEC silent
Source IDs: REG D-05, S-3
Disposition: BLOCKED-DEC
Rationale: Open scope ambiguity
Evidence gap: -
────────────────────────────────────────
Master ID: MF-051
Domain: Integration / payment
Functionality: Authoritative payment state, webhook signature, dedup, partial/failed/reversed/unresolved handling
Expected behaviour / AC: AC-12.17..12.19; AC-25.x
Status: IIV
Evidence: T/M: payment_flow.process_zoho_webhook; test_payment_reconciliation.py
Validation: V2: mocked
Dependency / blocker: MF-043
SPEC / decision: SPEC §12.17-12.19, §25
Source IDs: REG B-02
Disposition: VALIDATE
Rationale: Signature scheme assumed
Evidence gap: ZOHO_PAYMENTS_FINDINGS.md assumptions
────────────────────────────────────────
Master ID: MF-052
Domain: Integration / inventory
Functionality: Zoho Inventory item/stock read as stock authority
Expected behaviour / AC: No local stock authority (AC-14.x)
Status: IIV
Evidence: M/T: integrations/zoho_inventory.py; test_zoho_inventory.py (25)
Validation: V2: mocked
Dependency / blocker: Zoho OAuth credentials, test organisation
SPEC / decision: SPEC §14, §3.4
Source IDs: REG B-05
Disposition: VALIDATE
Rationale: Mocked only
Evidence gap: Field names unverified
────────────────────────────────────────
Master ID: MF-053
Domain: Integration / Zoho
Functionality: Sales Order create, lookup by EKI reference, timeout recovery, duplicate-outbox safety
Expected behaviour / AC: AC-24.1; AC-25.x
Status: IIV
Evidence: M/T: same file
Validation: V2: mocked
Dependency / blocker: Zoho test organisation, tax ids
SPEC / decision: SPEC §24, §25
Source IDs: REG B-06
Disposition: VALIDATE
Rationale: Mocked only
Evidence gap: -
────────────────────────────────────────
Master ID: MF-054
Domain: Integration / Zoho
Functionality: Zoho tax/GST mapping, invoice trigger and numbering, discount-tax arithmetic, HSN, place of supply
Expected behaviour / AC: AC-13.x
Status: BLK
Evidence: S: INTEGRATION_MATRIX §3 (10 unknowns)
Validation: V1
Dependency / blocker: HU+DI/accountant; Zoho tax ids
SPEC / decision: SPEC §13.1-13.14 (esp. 13.14); §7.9
Source IDs: REG B-07, X-2; C4 CG-005
Disposition: BLOCKED-DEC
Rationale: CONFLICT FLAGGED (X-2): SPEC GST-on-undiscounted-amount rule vs usual tax-on-discounted arithmetic
Evidence gap: Zoho configuration not compared
────────────────────────────────────────
Master ID: MF-055
Domain: Integration / Zoho
Functionality: Customer mapping to Zoho contacts (shared contact vs approved creation)
Expected behaviour / AC: AC-24.1
Status: BLK
Evidence: S: adapter finds by e-mail, never creates
Validation: V1
Dependency / blocker: HU+DI decision (S-5)
SPEC / decision: SPEC §24; §3.12 covers Items only
Source IDs: REG B-08, S-5
Disposition: BLOCKED-DEC
Rationale: Unresolved decision
Evidence gap: -
────────────────────────────────────────
Master ID: MF-056
Domain: Integration / outbox
Functionality: Outbox and worker (AD-07): durable tasks, 3 total attempts, idempotent, exhausted -> exception state
Expected behaviour / AC: AC-25.x
Status: IVV
Evidence: T: test_outbox.py (42), test_retry_paths.py; run_outbox
Validation: V2 (earlier tree)
Dependency / blocker: Production scheduler (MF-092)
SPEC / decision: SPEC §25; AD-07
Source IDs: REG B-09
Disposition: NO ACTION
Rationale: Implemented, local
Evidence gap: Untested with real latency
────────────────────────────────────────
Master ID: MF-057
Domain: Integration / config
Functionality: Fail-closed provider wiring; production refuses stubs, console e-mail, TESTCODE
Expected behaviour / AC: AC-24.1; AC-26.x
Status: IVV
Evidence: T: test_settings.py, test_f06_boundaries.py (106 passed)
Validation: V2
Dependency / blocker: -
SPEC / decision: SPEC §26; ARCH §18
Source IDs: REG B-10, J-09
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: Only fake values used
────────────────────────────────────────
Master ID: MF-058
Domain: Integration / Zoho
Functionality: Amount integrity: Zoho SO total must equal amount paid
Expected behaviour / AC: AC-12.x
Status: IIV
Evidence: M/T
Validation: V2: mocked
Dependency / blocker: MF-053, MF-054
SPEC / decision: SPEC §12.13
Source IDs: REG B-11
Disposition: VALIDATE
Rationale: Surfaces at first sandbox run
Evidence gap: -
────────────────────────────────────────
Master ID: MF-059
Domain: Integration / test traceability
Functionality: TESTCODE across order/payment/outbox/reconciliation/provider
Expected behaviour / AC: Test transactions identifiable
Status: PART
Evidence: T: test_testcodes.py (28, uncommitted); orders.0022 not applied
Validation: V2
Dependency / blocker: Sandbox; cleanup policy
SPEC / decision: Project decision (B1)
Source IDs: REG B-12
Disposition: VALIDATE
Rationale: Provider meta_data propagation unobserved
Evidence gap: No cleanup tool
────────────────────────────────────────
Master ID: MF-060
Domain: Integration / payment
Functionality: Refund execution through the original payment mechanism
Expected behaviour / AC: AC-16.x
Status: PART
Evidence: S: operations.py records refund; "manual refund required" with a real gateway
Validation: V1
Dependency / blocker: HU+DI: automated refund at launch or staff-run manual (S-4)
SPEC / decision: SPEC §16.3, §16.5
Source IDs: REG B-13, S-4; C1 ORD-070
Disposition: BLOCKED-DEC
Rationale: Launch scope decision pending
Evidence gap: -
────────────────────────────────────────
Master ID: MF-061
Domain: Integration / payment
Functionality: Shared OAuth token cache across requests
Expected behaviour / AC: Avoid refresh rate limits
Status: PART
Evidence: S: gateway built per request
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §24
Source IDs: REG B-14
Disposition: FIX
Rationale: Defect-class gap; needs test
Evidence gap: -
────────────────────────────────────────
Master ID: MF-062
Domain: Integration / errors
Functionality: Real-provider error classification (auth, validation, 429, transient, ambiguous)
Expected behaviour / AC: AC-25.x
Status: IVV
Evidence: T: parametrised classification tests
Validation: V2: mocked
Dependency / blocker: -
SPEC / decision: SPEC §25
Source IDs: REG B-15
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: Outbox counts every class as one attempt
────────────────────────────────────────
Master ID: MF-063
Domain: Integration / Zoho Flow
Functionality: Existing "Zoho Flow salesorder add" (Shopify to Zoho) must not conflict with EffyKlean SO writes
Expected behaviour / AC: HU: workflow created intentionally
Status: BLK
Evidence: D: PROVIDER_EVIDENCE
Validation: V1
Dependency / blocker: HU inspection before first sandbox write
SPEC / decision: SPEC §24
Source IDs: REG B-16; C1 INT-011
Disposition: BLOCKED-DEC
Rationale: Must be inspected before change
Evidence gap: -
────────────────────────────────────────
Master ID: MF-064
Domain: Payments / assisted
Functionality: Bank-transfer / UPI assisted payment verification and Zoho SO creation point
Expected behaviour / AC: AC-12.x
Status: BLK
Evidence: D: DC-22
Validation: V1
Dependency / blocker: HU+DI decision DC-22
SPEC / decision: SPEC §12.10, §12.11, §27.1, §27.3
Source IDs: REG G-03; C1 DRF-*
Disposition: BLOCKED-DEC
Rationale: SPEC requires verification by Admin; mechanism undecided
Evidence gap: Do not REJECT: SPEC requires it
────────────────────────────────────────
Master ID: MF-065
Domain: Admin / orders
Functionality: Per-order financial reconciliation view (customer paid, provider, settlement, Zoho)
Expected behaviour / AC: AC-12.12; AC-28.x
Status: UNV
Evidence: S: reconciliation, unresolved-payments routes exist
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §12.12, §28.3
Source IDs: C1 ORD-044; REG B-04
Disposition: VALIDATE
Rationale: Whether the per-order view meets §12.12 not checked
Evidence gap: -
────────────────────────────────────────
Master ID: MF-066
Domain: Integration / reconciliation
Functionality: Unresolved-payment hold and reconciliation
Expected behaviour / AC: AC-12.18
Status: IIV
Evidence: T: test_payment_reconciliation.py
Validation: V2
Dependency / blocker: Scheduler (MF-092)
SPEC / decision: SPEC §12.18
Source IDs: REG B-04
Disposition: VALIDATE
Rationale: No production schedule
Evidence gap: -
────────────────────────────────────────
Master ID: MF-070
Domain: Shipping
Functionality: Shipment created only by Zoho -> Shiprocket (no second writer)
Expected behaviour / AC: AC-18.x
Status: BLK
Evidence: S: real adapter request_fulfilment raises ZohoNotSupportedError; stub still simulates
Validation: V1
Dependency / blocker: HU+DI (DC-18)
SPEC / decision: SPEC §18.3
Source IDs: REG C-01, X-1; C1 ORD-080, ORD-088
Disposition: BLOCKED-DEC
Rationale: CONFLICT FLAGGED (X-1): existing dispatch flow expects a tracking reference
Evidence gap: Reported, not resolved
────────────────────────────────────────
Master ID: MF-071
Domain: Shipping
Functionality: Shipment status/tracking return path into orders
Expected behaviour / AC: AC-18.x; AC-15.x
Status: MISS
Evidence: S: tracking shown only if stored; no inbound reader
Validation: V1
Dependency / blocker: MF-070
SPEC / decision: SPEC §18, §15.7
Source IDs: REG C-02; C2 BR-F08, BR-W05; C3 EC-F08, EC-W04; C4 CG-006
Disposition: BLOCKED-DEC
Rationale: Depends on shipping-handoff decision
Evidence gap: -
────────────────────────────────────────
Master ID: MF-072
Domain: Shipping
Functionality: Customer tracking page by EKI id + contact (no internal states shown)
Expected behaviour / AC: AC-15.x; §3.24
Status: IVV
Evidence: T/B: test_customer_accounts.py; /track/ V4 200
Validation: V2; V4
Dependency / blocker: -
SPEC / decision: SPEC §19, §3.24
Source IDs: REG D-04, D-10; C2 BR-F08, BR-L16; C3 EC-X05
Disposition: NO ACTION
Rationale: Implemented; carrier status absent (MF-071)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-073
Domain: Shipping
Functionality: Shipment failure/recovery (SHIPMENT_FAILED, retry, outbox)
Expected behaviour / AC: AC-18.x
Status: IIV
Evidence: T with stub only
Validation: V2
Dependency / blocker: MF-070
SPEC / decision: SPEC §18, §25
Source IDs: REG C-04
Disposition: VALIDATE
Rationale: Re-prove after MF-070
Evidence gap: -
────────────────────────────────────────
Master ID: MF-074
Domain: Shipping
Functionality: Weight/dimension source and location -> pickup mapping
Expected behaviour / AC: AC-18.x
Status: BLK
Evidence: D: DC-19, DC-23
Validation: V1
Dependency / blocker: HU+DI
SPEC / decision: SPEC §18
Source IDs: REG C-05; C1 SET-015
Disposition: BLOCKED-DEC
Rationale: Decision open
Evidence gap: -
────────────────────────────────────────
Master ID: MF-075
Domain: Customer / accounts
Functionality: Accounts: register, sign in, setup, order history, reorder, details, password
Expected behaviour / AC: AC-19.x
Status: IVV
Evidence: T/B: test_customer_accounts.py; routes account/*
Validation: V2; V4 (sign-in 200, /account/ 303)
Dependency / blocker: D-D1 sign-in default awaiting confirmation
SPEC / decision: SPEC §19; AC-19.1..19.3
Source IDs: REG D-04, F-05; C2 BR-F07, BR-W03, BR-P17, BR-L13; C3 EC-P37, EC-X08, EC-F09, EC-L02
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: Sign-in method is an implementation default
────────────────────────────────────────
Master ID: MF-076
Domain: Customer / orders
Functionality: Cancellation (rules, charge, refund record)
Expected behaviour / AC: AC-16.x
Status: IIV
Evidence: T: test_order_operations.py
Validation: V2
Dependency / blocker: MF-060 (refund)
SPEC / decision: SPEC §16; AC-16.1..16.9
Source IDs: REG D-07; C3 EC-W05, EC-F10
Disposition: VALIDATE
Rationale: Refund is manual
Evidence gap: -

  Ran 2 shell commands

Part 1b (MF-077 to MF-121). Correction to Part 1a: the scheduler dependency on MF-056 and MF-066 is MF-109, not MF-092.

Master ID: MF-077
Domain: Customer / orders
Functionality: Replacement with customer video evidence (CR-008)
Expected behaviour / AC: AC-17.x
Status: IIV
Evidence: T/B local
Validation: V2; VB
Dependency / blocker: Video upload channel, storage, retention (HU+DI)
SPEC / decision: SPEC §17; CR-008
Source IDs: REG D-08; C3 EC-W06; C2 BR-W08
Disposition: VALIDATE
Rationale: Storage/retention undecided
Evidence gap: -
────────────────────────────────────────
Master ID: MF-078
Domain: Customer / invoices
Functionality: GST amounts and invoice number/status visible in Admin; customer invoice access
Expected behaviour / AC: AC-13.8
Status: MISS
Evidence: S: no GST computation/invoice code; Admin order page has an Invoice section (reference only)
Validation: V1
Dependency / blocker: MF-054; S-2 (customer download)
SPEC / decision: SPEC §13.10
Source IDs: REG D-06, S-2; C1 ORD-039; C4 CG-005
Disposition: BLOCKED-DEC
Rationale: Depends on Zoho mapping
Evidence gap: Admin Invoice section content not read
────────────────────────────────────────
Master ID: MF-079
Domain: Customer / notifications
Functionality: Transactional e-mail events N1..N11 (confirmation, shipping, etc.), e-mail only
Expected behaviour / AC: AC-20.x
Status: MISS
Evidence: D: exit gate §3.4 (nothing sent); console backend refused in production
Validation: V1
Dependency / blocker: E-mail provider, sender domain, wording, event matrix (DC-21)
SPEC / decision: SPEC §20; AC-20.1..20.5
Source IDs: REG D-09; C1 SET-021, SET-022, ORD-063, ORD-089; C4 CG-007
Disposition: BLOCKED-DEC
Rationale: A paid order with no confirmation is a launch gap
Evidence gap: -
────────────────────────────────────────
Master ID: MF-080
Domain: Customer / orders
Functionality: Order timeline visible to customer without internal states
Expected behaviour / AC: §3.24
Status: IVV
Evidence: T: track page tests
Validation: V2
Dependency / blocker: -
SPEC / decision: SPEC §3.24, §19.4
Source IDs: REG D-10
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: -
────────────────────────────────────────
Master ID: MF-081
Domain: B2B / distributor
Functionality: Distributor application, review, role provisioning, three-month suspension, pricing proposal/approval
(CR-006)
Expected behaviour / AC: AC-9.x
Status: IVV
Evidence: T: test_distributor_applications.py, test_business_accounts.py, test_distributor_pricing.py
Validation: V2
Dependency / blocker: -
SPEC / decision: SPEC §9; AC-9.1..9.10; CR-006, CR-009
Source IDs: REG G-01; C3 EC-W07, EC-P21; C4 CG-034
Disposition: NO ACTION
Rationale: Implemented; stronger than BRM
Evidence gap: -
────────────────────────────────────────
Master ID: MF-082
Domain: B2B / bulk
Functionality: Bulk enquiry, negotiated quotes, no stacking, savings
Expected behaviour / AC: AC-10.x
Status: IVV
Evidence: T: test_bulk_quotes.py; /bulk-enquiry/ V4 200
Validation: V2; V4
Dependency / blocker: -
SPEC / decision: SPEC §10; AC-10.1..10.12
Source IDs: REG G-02; C2 BR-F11, BR-W04, BR-P14, BR-P15; C3 EC-X06, EC-F11
Disposition: NO ACTION
Rationale: Implemented; BRM has only a lead form
Evidence gap: -
────────────────────────────────────────
Master ID: MF-083
Domain: B2B / GST
Functionality: Distributor GST handling during Zoho outage
Expected behaviour / AC: AC-13.7
Status: BLK
Evidence: D: depends on B-07
Validation: V1
Dependency / blocker: MF-054
SPEC / decision: SPEC §13.13
Source IDs: REG G-04
Disposition: BLOCKED-DEC
Rationale: Depends on tax mapping
Evidence gap: -
────────────────────────────────────────
Master ID: MF-084
Domain: Content / policy
Functionality: Own Privacy, Terms and Refund/Contact-information pages (footer currently links to effyklean.com)
Expected behaviour / AC: Policy content per §23
Status: BLK
Evidence: S/V4: links to effyklean.com/policies/*; /pages/privacy-policy/ 404 locally
Validation: V4; V3
Dependency / blocker: HU supplies approved legal text
SPEC / decision: SPEC §23.2, §23.4, §26.2
Source IDs: C3 EC-P30..P34, EC-L06, EC-W10; C2 BR-P04, BR-P05, BR-P06, BR-P08, BR-L17; C4 CG-008
Disposition: BLOCKED-DEC
Rationale: Legal text must not be invented (§23.4)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-085
Domain: Content / policy
Functionality: Shipping, cancellation, replacement, FAQ, About, Values pages
Expected behaviour / AC: AC-23.x
Status: IIV
Evidence: S/V4: /shipping-and-delivery/, /cancellation/, /replacement/, /faq/, /about-us/, /our-values/ all 200
Validation: V4
Dependency / blocker: Content review
SPEC / decision: SPEC §23; AC-23.1..23.3
Source IDs: C3 EC-P18, EC-P19, EC-P20, EC-X10; C2 BR-P03, BR-P07, BR-P09
Disposition: VALIDATE
Rationale: Content correctness not reviewed
Evidence gap: -
────────────────────────────────────────
Master ID: MF-086
Domain: Content / blog
Functionality: Blog index and posts (3 posts in media/blog_source); Admin blog editor
Expected behaviour / AC: Content per §23
Status: PART
Evidence: V4: /blog/ 404; S: blog route exists; no blog editor route
Validation: V4; V1
Dependency / blocker: Cause of 404
SPEC / decision: SPEC §23
Source IDs: C3 EC-P26..P29; C2 BR-B01..B12, BR-F15, BR-L18; C4 CG-022; C1 CNT-007
Disposition: FIX
Rationale: Route exists but returns 404 in the running instance
Evidence gap: Cause unverified (no published posts?)
────────────────────────────────────────
Master ID: MF-087
Domain: Content / hub
Functionality: Knowledge hub, formulation guides, ad landing pages
Expected behaviour / AC: No requirement
Status: MISS
Evidence: F: BRM 87 articles, 2 landers
Validation: V3
Dependency / blocker: -
SPEC / decision: SPEC silent
Source IDs: C2 BR-P11..P13, BR-W09, BR-L10; C4 CG-026
Disposition: NO ACTION
Rationale: Enhancement, deferred
Evidence gap: -
────────────────────────────────────────
Master ID: MF-088
Domain: Content / media
Functionality: Videos page and media hosting (videos hot-link the old site)
Expected behaviour / AC: Videos available at launch
Status: BLK
Evidence: D: DC-25; V4 /videos/ 200
Validation: V4
Dependency / blocker: Copy media before old site stops serving (HU+DI)
SPEC / decision: SPEC §23
Source IDs: REG E-08; C3 EC-P22, EC-W11; C2 BR-F15
Disposition: BLOCKED-DEC
Rationale: P0 if videos launch
Evidence gap: -
────────────────────────────────────────
Master ID: MF-089
Domain: Content / contact
Functionality: Contact form (fail-closed until privacy wording and retention are recorded)
Expected behaviour / AC: AC-26.x
Status: BLK
Evidence: S: production.py; V4 /contact-us/ 200
Validation: V4; V2
Dependency / blocker: Privacy wording, retention (HU+DI)
SPEC / decision: SPEC §26.2, §4.1
Source IDs: REG H-05; C2 BR-F09, BR-P02, BR-W06, BR-L19; C3 EC-P17, EC-F13, EC-W08, EC-X09, EC-L12
Disposition: BLOCKED-DEC
Rationale: Production refuses until recorded
Evidence gap: No notification e-mail
────────────────────────────────────────
Master ID: MF-090
Domain: Content / subscribe
Functionality: Newsletter subscription with mailbox verification and unsubscribe
Expected behaviour / AC: AC-20.5; §26.2
Status: BLK
Evidence: T: SUBSCRIBE_VERIFIED doc; V4 /subscribe/ 200
Validation: V4; V2
Dependency / blocker: E-mail provider (MF-079)
SPEC / decision: SPEC §20.5, §26.2
Source IDs: REG H-06; C2 BR-F10, BR-W07, BR-L21; C3 EC-X07, EC-F12, EC-W09, EC-L09
Disposition: BLOCKED-DEC
Rationale: No mail provider
Evidence gap: -
────────────────────────────────────────
Master ID: MF-091
Domain: SEO / URL
Functionality: SEO baseline (canonical, description, sitemap, robots, og); canonical host http://www.effyklean.in
Expected behaviour / AC: AC-22.1..22.2
Status: IVV
Evidence: T: test_storefront_seo.py
Validation: V2; V4 (sitemap 9 URLs, robots 200)
Dependency / blocker: Domain live
SPEC / decision: SPEC §22; AC-22.x
Source IDs: REG E-06; C3 EC-F16, EC-P38
Disposition: NO ACTION
Rationale: Implemented; real-domain proof pending
Evidence gap: -
────────────────────────────────────────
Master ID: MF-092
Domain: SEO / URL
Functionality: Redirect and URL-parity plan from effyklean.com paths to effyklean.in routes
Expected behaviour / AC: No requirement text; SEO continuity
Status: MISS
Evidence: F: .com paths /products/<handle>, /collections/, /pages/, /blogs/, /policies/
Validation: V3
Dependency / blocker: Decision on cut-over strategy
SPEC / decision: SPEC §22, §29
Source IDs: C4 CG-009
Disposition: BLOCKED-DEC
Rationale: Cut-over decision not recorded
Evidence gap: -
────────────────────────────────────────
Master ID: MF-093
Domain: Marketing / analytics
Functionality: Analytics and marketing events with consent
Expected behaviour / AC: AC-26.x
Status: MISS
Evidence: F: .com gtag, BRM GTM; .in none
Validation: V3; V1
Dependency / blocker: Cookie-consent wording (HU+DI)
SPEC / decision: SPEC §26.2, §3.14
Source IDs: REG I-04; C2 BR-F17; C3 EC-F15; C4 CG-029
Disposition: BLOCKED-DEC
Rationale: Consent first; no wording decided
Evidence gap: -
────────────────────────────────────────
Master ID: MF-094
Domain: Marketing / contact
Functionality: Floating WhatsApp button (.com app) and language option (Weglot)
Expected behaviour / AC: SPEC §20.3 WhatsApp optional
Status: MISS
Evidence: F: .com markup (72 WhatsApp mentions, 1 Weglot script)
Validation: V3
Dependency / blocker: HU+DI decision
SPEC / decision: SPEC §20.3 (optional)
Source IDs: C3 EC-L10, EC-L11, EC-F18, EC-F19; C2 BR-F19, BR-F20; C4 CG-027, CG-028
Disposition: BLOCKED-DEC
Rationale: Optional channels; no decision to include
Evidence gap: Language usage unverified
────────────────────────────────────────
Master ID: MF-095
Domain: Admin / catalogue
Functionality: Catalogue revision workflow: draft, submit, approve, publish, quarterly review; bulk/export
Expected behaviour / AC: AC-6.x; AC-27.x
Status: IVV
Evidence: T: test_admin_workflow.py, test_product_admin.py
Validation: V2
Dependency / blocker: -
SPEC / decision: SPEC §6, §27.1
Source IDs: REG H-01; C2 BR-PR05; C1 PRD-*
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: -
────────────────────────────────────────
Master ID: MF-096
Domain: Admin / security
Functionality: Staff auth, mandatory MFA, throttling, recovery codes; Admin URL path EKIAdmin2026 flagged for
configuration review
Expected behaviour / AC: AC-26.x; ARCH §18
Status: IVV
Evidence: T: test_admin_auth.py; backoffice/mfa.py
Validation: V2
Dependency / blocker: Production session store, secrets, URL review
SPEC / decision: SPEC §26; ARCH §18
Source IDs: REG H-02; C3 EC-X12; C1 USR-008, USR-009
Disposition: NO ACTION
Rationale: Implemented; production review open
Evidence gap: Admin URL review pending
────────────────────────────────────────
Master ID: MF-097
Domain: Admin / orders
Functionality: Order tools: retry Zoho, retry shipment, cancel, edit, refund record, delivery, return, replacement,
reconciliation queue
Expected behaviour / AC: AC-27.x
Status: IIV
Evidence: T: test_admin_order_actions.py; routes orders/<ref>/*
Validation: V2 (stubs)
Dependency / blocker: Real adapters (MF-053, MF-070)
SPEC / decision: SPEC §27.1; AC-27.1
Source IDs: REG H-03; C1 ORD-024..099
Disposition: VALIDATE
Rationale: Stub-level proof only
Evidence gap: -
────────────────────────────────────────
Master ID: MF-098
Domain: Admin / audit
Functionality: Append-only audit trail with export
Expected behaviour / AC: AC-26.x
Status: IVV
Evidence: T: backoffice/audit.py; route audit/export
Validation: V2; V1
Dependency / blocker: -
SPEC / decision: SPEC §26.3
Source IDs: REG H-04; C1 SYS-001, SYS-002
Disposition: NO ACTION
Rationale: Implemented
Evidence gap: -
────────────────────────────────────────
Master ID: MF-099
Domain: Admin / operations
Functionality: Worker/reconciliation operator runbook and outbox list page
Expected behaviour / AC: AC-25.x
Status: PART
Evidence: D: runbook (4af12e0); S: no outbox list route
Validation: V1
Dependency / blocker: MF-109 supervisor
SPEC / decision: SPEC §25
Source IDs: REG H-07; C1 INT-004; C4 CG-010
Disposition: IMPLEMENT
Rationale: Operational visibility for an existing approved component (AD-07)
Evidence gap: Admin page contents unverified
────────────────────────────────────────
Master ID: MF-100
Domain: Admin / reports
Functionality: Baseline sales/order reports (7/30/90 days) and customer export
Expected behaviour / AC: §28.4: small generic baseline
Status: IVV
Evidence: T: test_admin_reports.py; customer_export
Validation: V2
Dependency / blocker: Net vs gross/GST definitions wait on MF-054
SPEC / decision: SPEC §28.4; AC-28.1
Source IDs: REG I-01, I-02; C1 ANA-*
Disposition: NO ACTION
Rationale: Implemented as the approved baseline; enhancements deferred by §28.4
Evidence gap: -
────────────────────────────────────────
Master ID: MF-101
Domain: Admin / inventory
Functionality: Inventory / low-stock view
Expected behaviour / AC: SPEC P0-6 low stock
Status: MISS
Evidence: S: no low-stock code
Validation: V1
Dependency / blocker: Real Zoho stock read (MF-052)
SPEC / decision: SPEC §14
Source IDs: REG I-03; C1 PRD-008
Disposition: BLOCKED-DEC
Rationale: Needs real stock source
Evidence gap: -
────────────────────────────────────────
Master ID: MF-102
Domain: Admin / orders
Functionality: Order export (CSV) and scope/format choices
Expected behaviour / AC: §26.2 privacy; recommended
Status: MISS
Evidence: S: no orders/export route (confirmed)
Validation: V1
Dependency / blocker: PII handling and audit of every export
SPEC / decision: SPEC §26.2
Source IDs: C1 ORD-021, ORD-106, ORD-132, ORD-133; C4 CG-012
Disposition: IMPLEMENT
Rationale: Previously ACCEPT-recommended in Part 1 M2; not yet approved by HU+DI
Evidence gap: Recommendation only
────────────────────────────────────────
Master ID: MF-103
Domain: Admin / orders
Functionality: Order comments/timeline completeness; list filters for product, amount, tags
Expected behaviour / AC: Recommended (Part 1 B4, B5)
Status: PART
Evidence: S: order detail has a Timeline section; sort/search/payment/shipment/date filters exist
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §15.7, §27.1
Source IDs: C1 ORD-013, ORD-017..020, ORD-033, ORD-034; C4 CG-013, CG-014
Disposition: IMPLEMENT
Rationale: Part-built; note: Comparison 4 CG-014 wrongly says sorting is missing (ORD-007 is implemented)
Evidence gap: See reconciliation correction
────────────────────────────────────────
Master ID: MF-104
Domain: Admin / staff
Functionality: Staff invite/create and MFA reset
Expected behaviour / AC: Roles fixed; creation mechanism undecided (D-F2)
Status: BLK
Evidence: S: staff routes toggle/role/signins only
Validation: V1
Dependency / blocker: HU+DI decision D-F2
SPEC / decision: SPEC §5.4, §27.4
Source IDs: C1 USR-003, USR-004; C4 CG-015
Disposition: BLOCKED-DEC
Rationale: Decision open
Evidence gap: -
────────────────────────────────────────
Master ID: MF-105
Domain: Admin / customers
Functionality: Customer sign-in help (password reset by staff) and customer data-request export
Expected behaviour / AC: Privacy §26.2
Status: BLK
Evidence: D: D-D1, D-D2
Validation: V1
Dependency / blocker: HU+DI
SPEC / decision: SPEC §26.2
Source IDs: C1 CUS-018, CUS-028; C4 CG-016
Disposition: BLOCKED-DEC
Rationale: Decision open
Evidence gap: -
────────────────────────────────────────
Master ID: MF-106
Domain: Admin / assisted orders
Functionality: Admin-assisted / manual / draft orders using the same commercial rules
Expected behaviour / AC: AC-27.1
Status: MISS
Evidence: S: no draft routes (confirmed)
Validation: V1
Dependency / blocker: DC-22 decision
SPEC / decision: SPEC §27.3 (required), §12.11
Source IDs: C1 DRF-001..DRF-021; C4 CG-018
Disposition: BLOCKED-DEC
Rationale: SPEC §27.3 requires assisted orders; mechanism blocked on DC-22 (REJECT would conflict with SPEC)
Evidence gap: -
────────────────────────────────────────
Master ID: MF-107
Domain: Infrastructure / release
Functionality: Hosting, HTTPS, domain, WSGI/ASGI server and deployment recipe (Phase 2)
Expected behaviour / AC: Public HTTPS service on http://www.effyklean.in
Status: MISS
Evidence: S: no Dockerfile or server config; only compose.yaml (database)
Validation: V1; V3: effyklean.in resolves in DNS but TLS fails (2026-10-12)
Dependency / blocker: Phase 2 needs its own authorisation (HU+DI)
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-01; C4 CG-001
Disposition: BLOCKED-DEC
Rationale: Phase 2 hosting is not authorised (CLAUDE.md)
Evidence gap: Hosting design undecided
────────────────────────────────────────
Master ID: MF-108
Domain: Infrastructure / release
Functionality: Transport security: HSTS, HTTPS redirect, secure cookies, storefront security headers
Expected behaviour / AC: AC-26.x; ARCH §18
Status: MISS
Evidence: S: check --deploy with dummy values gives 4 warnings (W001 SecurityMiddleware absent)
Validation: V1
Dependency / blocker: Header and CSRF posture decision
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-02
Disposition: IMPLEMENT
Rationale: Security baseline required by SPEC §26.1 and ARCH §18; design not yet decided
Evidence gap: Not tested behind a real proxy
────────────────────────────────────────
Master ID: MF-109
Domain: Infrastructure / release
Functionality: Process supervision for run_outbox, retry_integrations, reconciliation, dispatch_orders
Expected behaviour / AC: AC-25.x
Status: MISS
Evidence: S: management commands exist; no scheduler, unit or cron definition
Validation: V1
Dependency / blocker: Hosting (MF-107)
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-03
Disposition: IMPLEMENT
Rationale: AD-07 worker is useless in production without a scheduler
Evidence gap: -
────────────────────────────────────────
Master ID: MF-110
Domain: Infrastructure / release
Functionality: Secrets management (DC-05); .env only locally
Expected behaviour / AC: AC-26.x; SPEC §26.4
Status: BLK
Evidence: D: decision DC-05 open
Validation: V1
Dependency / blocker: HU+DI decision DC-05
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-04
Disposition: BLOCKED-DEC
Rationale: Decision open
Evidence gap: -
────────────────────────────────────────
Master ID: MF-111
Domain: Infrastructure / release
Functionality: Observability: logging, error tracking, alerting on exhausted outbox and unresolved payments
Expected behaviour / AC: AC-25.x
Status: PART
Evidence: S: LOGGING in base.py, correlation ids, Admin queues; no external monitoring
Validation: V1
Dependency / blocker: External monitoring choice
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-05
Disposition: IMPLEMENT
Rationale: Alerting is needed to operate AD-07 safely
Evidence gap: Monitoring tool not chosen
────────────────────────────────────────
Master ID: MF-112
Domain: Infrastructure / release
Functionality: Backups and restore drill
Expected behaviour / AC: SPEC §25 reliability
Status: MISS
Evidence: S: no backup docs or scripts in repo
Validation: V1
Dependency / blocker: Hosting (MF-107)
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-06
Disposition: IMPLEMENT
Rationale: Required before production data exists
Evidence gap: -
────────────────────────────────────────
Master ID: MF-113
Domain: Infrastructure / release
Functionality: Migrations: apply and rollback plan (dev DB lacks recent migrations; orders.0022 new)
Expected behaviour / AC: AC-25.x
Status: PART
Evidence: S: makemigrations --check clean earlier; migrations applied only to the demo DB
Validation: V1
Dependency / blocker: Authorisation to migrate non-test databases
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-07
Disposition: BLOCKED-DEC
Rationale: Authorisation required to alter non-test databases
Evidence gap: Rollback notes missing
────────────────────────────────────────
Master ID: MF-114
Domain: Infrastructure / release
Functionality: Performance and load baseline (page, checkout and Zoho latency budget)
Expected behaviour / AC: SPEC §30.2, §30.4
Status: MISS
Evidence: S: no load test; suite takes about 22 minutes
Validation: V1
Dependency / blocker: Hosting (MF-107)
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-08
Disposition: IMPLEMENT
Rationale: SPEC §30.4 leaves targets to build time
Evidence gap: Targets not defined
────────────────────────────────────────
Master ID: MF-115
Domain: Infrastructure / release
Functionality: Release acceptance gate (exit gate rows 3, 5, 11 blocked)
Expected behaviour / AC: All P0 register rows closed with sandbox/production proof
Status: BLK
Evidence: D: PHASE1_EXIT_GATE_2026-10-11.md
Validation: V1
Dependency / blocker: MF-043, MF-052, MF-053, MF-054, MF-107..MF-113
SPEC / decision: SPEC §25, §26, §30; ARCH §18
Source IDs: REG J-10
Disposition: BLOCKED-DEC
Rationale: Gate not met
Evidence gap: -
────────────────────────────────────────
Master ID: MF-116
Domain: Admin / Shopify-only
Functionality: Shopify Online Store themes, theme editor, Liquid templates, page templates, app store, apps, billing
plan, POS
Expected behaviour / AC: AC-1.2: no runtime dependency on Shopify
Status: EXC
Evidence: D: inventory CNT-014, CNT-041, PRD-046, CNT-004, INT-007 (permanent exclusion)
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §29.1; AC-1.2
Source IDs: C4 CG-036; C3 EC-L07; C1 CNT-004, CNT-014, CNT-041, PRD-046, INT-007..INT-009
Disposition: REJECT/OOS
Rationale: Permanent exclusion recorded in the inventory (Part 1 G6); SPEC has no theme clause (grep: none)
Evidence gap: Exclusion basis is a carried HU+DI decision, not a SPEC sentence
────────────────────────────────────────
Master ID: MF-117
Domain: Storefront / API
Functionality: Storefront JSON API under /api/v1/ (modules.storefront.urls)
Expected behaviour / AC: Not described in SPEC
Status: UNV
Evidence: S: config/urls.py include("modules.storefront.urls")
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC silent; ARCH API framework NOT LOCKED
Source IDs: C3 EC-X11
Disposition: VALIDATE
Rationale: Purpose and exposure not assessed in the comparisons
Evidence gap: Endpoints not enumerated
────────────────────────────────────────
Master ID: MF-118
Domain: Storefront / navigation
Functionality: Primary navigation and footer link set (Home, Products with format filters, About, Values, Contact, FAQ,

Videos, Bulk, Distributor, Track, Account, Cart, Subscribe)
Expected behaviour / AC: Navigation per SPEC §23.2 content areas
Status: IIV
Evidence: V4: home HTML link set; T: test_storefront_shell.py (modified)
Validation: V4; V2
Dependency / blocker: MF-002 (home-page link rearrangement uncommitted)
SPEC / decision: SPEC §23.2
Source IDs: C3 EC-L01, EC-L05; C2 BR-L12, BR-L20
Disposition: VALIDATE
Rationale: HU-approved rearrangement not yet committed; no Blogs menu on .in
Evidence gap: Rendered navigation unseen
────────────────────────────────────────
Master ID: MF-119
Domain: Storefront / navigation
Functionality: Social links (Facebook, Instagram, YouTube) and support contact details
Expected behaviour / AC: SPEC §4.1 canonical contact details
Status: IVV
Evidence: V4: footer links present (Instagram, Facebook, YouTube, mailto Support@EffyKlean.com, tel +919422618051)
Validation: V4
Dependency / blocker: -
SPEC / decision: SPEC §4.1, §23.3
Source IDs: C3 EC-L05, EC-L12; C2 BR-F18, BR-L20
Disposition: NO ACTION
Rationale: Present on the local home page
Evidence gap: Canonical details not re-checked against §4.1
────────────────────────────────────────
Master ID: MF-120
Domain: Storefront / payment
Functionality: No payment, no dispatch: order created only after verified payment; outbox refuses shipment without a
SUCCEEDED payment
Expected behaviour / AC: AC-12.17; AC-15.x
Status: IVV
Evidence: T/B: exit gate row 4, test_e2e_prototype.py, test_outbox.py
Validation: V2; VB historical
Dependency / blocker: Repeat under provider sandbox (MF-043)
SPEC / decision: SPEC §12.17, §15
Source IDs: REG B-03
Disposition: NO ACTION
Rationale: Implemented; regression guard
Evidence gap: Stub-level only
────────────────────────────────────────
Master ID: MF-121
Domain: Storefront / content
Functionality: GST discoverability and a single source for customer-facing rules (storefront/rules.py)
Expected behaviour / AC: RM-06, RM-08; AC-13.x
Status: IIV
Evidence: S: storefront/rules.py, policy pages
Validation: V1
Dependency / blocker: -
SPEC / decision: SPEC §13.12, §23.5
Source IDs: REG E-05
Disposition: VALIDATE
Rationale: No test proves every page cites rules.py
Evidence gap: -

§1 covers MF-001 to MF-121 (103 rows). I labelled MF-102 "Order export" in this paste, which matches its sources
(ORD-021, ORD-106, ORD-132, ORD-133).

Next is §2, the Orders domain.

  Ran 6 shell commands

Inventory's done — 597 master rows. I'll start walking through the Shopify Admin sections one at a time, beginning with
Orders, using shorthand codes defined in a legend to keep things compact. · summary

  Ran 2 shell commands

§2 Shopify Admin capabilities, Orders (MA-ORD-001 to MA-ORD-145, 119 rows)

Codes used in §2 to §6 (to avoid repeating the same text 490 times)
- Source IDs: The original inventory ID is the suffix of the Master ID, so it is not repeated. SA-Axx is a Comparison 1
  area row. CG-xxx is a Comparison 4 gap. MF-xxx is a §1 row that covers the same function. C1 SA-D means Comparison 1
  re-verified the row.
- Evidence: O: is the Shopify observation tier (OBS 2026-10-05; OBS-L 2026-10-10; DOC = not seen on this store; UNK =
  unreachable; API; — = EffyKlean-originated). T marks a row with named tests. S: is static evidence from 2026-10-12.
- Rationale codes:
  - R1: Implemented but not individually validated on the current tree.
  - R2: Prior inventory recommendation ACCEPT (a recommendation, not an approval).
  - R3: Deferred enhancement; no SPEC requirement identified in the family clause.
  - R4: Implemented and accepted by HU+DI (Orders batch 1, 2026-10-10).
  - R5: Local simulation; needs provider proof.
- Evidence-gap codes:
  - G1: No row-level test trace (register A-03); full suite not re-run (A-04).
  - G2: Checked against the family SPEC clause only.
  - G3: Recommendation only.
  - G4: Earlier tree; suite not re-run.
  - G5: Stale in Comparison 1 (see reconciliation).
  - G6: Inventory row and decision log disagree.
  - G7: DOC tier: a standard Shopify capability, not seen on this store.
  - G8: Recommendation only; no SPEC clause or decision cited.
  - G9: EffyKlean-originated row (no Shopify counterpart).
  - G10: Simulation labelled; no provider contact.
  - G11: Contents unreachable.
- Dependency column: DC-…, D-… and CR-… are decision IDs from the benchmark matrix and mapping documents. A bare
  ORD-nnn refers to another row.
- Expected column: The prefix says what kind of expectation it is: "Existing" behaviour, "Works as inventoried",
  "Recommended, not approved", "Subject to decision", "Not required" (an enhancement with no requirement), or "None
  (excluded)".
- Shopify-side evidence for every row: carried from your walks; not re-observed in this task.

Master ID: MA-ORD-001
Domain: Orders
Functionality: List of orders with pagination
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-002
Domain: Orders
Functionality: Status tabs (All, open, cancelled, etc.)
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: DC-14
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-003
Domain: Orders
Functionality: Free-text search (EKI ID, name, email, phone, GST, reference)
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-004
Domain: Orders
Functionality: Filter by payment status
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-005
Domain: Orders
Functionality: Filter by shipment status
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-006
Domain: Orders
Functionality: Filter by date range
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G4
────────────────────────────────────────
Master ID: MA-ORD-007
Domain: Orders
Functionality: Sort by any column (date, total, customer)
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; CG-014
Disposition: NO ACTION
Rationale: R4
Evidence gap: G5
────────────────────────────────────────
Master ID: MA-ORD-008
Domain: Orders
Functionality: Column: items count
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G5
────────────────────────────────────────
Master ID: MA-ORD-009
Domain: Orders
Functionality: Column: "Fulfil by" date (dispatch due)
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; MF-049
Disposition: NO ACTION
Rationale: R4
Evidence gap: G5
────────────────────────────────────────
Master ID: MA-ORD-010
Domain: Orders
Functionality: Column: sales channel
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: HU+DI decision DEFER 2026-10-10 (inventory recommendation had said REJECT: conflict flagged, decision
prevails)
Evidence gap: G6
────────────────────────────────────────
Master ID: MA-ORD-011
Domain: Orders
Functionality: Column: delivery method
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: HU+DI decision DEFER 2026-10-10 (inventory recommendation had said REJECT: conflict flagged, decision
prevails)
Evidence gap: G6
────────────────────────────────────────
Master ID: MA-ORD-012
Domain: Orders
Functionality: Column: delivery status (carrier)
Expected behaviour / AC: Existing; AC-15.x; AC-27.1
Status: IVV
Evidence: O:OBS; T
Validation: V2H
Dependency / blocker: DC-18
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R4
Evidence gap: G5
────────────────────────────────────────
Master ID: MA-ORD-013
Domain: Orders
Functionality: Column and filter: tags
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: ORD-035
SPEC / decision: §15, §27.1
Source IDs: SA-A02; CG-014; MF-103
Disposition: NO ACTION
Rationale: R3: with ORD-035
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-014
Domain: Orders
Functionality: Column: flags (risk, payment issues, edited, cancel requested)
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: IMPLEMENT
Rationale: R2: show reconciliation, edited, cancelled flags that already exist as data
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-015
Domain: Orders
Functionality: Saved views / custom list tabs
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R3: little value at current volume
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-016
Domain: Orders
Functionality: Choose visible columns
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R3: not needed at current volume
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-017
Domain: Orders
Functionality: Filter by customer / customer type (B2C, Distributor, Bulk)
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: PART
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; CG-014; MF-103
Disposition: IMPLEMENT
Rationale: R2: after Distributor/Bulk orders exist
Evidence gap: G3; G7
────────────────────────────────────────
Master ID: MA-ORD-018
Domain: Orders
Functionality: Filter by product / SKU
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; CG-014; MF-103
Disposition: IMPLEMENT
Rationale: R2: finding every order for one product is a routine operations need
Evidence gap: G3; G7
────────────────────────────────────────
Master ID: MA-ORD-019
Domain: Orders
Functionality: Filter by amount range
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; CG-014; MF-103
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2; G7
────────────────────────────────────────
Master ID: MA-ORD-020
Domain: Orders
Functionality: Filter by tags, channel, risk level, delivery method, return status, location
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02; MF-103
Disposition: NO ACTION
Rationale: R3: revisit after the underlying data exists
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-021
Domain: Orders
Functionality: Export orders (CSV)
Expected behaviour / AC: Recommended, not approved; AC-26.x
Status: MISS
Evidence: O:OBS; S: no orders/export route
Validation: V1
Dependency / blocker: -
SPEC / decision: §26.2, §27
Source IDs: SA-A02; CG-012; MF-102; C1 SA-D
Disposition: IMPLEMENT
Rationale: R2: Part 1 M2 recommendation stands
Evidence gap: G3; PII/audit rules apply
────────────────────────────────────────
Master ID: MA-ORD-022
Domain: Orders
Functionality: Print selected orders (from list)
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-038
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R3: with ORD-038
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-023
Domain: Orders
Functionality: Order count / stats strip (orders, items ordered, returns, fulfilled)
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A02
Disposition: NO ACTION
Rationale: R3: Reports covers the need
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-030
Domain: Orders
Functionality: View customer, contact, addresses
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-031
Domain: Orders
Functionality: View line items (title, SKU, price, quantity, line total)
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-032
Domain: Orders
Functionality: View payment summary (subtotal, discount, GST, total, paid)
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-033
Domain: Orders
Functionality: View timeline of events
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; CG-013; MF-097; MF-103
Disposition: IMPLEMENT
Rationale: R2: Part 1 B4
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-034
Domain: Orders
Functionality: Staff comments on the order timeline (add, with attribution)
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS; S: no order-comment route
Validation: V1
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; CG-013; MF-097; MF-103; C1 SA-D
Disposition: IMPLEMENT
Rationale: R2: Part 1 B5
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-035
Domain: Orders
Functionality: Order tags (add, remove)
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3: tag storage
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-036
Domain: Orders
Functionality: Archive / unarchive order
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS; S: no archive route
Validation: V1
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097; C1 SA-D
Disposition: NO ACTION
Rationale: R3: lists are filterable by state; no case for hiding orders yet
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-037
Domain: Orders
Functionality: Fraud / risk level display and analysis
Expected behaviour / AC: Subject to decision; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: live order page shows Low/Medium/High risk with a chargeback message; Razorpay risk fields not
checked
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-038
Domain: Orders
Functionality: Print order / packing slip
Expected behaviour / AC: Not required; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §26.2, §27
Source IDs: SA-A03; CG-005; MF-097
Disposition: NO ACTION
Rationale: R3: dispatch is Zoho/Shiprocket-driven; revisit when DC-17/18 land
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-039
Domain: Orders
Functionality: Print invoice / GST tax invoice
Expected behaviour / AC: Subject to decision; AC-13.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A03; CG-005; MF-078; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: invoice details visible on the order; the printable GST invoice comes from Zoho (SPEC invoice
rules)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-040
Domain: Orders
Functionality: Source / attribution (first session, referral)
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3: with H2
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-041
Domain: Orders
Functionality: Customer order count shown on the order
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: IMPLEMENT
Rationale: R2: small, derived data
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-042
Domain: Orders
Functionality: Payment reference (confirmation #, gateway, checkout reference)
Expected behaviour / AC: Works as inventoried; AC-12.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §12
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-043
Domain: Orders
Functionality: Order references (EKI ID, checkout ref, Zoho ref, Shiprocket ref)
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-044
Domain: Orders
Functionality: Integration activity panel (Zoho, Shiprocket, Razorpay)
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0S
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-065; MF-097
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10
────────────────────────────────────────
Master ID: MA-ORD-045
Domain: Orders
Functionality: Link to customer record
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-046
Domain: Orders
Functionality: Next / previous order navigation
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-047
Domain: Orders
Functionality: Order notes from the customer (checkout notes)
Expected behaviour / AC: Subject to decision; AC-15.x; AC-27.1
Status: UNV
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: not yet checked whether checkout collects a note
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-ORD-048
Domain: Orders
Functionality: Additional order details / custom attributes (company name, GST number from cart)
Expected behaviour / AC: Works as inventoried; AC-13.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-049
Domain: Orders
Functionality: Residential-address flag on the delivery address
Expected behaviour / AC: Recommended, not approved; AC-18.x
Status: MISS
Evidence: O:—
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: IMPLEMENT
Rationale: R2: Part 1 B3
Evidence gap: G3; G9
────────────────────────────────────────
Master ID: MA-ORD-060
Domain: Orders
Functionality: Cancel order (Admin)
Expected behaviour / AC: Works as inventoried; AC-16.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §16
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-061
Domain: Orders
Functionality: Cancel with reason
Expected behaviour / AC: Works as inventoried; AC-16.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §16
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-062
Domain: Orders
Functionality: Cancel and restock inventory toggle
Expected behaviour / AC: None (excluded); AC-16.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §16
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (cited in inventory note); Zoho owns stock
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-063
Domain: Orders
Functionality: Cancel and notify customer toggle
Expected behaviour / AC: Subject to decision; AC-16.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §16
Source IDs: SA-A03; MF-079; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: transactional e-mail, DC-21
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-064
Domain: Orders
Functionality: Customer-initiated cancellation
Expected behaviour / AC: Subject to decision; AC-16.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: D-C2
SPEC / decision: §16
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: decision D-C2 on guest authentication
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-065
Domain: Orders
Functionality: Edit delivery name, address, phone before handover
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-066
Domain: Orders
Functionality: Edit customer e-mail, GST number, GST name
Expected behaviour / AC: Subject to decision; AC-13.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: D-C1, DC-08
SPEC / decision: §13
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: broader than DC-08
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-067
Domain: Orders
Functionality: Edit line items (add, remove, change quantity)
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: FEATURE_MAPPING parent row B8 (carried HU+DI review)
Evidence gap: CONFLICT FLAGGED: route orders/<ref>/edit (order corrections) exists; scope vs this REJECT unverified
────────────────────────────────────────
Master ID: MA-ORD-068
Domain: Orders
Functionality: Edit prices or apply a discount to a placed order
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory says "same reason" as ORD-067
Evidence gap: CONFLICT FLAGGED: route orders/<ref>/edit exists; scope vs this REJECT unverified
────────────────────────────────────────
Master ID: MA-ORD-069
Domain: Orders
Functionality: Refund (money back)
Expected behaviour / AC: None (excluded); AC-16.x; AC-12.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §16.3, §12
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.5 and §16.10 (cited in inventory note); frozen rule
Evidence gap: Cancellation refunds under SPEC §16 are separate (see MA-ORD-070)
────────────────────────────────────────
Master ID: MA-ORD-070
Domain: Orders
Functionality: Refund execution after an approved cancellation
Expected behaviour / AC: Subject to decision; AC-16.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-15
SPEC / decision: §16
Source IDs: SA-A03; MF-060; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: cancellation refund (80%) needs a real refund, DC-15; labelled simulation
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-071
Domain: Orders
Functionality: Return items / create return
Expected behaviour / AC: None (excluded); AC-17.x; AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §17, §14.10
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.5 and §16.10 (cited in inventory note); frozen rule
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-072
Domain: Orders
Functionality: Replacement (damaged / wrong item), with evidence
Expected behaviour / AC: Works as inventoried; AC-17.x; AC-14.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §17, §14.10
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-073
Domain: Orders
Functionality: Exchange
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory says covered by replacement
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-074
Domain: Orders
Functionality: Store credit issue
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.2 (no loyalty or credit)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-075
Domain: Orders
Functionality: Return label / return shipping
Expected behaviour / AC: None (excluded); AC-17.x; AC-14.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: ORD-071
SPEC / decision: §17, §14.10
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.5; with ORD-071
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-ORD-076
Domain: Orders
Functionality: Inspect returned package before restock
Expected behaviour / AC: Subject to decision; AC-17.x; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §17, §14.10
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: Zoho inventory, DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-077
Domain: Orders
Functionality: Mark as paid (manual payment)
Expected behaviour / AC: Subject to decision; AC-12.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §12
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: applies to Distributor/Bulk offline payment, DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-078
Domain: Orders
Functionality: Capture authorized payment
Expected behaviour / AC: Subject to decision; AC-12.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §12
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: payment capture mode (auto vs manual) is not recorded; confirm
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-ORD-079
Domain: Orders
Functionality: Request payment / send payment link
Expected behaviour / AC: Not required; AC-12.x
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: ORD-110
SPEC / decision: §12
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3: with ORD-110
Evidence gap: G2; G7
────────────────────────────────────────
Master ID: MA-ORD-080
Domain: Orders
Functionality: Fulfil items (create fulfilment)
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-070; MF-097
Disposition: REJECT/OOS
Rationale: Basis: FEATURE_MAPPING parent row B18 (carried HU+DI review); SPEC §18.3 (Zoho then Shiprocket)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-081
Domain: Orders
Functionality: Add tracking number manually
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: FEATURE_MAPPING parent row B18 (carried HU+DI review)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-082
Domain: Orders
Functionality: Retry failed Zoho submission / Shiprocket shipment request
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0S
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10
────────────────────────────────────────
Master ID: MA-ORD-083
Domain: Orders
Functionality: Resolve a fulfilment exception
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0S
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10
────────────────────────────────────────
Master ID: MA-ORD-084
Domain: Orders
Functionality: Mark delivered (record delivery)
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0S
Dependency / blocker: DC-18
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10
────────────────────────────────────────
Master ID: MA-ORD-085
Domain: Orders
Functionality: Hold / release fulfilment hold
Expected behaviour / AC: Not required; AC-18.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3: no case recorded; Admin can already hold via cancel/edit paths
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-086
Domain: Orders
Functionality: Move fulfilment to another location
Expected behaviour / AC: None (excluded); AC-18.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: HU decision, locations settled (PROJECT_LOG); Zoho chooses
Evidence gap: Inventory recommendation only
────────────────────────────────────────
Master ID: MA-ORD-087
Domain: Orders
Functionality: Split fulfilment across locations
Expected behaviour / AC: Subject to decision; AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: confirm whether multi-package/multi-location shipments are in scope
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-ORD-088
Domain: Orders
Functionality: Create shipping label
Expected behaviour / AC: Not required; AC-18.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-18
SPEC / decision: §18
Source IDs: SA-A03; MF-070; MF-097
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: with DC-18
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-089
Domain: Orders
Functionality: Resend order confirmation / invoice / shipping e-mail
Expected behaviour / AC: Subject to decision; AC-18.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §18
Source IDs: SA-A03; CG-007; MF-079; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-21
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-090
Domain: Orders
Functionality: Send invoice to customer (draft order invoice)
Expected behaviour / AC: Subject to decision; AC-13.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A03; CG-018; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: with drafts
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-091
Domain: Orders
Functionality: Duplicate order
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; CG-018; MF-097
Disposition: NO ACTION
Rationale: R3: with drafts
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-092
Domain: Orders
Functionality: Merge / split orders
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: financial record integrity
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-ORD-093
Domain: Orders
Functionality: Unarchive order
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-036
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: NO ACTION
Rationale: R3: with ORD-036
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-094
Domain: Orders
Functionality: Mark order as "needs attention" / resolve reconciliation item
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: SA-A03; MF-097
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-095
Domain: Orders
Functionality: Cancel a Distributor/Bulk order as an Admin case
Expected behaviour / AC: Subject to decision; AC-16.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §16
Source IDs: SA-A03; MF-097
Disposition: BLOCKED-DEC
Rationale: Blocked: D/B orders do not yet exist
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-100
Domain: Orders
Functionality: Bulk select orders on the list
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: CG-012
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-101
Domain: Orders
Functionality: Bulk tag / untag
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: ORD-035
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: needs ORD-035
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-102
Domain: Orders
Functionality: Bulk archive
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-103
Domain: Orders
Functionality: Bulk fulfil / create labels
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: automation owns fulfilment
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-ORD-104
Domain: Orders
Functionality: Bulk print packing slips / invoices
Expected behaviour / AC: Not required; AC-13.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: CG-005
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-105
Domain: Orders
Functionality: Bulk cancel
Expected behaviour / AC: None (excluded); AC-16.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §16
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: unsafe at volume, single action keeps the audit clean
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-106
Domain: Orders
Functionality: Bulk export selected
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-021
SPEC / decision: §15, §27.1
Source IDs: CG-012; MF-102
Disposition: IMPLEMENT
Rationale: R2: with ORD-021
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-107
Domain: Orders
Functionality: Order ID prefix and format setting
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-108
Domain: Orders
Functionality: Auto-archive when paid and fulfilled
Expected behaviour / AC: Not required; AC-18.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: ORD-036
SPEC / decision: §18
Source IDs: -
Disposition: NO ACTION
Rationale: R3: with ORD-036
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-109
Domain: Orders
Functionality: Order status page / customer order tracking
Expected behaviour / AC: Works as inventoried; AC-18.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ORD-110
Domain: Orders
Functionality: Abandoned checkouts list
Expected behaviour / AC: Subject to decision; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Blocked: needs checkout capture of identity before payment; SPEC creates an Order only after payment
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-111
Domain: Orders
Functionality: Abandoned checkout recovery e-mail
Expected behaviour / AC: Subject to decision; AC-20.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21, ORD-110
SPEC / decision: §20
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-21 and ORD-110
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-112
Domain: Orders
Functionality: Payment reminder
Expected behaviour / AC: Subject to decision; AC-12.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §12
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Blocked: no reason recorded in the inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-113
Domain: Orders
Functionality: Order-edit request from customer ("change request")
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: Customer Care handles it
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-114
Domain: Orders
Functionality: Disputes / chargebacks
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-16
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: DC-16
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-115
Domain: Orders
Functionality: Delivery estimate (manual dates)
Expected behaviour / AC: Not required; AC-18.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-116
Domain: Orders
Functionality: Order routing rules to locations
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: HU decision, locations settled (PROJECT_LOG); Zoho chooses
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-120
Domain: Orders
Functionality: Order list column "Destination" (ship-to)
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: IMPLEMENT
Rationale: R2: helps GST reporting and dispatch checks
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-121
Domain: Orders
Functionality: Order list column "Return status"
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.5; frozen rule
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-122
Domain: Orders
Functionality: Order list column "PO number"
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: with DRF-009
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-123
Domain: Orders
Functionality: Order list column "Label status"
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: IIV
Evidence: O:OBS-L
Validation: V0S
Dependency / blocker: DC-18
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10
────────────────────────────────────────
Master ID: MA-ORD-124
Domain: Orders
Functionality: Order detail: "View map" of the delivery address
Expected behaviour / AC: Not required; AC-18.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-125
Domain: Orders
Functionality: Order detail: source session ("1st session from Google, 3 sessions"), "View conversion details"
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: with ANA-012
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-126
Domain: Orders
Functionality: Order detail: "This is their 1st order" customer-history line
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-041
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: IMPLEMENT
Rationale: R2: derived data (see ORD-041)
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-130
Domain: Orders
Functionality: Order list "All locations" filter
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: no use while one dispatch source is configured
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-131
Domain: Orders
Functionality: Order list stats strip: orders, items ordered, sales reversals, orders fulfilled, delivered …
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-18
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: Reports covers part; fulfilment-time is useful once real Shiprocket data exists
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-132
Domain: Orders
Functionality: Export orders: scope choices (current page, all orders, selected, matching search, by date)
Expected behaviour / AC: Recommended, not approved; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-021
SPEC / decision: §15, §27.1
Source IDs: CG-012; MF-102
Disposition: IMPLEMENT
Rationale: R2: with ORD-021; keep scope choices
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-133
Domain: Orders
Functionality: Export format choice (CSV for spreadsheets, plain CSV)
Expected behaviour / AC: Recommended, not approved; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-021
SPEC / decision: §26.2, §27
Source IDs: CG-012; MF-102
Disposition: IMPLEMENT
Rationale: R2: with ORD-021
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ORD-134
Domain: Orders
Functionality: Export transaction histories (payment transactions)
Expected behaviour / AC: Not required; AC-12.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-15
SPEC / decision: §12
Source IDs: -
Disposition: NO ACTION
Rationale: R3: until DC-15
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-135
Domain: Orders
Functionality: Bulk "Print packing slips" for selected orders
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-038
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: with ORD-038
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-136
Domain: Orders
Functionality: Bulk "Mark as": Unfulfilled, In progress, Fulfilled, On hold, Delivered
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: state is system-derived
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-137
Domain: Orders
Functionality: "Mark as delivered" on a single fulfilment
Expected behaviour / AC: Subject to decision; AC-18.x
Status: IIV
Evidence: O:OBS-L
Validation: V0S
Dependency / blocker: DC-18
SPEC / decision: §18
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Blocked: real delivery status is Shiprocket's (DC-18)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-138
Domain: Orders
Functionality: Bulk "Capture payments"
Expected behaviour / AC: None (excluded); AC-12.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-078
SPEC / decision: §12
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: capture is a gateway-flow matter, not a bulk Admin action
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-139
Domain: Orders
Functionality: Bulk "Request fulfillment" and "Cancel fulfillment requests"
Expected behaviour / AC: None (excluded); AC-16.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §16
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: Zoho/Shiprocket automation owns fulfilment
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-140
Domain: Orders
Functionality: Bulk "Change fulfillment location"
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: HU decision, locations settled (PROJECT_LOG)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-141
Domain: Orders
Functionality: Bulk "Run Flow automation" on orders
Expected behaviour / AC: None (excluded); AC-15.x; AC-27.1
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ORD-142
Domain: Orders
Functionality: Order "More actions": Edit, Duplicate, Archive/Unarchive, View order status page, Print order page …
Expected behaviour / AC: Works as inventoried; AC-15.x; AC-27.1
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: VALIDATE
Rationale: Inventory says covered for the status page (customer tracking exists); other items per their own rows
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-143
Domain: Orders
Functionality: Link from Admin order to the customer's order status page
Expected behaviour / AC: Not required; AC-15.x; AC-27.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §15, §27.1
Source IDs: -
Disposition: NO ACTION
Rationale: R3: tracking page exists for customers
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ORD-144
Domain: Orders
Functionality: Order header "Refund" and "Return" buttons
Expected behaviour / AC: None (excluded); AC-16.x; AC-12.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-069, ORD-071
SPEC / decision: §16.3, §12
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.5 and §16.10 (as ORD-069, ORD-071)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ORD-145
Domain: Orders
Functionality: Fulfilment card "..." menu (not opened; contents unobserved)
Expected behaviour / AC: Subject to decision; AC-18.x
Status: UNV
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Blocked: contents not observed; cannot assess
Evidence gap: G11

§2 covers MA-ORD-001 to MA-ORD-145 (119 rows). The ORD IDs have gaps because the inventory skips numbers. Rows ORD-010,
011, 067 and 068 carry flagged conflicts.

Next is §3 (Draft orders, Products, Collections, Inventory, Gift cards).

  Ran 1 shell command

§3 Shopify Admin capabilities: Draft orders, Products, Collections, Inventory, Gift cards (MA-DRF-001 to MA-GFT-002,
130 rows)

All codes are as defined in §2. Two clarifications for this section:
- All MA-DRF rows stay BLOCKED-DEC and none is REJECT/OOS (except the shipping line, which is excluded by SPEC §3.8).
  SPEC §27.3 requires admin-assisted orders, so I did not treat drafts as an out-of-scope Shopify concept.
- The cross-link for MA-PRD-067 is MF-026 (the storefront already renders related-product links).

Master ID: MA-DRF-001
Domain: Draft orders
Functionality: Draft order list
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS; S: no draft routes
Validation: V1
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018; MF-106; C1 SA-D
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-22 (Distributor/Bulk order handling)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-002
Domain: Draft orders
Functionality: Create draft order for a customer
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-003
Domain: Draft orders
Functionality: Add products / custom items
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: custom (non-catalogue) items conflict with Zoho-mapped items
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-004
Domain: Draft orders
Functionality: Apply named order discount to a draft
Expected behaviour / AC: Subject to decision; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: existing practice versus SPEC §3.7. Confirm whether negotiated discounts on assisted orders
are intended (E16)
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-DRF-005
Domain: Draft orders
Functionality: Tax-exempt flag on a draft
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: GST mapping open
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-006
Domain: Draft orders
Functionality: Draft shipping / delivery line
Expected behaviour / AC: None (excluded); AC-27.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.8 (no shipping charge)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-007
Domain: Draft orders
Functionality: Send draft invoice / payment link
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21, DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-21, DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-008
Domain: Draft orders
Functionality: Complete draft as paid / payment pending
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-009
Domain: Draft orders
Functionality: PO number on a draft
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22; useful for B2B
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-010
Domain: Draft orders
Functionality: Draft order timeline and notes
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-011
Domain: Draft orders
Functionality: Delete / duplicate draft
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:DOC
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-DRF-020
Domain: Draft orders
Functionality: Draft statuses: Open, Invoice sent, Completed, Submitted for review
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-22
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DRF-021
Domain: Draft orders
Functionality: Draft "Submitted for review" (approval step before an order)
Expected behaviour / AC: Subject to decision; AC-27.x
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §27.3, §12.11
Source IDs: SA-A04; CG-018; MF-106
Disposition: BLOCKED-DEC
Rationale: Blocked: SPEC §27.3 requires approvals on assisted orders; Director approves D/B pricing
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-001
Domain: Products
Functionality: Product list with pagination, thumbnails, status badges
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-002
Domain: Products
Functionality: Search products (ID, Zoho item, name)
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-003
Domain: Products
Functionality: Filter by status
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-004
Domain: Products
Functionality: Filter by category / product type / use case
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-005
Domain: Products
Functionality: Filter by vendor
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: EffyKlean is the only vendor
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-006
Domain: Products
Functionality: Filter by tag
Expected behaviour / AC: Recommended, not approved; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: tags exist and customers filter by them
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-PRD-007
Domain: Products
Functionality: Filter by collection / sales channel
Expected behaviour / AC: Not required; AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: see COL, CHN
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-008
Domain: Products
Functionality: Filter by stock level (low, out)
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §14, §3.4
Source IDs: SA-A05; CG-011; MF-101
Disposition: BLOCKED-DEC
Rationale: Blocked: Zoho availability, DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-009
Domain: Products
Functionality: Sort the list
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-010
Domain: Products
Functionality: Column: inventory ("N in stock")
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §14, §3.4
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-011
Domain: Products
Functionality: Column: category, product type
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-012
Domain: Products
Functionality: Column: channels
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: single channel
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-013
Domain: Products
Functionality: Saved product views
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-014
Domain: Products
Functionality: Export products (CSV)
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS; S: route products/export
Validation: V1
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-015
Domain: Products
Functionality: Product count by status summary
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:DOC
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G7
────────────────────────────────────────
Master ID: MA-PRD-020
Domain: Products
Functionality: Create product
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-021
Domain: Products
Functionality: Edit product content as a revision
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-022
Domain: Products
Functionality: Duplicate product
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-023
Domain: Products
Functionality: Title
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-024
Domain: Products
Functionality: Description (rich text)
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-025
Domain: Products
Functionality: Short description / benefits / usage / safety
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-026
Domain: Products
Functionality: Price (MRP)
Expected behaviour / AC: Works as inventoried; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §7
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-027
Domain: Products
Functionality: Compare-at price
Expected behaviour / AC: Works as inventoried; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §7
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-028
Domain: Products
Functionality: Unit price with measurement (price per litre)
Expected behaviour / AC: Subject to decision; AC-7.x
Status: UNV
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §7
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: not checked in the product form
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-029
Domain: Products
Functionality: Charge-tax flag
Expected behaviour / AC: Works as inventoried; AC-13.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-030
Domain: Products
Functionality: Cost per item
Expected behaviour / AC: Not required; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §7
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3: Part 1 C16; Zoho may hold cost
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-031
Domain: Products
Functionality: SKU
Expected behaviour / AC: Works as inventoried; AC-14.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §14, §3.4
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-032
Domain: Products
Functionality: Barcode
Expected behaviour / AC: Not required; AC-14.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14, §3.4
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-033
Domain: Products
Functionality: Zoho item link / mapping
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-PRD-034
Domain: Products
Functionality: Track quantity / sell when out of stock
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14, §3.4
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (no local stock authority); inventory: Zoho owns availability
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-035
Domain: Products
Functionality: Quantity per location
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-036
Domain: Products
Functionality: Weight
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-19
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-19 weight and dimension master
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-037
Domain: Products
Functionality: Package / dimensions
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-19
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-19
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-038
Domain: Products
Functionality: Country of origin
Expected behaviour / AC: Not required; AC-13.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3: domestic only
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-039
Domain: Products
Functionality: HS code
Expected behaviour / AC: Subject to decision; AC-13.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: GST invoice needs HSN
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-040
Domain: Products
Functionality: Physical product / requires shipping
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: all products are physical
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-041
Domain: Products
Functionality: Product type / category / tags
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-042
Domain: Products
Functionality: Vendor
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-043
Domain: Products
Functionality: Shopify taxonomy category
Expected behaviour / AC: None (excluded); AC-13.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: EffyKlean has its own category set
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-044
Domain: Products
Functionality: Metafields (pinned custom data)
Expected behaviour / AC: None (excluded); AC-22.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §22
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: FEATURE_MAPPING parent row L11 (carried HU+DI review)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-045
Domain: Products
Functionality: Google-feed fields (age group, condition, gender, MPN)
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3: with I2
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-046
Domain: Products
Functionality: Theme template selector
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; MF-116
Disposition: REJECT/OOS
Rationale: Basis: Shopify themes permanently excluded (inventory CNT-014; AC-1.2 no Shopify dependency)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-047
Domain: Products
Functionality: Verified commercial data marker (MRP, concentrate, Zoho)
Expected behaviour / AC: Subject to decision; AC-6.x
Status: MISS
Evidence: O:—
Validation: V0
Dependency / blocker: D-B1
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: decision D-B1
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-PRD-048
Domain: Products
Functionality: Concentrate quantity / dilution data
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-PRD-050
Domain: Products
Functionality: Product status: draft, in review, approved, published
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-051
Domain: Products
Functionality: Submit / return / approve / publish workflow
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; MF-095
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-052
Domain: Products
Functionality: Archive / unpublish a published product
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-10
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-10
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-053
Domain: Products
Functionality: "Unlisted" (reachable by link only)
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.15 (Shopify Unlisted products parked); FEATURE_MAPPING parent row C4
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-054
Domain: Products
Functionality: Delete product
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: financial and audit history, archive instead
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-PRD-055
Domain: Products
Functionality: Product history / timeline
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-056
Domain: Products
Functionality: Preview an unpublished revision
Expected behaviour / AC: Recommended, not approved; AC-6.x
Status: PART
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: Part 1 C14
Evidence gap: G3; G7
────────────────────────────────────────
Master ID: MA-PRD-057
Domain: Products
Functionality: Schedule publish date
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-058
Domain: Products
Functionality: Upload, reorder and set primary image
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-059
Domain: Products
Functionality: Image alt text
Expected behaviour / AC: Recommended, not approved; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: Part 1 C9
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-PRD-060
Domain: Products
Functionality: Video and 3D media on a product
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-25
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3: DC-25
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-061
Domain: Products
Functionality: Media from the Files library
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-062
Domain: Products
Functionality: SEO title and meta description
Expected behaviour / AC: Recommended, not approved; AC-22.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-26
SPEC / decision: §22
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: Part 1 C12
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-PRD-063
Domain: Products
Functionality: URL handle (slug) edit
Expected behaviour / AC: Recommended, not approved; AC-22.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-27, DC-28
SPEC / decision: §22
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: with DC-28
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-PRD-064
Domain: Products
Functionality: Variants and options (size, colour)
Expected behaviour / AC: Not required; AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; MF-024
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: Part 1 C19; single-variant pattern OBS/API (see MF-024)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-065
Domain: Products
Functionality: Product family / pack-size grouping
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:—
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2; G9
────────────────────────────────────────
Master ID: MA-PRD-066
Domain: Products
Functionality: Bundles / combo packs as products
Expected behaviour / AC: Subject to decision; AC-6.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-33
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: combo rules, DC-33
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-067
Domain: Products
Functionality: Related / complementary products
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; MF-026
Disposition: NO ACTION
Rationale: R3: OBS shows related-products metafields
Evidence gap: G2; see MF-026 (storefront already renders related products)
────────────────────────────────────────
Master ID: MA-PRD-068
Domain: Products
Functionality: Reviews and ratings
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; MF-033
Disposition: NO ACTION
Rationale: R3 (see MF-033: scope ambiguity S-1 open)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-069
Domain: Products
Functionality: Product boosts / search ranking
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: Search & Discovery app
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-070
Domain: Products
Functionality: Selling plans / subscriptions
Expected behaviour / AC: Not required; AC-6.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: no requirement exists
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-PRD-071
Domain: Products
Functionality: Product quantity rules and price breaks
Expected behaviour / AC: Not required; AC-7.x
Status: EXC
Evidence: O:API
Validation: V0
Dependency / blocker: -
SPEC / decision: §7
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: see E15 (SPEC §3.6 excludes a general B2C quantity
discount)
Evidence gap: Shopify API 2026-07 restamp, not re-checked
────────────────────────────────────────
Master ID: MA-PRD-072
Domain: Products
Functionality: Import products (CSV)
Expected behaviour / AC: Not required; AC-6.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; CG-021
Disposition: NO ACTION
Rationale: R3: Part 1 M1
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-073
Domain: Products
Functionality: Bulk edit (spreadsheet-style editor)
Expected behaviour / AC: Not required; AC-6.x
Status: PART
Evidence: O:OBS-L; S: route products/bulk (scope unverified)
Validation: V1
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; CG-021; C1 SA-D
Disposition: NO ACTION
Rationale: R3: revision workflow makes bulk edits an approval question
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-074
Domain: Products
Functionality: Bulk change status, tags, category
Expected behaviour / AC: Not required; AC-6.x
Status: PART
Evidence: O:OBS; S: route products/bulk (scope unverified)
Validation: V1
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; CG-021; C1 SA-D
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-075
Domain: Products
Functionality: Product translations
Expected behaviour / AC: Not required; AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: with I5
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-083
Domain: Products
Functionality: Product/collection status "Suspended" (in addition to Active, Draft, Unlisted)
Expected behaviour / AC: Not required; AC-6.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: meaning unconfirmed; ask whether the business uses it
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-084
Domain: Products
Functionality: Product category determines tax rates (Shopify taxonomy)
Expected behaviour / AC: None (excluded); AC-13.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: SPEC §13.9 (Zoho item master is authoritative for tax data); inventory: category does not drive tax
here
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-090
Domain: Products
Functionality: Bulk bar "Bulk edit" (spreadsheet editor)
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; CG-021
Disposition: NO ACTION
Rationale: R3: as PRD-073
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-091
Domain: Products
Functionality: Bulk archive / unlist products
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-10
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-10
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-092
Domain: Products
Functionality: Bulk delete products
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: financial and audit history
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-093
Domain: Products
Functionality: Bulk include/exclude in sales channels and catalogs
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: single channel
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-094
Domain: Products
Functionality: Bulk add/remove tags
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-095
Domain: Products
Functionality: Bulk add to / remove from collections
Expected behaviour / AC: Subject to decision; AC-6.x
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-29
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-29
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-096
Domain: Products
Functionality: "Create email campaign" from selected products
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14 (no campaign engine)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-097
Domain: Products
Functionality: Export products dialog
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: IIV
Evidence: O:OBS-L; S: route products/export
Validation: V1
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-PRD-098
Domain: Products
Functionality: Import products: CSV with downloadable sample, or "import from your platform" (Etsy, TikTok …)
Expected behaviour / AC: Not required; AC-6.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: NO ACTION
Rationale: R3: CSV (as PRD-072); inventory says REJECT platform imports
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-100
Domain: Products
Functionality: Product list filters: vendor, tag, status, category, sales channel, catalogs, type, collection …
Expected behaviour / AC: Recommended, not approved; AC-6.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: IMPLEMENT
Rationale: R2: tag filter (PRD-006); inventory defers collection and rejects vendor
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-PRD-101
Domain: Products
Functionality: Product sort by created and updated date
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: UNV
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: SA-A05
Disposition: VALIDATE
Rationale: Not verified: cheap; confirm existing sorts first
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-102
Domain: Products
Functionality: Rich-text description editor tools (headings, colour, alignment, tables)
Expected behaviour / AC: Works as inventoried; AC-6.x
Status: UNV
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §6, §27.1
Source IDs: -
Disposition: VALIDATE
Rationale: Not verified: confirm what the current editor supports
Evidence gap: -
────────────────────────────────────────
Master ID: MA-PRD-103
Domain: Products
Functionality: Barcode type selector (GTIN, UPC, EAN, ISBN, ASIN, NS-PID, custom)
Expected behaviour / AC: Not required; AC-14.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14, §3.4
Source IDs: -
Disposition: NO ACTION
Rationale: R3: with PRD-032
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-PRD-104
Domain: Products
Functionality: Inventory adjustment on the product page with a reason; unavailable breakdown
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14, §3.4
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (no local stock authority)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-PRD-105
Domain: Products
Functionality: Package picker and "Manage packages" (sample box 22×13.7×4.2 cm)
Expected behaviour / AC: Subject to decision; AC-6.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-19
SPEC / decision: §6, §27.1
Source IDs: -
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: DC-19 decides where weight and package data live
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-COL-001
Domain: Collections
Functionality: Collections list
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-29
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3: DC-29
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-002
Domain: Collections
Functionality: Create manual collection
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-003
Domain: Collections
Functionality: Create automated collection by rules
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-004
Domain: Collections
Functionality: Collection image, description, SEO
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-005
Domain: Collections
Functionality: Collection sort order
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-006
Domain: Collections
Functionality: Add / remove products in collection
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-007
Domain: Collections
Functionality: Separate combo collections
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.11 (frozen rule)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-COL-008
Domain: Collections
Functionality: Collection channel availability
Expected behaviour / AC: None (excluded); AC-6.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-COL-009
Domain: Collections
Functionality: Catalogs / price lists (B2B, markets)
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3: with E15
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-COL-010
Domain: Collections
Functionality: Price override / adjustment per catalog
Expected behaviour / AC: Not required; AC-6.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §6; §3.11
Source IDs: SA-A06
Disposition: NO ACTION
Rationale: R3: with E15
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-INV-001
Domain: Inventory & purchasing
Functionality: Inventory page (per location counts)
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: BLOCKED-DEC
Rationale: Blocked: read-only view of Zoho; DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-002
Domain: Inventory & purchasing
Functionality: States: available, committed, unavailable, on hand, incoming
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: BLOCKED-DEC
Rationale: Blocked: Zoho semantics
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-003
Domain: Inventory & purchasing
Functionality: Adjust quantity
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (no local stock authority)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-004
Domain: Inventory & purchasing
Functionality: Adjustment history
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (no local stock authority)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-005
Domain: Inventory & purchasing
Functionality: Reserve / commit stock
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: SPEC §14.3 and §3.4 (no reservation engine)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-006
Domain: Inventory & purchasing
Functionality: Low-stock alert
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:DOC
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08; MF-101
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-17
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-INV-007
Domain: Inventory & purchasing
Functionality: Locations list
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: BLOCKED-DEC
Rationale: Blocked: three locations OBS; locations query denied by scopes (API)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-008
Domain: Inventory & purchasing
Functionality: Add / edit / deactivate location
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: HU decision, locations settled (PROJECT_LOG)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-009
Domain: Inventory & purchasing
Functionality: Inventory-by-location report
Expected behaviour / AC: Subject to decision; AC-14.x
Status: BLK
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: BLOCKED-DEC
Rationale: Blocked: no reason recorded in the inventory
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-INV-010
Domain: Inventory & purchasing
Functionality: Purchase orders
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: FEATURE_MAPPING parent row F4 (carried HU+DI review)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INV-011
Domain: Inventory & purchasing
Functionality: Transfers between locations
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: empty, unused
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-012
Domain: Inventory & purchasing
Functionality: Suppliers
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-INV-013
Domain: Inventory & purchasing
Functionality: Inventory CSV import / export
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A07; SA-A08
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4 (Zoho is stock authority); inventory recommendation
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-INV-020
Domain: Inventory & purchasing
Functionality: Inventory column "Bin name"
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: warehouse detail belongs to Zoho
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-021
Domain: Inventory & purchasing
Functionality: Inventory quick-transfer popover
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-022
Domain: Inventory & purchasing
Functionality: Export inventory (from all locations)
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A08
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.4; inventory: Zoho owns stock
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-023
Domain: Inventory & purchasing
Functionality: Incoming popover with "Create transfer"
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INV-024
Domain: Inventory & purchasing
Functionality: Purchase order list: statuses Draft, Ordered, Archived; supplier, destination, received, expected …
Expected behaviour / AC: None (excluded); AC-14.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §14; §3.4
Source IDs: SA-A08
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: empty and unused
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-GFT-001
Domain: Gift cards
Functionality: Create / sell / redeem gift cards
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: no clause; §3.2
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: not found on the store and SPEC has no gift card
Evidence gap: G8; G11
────────────────────────────────────────
Master ID: MA-GFT-002
Domain: Gift cards
Functionality: Gift card liability reporting
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: no clause; §3.2
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8; G7

§3 covers MA-DRF-001 to MA-GFT-002 (130 rows). I made a few corrections while pasting:
- MA-PRD-053 basis: SPEC §3.15 parks the Shopify Unlisted products, and the "Unlisted" product status is the same
  concept. The inventory's own basis was parent row C4.
- MA-PRD-084: I added SPEC §13.9 as the basis (tax data comes from the Zoho item master).
- Hand-completed cells: where the generator had cut a cell mid-phrase, I restored the full text, for example the "DOC
  tier" gap notes, which became G7.

Next is §4 (Customers, B2B and Discounts).

  Ran 1 shell command

§4 Shopify Admin capabilities: Customers, B2B and Discounts (MA-CUS-001 to MA-DSC-041, 74 rows)

Codes are as in §2. Two cross-links apply to the Discounts rows. MF-047 covers the combo-or-coupon behaviour that is
still an HU+DI-confirmation default (see MA-DSC-018). MF-048 covers coupon management (see MA-DSC-015 and MA-DSC-017).

Master ID: MA-CUS-001
Domain: Customers & B2B
Functionality: Customer list (name, phone, orders, total spent, last order)
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-002
Domain: Customers & B2B
Functionality: Search customers
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-003
Domain: Customers & B2B
Functionality: Filter customers (location, orders, spend, consent)
Expected behaviour / AC: Not required; AC-20.5; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09; CG-019
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-004
Domain: Customers & B2B
Functionality: Customer detail: contact, invoice details
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-005
Domain: Customers & B2B
Functionality: Customer order history
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-006
Domain: Customers & B2B
Functionality: Customer addresses (multiple, default)
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: UNV
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: BLOCKED-DEC
Rationale: Blocked: account address book vs order addresses not compared
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-007
Domain: Customers & B2B
Functionality: Edit customer details (as Admin)
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3: DC-31
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-008
Domain: Customers & B2B
Functionality: Create customer manually
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3: DC-31
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-009
Domain: Customers & B2B
Functionality: Delete / anonymise customer
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: D-D2
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: BLOCKED-DEC
Rationale: Blocked: decision D-D2
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-010
Domain: Customers & B2B
Functionality: Customer notes (private)
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS; S: route customers/<key>/notes
Validation: V1
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-011
Domain: Customers & B2B
Functionality: Customer tags
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS; S: route customers/<key>/tags
Validation: V1
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-012
Domain: Customers & B2B
Functionality: Marketing consent display (e-mail, SMS, WhatsApp)
Expected behaviour / AC: Works as inventoried; AC-20.5; AC-26.x
Status: PART
Evidence: O:API
Validation: V0
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09
Disposition: VALIDATE
Rationale: Inventory says covered for display; changes deferred
Evidence gap: Shopify API 2026-07 restamp, not re-checked
────────────────────────────────────────
Master ID: MA-CUS-013
Domain: Customers & B2B
Functionality: Edit marketing consent
Expected behaviour / AC: Not required; AC-20.5; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3: consent changes must be recorded, not silently edited
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-014
Domain: Customers & B2B
Functionality: Tax-exempt flag
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: EXC
Evidence: O:API
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: GST mapping decision
Evidence gap: Genuine ambiguity per inventory; API tier not re-checked
────────────────────────────────────────
Master ID: MA-CUS-015
Domain: Customers & B2B
Functionality: Customer metafields (budget, state, PIN from enquiry form)
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: Excluded/not applicable: (intake)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-016
Domain: Customers & B2B
Functionality: Customer account state (enabled, disabled, invited)
Expected behaviour / AC: Recommended, not approved; AC-19.x; AC-26.x
Status: PART
Evidence: O:API
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: IMPLEMENT
Rationale: R2: after DC-31/32
Evidence gap: G3; API tier not re-checked
────────────────────────────────────────
Master ID: MA-CUS-017
Domain: Customers & B2B
Functionality: Send account invite
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: DC-21
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-CUS-018
Domain: Customers & B2B
Functionality: Reset customer password / sign-in help
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: BLK
Evidence: O:DOC
Validation: V0
Dependency / blocker: D-D1
SPEC / decision: §19, §26.2
Source IDs: SA-A09; CG-016; MF-105
Disposition: BLOCKED-DEC
Rationale: Blocked: no reset flow; D-D1
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-CUS-019
Domain: Customers & B2B
Functionality: Customer timeline
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-020
Domain: Customers & B2B
Functionality: Merge customers
Expected behaviour / AC: None (excluded); AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: identity integrity
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CUS-021
Domain: Customers & B2B
Functionality: Customer segments (list)
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; SA-A10; CG-019
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-022
Domain: Customers & B2B
Functionality: Create segment by filter (ShopifyQL-like)
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; CG-019
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-023
Domain: Customers & B2B
Functionality: Segment membership counts / use in marketing
Expected behaviour / AC: None (excluded); AC-20.5; AC-26.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14 (no campaign engine)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-024
Domain: Customers & B2B
Functionality: Companies (B2B)
Expected behaviour / AC: None (excluded); AC-9.x; AC-10.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: 0 companies on the store
Evidence gap: EffyKlean B2B uses business accounts (SPEC §9/§10), not Shopify Companies
────────────────────────────────────────
Master ID: MA-CUS-025
Domain: Customers & B2B
Functionality: Company locations, contacts, payment terms
Expected behaviour / AC: None (excluded); AC-9.x; AC-10.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: EffyKlean B2B uses business accounts, not Shopify Companies; G7
────────────────────────────────────────
Master ID: MA-CUS-026
Domain: Customers & B2B
Functionality: Customer export
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS; S: route customers/export
Validation: V1
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CUS-027
Domain: Customers & B2B
Functionality: Customer import
Expected behaviour / AC: None (excluded); AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.16 (no automatic customer migration); inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CUS-028
Domain: Customers & B2B
Functionality: Customer data request (export one customer)
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: BLK
Evidence: O:DOC
Validation: V0
Dependency / blocker: D-D2
SPEC / decision: §19, §26.2
Source IDs: SA-A09; CG-016; MF-105
Disposition: BLOCKED-DEC
Rationale: Blocked: D-D2
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-CUS-029
Domain: Customers & B2B
Functionality: Distributor application review and status
Expected behaviour / AC: Works as inventoried; AC-9.x; AC-10.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09; MF-081
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-CUS-030
Domain: Customers & B2B
Functionality: Distributor account created on approval
Expected behaviour / AC: Subject to decision; AC-9.x; AC-10.x
Status: BLK
Evidence: O:—
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §9, §10
Source IDs: SA-A09; SA-A11; MF-081
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-31/32
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-CUS-031
Domain: Customers & B2B
Functionality: Distributor pricing slabs and overrides
Expected behaviour / AC: Subject to decision; AC-9.x; AC-10.x
Status: BLK
Evidence: O:—
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09; SA-A11; MF-081
Disposition: BLOCKED-DEC
Rationale: Blocked: after configuration is approved
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-CUS-032
Domain: Customers & B2B
Functionality: Bulk enquiry intake, status and notes
Expected behaviour / AC: Works as inventoried; AC-9.x; AC-10.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09; SA-A11; MF-082
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-CUS-033
Domain: Customers & B2B
Functionality: Bulk proposal and negotiated pricing record
Expected behaviour / AC: Subject to decision; AC-9.x; AC-10.x
Status: BLK
Evidence: O:—
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09; SA-A11; MF-082
Disposition: BLOCKED-DEC
Rationale: Blocked: after configuration is approved
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-CUS-040
Domain: Customers & B2B
Functionality: Customer list optional columns: e-mail, phone, first/last name, postal code, language, ID …
Expected behaviour / AC: Not required; AC-20.5; AC-26.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-041
Domain: Customers & B2B
Functionality: Customer "deletable" flag (can this customer be deleted)
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: D-D2
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: BLOCKED-DEC
Rationale: Blocked: D-D2
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-043
Domain: Customers & B2B
Functionality: Customer notification language ("Will receive notifications in English")
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3: DC-21
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-044
Domain: Customers & B2B
Functionality: "Create order" from the customer page
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3: with drafts (but see MF-106: SPEC §27.3 requires assisted orders)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-045
Domain: Customers & B2B
Functionality: Customer "Collect tax" setting
Expected behaviour / AC: Subject to decision; AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: GST mapping (see CUS-014)
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-CUS-050
Domain: Customers & B2B
Functionality: Bulk "Delete customer"
Expected behaviour / AC: Subject to decision; AC-9.x; AC-10.x
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: D-D2
SPEC / decision: §9, §10
Source IDs: SA-A09; CG-016
Disposition: BLOCKED-DEC
Rationale: Blocked: D-D2
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CUS-051
Domain: Customers & B2B
Functionality: Bulk "Add to company"
Expected behaviour / AC: None (excluded); AC-9.x; AC-10.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CUS-052
Domain: Customers & B2B
Functionality: Bulk "Remove tags"
Expected behaviour / AC: Not required; AC-9.x; AC-10.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §9, §10
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-053
Domain: Customers & B2B
Functionality: "Select all in this store" (selection beyond the page)
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-054
Domain: Customers & B2B
Functionality: Segment actions: use, duplicate, export, rename, delete
Expected behaviour / AC: Not required; AC-19.x; AC-26.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; CG-019
Disposition: NO ACTION
Rationale: R3: with CUS-021
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CUS-055
Domain: Customers & B2B
Functionality: Describe-your-segment (natural-language segment builder)
Expected behaviour / AC: None (excluded); AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CUS-056
Domain: Customers & B2B
Functionality: Import customers by CSV dialog
Expected behaviour / AC: None (excluded); AC-19.x; AC-26.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.16 (as CUS-027)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-DSC-001
Domain: Discounts
Functionality: Discount list
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-002
Domain: Discounts
Functionality: Search and status tabs
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-003
Domain: Discounts
Functionality: Filter by date, type, method
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-004
Domain: Discounts
Functionality: Create a code discount
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-005
Domain: Discounts
Functionality: Percentage or fixed value
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-006
Domain: Discounts
Functionality: Applies to specific products
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-007
Domain: Discounts
Functionality: Applies to collections / categories
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-29
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3: DC-29
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-008
Domain: Discounts
Functionality: Minimum purchase amount
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-047
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-009
Domain: Discounts
Functionality: Minimum quantity
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-010
Domain: Discounts
Functionality: Total usage limit
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-011
Domain: Discounts
Functionality: One use per customer
Expected behaviour / AC: Subject to decision; AC-21.x; AC-7.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: BLOCKED-DEC
Rationale: Blocked: needs customer identity, DC-31
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DSC-012
Domain: Discounts
Functionality: Customer eligibility (all, segment, specific)
Expected behaviour / AC: Subject to decision; AC-21.x; AC-7.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-31
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: BLOCKED-DEC
Rationale: Blocked: all/new customers after DC-31; DEFER segments
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DSC-013
Domain: Discounts
Functionality: Start and end dates
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-014
Domain: Discounts
Functionality: Edit / deactivate / delete a discount
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-015
Domain: Discounts
Functionality: Duplicate discount
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:DOC; S: route coupons/<code>/duplicate
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G7
────────────────────────────────────────
Master ID: MA-DSC-016
Domain: Discounts
Functionality: Generate random code
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-017
Domain: Discounts
Functionality: Bulk-generate unique codes
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:DOC; S: route coupons/bulk
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-048; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G7
────────────────────────────────────────
Master ID: MA-DSC-018
Domain: Discounts
Functionality: Combinations with other discounts
Expected behaviour / AC: Subject to decision; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: D-E1
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-047
Disposition: BLOCKED-DEC
Rationale: Blocked: decision D-E1 (combo-versus-coupon default awaiting confirmation)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DSC-019
Domain: Discounts
Functionality: Used count and sales total
Expected behaviour / AC: Recommended, not approved; AC-21.x; AC-7.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: IMPLEMENT
Rationale: R2: Part 1 E8
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-DSC-020
Domain: Discounts
Functionality: Automatic discount (no code)
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:API
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3: API shows none exist today
Evidence gap: G2; API tier not re-checked
────────────────────────────────────────
Master ID: MA-DSC-021
Domain: Discounts
Functionality: Buy X get Y
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-022
Domain: Discounts
Functionality: Amount off order (distinct from product)
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-DSC-023
Domain: Discounts
Functionality: Free shipping discount
Expected behaviour / AC: None (excluded); AC-21.x; AC-7.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.8 (no shipping charge)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-DSC-024
Domain: Discounts
Functionality: Sales-channel limitation of a discount
Expected behaviour / AC: None (excluded); AC-21.x; AC-7.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: single channel
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-DSC-025
Domain: Discounts
Functionality: Discount timeline / comments
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3: audit trail exists
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-026
Domain: Discounts
Functionality: Combo pack pricing (rule set)
Expected behaviour / AC: Subject to decision; AC-21.x; AC-7.x
Status: PART
Evidence: O:—
Validation: V0
Dependency / blocker: DC-33
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12; MF-046
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-33
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-DSC-027
Domain: Discounts
Functionality: Distributor/Bulk exclusion from promotions
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: VALIDATE
Rationale: R1 (SPEC §3.7 exclusion must hold)
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-DSC-040
Domain: Discounts
Functionality: Discount list filters (status active/scheduled/expired, type, method, sales channel) and sort …
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-DSC-041
Domain: Discounts
Functionality: Staff comments with @mention and links to records (orders, drafts, customers, products, variants …)
Expected behaviour / AC: Not required; AC-21.x; AC-7.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-034
SPEC / decision: §21, §7; §3.6, §3.7
Source IDs: SA-A12
Disposition: NO ACTION
Rationale: R3: with ORD-034
Evidence gap: G2

§4 covers MA-CUS-001 to MA-DSC-041 (74 rows). Corrections made while pasting:
- MA-CUS-027 and MA-CUS-056 (customer import): SPEC §3.16 (no automatic migration of Shopify customers) is the better
  basis than the generic one.
- MA-CUS-044: I added the note that SPEC §27.3 requires assisted orders.

Next is §5 (Content, Marketing, Channels and Analytics).

  Ran 5 shell commands

§5 Shopify Admin capabilities: Content, Marketing, Channels and Analytics (MA-CNT-001 to MA-ANA-027, 69 rows)

Two additions to the code legend, because I found more stale inventory statuses in this pass:
- G12: The inventory status was stale (the capability was implemented later). The evidence is a static route or
  template check on 2026-10-12 only, which shows the element exists and not that it works.
- Δ2: Re-verified in this task and not in Comparison 1.

Rows re-verified here are MA-CNT-001/003/005/006/018 and MA-ANA-005/006/008/009/010. Six rows of §4 (MA-CUS-003/019 and
MA-DSC-002/003/019/040) are also now IIV, and they supersede the §4 text above. They are repeated in the §4 addendum
after §6.

Master ID: MA-CNT-001
Domain: Content
Functionality: Pages: list, create, edit, publish
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS; S: routes content/pages/* (new, submit, approve, publish, hide)
Validation: V1
Dependency / blocker: DC-24
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CNT-002
Domain: Content
Functionality: Page SEO fields
Expected behaviour / AC: Recommended, not approved; AC-22.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-26
SPEC / decision: §22
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: IMPLEMENT
Rationale: R2: with DC-26
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-CNT-003
Domain: Content
Functionality: Page visibility / schedule
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS; S: content_page.html "Publish at (IST), when scheduling"
Validation: V1
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CNT-004
Domain: Content
Functionality: Page templates
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-116
Disposition: REJECT/OOS
Rationale: Basis: Shopify themes/templates permanently excluded (inventory CNT-014; AC-1.2)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CNT-005
Domain: Content
Functionality: Navigation menus: header, footer, account
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS; S: routes content/nav/* (new, toggle, delete, defaults)
Validation: V1
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CNT-006
Domain: Content
Functionality: Blog list / create / edit posts
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS; S: content_views kind PAGE or BLOG with post_date
Validation: V1
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-086; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CNT-007
Domain: Content
Functionality: Blog post author, tags, excerpt, image
Expected behaviour / AC: Not required; AC-23.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A15; SA-A16; CG-022; MF-086
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CNT-008
Domain: Content
Functionality: Blog comments moderation
Expected behaviour / AC: Not required; AC-23.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-CNT-009
Domain: Content
Functionality: Files library: upload, alt text, delete
Expected behaviour / AC: Not required; AC-23.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-25
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: R3: DC-25
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CNT-010
Domain: Content
Functionality: Files: references (where used)
Expected behaviour / AC: Not required; AC-23.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CNT-011
Domain: Content
Functionality: Metaobjects (definitions, entries)
Expected behaviour / AC: None (excluded); AC-22.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §22
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CNT-012
Domain: Content
Functionality: Redirects (URL redirects)
Expected behaviour / AC: Recommended, not approved; AC-23.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-28
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-092
Disposition: IMPLEMENT
Rationale: R2: Part 1 G5 (see MF-092: redirect plan undecided)
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-CNT-013
Domain: Content
Functionality: Sitemap / robots
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-091
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CNT-014
Domain: Content
Functionality: Themes: library, customise, edit code
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-116
Disposition: REJECT/OOS
Rationale: Basis: permanent exclusion recorded in the inventory (Part 1 G6); AC-1.2
Evidence gap: Exclusion is a carried decision, not a SPEC sentence
────────────────────────────────────────
Master ID: MA-CNT-015
Domain: Content
Functionality: Online Store preferences (title, meta, social image, password page)
Expected behaviour / AC: Not required; AC-22.x
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §22
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2; G7
────────────────────────────────────────
Master ID: MA-CNT-016
Domain: Content
Functionality: Storefront search settings and filters (Search & Discovery)
Expected behaviour / AC: Not required; AC-23.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CNT-017
Domain: Content
Functionality: How-to videos page
Expected behaviour / AC: Not required; AC-23.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-25
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-088
Disposition: NO ACTION
Rationale: R3: DC-25 (storefront /videos/ exists; Admin management not checked)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CNT-018
Domain: Content
Functionality: FAQ management
Expected behaviour / AC: Works as inventoried; AC-23.x
Status: IIV
Evidence: O:OBS; S: routes content/faq/* (new, submit, approve, publish, takedown)
Validation: V1
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CNT-019
Domain: Content
Functionality: Forms (Shopify Forms) builder
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: EffyKlean builds intake forms in code
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-CNT-020
Domain: Content
Functionality: Customer-facing chat / chatbot (Tidio)
Expected behaviour / AC: Not required; AC-23.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: third-party SaaS (CLAUDE.md principle 5)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CNT-040
Domain: Content
Functionality: Pages list: title, visibility, content excerpt, updated; 6 pages (videos, distributor enquiry …)
Expected behaviour / AC: Recommended, not approved; AC-23.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: IMPLEMENT
Rationale: R2: as CNT-001
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-CNT-041
Domain: Content
Functionality: Themes: published theme, draft themes, update, edit theme, import, theme store
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16; MF-116
Disposition: REJECT/OOS
Rationale: Basis: permanent exclusion (inventory CNT-014); AC-1.2
Evidence gap: Exclusion is a carried decision
────────────────────────────────────────
Master ID: MA-CNT-042
Domain: Content
Functionality: Online Store home: 30-day sessions by device (mobile, desktop, tablet)
Expected behaviour / AC: Not required; AC-23.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23
Source IDs: SA-A13; SA-A14; SA-A16
Disposition: NO ACTION
Rationale: R3: with ANA-012
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-MKT-001
Domain: Marketing & markets
Functionality: Marketing campaigns
Expected behaviour / AC: None (excluded); AC-26.x
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14 (no campaign engine)
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-MKT-002
Domain: Marketing & markets
Functionality: Attribution
Expected behaviour / AC: Not required; AC-26.x
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: with H2
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-MKT-003
Domain: Marketing & markets
Functionality: Automations / Autopilot
Expected behaviour / AC: None (excluded); AC-26.x
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-MKT-004
Domain: Marketing & markets
Functionality: Shopify Email / Messaging campaigns
Expected behaviour / AC: None (excluded); AC-26.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14 (no campaign engine); SPEC §20.5 separates transactional and marketing communication
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-MKT-005
Domain: Marketing & markets
Functionality: Newsletter sign-up and consent
Expected behaviour / AC: Not required; AC-26.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20; MF-090
Disposition: NO ACTION
Rationale: R3: DC-21 (subscribe flow is MF-090)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-MKT-006
Domain: Marketing & markets
Functionality: Abandoned cart automations
Expected behaviour / AC: Not required; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-MKT-007
Domain: Marketing & markets
Functionality: Social posting / audiences
Expected behaviour / AC: None (excluded); AC-26.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-MKT-010
Domain: Marketing & markets
Functionality: Markets: India (INR)
Expected behaviour / AC: Works as inventoried; AC-26.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: VALIDATE
Rationale: R1 (SPEC §2.1 India/INR only)
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-MKT-011
Domain: Marketing & markets
Functionality: International markets, duties, local pricing
Expected behaviour / AC: Not required; AC-26.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory; SPEC §3.1 excludes international workflows
Evidence gap: -
────────────────────────────────────────
Master ID: MA-MKT-012
Domain: Marketing & markets
Functionality: Languages and translations
Expected behaviour / AC: Not required; AC-26.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20; MF-094
Disposition: NO ACTION
Rationale: R3: six unpublished
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-MKT-013
Domain: Marketing & markets
Functionality: Market-specific domains / rollouts
Expected behaviour / AC: Not required; AC-26.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §3.14, §26.2
Source IDs: SA-A17; SA-A20
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CHN-001
Domain: Sales channels
Functionality: Online Store channel
Expected behaviour / AC: Works as inventoried; AC-29.x
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-CHN-002
Domain: Sales channels
Functionality: Point of Sale
Expected behaviour / AC: Subject to decision; AC-29.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: should POS sales ever appear in EffyKlean? HU settled the POS locations only as configured
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-CHN-003
Domain: Sales channels
Functionality: Facebook & Instagram channel
Expected behaviour / AC: Not required; AC-29.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CHN-004
Domain: Sales channels
Functionality: Google & YouTube channel / product feed
Expected behaviour / AC: Not required; AC-29.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CHN-005
Domain: Sales channels
Functionality: WhatsApp channel
Expected behaviour / AC: Not required; AC-29.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20; MF-094
Disposition: NO ACTION
Rationale: R3: Shiprocket WhatsApp notifications stay (HU); SPEC §20.3 WhatsApp optional
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-CHN-006
Domain: Sales channels
Functionality: Agentic / AI channel
Expected behaviour / AC: Not required; AC-29.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-CHN-007
Domain: Sales channels
Functionality: Marketplaces / Shop app
Expected behaviour / AC: Not required; AC-29.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-CHN-008
Domain: Sales channels
Functionality: Pixels and customer events (Meta, Google)
Expected behaviour / AC: Not required; AC-29.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §29, §3.14
Source IDs: SA-A20; MF-093
Disposition: NO ACTION
Rationale: R3: consent rules (see MF-093)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-001
Domain: Analytics
Functionality: Reports page: sales by day
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-100
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ANA-002
Domain: Analytics
Functionality: Top products by sales
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-100
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ANA-003
Domain: Analytics
Functionality: Orders by status
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-100
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ANA-004
Domain: Analytics
Functionality: Payment attempts report
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS
Validation: V0B
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-100
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-ANA-005
Domain: Analytics
Functionality: Date-range selection on reports
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS; S: reports.html From/To date; insight_views._report_range
Validation: V1
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-ANA-006
Domain: Analytics
Functionality: Compare to previous period
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS; S: insight_views computes previous_period; display not verified
Validation: V1
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-ANA-007
Domain: Analytics
Functionality: Sales by customer / customer type
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-008
Domain: Analytics
Functionality: Sales by discount
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:OBS; S: reports.html "Sales by discount"
Validation: V1
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-ANA-009
Domain: Analytics
Functionality: Sales by state / location (GST relevance)
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:DOC; S: reports.html "Sales by delivery state"
Validation: V1
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12; G7
────────────────────────────────────────
Master ID: MA-ANA-010
Domain: Analytics
Functionality: Average order value
Expected behaviour / AC: Works as inventoried; AC-28.1
Status: IIV
Evidence: O:DOC; S: docs/foundation/LOCAL_DEMO.md lists average order value in Reports
Validation: V1
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12; G7
────────────────────────────────────────
Master ID: MA-ANA-011
Domain: Analytics
Functionality: Returning customer rate / cohorts
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-012
Domain: Analytics
Functionality: Sessions, conversion rate, traffic sources
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-093
Disposition: NO ACTION
Rationale: R3: storefront analytics (see MF-093)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-013
Domain: Analytics
Functionality: Live view
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-014
Domain: Analytics
Functionality: Product analysis: ABC, sell-through, days of inventory
Expected behaviour / AC: Subject to decision; AC-28.1
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: BLOCKED-DEC
Rationale: Blocked: Zoho stock
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ANA-015
Domain: Analytics
Functionality: Finance: payments, taxes, payouts
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3: provider settlement; settlement is not a dispatch gate
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-016
Domain: Analytics
Functionality: Tax / GST summary report
Expected behaviour / AC: Subject to decision; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; MF-054
Disposition: BLOCKED-DEC
Rationale: Blocked: GST mapping open
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ANA-017
Domain: Analytics
Functionality: Custom reports / saved reports
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-018
Domain: Analytics
Functionality: Report export and scheduling
Expected behaviour / AC: Recommended, not approved; AC-28.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; CG-017
Disposition: IMPLEMENT
Rationale: R2: export; inventory defers scheduling
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-ANA-019
Domain: Analytics
Functionality: Bulk-customer savings report
Expected behaviour / AC: Subject to decision; AC-28.1
Status: BLK
Evidence: O:—
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4; §10.13, §28.2
Source IDs: SA-A18; SA-A19
Disposition: BLOCKED-DEC
Rationale: Blocked: no reason recorded in the inventory; SPEC §28.2 requires Bulk customers to see cumulative savings
Evidence gap: G9
────────────────────────────────────────
Master ID: MA-ANA-020
Domain: Analytics
Functionality: Search-terms report
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19; CG-017
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-021
Domain: Analytics
Functionality: Behaviour reports: conversion, bounce, landing pages, device, search terms with no results, search …
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3: with ANA-012
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-022
Domain: Analytics
Functionality: Customer reports: RFM analysis and list, predicted spend tiers, one-time customers, returning …
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-023
Domain: Analytics
Functionality: Finance reports: finance summary, gross profit by order, cost of goods sold, net payments by …
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3: needs cost and settlement data
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-024
Domain: Analytics
Functionality: Acquisition reports: sessions by referrer/location, visitors
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-ANA-025
Domain: Analytics
Functionality: Inventory report: ABC product analysis
Expected behaviour / AC: Subject to decision; AC-28.1
Status: BLK
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: BLOCKED-DEC
Rationale: Blocked: Zoho stock, DC-17
Evidence gap: -
────────────────────────────────────────
Master ID: MA-ANA-026
Domain: Analytics
Functionality: Storefront-agent (AI) session and conversation reports
Expected behaviour / AC: None (excluded); AC-28.1
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-ANA-027
Domain: Analytics
Functionality: Pin a report; report library by category
Expected behaviour / AC: Not required; AC-28.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §28.4
Source IDs: SA-A18; SA-A19
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2

§5 covers MA-CNT-001 to MA-ANA-027 (69 rows). Two points on the paste:
- MA-ANA-019 (Bulk-customer savings report): I flagged this row because SPEC §28.2 requires Bulk customers to see
  cumulative savings, so a customer-facing view is required. It is not a Shopify-only concept, and the inventory
  blocked it without a reason.
- MF-086 (blog): Blog posts are Admin content pages of kind BLOG, so the "no blog editor" statements in Comparisons 2,
  3 and 4 are wrong. Only the /blog/ 404 remains.

Next is §6 (Settings, Integrations, Staff and System).

  Ran 1 shell command

§6 Shopify Admin capabilities: Settings, Integrations, Staff and System (MA-SET-001 to MA-SYS-022, 102 rows)

Notes for this section:
- Source IDs for MA-SET-*: Comparison 1 mapped the whole SET family to several settings areas. I abbreviate the long
  list to SA-A22 to A33 and keep any specific CG or MF links. SA-A30 is the notification-settings area and applies to
  SET-021 and SET-022.
- Payment-provider wording: Rows that name Razorpay (SET-005, INT-002, and ORD-044 earlier) reflect the Shopify store.
  The selected EffyKlean provider is Zoho Payments (CR-007), so their EffyKlean counterpart is MF-043/MF-051.
- MA-SET-023 stale text: The inventory says "AD-07 not yet built", but AD-07 is now built locally (2026-10-11).

Master ID: MA-SET-001
Domain: Settings
Functionality: General: store name, contact e-mail and phone, address
Expected behaviour / AC: Subject to decision
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-06
SPEC / decision: no direct clause (SPEC §4.1 canonical contact)
Source IDs: SA-A22–A33
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-06
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-002
Domain: Settings
Functionality: General: currency, time zone, units
Expected behaviour / AC: None (excluded); AC-2.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §2, §30
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.1 (INR, IST fixed)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-003
Domain: Settings
Functionality: Brand assets: logo, colours, slogan, social links
Expected behaviour / AC: Not required
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-004
Domain: Settings
Functionality: Plan, billing, subscription
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only (self-hosted)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-005
Domain: Settings
Functionality: Payments: Razorpay settings
Expected behaviour / AC: Recommended, not approved; AC-12.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-15
SPEC / decision: §12 (CR-007: Zoho Payments)
Source IDs: SA-A22–A33; MF-043
Disposition: IMPLEMENT
Rationale: R2: after DC-15
Evidence gap: G3; row wording predates CR-007
────────────────────────────────────────
Master ID: MA-SET-006
Domain: Settings
Functionality: Payments: capture mode
Expected behaviour / AC: Subject to decision; AC-12.x
Status: UNV
Evidence: O:OBS
Validation: V0
Dependency / blocker: ORD-078
SPEC / decision: §12
Source IDs: SA-A22–A33
Disposition: BLOCKED-DEC
Rationale: Blocked: not recorded
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-007
Domain: Settings
Functionality: Payments: manual payment methods
Expected behaviour / AC: Subject to decision; AC-12.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-22
SPEC / decision: §12.10, §12.11
Source IDs: SA-A22–A33; MF-064
Disposition: BLOCKED-DEC
Rationale: Blocked: after DC-22 (SPEC allows bank transfer/UPI for Distributor/Bulk)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-008
Domain: Settings
Functionality: Payments: COD
Expected behaviour / AC: None (excluded); AC-12.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §12; §3.9
Source IDs: SA-A22–A33; MF-042
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.9 (COD removed in v0.7)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-009
Domain: Settings
Functionality: Payments: PayPal / alternative gateways
Expected behaviour / AC: None (excluded); AC-12.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §12
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: SPEC §12.1 (Zoho Payments is the selected provider; Razorpay not a fallback per project record);
inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-010
Domain: Settings
Functionality: Payment customizations (hide / reorder methods)
Expected behaviour / AC: Not required; AC-12.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §12
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-011
Domain: Settings
Functionality: Checkout settings: required fields, GST fields, order notes
Expected behaviour / AC: Not required; AC-11.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §11
Source IDs: SA-A22–A33; SA-A25
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-012
Domain: Settings
Functionality: Checkout customisation
Expected behaviour / AC: None (excluded); AC-11.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §11
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: unavailable on the plan
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-013
Domain: Settings
Functionality: Customer accounts settings (sign-in type, self-serve returns, store credit)
Expected behaviour / AC: Not required; AC-19.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: D-D1
SPEC / decision: §19
Source IDs: SA-A22–A33; SA-A26
Disposition: NO ACTION
Rationale: R3: D-D1
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-014
Domain: Settings
Functionality: Shipping profiles, zones, rates
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A22–A33; MF-044
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.8 (no shipping charge)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-015
Domain: Settings
Functionality: Packages and packing slip template
Expected behaviour / AC: Not required; AC-18.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-19
SPEC / decision: §18
Source IDs: SA-A22–A33; MF-074
Disposition: NO ACTION
Rationale: R3: DC-19
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-016
Domain: Settings
Functionality: Local delivery and pickup
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: off on the store
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-017
Domain: Settings
Functionality: Carrier accounts / shipping labels
Expected behaviour / AC: Not required; AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-18
SPEC / decision: §18
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: Shiprocket, DC-18
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-018
Domain: Settings
Functionality: Taxes: GST rates and state overrides
Expected behaviour / AC: Subject to decision; AC-13.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A22–A33; MF-054
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: GST mapping
Evidence gap: Genuine ambiguity per inventory
────────────────────────────────────────
Master ID: MA-SET-019
Domain: Settings
Functionality: Duties at checkout
Expected behaviour / AC: None (excluded); AC-13.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.1 (domestic only)
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-020
Domain: Settings
Functionality: Locations
Expected behaviour / AC: None (excluded); AC-18.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §18
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: HU decision, locations settled (PROJECT_LOG); no EffyKlean location settings
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-021
Domain: Settings
Functionality: Notifications: customer e-mail templates (confirmation, shipping, cancel, refund, payment error)
Expected behaviour / AC: Subject to decision; AC-12.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §20
Source IDs: SA-A22–A33; SA-A30; CG-007; MF-079
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-21
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-022
Domain: Settings
Functionality: Notifications: staff e-mails (new order, store summary, disputes)
Expected behaviour / AC: Subject to decision; AC-20.x
Status: BLK
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §20
Source IDs: SA-A22–A33; SA-A30; CG-007; MF-079
Disposition: BLOCKED-DEC
Rationale: Blocked: DC-21
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-023
Domain: Settings
Functionality: Notifications: order-creation webhook
Expected behaviour / AC: Not required; AC-20.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: AD-07
SPEC / decision: §20
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: Excluded/not applicable: by design
Evidence gap: Inventory text "AD-07 not yet built" is stale (AD-07 now built)
────────────────────────────────────────
Master ID: MA-SET-024
Domain: Settings
Functionality: Notification SMS / WhatsApp templates
Expected behaviour / AC: Not required; AC-20.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §20; §3.3
Source IDs: SA-A22–A33; MF-094
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory: Shiprocket WhatsApp stays; SPEC §3.3 excludes SMS
Evidence gap: G7
────────────────────────────────────────
Master ID: MA-SET-025
Domain: Settings
Functionality: Apps and sales channels settings
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33; MF-116
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2 (no Shopify dependency); inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-026
Domain: Settings
Functionality: Domains
Expected behaviour / AC: None (excluded); AC-2.1
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §2, §30
Source IDs: SA-A22–A33; MF-107
Disposition: REJECT/OOS
Rationale: Basis: Shopify domain settings have no EffyKlean equivalent; the real domain/hosting task is MF-107;
inventory notes effyklean.in attached with invalid DNS (migration)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-027
Domain: Settings
Functionality: Customer events (pixels)
Expected behaviour / AC: Not required
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33; MF-093
Disposition: NO ACTION
Rationale: R3 (see MF-093: consent first)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-028
Domain: Settings
Functionality: Metafields and metaobjects definitions
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-029
Domain: Settings
Functionality: Languages
Expected behaviour / AC: Not required; AC-2.1
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §2, §30
Source IDs: SA-A22–A33; MF-094
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-030
Domain: Settings
Functionality: Customer privacy: cookie banner, data requests, consent
Expected behaviour / AC: Subject to decision; AC-23.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §23, §26.2
Source IDs: SA-A22–A33; MF-093
Disposition: BLOCKED-DEC
Rationale: Blocked: legal text from HU
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-031
Domain: Settings
Functionality: Policies: refund, privacy, terms, shipping, contact
Expected behaviour / AC: Recommended, not approved; AC-18.x
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-24
SPEC / decision: §23
Source IDs: SA-A22–A33; MF-084; MF-085
Disposition: IMPLEMENT
Rationale: R2: per DC-24; text is HU's (see MF-084: blocked)
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-SET-032
Domain: Settings
Functionality: Gift cards settings
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause; §3.2
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-033
Domain: Settings
Functionality: Order ID prefix / auto-archive
Expected behaviour / AC: Works as inventoried
Status: PART
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §15 (EKI order ID)
Source IDs: SA-A22–A33; MA-ORD-107
Disposition: VALIDATE
Rationale: Inventory says covered
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-034
Domain: Settings
Functionality: Feature previews / labs
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-SET-035
Domain: Settings
Functionality: Store activity log
Expected behaviour / AC: Works as inventoried
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §26.3
Source IDs: SA-A22–A33; MF-098
Disposition: VALIDATE
Rationale: Inventory says covered: audit trail exists
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-050
Domain: Settings
Functionality: Transfer or move the store to an organization / external owner
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-052
Domain: Settings
Functionality: Billing: list of bills (number, date, reason, total, status)
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-055
Domain: Settings
Functionality: Taxes: "Global collected tax report"
Expected behaviour / AC: Subject to decision; AC-13.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §13
Source IDs: SA-A22–A33; MF-054
Disposition: BLOCKED-DEC
Rationale: Blocked: GST mapping open
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-056
Domain: Settings
Functionality: Taxes: country of origin and HS codes recorded on 0 of 66 variants
Expected behaviour / AC: Subject to decision; AC-13.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §13.9
Source IDs: SA-A22–A33; MA-PRD-039
Disposition: BLOCKED-DEC
Rationale: Blocked: confirms no HSN data in Shopify
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-057
Domain: Settings
Functionality: Legal notice policy (not set)
Expected behaviour / AC: Not required; AC-23.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23, §26.2
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: R3: legal text is HU's
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-058
Domain: Settings
Functionality: Privacy: "Shopify Network Intelligence" (enabled)
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23, §26.2
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: Shopify-only service; AC-1.2 (no Shopify dependency)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-059
Domain: Settings
Functionality: Privacy: double opt-in for marketing; e-mail and SMS marketing in checkout
Expected behaviour / AC: Not required; AC-11.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §11
Source IDs: SA-A22–A33; MF-090
Disposition: NO ACTION
Rationale: R3: DC-21 (EffyKlean subscribe already uses mailbox verification)
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-060
Domain: Settings
Functionality: Policies: "Default rules" for policy pages
Expected behaviour / AC: None (excluded); AC-23.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §23, §26.2
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-061
Domain: Settings
Functionality: Staff notification: "Fulfillment request notification" to a fulfilment service
Expected behaviour / AC: None (excluded); AC-20.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §20
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: SPEC §18.3 (Zoho/Shiprocket own fulfilment); inventory
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-070
Domain: Settings
Functionality: Payment customization "Hides COD payment method for non-MagicX shipping methods" (active)
Expected behaviour / AC: None (excluded); AC-12.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §12; §3.9
Source IDs: SA-A22–A33; MF-042
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.9 (COD); informational evidence that COD rules exist in Shopify
Evidence gap: -
────────────────────────────────────────
Master ID: MA-SET-071
Domain: Settings
Functionality: Razorpay Magic Checkout (one-click checkout)
Expected behaviour / AC: Not required; AC-11.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-15
SPEC / decision: §11
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: R3: separate Razorpay product; provider is now Zoho Payments (CR-007); SPEC silent
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-072
Domain: Settings
Functionality: Customer sign-in connections: Google, Facebook
Expected behaviour / AC: Not required; AC-19.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: D-D1
SPEC / decision: §19
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: R3: with the sign-in decision
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-073
Domain: Settings
Functionality: Packing slip template (editable HTML/Liquid; ship-to, PO number, order name)
Expected behaviour / AC: Not required
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-038
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: NO ACTION
Rationale: R3: with ORD-038
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-074
Domain: Settings
Functionality: Metafield definitions in use: product boosts, related and complementary products, Google custom …
Expected behaviour / AC: None (excluded)
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: no direct clause
Source IDs: SA-A22–A33
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory: unused
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SET-075
Domain: Settings
Functionality: Languages: English published (4 domains); Hindi, Kannada, Malayalam, Marathi, Tamil, Telugu …
Expected behaviour / AC: Not required; AC-2.1
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §2, §30
Source IDs: SA-A22–A33; MF-094
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SET-076
Domain: Settings
Functionality: Payment capture method (label only; value not readable)
Expected behaviour / AC: Subject to decision; AC-12.x
Status: UNV
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-078
SPEC / decision: §12
Source IDs: SA-A22–A33
Disposition: BLOCKED-DEC
Rationale: Blocked: value hidden in a nested control
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INT-001
Domain: Integrations & apps
Functionality: Integration readiness checks
Expected behaviour / AC: Works as inventoried; AC-24.1; AC-25.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-INT-002
Domain: Integrations & apps
Functionality: Payment webhook log (inventory wording: Razorpay)
Expected behaviour / AC: Works as inventoried; AC-24.1; AC-25.x
Status: IIV
Evidence: O:—
Validation: V0S
Dependency / blocker: -
SPEC / decision: §24, §25; §12.19
Source IDs: SA-A32; MF-051
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10; G9
────────────────────────────────────────
Master ID: MA-INT-003
Domain: Integrations & apps
Functionality: Reconciliation queue
Expected behaviour / AC: Works as inventoried; AC-24.1; AC-25.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-066
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-INT-004
Domain: Integrations & apps
Functionality: Outbox / worker view
Expected behaviour / AC: Recommended, not approved; AC-24.1; AC-25.x
Status: PART
Evidence: O:—; S: AD-07 built; no outbox list route
Validation: V1
Dependency / blocker: AD-07
SPEC / decision: §24, §25
Source IDs: SA-A32; CG-010; MF-099; C1 SA-D
Disposition: IMPLEMENT
Rationale: R2: when AD-07 is built
Evidence gap: G3; G9
────────────────────────────────────────
Master ID: MA-INT-005
Domain: Integrations & apps
Functionality: Zoho mapping health and sync status
Expected behaviour / AC: Recommended, not approved; AC-24.1; AC-25.x
Status: PART
Evidence: O:—
Validation: V0
Dependency / blocker: DC-17
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: IMPLEMENT
Rationale: R2: after DC-17
Evidence gap: G3; G9
────────────────────────────────────────
Master ID: MA-INT-006
Domain: Integrations & apps
Functionality: Shiprocket status
Expected behaviour / AC: Works as inventoried; AC-24.1; AC-25.x
Status: IIV
Evidence: O:—
Validation: V0S
Dependency / blocker: DC-18
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-071
Disposition: VALIDATE
Rationale: R5
Evidence gap: G10; G9
────────────────────────────────────────
Master ID: MA-INT-007
Domain: Integrations & apps
Functionality: App store / marketplace
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-116
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2 (no Shopify dependency); CLAUDE.md principle 5 (no extra SaaS); inventory
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INT-008
Domain: Integrations & apps
Functionality: Custom/private apps and API tokens
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INT-009
Domain: Integrations & apps
Functionality: Shopify Flow
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-116
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2; inventory recommendation only (contents UNK)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INT-010
Domain: Integrations & apps
Functionality: Webhook subscriptions config
Expected behaviour / AC: Not required; AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: NO ACTION
Rationale: Shopify-only or excluded; deferred in inventory
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INT-011
Domain: Integrations & apps
Functionality: Zoho Flow workflows
Expected behaviour / AC: Subject to decision; AC-24.1; AC-25.x
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-063
Disposition: BLOCKED-DEC
Rationale: Inventory FLAG: contents unknown; inspect before any change
Evidence gap: Genuine ambiguity per inventory; G11
────────────────────────────────────────
Master ID: MA-INT-020
Domain: Integrations & apps
Functionality: Flow workflows: eight Shopify-template marketing workflows (welcome discount e-mail, thank …
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: ORD-110
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: REJECT/OOS
Rationale: Basis: SPEC §3.14 (no campaign engine) for the marketing flows; abandoned-cart/welcome flows relate to
ORD-110
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INT-021
Domain: Integrations & apps
Functionality: Flow: workflow tags, last run, version history
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-INT-022
Domain: Integrations & apps
Functionality: "EffyZohoFlow" custom app and "Zoho Inventory" app (names only; configuration deliberately not read)
Expected behaviour / AC: Subject to decision; AC-24.1; AC-25.x
Status: UNV
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32; MF-063
Disposition: BLOCKED-DEC
Rationale: Blocked: credential risk
Evidence gap: -
────────────────────────────────────────
Master ID: MA-INT-023
Domain: Integrations & apps
Functionality: App row menu: open, view details, get support, uninstall
Expected behaviour / AC: None (excluded); AC-24.1; AC-25.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §24, §25
Source IDs: SA-A32
Disposition: REJECT/OOS
Rationale: Basis: AC-1.2; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-001
Domain: Staff & security
Functionality: Staff list
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:UNK
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G11
────────────────────────────────────────
Master ID: MA-USR-002
Domain: Staff & security
Functionality: Deactivate / reactivate staff
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:UNK
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G11
────────────────────────────────────────
Master ID: MA-USR-003
Domain: Staff & security
Functionality: Create staff / invite
Expected behaviour / AC: Subject to decision; AC-5.1; AC-26.x; AC-27.x
Status: BLK
Evidence: O:UNK
Validation: V0
Dependency / blocker: D-F2
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; CG-015; MF-104
Disposition: BLOCKED-DEC
Rationale: Blocked: D-F2
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-USR-004
Domain: Staff & security
Functionality: Reset staff MFA
Expected behaviour / AC: Subject to decision; AC-5.1; AC-26.x; AC-27.x
Status: BLK
Evidence: O:UNK
Validation: V0
Dependency / blocker: D-F2
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; CG-015; MF-104
Disposition: BLOCKED-DEC
Rationale: Blocked: D-F2
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-USR-005
Domain: Staff & security
Functionality: Roles (Admin, Director)
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:UNK
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G11
────────────────────────────────────────
Master ID: MA-USR-006
Domain: Staff & security
Functionality: Granular per-area permissions
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:UNK
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: SPEC §27.4 defers detailed permission matrices; inventory recommendation REJECT (Part 1 K4)
Evidence gap: G8; G11
────────────────────────────────────────
Master ID: MA-USR-007
Domain: Staff & security
Functionality: Permission matrix confirm
Expected behaviour / AC: Subject to decision; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:UNK
Validation: V0B
Dependency / blocker: D-F1
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: BLOCKED-DEC
Rationale: Blocked: D-F1
Evidence gap: G11
────────────────────────────────────────
Master ID: MA-USR-008
Domain: Staff & security
Functionality: Staff sign-in with MFA, lockout
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:UNK
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; MF-096
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G11
────────────────────────────────────────
Master ID: MA-USR-009
Domain: Staff & security
Functionality: Recovery codes
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; MF-096
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-USR-010
Domain: Staff & security
Functionality: Own account: profile, password, sessions
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:DOC; S: account.html password, sessions, recent sign-in activity
Validation: V1
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12; G7
────────────────────────────────────────
Master ID: MA-USR-011
Domain: Staff & security
Functionality: Staff activity / sign-in history
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:OBS-L; S: route staff/<pk>/signins
Validation: V1
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-USR-012
Domain: Staff & security
Functionality: Collaborator accounts (agencies)
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: SPEC §5.1 (exactly five business roles plus staff roles); inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-013
Domain: Staff & security
Functionality: Staff permission to see cost, reports, export
Expected behaviour / AC: Not required; AC-5.1; AC-26.x; AC-27.x
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2; G7
────────────────────────────────────────
Master ID: MA-USR-020
Domain: Staff & security
Functionality: Users: tabs Active, Pending, POS app-only, Requests; roles Store owner, Administrator and a custom …
Expected behaviour / AC: Subject to decision; AC-5.1; AC-26.x; AC-27.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: BLOCKED-DEC
Rationale: Blocked: permissions now read; see SHOPIFY_ADMIN_FLAGGED_ISSUES_INVESTIGATION.md §3
Evidence gap: -
────────────────────────────────────────
Master ID: MA-USR-021
Domain: Staff & security
Functionality: Per-user "secure sign-in method required" flag
Expected behaviour / AC: Works as inventoried; AC-5.1; AC-26.x; AC-27.x
Status: IIV
Evidence: O:OBS-L
Validation: V0B
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23; MF-096
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1
────────────────────────────────────────
Master ID: MA-USR-022
Domain: Staff & security
Functionality: Permission "Requests" tab (staff asking for access)
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-023
Domain: Staff & security
Functionality: POS app-only users
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found; inventory recommendation only
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-030
Domain: Staff & security
Functionality: Roles page: 17 roles in three categories (store, organization, point of sale), "Add role" for …
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: SPEC §27.4 defers detailed permission matrices; inventory: custom role builder, see USR-031
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-031
Domain: Staff & security
Functionality: Role permission catalogue (e.g. orders: edit, apply discounts, set payment terms, charge card …)
Expected behaviour / AC: None (excluded); AC-5.1; AC-26.x; AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: REJECT/OOS
Rationale: Basis: inventory: per-permission editing rejected, but usable as input to a role review (the "§13" in the
inventory note is the issues record, not SPEC)
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-USR-032
Domain: Staff & security
Functionality: Users: "Security" page (monitor user activity, collaborator request code)
Expected behaviour / AC: Recommended, not approved; AC-5.1; AC-26.x; AC-27.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §5.4, §26, §27.4
Source IDs: SA-A23
Disposition: IMPLEMENT
Rationale: R2: activity monitoring as K3; inventory rejects collaborators
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-SYS-001
Domain: System & search
Functionality: Audit trail viewer
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34; MF-098
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-SYS-002
Domain: System & search
Functionality: Audit export
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:—; S: route audit/export
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34; MF-098; C1 SA-D
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-SYS-003
Domain: System & search
Functionality: Global search
Expected behaviour / AC: Recommended, not approved; AC-27.x
Status: PART
Evidence: O:OBS; S: route search, search.html (orders, customers, products)
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34
Disposition: IMPLEMENT
Rationale: R2: Part 1 M3 (a search page exists; scope vs recommendation not compared)
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-SYS-004
Domain: System & search
Functionality: Command palette / keyboard shortcuts
Expected behaviour / AC: Not required; AC-27.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SYS-005
Domain: System & search
Functionality: Notification centre
Expected behaviour / AC: Not required; AC-27.x
Status: MISS
Evidence: O:OBS
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §27
Source IDs: SA-A34; CG-020
Disposition: NO ACTION
Rationale: R3: DC-21
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SYS-006
Domain: System & search
Functionality: Home to-do overview
Expected behaviour / AC: Recommended, not approved; AC-27.x
Status: PART
Evidence: O:OBS; S: dashboard.html "To do"
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A01; SA-A34
Disposition: IMPLEMENT
Rationale: R2: Part 1 A1 (a "To do" panel exists; completeness unverified)
Evidence gap: G3
────────────────────────────────────────
Master ID: MA-SYS-007
Domain: System & search
Functionality: Home recent activity
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:OBS; S: dashboard.html "Recent activity"
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A01; SA-A34; CG-020; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-SYS-008
Domain: System & search
Functionality: Home business metrics
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:OBS; S: dashboard.html "Business figures"
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A01; SA-A34; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-SYS-009
Domain: System & search
Functionality: Setup guide / promotions
Expected behaviour / AC: None (excluded); AC-27.x
Status: EXC
Evidence: O:OBS
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34
Disposition: REJECT/OOS
Rationale: Basis: Shopify-only; AC-1.2; inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SYS-010
Domain: System & search
Functionality: AI assistant (Sidekick)
Expected behaviour / AC: None (excluded); AC-27.x
Status: EXC
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34
Disposition: REJECT/OOS
Rationale: Basis: Shopify-only; AC-1.2; inventory recommendation
Evidence gap: G8
────────────────────────────────────────
Master ID: MA-SYS-011
Domain: System & search
Functionality: Help centre / support link
Expected behaviour / AC: Not required; AC-27.x
Status: MISS
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A34
Disposition: NO ACTION
Rationale: R3
Evidence gap: G2; G7
────────────────────────────────────────
Master ID: MA-SYS-012
Domain: System & search
Functionality: Responsive accessible shell
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:—
Validation: V0B
Dependency / blocker: -
SPEC / decision: §27
Source IDs: -
Disposition: VALIDATE
Rationale: R1
Evidence gap: G1; G9
────────────────────────────────────────
Master ID: MA-SYS-013
Domain: System & search
Functionality: Multi-store switcher
Expected behaviour / AC: None (excluded); AC-27.x
Status: EXC
Evidence: O:DOC
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: -
Disposition: REJECT/OOS
Rationale: Basis: no EffyKlean requirement found (single store); inventory recommendation only
Evidence gap: G8; G7
────────────────────────────────────────
Master ID: MA-SYS-020
Domain: System & search
Functionality: Home: Alerts feed (unread count, "view unread only")
Expected behaviour / AC: Not required; AC-27.x
Status: MISS
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: DC-21
SPEC / decision: §27
Source IDs: SA-A01; CG-020
Disposition: NO ACTION
Rationale: R3: same as SYS-005
Evidence gap: G2
────────────────────────────────────────
Master ID: MA-SYS-021
Domain: System & search
Functionality: Recents list in search
Expected behaviour / AC: Works as inventoried; AC-27.x
Status: IIV
Evidence: O:OBS-L; S: search.html "Recent searches"
Validation: V1
Dependency / blocker: -
SPEC / decision: §27
Source IDs: Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-SYS-022
Domain: System & search
Functionality: Home: last-30-days sessions, sales, orders, conversion and live visitors cards
Expected behaviour / AC: Recommended, not approved; AC-27.x
Status: PART
Evidence: O:OBS-L
Validation: V0
Dependency / blocker: -
SPEC / decision: §27
Source IDs: SA-A01
Disposition: IMPLEMENT
Rationale: R2: sales and orders (as SYS-008); inventory defers traffic
Evidence gap: G3

§6 covers MA-SET-001 to MA-SYS-022 (102 rows). I made a few edits while pasting, listed here so they can be traced:
- MA-SET-009 and MA-INT-007/008/009/021/023: I added AC-1.2 as part of the basis.
- MA-USR-006 and MA-USR-030: The basis is now SPEC §27.4, which defers detailed permission matrices. The earlier SPEC
  §13 cite was a false match.
- MA-USR-012: The basis is SPEC §5.1.
- MA-SYS-003 and MA-SYS-006: I noted the existing search route and the dashboard "To do" panel.

§4 addendum: rows superseding §4

Master ID: MA-CUS-003
Domain: Customers & B2B
Functionality: Filter customers (location, orders, spend, consent)
Expected behaviour / AC: Works as inventoried; AC-20.5; AC-26.x
Status: IIV
Evidence: O:OBS; S: customers.html filters: location, consent, orders, spend, tag
Validation: V1
Dependency / blocker: -
SPEC / decision: §20.5, §26.2
Source IDs: SA-A09; CG-019; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-CUS-019
Domain: Customers & B2B
Functionality: Customer timeline
Expected behaviour / AC: Works as inventoried; AC-19.x; AC-26.x
Status: IIV
Evidence: O:OBS; S: customer_detail.html "Timeline"
Validation: V1
Dependency / blocker: -
SPEC / decision: §19, §26.2
Source IDs: SA-A09; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-DSC-002
Domain: Discounts
Functionality: Search and status tabs
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS; S: discounts.html search and Status filter
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7
Source IDs: SA-A12; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-DSC-003
Domain: Discounts
Functionality: Filter by date, type, method
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS; S: discounts.html Created from/to, Type
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7
Source IDs: SA-A12; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-DSC-019
Domain: Discounts
Functionality: Used count and sales total
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS; S: discounts.html "Used", "Sales", "Discount given"
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7
Source IDs: SA-A12; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12
────────────────────────────────────────
Master ID: MA-DSC-040
Domain: Discounts
Functionality: Discount list filters (status, type, method, sales channel) and sort
Expected behaviour / AC: Works as inventoried; AC-21.x; AC-7.x
Status: IIV
Evidence: O:OBS-L; S: discounts.html search, Status, Type, date filters
Validation: V1
Dependency / blocker: -
SPEC / decision: §21, §7
Source IDs: SA-A12; Δ2
Disposition: VALIDATE
Rationale: R1
Evidence gap: G12

Now the reconciliation in §7. First I'll compute exact counts.

  Ran 3 shell commands

§7 Coverage reconciliation

Corrected row. The following supersedes MF-086 in §1, because blog posts are Admin content pages of kind BLOG.

Master ID: MF-086
Domain: Content / blog
Functionality: Blog index and posts (3 posts in media/blog_source); blog posts are Admin content pages of kind BLOG
Expected behaviour / AC: Content per §23
Status: PART
Evidence: V4: /blog/ 404; S: blog route exists; content_views supports kind BLOG with post_date
Validation: V4; V1
Dependency / blocker: Cause of 404 (likely no published BLOG page in the running instance)
SPEC / decision: SPEC §23
Source IDs: C3 EC-P26..P29; C2 BR-B01..B12, BR-F15, BR-L18; C4 CG-022; C1 CNT-006, CNT-007
Disposition: FIX
Rationale: Route exists but returns 404 in the running instance; Comparisons 2, 3 and 4 wrongly said Admin has no blog
editor
Evidence gap: Cause unverified

7.1 Rows reviewed per source

┌──────────────┬───────────────┬──────────────────────────────────────────────────────────────────────────────────┐
│    Source    │ Original rows │                                      Notes                                       │
│              │    reviewed   │                                                                                  │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│              │               │ 494 inventory function rows (Appendix A), 34 area rows (SA-A01 to SA-A34) and 16 │
│ Comparison 1 │ 544           │  re-verified deltas (SA-D01 to SA-D16). The inventory also holds 12 decision-log │
│              │               │  rows, which are not in Comparison 1.                                            │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ Comparison 2 │ 128           │ BR-P 18, BR-PR 5, BR-L 21, BR-C 43, BR-B 12, BR-F 20, BR-W 9.                    │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ Comparison 3 │ 98            │ EC-P 38, EC-X 12, EC-L 12, EC-F 19, EC-W 11, EC-V 6.                             │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ Comparison 4 │ 36            │ CG-001 to CG-036.                                                                │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ Readiness    │ 76            │ A-01 to J-10.                                                                    │
│ register     │               │                                                                                  │
├──────────────┼───────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ Total        │ 882           │                                                                                  │
└──────────────┴───────────────┴──────────────────────────────────────────────────────────────────────────────────┘

7.2 Unique master rows produced

597 in total. Of these, 103 are MF rows (platform and cross-cutting functions, with 17 more of them still sitting in §1
as UNV) and 494 are MA rows (the Shopify Admin capabilities, one per inventory row, 1:1 with the original IDs).

┌─────────────┬──────┐
│ Disposition │ Rows │
├─────────────┼──────┤
│ NO ACTION   │ 180  │
├─────────────┼──────┤
│ VALIDATE    │ 137  │
├─────────────┼──────┤
│ BLOCKED-DEC │ 120  │
├─────────────┼──────┤
│ REJECT/OOS  │ 117  │
├─────────────┼──────┤
│ IMPLEMENT   │ 41   │
├─────────────┼──────┤
│ FIX         │ 2    │
└─────────────┴──────┘

┌────────┬──────┐
│ Status │ Rows │
├────────┼──────┤
│ MISS   │ 154  │
├────────┼──────┤
│ EXC    │ 148  │
├────────┼──────┤
│ IIV    │ 131  │
├────────┼──────┤
│ BLK    │ 68   │
├────────┼──────┤
│ PART   │ 46   │
├────────┼──────┤
│ IVV    │ 33   │
├────────┼──────┤
│ UNV    │ 17   │
└────────┴──────┘

Per family, the dispositions are: Orders NO ACTION 45 / VALIDATE 20 / IMPLEMENT 13 / REJECT 22 / BLOCKED 19. Products
NO ACTION 24 / VALIDATE 28 / IMPLEMENT 6 / REJECT 16 / BLOCKED 13. Draft orders BLOCKED 12 / REJECT 1 (the shipping
line). The MF rows have BLOCKED 35 / NO ACTION 28 / VALIDATE 24 / IMPLEMENT 9 / FIX 2 / REJECT 5.

7.3 Original IDs mapped to master rows

- Inventory IDs (ORD-001 etc.): One-to-one onto MA-<ID>, so 494 maps to 494. The 12 decision-log rows (Orders batch 1)
  are folded into MA-ORD-001 to MA-ORD-012.
- Comparison 1 areas: The 34 SA-A rows attach to the MA rows of their family as Source IDs, and the 16 SA-D rows are
  marked C1 SA-D on the rows they re-verified. SA-A21 (Settings > General) has no explicit listing because its
  inventory range was "SET-001.."; it corresponds to MA-SET-001 to MA-SET-003. The MA-SET rows list SA-A22–A33 (some of
  those should read SA-A21–A33).
- BRM rows (128): All map to 33 MF rows. Highlights:
  - 43 collections and 12 blogs collapse into MF-032 and MF-086.
  - 20 BRM functions go to MF-021/022/024/027/029/033/034/040/045/072/082/090 and others.
  - Pages and links go to the matching content, account, cart and policy rows.
- Storefront rows (98): All map to 37 MF rows. Highlights:
  - 15 product pages and the catalogue feed collapse into MF-020/023.
  - The 5 policy pages collapse into MF-084.
  - The .in-only routes map to MF-040/041/072/075/082/089/090/117.
  - The 6 visual rows map to MF-007.
- Consolidated gaps (36): All 36 are mapped. 31 map to MF rows and 15 map to MA rows. 10 map to both, and 5 map only to
  MA rows (CG-011, CG-017, CG-019, CG-020, CG-021).
- Register rows (76): All 76 are cited, in 74 MF rows (A-01 and A-06 share MF-001).

7.4 Duplicates consolidated

338 comparison and register rows (128 BRM, 98 storefront, 36 gaps, 76 register) collapse into the 103 MF rows. 37 BRM
or storefront IDs are cited by more than one MF row, so the overlap is traceable in both directions. The detail:
- 43 BRM collections, 12 BRM blogs and 21 BRM navigation links collapse into 3 master rows.
- 15 product pages and 5 policy pages collapse into 2 each.
- The MA side has no duplicates (1:1 with the inventory). Admin-side overlaps with the register (for example H-01 to
  H-04, I-01 to I-03) are handled by cross-referencing MF-095 to MF-100 against the MA rows.

7.5 Rows excluded as out of scope or not applicable

117 rows are REJECT/OOS, and a further 23 EXC rows are NO ACTION (Shopify-only concepts deferred in the inventory).
- Strong basis (39 rows): a SPEC clause, an HU+DI decision or a frozen rule. The preserved exclusions are:
  - COD (§3.9): MF-042, MA-SET-008, MA-SET-070.
  - Shipping charge (§3.8): MF-044, MA-SET-014, MA-DRF-006, MA-DSC-023.
  - Combo collections (§3.11): MF-030, MA-COL-007.
  - Themes and templates: MF-116, MA-CNT-004, MA-CNT-014, MA-CNT-041, MA-PRD-046. These rest on an inventory-recorded
    "permanent exclusion", and the SPEC has no theme clause (grep found none), so this is a carried decision and not a
    SPEC sentence.
  - Returns and refunds (§3.5): MA-ORD-069, MA-ORD-071, MA-ORD-075, MA-ORD-121, MA-ORD-144.
  - Loyalty or credit (§3.2): MA-ORD-074.
  - Stock authority (§3.4): MA-ORD-062, MA-INV-003/004/005, MA-PRD-034, MA-PRD-104.
  - Locations (HU decision): MA-ORD-086/116/140, MA-INV-008, MA-SET-020.
  - Campaign engine (§3.14): MA-MKT-001/003/004, MA-CUS-023.
- Weak basis (78 rows): these rest only on the inventory's own recommendation, or on the capability being Shopify-only.
  Each says so in its Evidence gap column (G8). HU+DI may want to confirm these in bulk.

7.6 Rows not assessed, or assessed on thin evidence

- Unverified (17 rows): MF-006, MF-007, MF-008, MF-009, MF-027, MF-034, MF-065, MF-117, MA-ORD-047, MA-ORD-145,
  MA-PRD-028, MA-PRD-101, MA-PRD-102, MA-CUS-006, MA-SET-006, MA-SET-076, MA-INT-022.
- No validation this session: 365 of the 494 MA rows are V0. A further 75 rest only on an earlier browser walk (V0B),
  and 8 on a labelled simulation (V0S). Only 36 got a static check this session (V1), and 10 have HU+DI batch-1
  acceptance (V2H).
- Shopify side: nothing was re-observed. DOC-tier (36 rows) and UNK-tier (14 rows) capabilities are leads only.
- Provider side: no row has sandbox or production proof.

7.7 Conflicts flagged (not resolved), and corrections to earlier work

Conflicts for HU+DI:
- MF-026: register E-09 says related-product links are out of scope, but the storefront code renders them.
- MF-054: the SPEC GST-on-undiscounted-amount rule versus the usual tax arithmetic (register X-2).
- MF-070: SPEC §18.3 versus the existing dispatch flow, which expects a tracking reference (register X-1).
- MA-ORD-010 and MA-ORD-011: the inventory said REJECT but HU+DI decided DEFER.
- MA-ORD-067 and MA-ORD-068: the inventory rejects order edits, but orders/<ref>/edit exists.
- MF-106/MF-064/MA-DRF-*: SPEC §27.3 and §12.11 require assisted orders and bank-transfer/UPI verification, so these
  cannot be rejected as Shopify concepts.
- MA-ANA-019: SPEC §28.2 requires customer-visible Bulk savings.

Corrections to my earlier comparison documents (those files were not modified):
1. ORD-007, ORD-008, ORD-009 and ORD-012 were implemented in Orders batch 1. Comparison 1 carried them as MISS or SIM,
   and Comparison 4 CG-014 wrongly says sorting is missing.
2. Blog posts are Admin content pages of kind BLOG. Comparisons 2, 3 and 4 said there was no blog editor, which is
   wrong. Only the /blog/ 404 remains.
3. 36 MA statuses were re-verified as more implemented than recorded: the 16 from Comparison 1 plus 20 found here
   (reports, customer filters, content pages, navigation and FAQ management, dashboard panels, discount filters,
   own-account sessions). Only the existence of the route or heading was checked.
4. The same kind of staleness likely affects other rows I did not check.

7.8 Source references I could not find, or did not open

- Every Comparison 1 to 4 ID and every register ID resolved, except that SA-A21 has no per-row listing (see §7.3).
- I cited the DC-xx, D-xx and CR-xx decision IDs, and the Part 1 B8/B18/C4/F4/G6/L11 parent rows, only as they appear
  in the inventory and register. I did not re-open EFFYKLEAN_BENCHMARK_COVERAGE_MATRIX.md,
  SHOPIFY_ADMIN_FEATURE_MAPPING.md, or ARCHITECTURE.md and the individual decision records, so those references are
  carried and not independently checked.
- The AC IDs are family-level ranges (for example AC-15.x) and not per-row criteria. Mapping each row to a single AC is
  the job of the missing traceability index (MF-003).

I have made no prioritisation and no implementation change. I wrote no repository files. The full 597-row dataset also
exists as a machine-readable file in my scratchpad (…/scratchpad/out/all.json and s1.md to s6.md) if HU+DI want it.

This is a natural boundary, so run /clear after you've reviewed it. I'm waiting for HU+DI to review the inventory and the proposed dispositions.

  Ran 2 shell commands

The master inventory is complete in the response above. It has 597 master rows, in six sections plus a reconciliation. I wrote no repository files, changed no code, and staged or committed nothing. The working tree is the same 32 paths as before (17 modified, 15 untracked).

The "TASK COMPLETED" message box and sound are showing now. The box stays open until you click OK.

Corrections to earlier comparison documents. Comparisons 1, 2, 3 and 4 contain errors that I found while consolidating; I did not edit those files. Details are in §7.7.
- ORD-007, ORD-008, ORD-009 and ORD-012 are already implemented, so gap CG-014 ("order list lacks sort") is wrong for
  sorting.
- Blog posts are Admin content pages of kind BLOG, so the "no blog editor" statements are wrong. Only the /blog/ 404 remains.
- 36 Admin statuses are more implemented than recorded. I checked only that the route or heading exists, and other rows may be stale in the same way.

Conflicts for HU+DI. None of these is resolved here.
- Related-product links exist in the storefront code, but the register says they are out of scope.
- ORD-010 and ORD-011: the inventory says REJECT, but HU+DI decided DEFER.
- The GST arithmetic and shipping handoff conflicts (register X-1 and X-2) are still open.
- SPEC §27.3 requires admin-assisted orders, so the draft-order rows are BLOCKED-DEC rather than rejected.

Evidence limits
- 365 of the 494 Shopify rows have no validation this session (V0). I did not re-read ARCHITECTURE.md or the individual
  decision records.
- 78 of the 117 proposed rejections rest only on the inventory's own recommendation, and 39 rest on a SPEC clause, a decision, or a frozen rule.

The full dataset is also in my scratchpad as …/scratchpad/out/all.json and s1.md to s6.md, outside the repository. Say if you want it moved somewhere.

---

## HU+DI disposition triage update (2026-10-22)

A later HU+DI disposition triage classifies the 597 records as follows: **256 Implemented, 243 BUILD, 9 LATER, 13 INVESTIGATE, 76 EXCLUDE** (total 597). This newer tally supersedes the earlier 250-question queue as the current aggregate disposition reference.

These categories are **work dispositions**, not verified implementation or validation counts. They are not interchangeable with this file's original evidence dispositions (NO ACTION, VALIDATE, BLOCKED-DEC, REJECT/OOS, IMPLEMENT, FIX), nor do they replace individual HU YES/NO capability decisions. In particular, this register's historical evidence labels remain intact and should not be silently recoded to match the newer tally.

The 13 INVESTIGATE records are not automatically questions for Hu; first gather evidence, validate dependencies, and reconcile prior decisions. The file AgntGapAnalysis/Deferred310_Disposition_Triage_DRAFT_2026-10-22.csv is a draft aid whose row-level classifications require verification against the authoritative 597-row source/decision ledger. Do not treat it as final row-by-row evidence. Reconcile each row to its source decision or governing rule before marking the record-level synchronization complete.

The implementation plan and status register carry the same aggregate tally and the rules for follow-up. This note is an addendum; it does not claim the full row-by-row reconciliation is complete.
