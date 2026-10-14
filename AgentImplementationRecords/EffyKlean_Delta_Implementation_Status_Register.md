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
| BLK-3 | No Zoho Inventory test organisation/OAuth credentials; no tax ids, no sandbox item mapping | B-05, B-06, B-07, B-08, B-11, C-01 | Provide in `.env`; state sandbox org id |
| BLK-4 | Shiprocket sandbox credentials not provided (plan routes shipping via Zoho; Zoho-side Shiprocket config is HU-side) | C-01, C-02, C-05 | Confirm approach / supply access |

Unaffected by BLK-2..4 once BLK-1 clears: all of Phase 0-2 and credential-free items in Phase 1, 5, 6 (partly), 7.

## Agent tasks (Plan §5; decision YES unless noted; source: Plan §5)
| Task | Phase | Status | Code / evidence | Outstanding |
|---|---|---|---|---|
| A-02 baseline review | 0 | Implemented (prior) | commit `f48cda5` | none; tree clean at start |
| A-04 full suite on committed tree | 0 | Validated (local, 2026-10-13) | run 1: 1888 passed, 6 failed; after test-only corrections: **1894 passed, 0 failed** (`scripts/ci.sh`, PostgreSQL 17, dev-DB server, `test_` database) | none; CI workflow itself still unrun |
| J-10 release gate | 0,7 | Pending | PHASE1_EXIT_GATE; rows 3,5,11 blocked | re-check at end |
| B-14 shared token cache | 1 | Pending | per-request gateway in `wiring.get_payment_gateway` | implement + test (BLK-1) |
| J-03 scheduler definition | 1,7 | Pending | commands exist, no schedule | implement |
| J-02 header/CSRF | 1 | Pending | `check --deploy` W001 | implement |
| A-05 CI workflow | 1 | Implemented (NOT validated; stays so until the workflow has actually run) | `.github/workflows/ci.yml` runs `scripts/ci.sh` on PostgreSQL 17 service | never executed (no push, no local DB); validate on first CI run |
| A-03 AC-to-test map | 1 | Pending | | produce index |
| F-01 combo regression | 1 | Pending | `orders/pricing.py:54-69` | add tests |
| J-08 load baseline | 1 | Pending | | |
| E-07 responsive rerun | 1 | Pending | | |
| orders.0022 dev migration | 1,7 | Pending | not applied to dev DB | review + apply (needs DB) |
| Local 1-2 product E2E (stubs) | 2 | Implemented (prior) | `test_e2e_prototype.py` | rerun + extend for failure/delay/duplicate cases |
| B-01 Zoho Payments sandbox session | 3 | **Session creation provider-verified (real sandbox)**; hosted checkout, signed return, webhook NOT exercised | Adapter creates a session (HTTP 201, ₹1.00, test sessions only); defect fixed: `meta_data` must be a list of `{key,value}` (dict gave 400 "JSON Not Well Formed"); mock tests updated | Sandbox checkout host unconfirmed (both `paymentssandbox.zoho.in` and `payments.zoho.in` serve an identical generic page for `/hostedcheckout/<key>` and `/hostedpages/<key>`; needs a browser/support); HTTPS return URL; signing key; webhook key |
| B-02 payment webhook | 3 | Blocked (BLK-2) | `process_zoho_webhook` mocked | real sandbox |
| B-05 Zoho stock read | 3 | Partly unblocked: test org `60091726840` read-verified (items/settings/contacts/sales orders; org empty, no writes). Real stock read needs test items = provider write, awaiting HU+DI |  adapter, 25 mocked tests | real sandbox |
| B-06 Sales Order create | 3 | Blocked (BLK-3) | mocked | real sandbox |
| B-11 SO total = amount paid | 3 | Blocked (BLK-2/3) | | |
| B-07 GST/tax/invoice mapping | 4 | Blocked (BLK-3) + SPEC 7.9 vs X-2 check | | HSN must be retrieved from documented records, not guessed |
| B-08 contact mapping | 4 | Blocked (BLK-3) | | |
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
