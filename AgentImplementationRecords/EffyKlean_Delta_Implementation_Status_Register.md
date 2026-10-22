# EffyKlean Delta Implementation — Status Register

Single working register. Plan reference copy: `EffyKlean_Delta_Implementation_Plan_13Oct2026.md` (source commit `cdfb0ac`).
Execution authorised by HU in the 2026-10-13 execution prompt; scope clarified by the HU+DI governance clarification of 2026-10-13 (see "Authorization record" below).
Production deployment, production credentials/writes, live customer payments, production config, DNS and cutover remain NOT authorised (separate authorization required). No push, no commit without separate approval.
Decision basis for all agent-task rows: Plan §5 (all YES). Status words: Pending / In Progress / Implemented / Validated / Blocked / Excluded.
"Implemented (prior)" = code exists from earlier sessions; it has **not** been re-run on the current tree (test DB unavailable, see Blockers).

## Authorization record (HU+DI governance clarification, effective 2026-10-13)
- Wording recorded: the later HU instruction to use the reconciled Delta implementation plan, maintain the local plan copy and this register, pursue Zoho sandbox integrations and proceed without another broad assessment **authorizes controlled local implementation within the plan's existing constraints**; it supersedes the earlier checkpoint limit of read-only discovery/planning **for this defined scope only**.
- The plan copy keeps its original header ("HU review draft — not yet approved"); that header is deliberately unchanged and does not imply approval at first publication. The Delta plan is the controlling plan for controlled local implementation **from 2026-10-13 onward**. Plan copy source commit: `cdfb0ac` (unchanged).
- Not permitted without separate authorization: production deployment/credentials/writes, live customer payments, production configuration, DNS, cutover.
- Preserved: frozen SPEC, approved architecture, explicit capability NO decisions, business rules, security controls, NO PAYMENT -> NO DISPATCH. A task marked YES in Plan §5 is **not** evidence that each underlying capability has an HU YES.
- Unresolved decision-evidence audit (Plan §2.3, 122 rows) is retained; affected capability IDs are tracked individually and none is inferred. Work on a capability whose decision/governing requirement is not established is not started; material conflicts -> STOP -> REPORT -> HU+DI DECIDE.
- Documentation preparation (this register, plan copy, log entries) is **not** implementation and **not** test validation. Mock evidence and real Zoho sandbox evidence are logged separately below.

## Session 1 (2026-10-13) — environment facts (actual, measured)
- Repo root `/mnt/d/Effykleanproject`, branch `main`, HEAD `d3b9ca8`, tree clean before this register was added.
- `.env` holds only Django, DB and (historical) Razorpay keys. **No Zoho Payments, Zoho Inventory or Shiprocket credentials exist.**
- Docker daemon is not running in WSL and `sudo` needs interactive auth; no local PostgreSQL. The test suite (`scripts/ci.sh`, PostgreSQL 17) cannot run. **No tests were run this session.**

## Sandbox-first sequencing (HU, 2026-10-13) — see CHECKPOINT_2026-10-13_SANDBOX_READINESS.md
New implementation items B-14, J-03, J-02, A-03, F-01, J-08, E-07 and `orders.0022` on the dev DB are **Pending, not started**, awaiting HU+DI prioritisation after
sandbox readiness review. Provider-dependent rows (B-01, B-02, B-05..B-08, B-11, B-16, C-01, C-02, C-05, G-03/G-04, I-03/I-04) stay Blocked/Pending: stubs and mocked
tests are not sandbox evidence. Readiness discovery (documentation only) completed 2026-10-13; it validated nothing.

## Blockers requiring HU (only HU can clear)
| ID | Blocker | Affects | Needed |
|---|---|---|---|
| BLK-1 | PostgreSQL unavailable: Docker daemon not running; agent cannot start it (sudo prompt) | every code change that must be tested (Phases 0-2, all validation) | Run `! sudo service docker start` (or start Docker Desktop), then `docker compose up -d db` |
| BLK-2 (partly cleared 2026-10-13: sandbox OAuth works) | Still missing: account signing key, webhook signing key, HTTPS return URL, hosted-checkout address | B-01, B-02, B-11 | Provide client id/secret/refresh token/account id/webhook secret in git-ignored `.env`, or confirm the sandbox does not exist (then document the limitation) |
| BLK-3 (refined 2026-10-15: org, credentials, read access and tax records now exist) | Still missing: item/contact/Sales Order create permission (401 on item create), HU+DI authorisation of the first sandbox Sales Order, Zoho Flow/workflow inspection for the test org, HU+DI rule on price/MRP ownership, tax-rate applicability | B-05, B-06, B-07, B-08, B-11, C-01 | Provide in `.env`; state sandbox org id |
| BLK-4 | Shiprocket sandbox credentials not provided (plan routes shipping via Zoho; Zoho-side Shiprocket config is HU-side) | C-01, C-02, C-05 | Confirm approach / supply access |

Unaffected by BLK-2..4 once BLK-1 clears: all of Phase 0-2 and credential-free items in Phase 1, 5, 6 (partly), 7.

