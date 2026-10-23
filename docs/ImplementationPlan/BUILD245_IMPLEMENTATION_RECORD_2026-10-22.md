## Current status reconciliation — 23 October 2026 (supersedes prior totals)

The 245-row BUILD ledger has 83 unique items marked `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. All 83 DONE rows are mapped to Implemented in the 597-item primary disposition because the implementation and test evidence is recorded for each. External/provider/legal/operational follow-ups remain explicitly recorded as gates; they are not misrepresented as completed. In particular, MF-089's code and tests are implemented, but the host still must schedule the contact-retention job and HU legal review of wording remains outstanding. Therefore MF-089 is counted as Implemented at code/feature level, not as operationally scheduled or legally approved.

**Current 597-item primary-disposition totals: 340 Implemented + 162 BUILD + 10 LATER + 9 INVESTIGATE + 76 EXCLUDE = 597.** The remaining 162 BUILD rows are 62 PARTIAL + 100 DEFERRED. The 83 reviewed DONE rows and their recorded evidence, limitations, and follow-ups are mapped in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv). The 22-Oct primary register and 18-Oct snapshot remain historical records; apply the current reconciliation overlay for future counts. This does not authorize production writes, deployment, provider actions, or implementation of deferred rows.

---

## Current status reconciliation — 23 October 2026 (supersedes 22-Oct totals)

The per-item BUILD ledger contains 245 unique IDs: 83 are `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. Reconciliation against the 597-item primary-disposition register promotes all 83 verified-DONE BUILD rows to `Implemented`. MF-089 is counted as `Implemented` at code/feature level; the host must still schedule the contact-retention job and HU legal review of wording remains outstanding. These external gates are not claimed complete. No item was promoted based on aggregate arithmetic alone; each promotion is listed in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv) with its row-level implementation, resolved-path, validation, evidence and limits.

**Current 597-item primary-disposition totals: 340 Implemented + 162 BUILD + 10 LATER + 9 INVESTIGATE + 76 EXCLUDE = 597.** The remaining 162 BUILD rows are 62 PARTIAL + 100 DEFERRED. This is the current count to use in future queries. The 22-Oct 597-row register and the 18-Oct source snapshot remain preserved as historical evidence; apply the 23-Oct reconciliation overlay for the current status. This does not authorize production writes, deployment, provider actions or work on deferred rows.

---

# BUILD-245 implementation record (2026-10-22)

Authority: HU+DI "Full BUILD Implementation Mandate and Mandatory Completion Audit" over the
22-Oct-2026 reconciled 597-row register (245 BUILD records). Per-record status, behaviour,
code paths (with line numbers), validation and limits: `BUILD245_LEDGER_2026-10-22.csv`.
Decisions and actions only HU / HU+DI can take: `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md`.

## Outcome (honest)
* 245 records: **83 DONE (verified), 62 PARTIAL, 100 DEFERRED, 0 NOT DONE.** Not complete.
* Every DEFERRED record is deferred for a recorded decision/blocker (frozen rule conflict, Zoho
  authority, unapproved provider/wording/legal text, no tracking data). None was moved to
  LATER/EXCLUDE; "recommend EXCLUDE" items are only recommendations.
* Final full suite on the final tree: `pytest -q -p no:cacheprovider` -> **2764 passed**, exit 0,
  1902.40 s, PostgreSQL 17.5 (local, throw-away), mock/local evidence. Ruff format/check clean;
  `makemigrations --check` no changes. CI was NOT run. Nothing staged, committed or pushed. (Superseded 2026-10-23: committed and pushed, CI green on `02ec994`, full suite 2765 passed; see the follow-up section.)

## What was built (packs)
Orders (channel, PO number, manual fulfilment, abandoned checkouts, business-order cancellation
charge decided by Admin), draft/assisted orders with payment link, contact retention and legal
hold (MF-089), sign-in help and data request (MF-105), payment reconciliation view (MF-065),
customer segments/bulk actions/companies/import, discounts (scopes, automatic, BxGy, comments),
rich text, product master data, attributes, families/links, product CSV import, commercial
verification marker, library images, verified-buyer reviews with moderation, read-only Zoho
stock copy + Inventory page + alert + CSV, report library with pins, read-only Settings overview,
Google product feed (off by default), packing-slip PO number.

## Migrations (all additive, applied only to throw-away test databases)
orders 0028-0034, catalogue 0012-0015, identity 0006-0008, backoffice 0004. (orders 0025-0027 were
from earlier sessions and were uncommitted then; all are committed now.) None applied to `effyklean` at the time; applied on 2026-10-23 after a verified backup (see the follow-up section and `PROJECT_LOG.md`).

## Existing tests changed (disclosed; none weakened to pass)
* `test_order_tools.py`: stats-strip test updated for the new cancelled/returned figures; settlement
  text assertion now the "Financial reconciliation" card.
* `test_customer_order_actions.py`: staff cancelling a business order now passes `charge="0"` (the
  Admin must state the charge; fixes a defect where the B2C 20% applied to Distributor/Bulk).