## Agent tasks (Plan §5; decision YES unless noted; source: Plan §5)
| Task | Phase | Status | Code / evidence | Outstanding |
|---|---|---|---|---|
| A-02 baseline review | 0 | Implemented (prior) | commit `f48cda5` | none; tree clean at start |
| A-04 full suite on committed tree | 0 | Validated (local, 2026-10-13) | run 1: 1888 passed, 6 failed; after test-only corrections: **1894 passed, 0 failed** (`scripts/ci.sh`, PostgreSQL 17, dev-DB server, `test_` database) | none; CI workflow itself still unrun |
| J-10 release gate | 0,7 | Pending | PHASE1_EXIT_GATE; rows 3,5,11 blocked | re-check at end |
| B-14 shared token cache | 1 | **Implemented 2026-10-15 (local, mocked)** | module-level per-credential cache in `integrations/zoho_payments.py` (lock, cleared on a 401), autouse test reset; test `test_the_access_token_is_shared_across_gateway_instances` | no real Zoho Payments sandbox evidence (BLK-1 unchanged) |
| J-03 scheduler definition | 1,7 | **Reconciled 2026-10-15: already implemented (Batch 1 checkpoint)** | `modules/backoffice/scheduling.py`, `show_schedule`, `run_scheduled`, `docs/foundation/SCHEDULER.md` (advisory-lock overlap guard) | no host schedules it; hosting undecided; intervals await HU+DI |
| J-02 header/CSRF | 1 | **Reconciled 2026-10-15: already implemented** | `check --deploy` (production settings, dummy env): W001 gone; remaining W003 (CSRF is enforced per view by design), W005/W021 (HSTS subdomains/preload not enabled: HU+DI decision) | HSTS scope decision |
| A-05 CI workflow | 1 | Implemented (NOT validated; stays so until the workflow has actually run) | `.github/workflows/ci.yml` runs `scripts/ci.sh` on PostgreSQL 17 service | never executed (no push, no local DB); validate on first CI run |
| A-03 AC-to-test map | 1 | **Reconciled 2026-10-15: index exists and is current** | `docs/foundation/AC_TEST_INDEX.md` (`scripts/ac_index.py --check` passes): 147 criteria, 2 named by a test function, 3 by a file, 142 unnamed | the coverage gap is real; closing it is test-writing work, not an index task |
| F-01 combo regression | 1 | **Reconciled 2026-10-15: tests already exist, pass** | `tests/test_combo_pricing.py`, 11 passed | none |
| J-08 load baseline | 1 | Pending | | |
| E-07 responsive rerun | 1 | Pending | | |
| orders.0022 dev migration | 1,7 | Pending | not applied to dev DB | review + apply (needs DB) |
| Local 1-2 product E2E (stubs) | 2 | Implemented (prior) | `test_e2e_prototype.py` | rerun + extend for failure/delay/duplicate cases |
| B-01 Zoho Payments sandbox session | 3 | **Session creation provider-verified (real sandbox)**; hosted checkout, signed return, webhook NOT exercised | Adapter creates a session (HTTP 201, ₹1.00, test sessions only); defect fixed: `meta_data` must be a list of `{key,value}` (dict gave 400 "JSON Not Well Formed"); mock tests updated | Sandbox checkout host unconfirmed (both `paymentssandbox.zoho.in` and `payments.zoho.in` serve an identical generic page for `/hostedcheckout/<key>` and `/hostedpages/<key>`; needs a browser/support); HTTPS return URL; signing key; webhook key |
| B-02 payment webhook | 3 | Blocked (BLK-2) | `process_zoho_webhook` mocked | real sandbox |
| B-05 Zoho stock read | 3 | **SUPERSEDED 2026-10-15 (current status: real sandbox READ of item and stock figure verified; the test org now holds 2 items; see the 2026-10-15 section).** Historical text: Partly unblocked: test org `60091726840` read-verified (items/settings/contacts/sales orders; org empty, no writes). Real stock read needs test items = provider write, awaiting HU+DI |  adapter, 25 mocked tests | real sandbox |
| B-06 Sales Order create | 3 | **SUPERSEDED 2026-10-15: Blocked by (a) token lacks `ZohoInventory.salesorders.CREATE`, (b) Flow duplicate risk unverified, (c) no explicit authorisation.** Historical: Blocked (BLK-3) | mocked | real sandbox |
| B-11 SO total = amount paid | 3 | Blocked (BLK-2/3); **2026-10-15: still blocked behind B-06 (mocked check only)** | | |
| B-07 GST/tax/invoice mapping | 4 | **SUPERSEDED 2026-10-15: tax records read and verified (see 2026-10-15 section); rate applicability per product remains an HU+DI/accountant decision.** Historical: Blocked (BLK-3) + SPEC 7.9 vs X-2 check | | HSN must be retrieved from documented records, not guessed |
| B-08 contact mapping | 4 | **SUPERSEDED 2026-10-15: link table and read-only reconciliation built; contact create blocked by missing `ZohoInventory.contacts.CREATE`.** Historical: Blocked (BLK-3) | | |
| B-16 HSN/tax validation; Zoho Flow no-conflict | 4 | Pending | read-only Flow inspection needs Zoho access | |
| C-01 Zoho→Shiprocket handoff | 4 | Blocked (BLK-3/4) | real adapter raises `ZohoNotSupportedError`; conflict X-1 handled by Plan MF-070 | |
| C-02 tracking return | 4 | Blocked (BLK-3/4) | | |
| C-04 weight/dimension | 4 | Pending | reuse product dimensions | |
| C-05 pickup mapping | 4 | Blocked (BLK-4) | | |
| D-06, D-07, D-09, B-13 (guardrail only) | 5 | Pending | no GST code in `modules/` | B-13 = enforce no-refund/no-return; no refund execution |
| H-05, H-06 | 5 | Pending | fail-closed | provider + approved wording (no invented legal text) |
| E-08/DC-22/DC-25, D-08 | 5 | Pending | videos hot-linked | storage choice |
| G-03, G-04, I-03, I-04 | 5 | Pending | I-03 needs real Zoho read | |
| N1–N11 | 6 | Pending | nothing sent | provider/sender domain |
| J-01…J-07 | 7 | Pending | no Dockerfile; DigitalOcean App Platform preferred, no AWS | deploy stays separately gated |
| Phase 8 ledger capabilities (ORD, DRF, PRD, COL, INV, CUS, DSC, GFT, CNT, MKT, CHN, ANA, SET, INT, USR, SYS) | 8 | Pending | much exists (Orders batch 1, discounts, staff, etc.) | per-ID rows to be added as each category is worked; 122-row audit (Plan §2.3) still unverified |

## Excluded (explicit NO, source Plan §5/§6 and §2.3) — not to be built
Wishlist, reviews/recommendations, server-side cart, related-product links (agent-labelled out of scope); COD (SET-008, SET-070); Razorpay Magic Checkout (SET-071); refund/return/store-credit execution (ORD-074/075/076/144, SET-013); ORD-140; COL-007; PRD-005/042/060; INT-007/008/009/020/021/023; USR-006/012/022/023/030/031; SYS-004/009/010/013; full working list of 50 in Plan §6.
## Deferred
MA-ORD-010, MA-ORD-011 (sales-channel and delivery-method columns), Plan §3.11.
## Evidence-only
ORD-145.

## Validation evidence log
| Date | What | Kind | Result |
|---|---|---|---|
| 2026-10-13 | Environment check (Docker, .env keys) | measurement | DB unavailable; no Zoho credentials |
| 2026-10-13 | `scripts/ci.sh` full suite, run 1 | Mock/local (no provider contact) | 1888 passed, 6 failed (22 min). Failed: tests/test_migrations.py::test_no_business_schema_after_migrate; tests/test_migrations.py::test_migration_bookkeeping_is_the_only_framework_table; tests/test_phase1_payments.py::test_concurrent_payment_starts_get_distinct_active_ids; tests/test_f05_boundaries.py::test_orders_package_contains_only_authorized_files; tests/test_f05_boundaries.py::test_integrations_are_dependency_free_boundaries; tests/test_foundation_boundaries.py::test_integrations_contain_no_provider_implementation |
| 2026-10-13 | `scripts/ci.sh` full suite, run 2 after test-only fixes | Mock/local | 1894 passed, 0 failed (23 min) |
| (none) | Real Zoho sandbox call | - | none; no provider has ever been contacted |
| 2026-10-13 | Zoho Payments sandbox: refresh-token exchange (`POST accounts.zoho.in/oauth/v2/token`, existing adapter logic, one request) | **Real sandbox** | HTTP 200, access token returned (not displayed or stored) |
| 2026-10-13 | Zoho Payments sandbox: authenticated read-only `GET https://paymentssandbox.zoho.in/api/v1/paymentsessions/<made-up id>?account_id=...` | **Real sandbox** | HTTP 400 "Payment session is invalid." Expected for a non-existent id: the sandbox API accepted the access token (an unauthenticated call gives 401 "Invalid Ticket Used") and routed the path. Confirms sandbox API base `https://paymentssandbox.zoho.in/api/v1`. No resource created |
| 2026-10-13 | Zoho Payments sandbox earlier probes: unauthenticated GETs to `paymentssandbox.zoho.in` | **Real sandbox** (no credentials) | `/` 302 to `/login`; `/api/v1/payments` 401 "Invalid Ticket Used"; bogus path 404 "Not Authorised" |
| 2026-10-13 | Zoho Payments sandbox OAuth failures before the credential fix | **Real sandbox** (diagnostic) | token endpoint returned HTTP 200 without a token, caused by a wrong client secret (`invalid_client_secret` seen via the OAuth helper); fixed by correcting the secret |

Evidence classes: **Mock** (fake/stubbed HTTP) and **Real sandbox** (genuine Zoho response) are recorded in separate rows and never merged. Currently: Mock = the 1894-test local suite (2026-10-13); Real sandbox = Zoho Payments OAuth and one authenticated read only (rows above); nothing else, and no Inventory or Shiprocket evidence.

| 2026-10-13 | Zoho Payments sandbox: `POST /paymentsessions` x5 (minimal body x2, adapter body, bisect probes; ₹1.00, return URL `example.invalid`/`example.com` placeholders, never paid) | **Real sandbox** | 201 with `payments_session_id` and `access_key`; adapter body failed 400 until `meta_data` was sent as a list of key/value objects; fixed |
| 2026-10-13 | GET `/hostedcheckout|hostedpages/<key>` on both Zoho hosts | **Real sandbox** (inconclusive) | all HTTP 200 generic "Hosted Pages" shell; host not confirmed |
| 2026-10-13 | Full suite after fixes (mock) | Mock | 1901 passed (1900 + 1 date-dependent test fixed); ran in 21m41s |

## Update 2026-10-13 (sandbox pass 2)
* Full suite 1901 passed / 0 failed in one run after final edits (mock evidence); ruff check and format clean.
* BLK-2 remains: signing key, webhook key, HTTPS return URL, checkout host (HU). Path-restricted tunnel method proven and stopped; webhook/return remain Blocked, no real-sandbox evidence yet.
* BLK-3 refined: Inventory test org `60091726840` read works; writes return 401 (token lacks create scopes) and the org has no taxes. No test records were created. B-06/B-07/B-11 stay Blocked.

## Batch 1 (Assessment `ASSESSMENT_50_TASK_BATCH_2026-10-14.md`, section 8) — implemented locally 2026-10-14
Authority: HU execution instruction of 2026-10-14 (first recommended batch, 55 tasks). Local code and tests only: no provider contact, no commit, no push, no deployment.
Status words as above; **Validated (mock/local)** = focused tests plus the full suite. No real-sandbox evidence is claimed for any row.
Section 8's range "T47-T51" includes T48/T49, while the same paragraph lists T48/T49 as second-wave; the count of 55 only works with them included, so they were implemented. HU+DI to confirm.