* `test_contact_form.py`: production guard now defaults to the approved wording.
* `test_admin_ux.py`: product-list query budget 28 -> 30 (two constant queries for the stock copy; the
  budget is about not growing with rows).
* Governance allow-lists extended for BUILD-authorised files, fields, routes, migrations and tables:
  `test_migrations.py`, `test_catalogue_model.py`, `test_catalogue_boundaries.py`,
  `test_f05_boundaries.py`, `test_f06_boundaries.py`, `test_f07b_boundaries.py`,
  `test_identity_boundaries.py`. Code that broke a boundary was fixed instead (identity no longer
  imports orders; storefront reads catalogue rules through `customer_view`; storefront payment-link
  errors come via `wiring`).
* `AC_TEST_INDEX.md` regenerated by `scripts/ac_index.py`.

## Self-introduced defects found and fixed during the work
* A settings edit briefly clobbered `MEDIA_PUBLIC_BASE_URL` (caught by `test_settings.py`, fixed).
* Boundary violations listed above (caught by the architecture guard tests, fixed in code).
* `data_request.py` selected subscribers directly; moved behind `subscriptions.record_for`.

## Not run / not evidenced
No CI; no browser check on this tree (last real-browser responsive check was 19-Oct); no real
provider call except one earlier read-only Zoho Inventory sandbox read for field names; no e-mail
sent; Zoho stock refresh not exercised through the app against the sandbox.

## Follow-up 2026-10-23: browser check of the new pages (MA-SYS-012 evidence)
Headless Chromium (playwright-core, local cache) against `runserver` on 127.0.0.1:8012 with a
throw-away database (seeded test data; Zoho blank), signed in as the local test Director with MFA:
47 Admin pages at 390, 768 and 1280 px = 141 checks, plus 5 storefront pages (including the new
account-help and review pages) at three widths. It found and I fixed two real defects the tests had
missed: the GST summary returned HTTP 500 for an order with an unrecognised delivery state (now
counted, not split, with a test), and the Customers page overflowed by 76 px at 390 px because of
`white-space:nowrap` on fieldset labels (CSS fix). Final run: 0 HTTP errors, 0 overflow, 0 missing
alt/labels/h1/lang issues. Limits: page-level overflow and basic label checks only; no tablet
visual-quality judgement; local data set. Focused tests re-run: 93 passed; the full suite was not
re-run for these two narrow changes.

The address book (MA-CUS-006) was NOT built: the single saved address, its three-month retention
and active-order protection are an explicit HU+DI decision (2026-10-16); several addresses need a
new retention/limit rule, so it is parked for HU+DI.


## Follow-up 2026-10-23 — local migration and status reconciliation

- CI fix commit `02ec994` is pushed; CI run `39885661301` succeeded.
- The local Docker PostgreSQL database `effyklean` was backed up with `pg_dump -Fc`; a restore was verified by comparing row counts across 62 tables (34 non-empty). The 15 pending migrations were then applied successfully. Post-migration `showmigrations` reports no unapplied migrations; `manage.py check` and `makemigrations --check` are clean. Existing data was preserved; the database was not reset or recreated.
- HU tested the local storefront and admin pages and reported that they work as expected.
- The latest agent report gives implementation-status totals of 83 DONE, 64 PARTIAL, 100 DEFERRED and 0 NOT DONE. These total 247, not the 245 BUILD records. The referenced per-item file `BUILD245_LEDGER_2026-10-22.csv` is absent from the public repository tree. These aggregate counts are recorded as reported, not reconciled or applied to individual rows. Do not infer item-level statuses until the agent supplies the missing per-item mapping and reconciles the discrepancy.
- Earlier verification on commit `02ec994`: 2,765 tests passed; Ruff format/check and Django checks were clean. The local migrations and HU's manual storefront/admin testing are separate follow-up evidence.


## Correction — BUILD-245 ledger located and reconciled (2026-10-23)

The public per-item ledger is present at `docs/ImplementationPlan/BUILD245_LEDGER_2026-10-22.csv`. The earlier note above saying it was absent from the public repository tree was incorrect and is superseded by this correction. The CSV contains 245 data rows and 245 unique non-empty IDs. Its row-level `primary_status` counts reconcile exactly: 83 `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED` (245 total); there are 0 `NOT DONE` rows. The later aggregate of 64 PARTIAL / 247 total was erroneous; use the ledger's 62 PARTIAL count. Individual BUILD status evidence is available directly in the CSV, so no status needs to be inferred from aggregate figures.

The 22-Oct baseline primary disposition was 257 Implemented, 245 BUILD, 10 LATER, 9 INVESTIGATE, and 76 EXCLUDE. Current 23-Oct disposition is 340 Implemented, 162 BUILD, 10 LATER, 9 INVESTIGATE, and 76 EXCLUDE; use the reconciliation overlay. These disposition counts are distinct from the BUILD ledger's implementation-status counts.