| Task | IDs | Status | Evidence (tests) / note |
|---|---|---|---|
| T01 | A-03, MF-003 | Validated | `scripts/ac_index.py`, `docs/foundation/AC_TEST_INDEX.md`, `tests/test_ac_index.py`. Result is honest: few tests cite AC ids, so most criteria show "no test names it" (a recording gap, not proof of no coverage) |
| T03 | J-03, B-04 | Validated (defs only) | `modules/backoffice/scheduling.py`, `docs/foundation/SCHEDULER.md`, `tests/test_scheduling.py`. Nothing is scheduled on any host; `publish-scheduled` deliberately absent (T41 blocked) |
| T04 | J-02 | Validated | `config/settings/*`, `tests/test_settings.py`; `check --deploy` leaves only W003 (per-view CSRF by design), W005, W021 (subdomain/preload not enabled: need own decision) |
| T05 | F-01 | Validated | `tests/test_combo_pricing.py` |
| T08 | E2E | Validated (stub) | `tests/test_e2e_prototype.py` (timeout, delayed, duplicate, abandoned, NO PAYMENT -> NO DISPATCH) |
| T09 | B-12 | Validated | `tests/test_testcode_traceability.py` (order list/detail, filter, exports, reconciliation) |
| T10 | B-13 guardrail | Validated | `tests/test_refund_guard.py` |
| T11 | PRD-013 etc | Validated | `modules/backoffice/listkit.py`; used by orders, payments, reports (products/customers keep their existing audited exports) |
| T12 | USR-007/013 | Validated | `tests/test_permissions.py`; new capabilities held by both roles pending HU+DI; no custom roles |
| T13, T14 | ORD-021/106/132/133/134 | Validated | `tests/test_order_tools.py` |
| T15-T20 | ORD-014..018, 023, 100, 120, 131 | Validated | same; T16 flags are derived state only (no risk score) |
| T21 | ORD-033 | Validated | staff timeline + customer-safe history; `tests/test_order_tools.py` |
| T22-T24 | ORD-034/035/036/093/101/108/013 | Validated | `OrderComment`, `OrderTag`, `OrderAdminState` (migration `orders.0023`); auto-archive default 7 days (confirm) |
| T25, T26 | ORD-041/126/046 | Validated | same |
| T27, T28 | ORD-047/049 | Validated | `tests/test_batch1_misc.py`; note never sent to providers (guard test) |
| T29 | ORD-038/022/135/104 | Validated | packing slip, single and bulk; no prices; no editable template |
| T30 | ORD-085 | Validated | hold blocks `request_shipment` only; nothing is released or dispatched by it |
| T31 | ORD-115 | Validated | customer sees it worded as an estimate |
| T33 | PRD-036/037, C-04 | Validated (contract only) | `docs/foundation/PRODUCT_LOGISTICS_MAPPING.md`; not wired to providers |
| T34 | INT-004/005 | Validated | Integrations page: outbox + mapping health; stale "adapter not built" claims corrected |
| T35 | INT-010 | **Partial** | `/webhooks` read-only; rejected (bad-signature) deliveries are not stored, so cannot be listed (would need a table and a decision) |
| T37 | PRD-006/100 | Validated | tag = use case filter; vendor filter is a decided NO (PRD-005) |
| T38 | PRD-062/063 | **Partial** | search title/description implemented (revision content, reviewed); slug edit **not** done: product ID is the fixed URL identity |
| T39 | CNT-012 | Validated | `UrlRedirect`, fallback middleware (404 only, fails open) |
| T40 | PRD-056 | Validated | staff-only revision preview |
| T41 | PRD-057 | **Blocked** | see Blockers below |
| T42 | PRD-028 | Validated | shown only for one clear volume |
| T43-T45 | PRD-030/032/038/039/103 | Validated | fields only, values never guessed; cost behind its own capability, audit omits amounts |
| T47 | PRD-073/074/090/094 | Validated | bulk category/tag edits change drafts only, preview first |
| T48, T49 | COL-001..006 | Validated | `Collection`, `CollectionItem`; text reviewed/published like pages; membership audited |
| T50 | CNT-009/010, PRD-061 | Validated | files library; referenced files cannot be deleted |
| T51 | CNT-007/002/040 | Validated | blog metadata, list columns |
| T52-T54 | CUS-007/008/012/013/016 | Validated | `tests/test_batch1_customers.py`; consent = staff-recorded override records, order evidence untouched |
| T60-T64 | SYS-003/005/006/007/008/011/020/021/022 | Validated | `tests/test_system_shell.py`; alerts are internal only |
| T65, T67 | ANA-007/018 | Validated | sales by customer type; CSV export, download only |

Migrations (repo only; **not applied to the development database `effyklean`**): `orders.0023_batch1_order_operations`, `catalogue.0010_batch1_product_master_fields_and_redirects`, `backoffice.0003_batch1_saved_views_and_alerts`.

### Batch 1 blockers / HU+DI decisions
* T41 scheduled publication: `revisions.authorize` accepts only a request-derived `StaffAuthority`, ARCHITECTURE s20 says nothing publishes automatically, and superseding the live revision at publish time would hide the product until go-live. Needs a decision on how a timed publication is authorised and held.
* T38 slug edit, T35 rejected-delivery log: see rows.
* Capability defaults (both roles hold the new export/cost/customer/media/redirect capabilities), auto-archive days, HSTS one year, scheduler intervals: working defaults awaiting confirmation.

| 2026-10-14 | Full suite after Batch 1 (final tree) | Mock/local | **2135 passed, 0 failed** (27m24s). An earlier run showed 24 failures: real defects fixed (redirect lookup hit the database for hostile 404 paths; Home query budget) and exact-inventory guard tests updated for the new files, fields, constraints, routes and middleware. `ruff check`, `ruff format --check`, `manage.py check`, `makemigrations --check` clean |

## Update 2026-10-15 (Zoho sandbox sync, two passes; local, uncommitted; Batch 1 still NOT accepted)
Report: `docs/foundation/ZOHO_INVENTORY_SANDBOX_VALIDATION_2026-10-15.md`; log entries in `PROJECT_LOG.md`. Migration `orders.0024_zoho_sync_tasks` is created and **not applied** to any persistent database.

| Item | Status | Evidence level | Notes |
|---|---|---|---|
| Sandbox target verification (configured org is the non-default test org `TestEffyKleanZohoIntegration`) | Done | Sandbox read-only | guard in `sync_zoho_items` |
| `sync_zoho_items` (dry run default; `--sku` required to apply; sandbox flag + confirmed org id) | Done | Mock + sandbox read | applied once: recorded real item ids for `EK-HHLD-AR`, `EK-HHLD-FCP` locally (local DB only) |
| Catalogue loaded into dev DB (15 source products, IN_REVIEW, unverified demo MRP) | Done | Local | nothing approved or published |
| Reconciliation (25 local SKUs vs 2 Zoho items; 2 matched, 13 imported + 2 fixtures absent, 8 stale fixtures; 4 local customer e-mails vs 2 Zoho contacts, 0 matched, 2 ambiguous) | Done | Sandbox read-only | price/name differences reported, nothing overwritten |
| Item create in Zoho (B-05/B-06 prerequisite) | **Blocked** | Sandbox refusal (401) | needs the item create permission; scopes not changed; not retried |
| Durable product/customer sync (`ZohoSyncTask`, `ZohoContactLink`), immediate trigger, 3 total attempts, error classes, ambiguous-timeout recovery, staff alert + Reconciliation table | Done (not applied to a database) | Mock/stub only | `ZOHO_SYNC_ENABLED` default off; Retry-After not honoured (transport exposes no headers) |
| Inbound customer link (`sync_zoho_customers`, e-mail match, read-only at Zoho) | Done | Mock; read-only dry run on sandbox | Zoho-created items/contacts are reported, not turned into website records (needs MRP/price rule; accounts need password/consent) |
| `PAYMENT_STUB_ONLY`, `ZOHO_INVENTORY_SANDBOX`, `ZOHO_SALES_ORDER_WRITES_AUTHORIZED`: production refuses the first two; Sales Order creation blocked in a declared sandbox until authorised | Done | Mock | |
| B-07 tax IDs: `...131` GST18 intra 18% (CGST9+SGST9) and `...051` IGST18 inter 18% exist in the test org | Partly: IDs verified; rate applicability and use in a write are HU+DI decisions | Sandbox read-only | not in `.env`, not used in any write |
| B-06 Sales Order create / website order into Zoho | **Blocked** | not run | Zoho Flow / workflow duplicate risk unverifiable (rule "Zoho Flow salesorder add" recorded in the live org 2026-10-09); needs HU inspection and explicit authorisation |
| B-08 contact mapping | Partly: stable link table and read-only reconciliation built; contact create unverified | Mock | two same-e-mail contacts in the test org are ambiguous |

HU+DI decisions open (unchanged, preserved): (1) item/contact/Sales Order create permission, (2) tax-rate applicability and authorisation to use the IDs, (3) imported MRP (safe only while IN_REVIEW; no provisional marker on the SKU), (4) website versus Zoho price (`EK-HHLD-AR` 180.00 vs 10.00; `EK-HHLD-FCP` 130.00 vs 80.00).

| 2026-10-15 | Full suite after the Zoho sync work (final tree, after the guard-list updates) | Mock/local | **2181 passed, 0 failed** (27m48s); `ruff check`, `ruff format --check`, `manage.py check`, `makemigrations --check --dry-run` clean. An earlier run showed 3 failures, all inventory guards (orders files, table list); the new files and tables were registered there |

## Update 2026-10-15 batch 3 (Zoho Inventory access matrix, scope gap, durability; local, uncommitted; Batch 1 still NOT accepted)
Report: `docs/foundation/ZOHO_INVENTORY_SANDBOX_VALIDATION_2026-10-15.md` (third-pass section). Older B-05..B-08 rows above are marked SUPERSEDED in place; their historical text is kept.

| Item | Status | Evidence level | Notes |
|---|---|---|---|
| OAuth token scopes (Zoho-reported): `settings.READ items.READ contacts.READ salesorders.READ` only | Verified | Real sandbox | `manage.py check_zoho_access` |
| Missing required scopes: `items.CREATE`, `contacts.CREATE`, `salesorders.CREATE`, `salesorders.UPDATE` (void) | **Blocked: HU action (new consent/refresh token)** | Real sandbox | scopes not changed by the agent |
| All 9 read operations in the matrix | Verified | Real sandbox read | org, items list/SKU/id, taxes, contacts list/email, sales orders by reference/id |
| Write operations (item/contact/Sales Order create, void) | Not tested; cannot succeed until scopes exist | Mock only | sync stops before sending when the scope is missing |
| Scope pre-check (no request sent for a known-missing scope; permanent stop with clear message) | Done | Mock | `ZohoInventory.require_scope` |
| `Retry-After` honoured (seconds form, clamped to 1 h; never shortens the 60 s / 300 s backoff) | Done | Mock | transport may return headers as a third element |
| Missing sync tables: clear command errors, Admin Home/Reconciliation do not crash, ERROR log when an intent cannot be recorded, alert when sync is enabled | Done | Mock/local | `orders.0024` still **not applied** to `effyklean` |
| Migration `orders.0024` validated on an isolated scratch database (migrate from zero, indexes, reverse to 0023, dropped) | Done | Local integration | standing DB confirmed to have no `orders_zoho*` tables |
| Zoho Flow / workflow rule identification and disablement | **Blocked: not inspectable by the agent; HU must inspect/capture** | none | no changes made; no Flow touched |
| Intentional sandbox prices (`EK-HHLD-AR` 180 vs 10, `EK-HHLD-FCP` 130 vs 80) | Recorded as intentional test data | HU statement | no production price rule inferred |

| 2026-10-15 | Full suite after the access-matrix batch (final tree) | Mock/local | **2190 passed, 0 failed** (30m25s); ruff, format, check, makemigrations clean |

## Update 2026-10-15 batch 4 (OAuth verification, Flow checklist, first-write plan; local, uncommitted; Batch 1 still NOT accepted)
Scopes granted and verified: NO (token still four READ scopes; eight-scope strings DOCS-VERIFIED). Account-role permissions: UNVERIFIED (not inspectable without a write). Real reads: VERIFIED. Real writes: NOT performed. Flow evidence: PENDING. `orders.0024`: scratch-validated, not applied to `effyklean`. Item write plan prepared, not executed. See `docs/foundation/ZOHO_OAUTH_FLOW_AND_FIRST_WRITE_PLAN_2026-10-15.md`.
Sandbox gate correction (2026-10-15): `ZOHO_INVENTORY_SANDBOX` is already True in `.env` (verified); no instruction to set or pass it again remains. Sandbox API base and every provider-write authorization gate (explicit HU authorization per write, Sales Order write block) are unchanged.
First real sandbox write (2026-10-15, HU authorized): one test item created (`ZZ-SBX-TEST-20261015-01`, id `4290031000000048001`), verified, marked inactive. Item create and mark-inactive VERIFIED; contact and Sales Order writes not performed.

## Update 2026-10-15 batch 5 (contact write, B-14, status reconciliation; local, uncommitted; Batch 1 still NOT accepted)
Real sandbox WRITE (HU authorized): one test contact `zz-sbx-test-20261015@example.invalid`, contact_id `4290031000000048016`, created, read back (customer, active), marked inactive (not deleted) in org `60091726840`. Customer count 2 to 3. Contact create/mark-inactive VERIFIED. Dry-run reconcile (read-only, after restarting the local DB container): create 15, unchanged 2, stale 8, Zoho-only 1 (the test item). B-14, J-02, J-03, A-03, F-01 closed or reconciled above. Not done: J-08 load baseline (needs a load tool and an agreed target), E-07 responsive rerun (needs a browser pass), Sales Order writes (Flow evidence and gate), B-02, C-01, C-02, C-05 (blocked), J-10 release gate.


## Update 2026-10-15 batch 6 (catalogue created in the Zoho sandbox; local, uncommitted; Batch 1 still NOT accepted)
Real sandbox writes (HU authorized): 10 website-catalogue items created in the test org (HSN 3402, GST18/IGST18, rate = website price) and mapped locally; 3 refused (duplicate item names `EK-HHLD-GC/LW/TC` vs `EK-BLP-000005/7/3`: HU+DI naming decision); 2 test fixtures not created; the 2 older sandbox items not overridden (`items.UPDATE` scope not granted). Item reconcile: Zoho now holds 13 items (10 new, 2 older, 1 inactive test item). Production price ownership, MRP, HSN-per-product and tax applicability stay open; sandbox data to be deleted before any production link.
Batch 6 follow-up: the 3 refused items were created with Zoho-only name suffix " - Household 1 L" after HU clarified HHLD (1 L) and BLP (5 L) are distinct products; 13 of 13 real website products now exist in the sandbox. Production item naming still open.

## Update 2026-10-15 batch 7 (GST rule, Sales Order safeguards, AC traceability, J-08/E-07; local, uncommitted; Batch 1 still NOT accepted)
Evidence label: MOCKED unless stated; no Sales Order created anywhere. Details: `docs/foundation/GST_RULE_AND_SALES_ORDER_SAFEGUARDS_2026-10-15.md`, `docs/foundation/J08_E07_BASELINE_2026-10-15.md`.

| Item | Status | Evidence | Remaining |
|---|---|---|---|
| B-07 GST rule (Karnataka CGST 9% + SGST 9%, elsewhere IGST 18%) | **Implemented and tested (local)** | `modules/orders/tax.py`; checkout refuses an unrecognised state; adapter refuses identical tax ids; 15+ new tests | tax-id env vars unset; accountant/legal certification not given; whether Admin shows the split undecided |
| B-06 Sales Order safeguards | **Safeguards implemented and tested (mocked); live write NOT enabled** | `tests/test_sales_order_safeguards.py` (7): payment gating, one order per reference, timeout recovery, write gate, retries, customer-first | gate in section 3 of the safeguards document; Flow is NOT a prerequisite (HU) |
| B-08 customer sync | Code and mocked tests complete; sandbox `sync_zoho_customers` **blocked by unapplied `orders.0024`** (command refused: tables missing) | `zoho_sync.py`, tests | HU authorisation to apply 0024 |
| B-02 payment webhook | Still blocked (BLK-2) | mocked tests exist; signing key, webhook key, HTTPS return URL, hosted-checkout address missing | HU supplies them |
| C-01, C-02, C-05 | **Blocked: decision and access, not code** | the real adapter still refuses shipment creation; no Shiprocket sandbox credentials (BLK-4); how a website order reaches Shiprocket (HU's separate Zoho automation vs a direct integration) and where tracking returns from is undecided | HU+DI: shipment handoff design; pickup-location mapping source |
| A-03 AC traceability | **Improved**: named by a test function 2 -> 24 (index regenerated; `--check` passes); 24 ids tagged on tests that demonstrably cover them (`# Covers AC-...`) | `docs/foundation/AC_TEST_INDEX.md` | 122 criteria still have no named test; most are NOT proven untested (many behaviours have unlabelled tests); labelling them needs per-criterion review |
| J-08 loading baseline | **Partial: server response-time baseline recorded** | `scripts/load_baseline.py`; table in the J-08/E-07 document | browser measurement and a numeric target (SPEC sets none) |
| E-07 responsive checks | **Not done (no browser tool)**; static evidence only | viewport meta tag and `@media` rules exist | headless browser or HU run, agreed widths/pages |


## Update 2026-10-15 batch 8 (guards, duplicate rule, AC categorisation, migration 0024 applied; Batch 1 still NOT accepted)
Boundary guards updated for `orders/tax.py` and `orders/zoho_sync.py` only (tests pass). E-mail OR phone potential-duplicate rule implemented in `zoho_sync` (reconcile + handler refusal; customer-detail sync deferred). AC categorisation recorded in `docs/foundation/AC_CATEGORISATION_2026-10-15.md`. `orders.0024_zoho_sync_tasks` applied to the development database `effyklean` (verified, two empty tables). Full suite 2249 passed (mock/local evidence only). Sync flags remain off; no provider write.

## Update 2026-10-15 batch 9 (checkout field alignment review; no code change; Batch 1 still NOT accepted)
Reference: `checkoutCart/Checkout - BRM HERBALS.html` (Di-Eval-Effyklean, raw file read; static HTML fields only). Compared with `modules/storefront/checkout_pages.py` (`TEXT_FIELDS`, `_validate`, `_address`).
| Reference field | EffyKlean | Disposition |
|---|---|---|
| email-or-mobile (single contact) | separate required name, mobile (10-digit IN), email | Covered; stricter by design (e-mail OR phone duplicate rule needs both) |
| marketing_opt_in (email) | `email_opt_in` -> `CustomerDetails.email_marketing_opt_in` | Covered end to end |
| firstName / lastName | single `customer_name`, per-address `res_name` / `ship_name` | Presentation difference only; no split (would change persisted schema) |
| address1 / address2 / city / zone / postalCode | `*_line1/_line2/_city/_state/_pin`, PIN 6 digits, state validated by `state_code` | Covered, server-validated |
| countryCode | none (India-only; non-Indian state refused) | Not added: international shipping is a new business rule |
| phone (shipping) | `customer_mobile` (one number) | Covered |
| billing_address_selector (same / different) | residential address + `same_as_residential` for shipping | Covered (residential acts as billing) |
| reductions (discount code) | applied on the cart page, carried through review token | Covered; placement differs (presentation) |
| sms_marketing_opt_in | WhatsApp opt-in instead | **HU+DI decision**: SMS consent is a new consent type and wording |
| save_shipping_information | none | **HU+DI decision**: new persistence of a guest's address |
No field was added; none fits existing approved scope without a new business rule or persistence. Remaining plan items (J-02, A-03, F-01) stay Pending until HU+DI name them; BLK-2 still blocks B-02. Nothing committed or pushed.

## Update 2026-10-16 batch 10 (optional "Save shipping information for future orders"; local only; Batch 1 still NOT accepted)
Dependency order: J-02 (already implemented), A-03 (index exists, 24 ids tagged) and F-01 (11 tests pass) were reconciled on 2026-10-15 and need no further work, so the batch is HU+DI's updated decision on saved shipping information.
| Item | Status | Evidence |
|---|---|---|
| Saved shipping address (signed-in `CustomerAccount` only) | **Implemented and tested locally** | `identity.SavedShippingAddress` + migration `identity.0005` (NOT applied to any non-test database), `modules/identity/saved_shipping.py`, `checkout_pages.py` (tick box, prefill, save at pay), `account_pages.py` (show + remove), `deletion.py` (owned by customer deletion), `tests/test_saved_shipping.py` (11 tests) |
| Guest saving | **Not implemented: unresolved decision** | A guest has no verified, stable identity (no session; e-mail/phone are unverified), so keying a stored address to them would let anyone who types that e-mail or phone read the address back. Needs HU+DI: signed-in-only (current), or a verified-identity design |
| Current order's shipping address | Still required and validated as before | `test_shipping_is_still_required_for_the_current_order` |
| SMS marketing opt-in | Not added (per instruction) | none |
Behaviour: off unless `SAVED_SHIPPING_ENABLED=1` (default off; with it off nothing is read, written or shown). One address per account, replaced by a later save, saved only when the box is explicitly ticked and the reviewed order is submitted for payment (also when payment then fails; the address is the customer's own). Customer removes it on `/account/`; it is deleted with the account (cascade) and does not block Director customer deletion. Orders keep their own delivery address.
**Disable:** leave/unset `SAVED_SHIPPING_ENABLED`. **Remove (not done; needs authorization):** drop the checkbox/prefill/panel code, revert `identity.0005` (`migrate identity 0004`), delete `saved_shipping.py`, the model and the tests.
Open HU+DI: privacy-notice wording and retention for saved addresses (page text is a placeholder: "saved to your account only ..."); guest saving (above); applying `identity.0005` to `effyklean`.
Validation (mock/local only): full suite 2256 passed, 4 failed before fixes (3 enumeration guards: identity file list, route list/index, schema table list; plus 1 real bug: Director customer deletion blocked by the new table, fixed by declaring it owned). After fixes the affected files were re-run (69 passed: saved shipping, accounts, deletion, migration, route and identity boundary tests); the full suite was NOT re-run after the fixes. `ruff check` and `ruff format --check` clean. `makemigrations` could not be run (pre-existing AppRegistryNotReady in the CLI check), so migration 0005 was hand-written; the migration test and model tests exercise it, but a `makemigrations --check` is still owed.

## Update 2026-10-16 batch 11 (saved-shipping retention, inventory-boundary journey tests; local only; Batch 1 still NOT accepted)
Reconciliation (no work repeated): J-02, A-03, F-01, J-03, B-14 already implemented/validated (rows above); `orders.0022`..`0024` are applied to `effyklean` (2026-10-14/15); A-05 CI still never run (needs a push); J-08 partial; E-07 needs a browser; provider rows B-02, B-06, B-11, C-01, C-02, C-05 stay blocked by BLK-2/3/4 (external access or authorisation, not code).
| Item | Status | Evidence |
|---|---|---|
| Saved-shipping retention (HU+DI: 3 months from the last successful delivery to the same address; renewed only by a courier-reported DELIVERED; not by an order, failed payment or undelivered dispatch) | **Implemented and tested locally** | `modules/identity/saved_shipping.py` (`expires_at`, `get`, `purge_expired`), `modules/orders/delivered_addresses.py` (delivery lookup passed to identity as a callback: no import in either direction), `purge_saved_shipping` command + scheduler job `saved-shipping` (daily 03:15, `docs/foundation/SCHEDULER.md`), model fields `saved_at`, `last_delivered_at` (migration `identity.0005` edited in place: never applied outside test databases), 9 retention tests in `tests/test_saved_shipping.py` |
| Migration consistency | Verified | `makemigrations --check --dry-run` (local settings, `.env` loaded): "No changes detected". The earlier CLI error was a missing environment, not a defect |
| Inventory boundary in the stub journey | **Tested** | `tests/test_e2e_prototype.py`: stock unavailable at review and at payment gives 409, no order, no captured payment, and the same cart buys once stock returns. Existing tests already cover failed payment, duplicate notifications and returns, delayed confirmation, abandoned attempts, Zoho/Shiprocket outages, no-payment-no-dispatch and same-day dispatch refusal |
Working defaults awaiting HU+DI confirmation: (1) before any delivery is recorded, the 3 months run from the day the address was saved (otherwise a never-delivered address would be kept indefinitely); (2) a delivery counts only if it is on or after the save date; (3) "same address" = all six fields equal ignoring case and spacing; a different address saved later restarts retention; saving the identical address again does not; (4) the purge runs even when the display flag is off. Privacy wording stays unpublished (the checkout/account text is a neutral placeholder). Not accepted: needs HU+DI confirmation of these defaults and of the wording; `identity.0005` is not applied to `effyklean`.
Validation: full suite 2271 passed, 0 failed (25 min, PostgreSQL, mock/local evidence only); `ruff check`, `ruff format --check`, `makemigrations --check` and `ac_index --check` clean. The home-page banner change and the earlier saved-shipping/deletion fixes are inside this run.

## Update 2026-10-16 batch 12 (migration applied to `effyklean`, catalogue recovery finding, publication checkpoint; Batch 1 still NOT accepted)
| Item | Status | Evidence |
|---|---|---|
| `identity.0005_saved_shipping_address` on the sandbox database `effyklean` | **Applied 2026-10-16 (HU authorised; sandbox, not reset)** | Target confirmed by `.env` (`DB_NAME=effyklean`, 127.0.0.1:5432, `config.settings.local`, DEBUG on; only `postgres` and `effyklean` exist on the server). The migration file was untracked and never applied elsewhere, so in-place editing was safe. `showmigrations`: no unapplied migration in any app; `makemigrations --check`: no changes. Table `identity_savedshippingaddress` exists with the expected columns, 0 rows (0 customer accounts). `tests/test_saved_shipping.py`: 20 passed (test database, not `effyklean`). Not re-applied or re-tested afterwards |
| Product catalogue recovery | **No code change needed; already present** | `media/catalogue_source/source.json` (retrieved 2026-10-09T22:01Z, 15 products, 30 images; `media/` is git-ignored) matches the 15 real products in `effyklean` (SKU ids 14-28: 7 `EK-HHLD-*`, 8 `EK-BLP-*`; created 2026-10-15 by the Zoho sandbox sync, PUBLISHED, each with description, usage text and 2 images). SKU ids 4-13 are labelled test fixtures. `import_catalogue_source.py` was not re-run: it keys on the source `sku`, which is empty in `source.json`, so it cannot match these rows and could create duplicates. MRP/prices/Zoho mapping are as set by the sandbox sync (HU: sandbox values may be overridden); production ownership of price/MRP is still undecided. No original "lost product" list exists in the repository, so whether `effyklean.com` carried products beyond these 15 is unverified |
| Plan header wording | Corrected (traceable note added; original header kept) | Plan copy, "Status correction (2026-10-16)" |
| Publication | See `PROJECT_LOG.md` 2026-10-16 publication entry for commit IDs | Pushed state is recorded there, not assumed here |
Disclosure: while checking configuration the agent printed the Zoho Inventory sandbox client id, client secret, refresh token and organisation id into the session transcript. They are test-organisation credentials, but HU should consider rotating them.

## Update 2026-10-16 batch 13 (consolidated closure pass; Batch 1 still NOT accepted)
A-05: CI green on `5f2ff5c` (run 38898823275). Payments sandbox: real session creation re-verified through the app gateway (provider-confirmed); payment completion, signed return and webhook still NOT evidenced (HTTPS reachable endpoint needed). Catalogue: 15 intended products present and visible; five local test products also visible, hide step awaits HU (see `PROJECT_LOG.md` 2026-10-16). Plan 2.3 122-row map: `docs/foundation/ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md` (84 rows not traced by ID; none accepted). Scheduler for saved-shipping purge: not configured on any host. Inventory credential rotation: deferred by HU.

---

## HU+DI disposition triage reconciliation (2026-10-22)

The current aggregate disposition tally for the **597-record register** supersedes the earlier 250-question queue as the current triage-count reference:

| Disposition | Records |
|---|---:|
| Implemented | 256 |
| BUILD | 243 |
| LATER | 9 |
| INVESTIGATE | 13 |
| EXCLUDE | 76 |
| **Total** | **597** |

These counts are dispositions, **not** verified implementation or validation counts. “Implemented” is not evidence by itself that each record's code is correct, tested or production-ready. The original master evidence labels (NO ACTION, VALIDATE, BLOCKED-DEC, REJECT/OOS, IMPLEMENT, FIX) and the capability YES/NO decision ledger remain distinct from this newer disposition classification.

Governance for follow-up:
- Do not present all 13 INVESTIGATE records as questions for Hu. Most require evidence gathering, validation, dependency checks or decision-history reconciliation.
- Do not ask Hu again about implemented scope or repeat a decision already captured in the project history. Search the authoritative decision ledger, previous HU+DI records and implementation evidence first.
- Preserve the existing task-specific DoDs and validation evidence. Do not convert a disposition into a completion claim.
- AgntGapAnalysis/Deferred310_Disposition_Triage_DRAFT_2026-10-22.csv is a draft working aid, not an authoritative row-by-row ledger; its own review-state column requires verification against the authoritative 597-row source/decision ledger.
- Row-level synchronization is complete only when each disposition is traceable to the applicable activity ID and a source decision or governing rule. If a record cannot yet be reconciled, keep it explicitly unresolved rather than guessing.

Next step: perform the record-level reconciliation into the plan and status register before moving on to the next genuinely unresolved HU+DI decision. The MF-089 contact-form policy proposal remains a separate pending policy decision; this tally does not approve it.
