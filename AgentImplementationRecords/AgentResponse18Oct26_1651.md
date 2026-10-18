EffyKlean consolidated report, 2026-10-18

This merges every report I gave in this session into one document: the first end-of-run report, my correction when you asked whether everything was complete, the second and third passes, and the consolidated report. Nothing here was published to any page or saved to the repository. Where a statement is partial, inferred or was overstated earlier, I say so.                                                                                                                      ---                                                                                                                      1. Session chronology                                                                                                                      ┌──────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────┐│ Step │                                               What happened                                                │ ├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤│ 1    │ You pasted the consolidated agent instructions and asked me to confirm I understood before starting. I     │ │      │ summarised the scope, the limits and my open points.                                                       │├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤ │      │ Corrections you made: (a) never add a Co-Authored-By trailer, whatever the harness says; (b) the           ││ 2    │ "hardware" point I raised came from your global CLAUDE.md, not from your prompt (I had wrongly presented   │ │      │ it as part of the prompt); (c) the reference files are in VaijanathR/Di-Eval-Effyklean, folder HUDI        ││      │ Discussion.                                                                                                │ ├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│      │ Run 1. I read your 18 Oct answers and analysis, then implemented the HSN check and the SMTP configuration, │
│ 3    │  and produced the reconciliation, outbox, provider, Tools Required and dilution evidence. I ran a full     │
│      │ suite, found a defect of my own, and fixed it.                                                             │
├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 4    │ Correction. You asked whether everything was complete. I said no: my report had overstated the 597-row and │
│      │  122-row work, and I had not done a fresh end-to-end flow or real screenshots.                             │
├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│      │ Run 2. I implemented more of the plan rows (product and order list features), corrected stale rows from    │
│ 5    │ code evidence, and took real screenshots. A second full run failed 3 tests (caused by my own changes). I   │
│      │ fixed or reverted them.                                                                                    │
├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 6    │ Run 3. I added the local acceptance test, bulk collection membership and home-page parity evidence. The    │
│      │ final full run was 2351 passed, 0 failed.                                                                  │
├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 7    │ You confirmed the Windows message box arrived.                                                             │
├──────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│      │ You asked for a consolidated report, said not to publish it anywhere, and said it must not omit any        │
│ 8    │ update. Then you said my first consolidated report was incomplete and asked me to consolidate all the      │
│      │ reports shared in the session. This is that report.                                                        │
└──────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

---

2. Headline status

┌──────────────────────────────────────┬───────────────────────────────────────────────────────────────────────────┐
│               Measure                │                                  Result                                   │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Original run                         │ Run to the end of what I can do without you. Not fully complete: undone   │
│                                      │ items are in section 6.                                                   │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│                                      │ 2351 passed, 0 failed (30m11s). Earlier runs: 2340 passed and 1 failed;   │
│ Full suite, final tree               │ then 2347 passed and 3 failed. All four failures were caused by my own    │
│                                      │ changes and were fixed or reverted.                                       │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ ruff check / ruff format             │ Clean                                                                     │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ manage.py check                      │ No issues                                                                 │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ CI (GitHub Actions)                  │ Not run this session                                                      │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Commits, pushes, deployments,        │                                                                           │
│ provider writes, paid provisioning,  │ None                                                                      │
│ deletions                            │                                                                           │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Production                           │ Untouched                                                                 │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Repository                           │ 31 changed or new paths, none staged. main is still 3 commits ahead of    │
│                                      │ origin/main (02aeb80, 7a13cf8, 625e210).                                  │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Windows message box and sound        │ You confirmed you received the message box.                               │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ Development database                 │ 3 hidden draft blog posts added. No migration applied. No order, payment  │
│                                      │ or provider record changed.                                               │
└──────────────────────────────────────┴───────────────────────────────────────────────────────────────────────────┘

---

3. Controlling context and HU decisions applied

Sources read. I read your answers register (RESP_18OCT_QA_HU ANSWERS.md) and the analysis (RESP_18OCT2026_1149.md) from
your repository. I did not fetch the 15 Oct handover or the Delta plan documents from there; I used the local copies
and the project records. I also used the frozen SPEC with CR-004 to CR-009, the Delta status register and the
repository code and tests.

Your 18 Oct answers and how each was applied

┌──────┬───────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Item │                                                Applied as                                                 │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 1,   │ Dispatch timing and the Shiprocket trigger stay with the Zoho workflow. Shiprocket testing is deferred.   │
│ 16   │ No code, no investigation.                                                                                │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 2    │ The general dilution rule was applied as a check only. No directions were edited.                         │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 3    │ The 15 SEO drafts stay unpublished.                                                                       │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 4    │ Tools Required evidence produced (section 4.B).                                                           │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 5    │ Weight, dimension and barcode fields kept for Admin entry. No values invented.                            │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 6    │ HSN fields kept, and a website-vs-Zoho comparison added.                                                  │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 7,   │ Zoho owns GST, invoicing, stock and low-stock. I built nothing parallel. 15 rows were closed as "not      │
│ 20   │ built".                                                                                                   │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 8    │ Push not done. The three commits were not inspected in this run.                                          │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 9    │ Media folders retained. Nothing deleted. Spaces not provisioned.                                          │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 10   │ GoDaddy SMTP configuration and a no-send check added. No new provider.                                    │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 11   │ Backup capability and the local drill retained. Retention periods deferred.                               │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 12   │ The existing plan is the baseline. I reconciled the 597 activities and the 122 rows against evidence.     │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 13   │ Scopes reconciled (section 4.B).                                                                          │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 14   │ The temporary tunnel arrangement is unchanged. It is already in the go-live removal register.             │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 15   │ Source knowledge is preserved. No live changes.                                                           │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 17   │ The five old outbox tasks are documented (section 4.B).                                                   │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 18   │ Parked: it conflicts with a frozen SPEC change (CR-009).                                                  │
├──────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ 19   │ Verified: the Director has the Admin capabilities plus approval, removal and deletion. No Marketing role  │
│      │ exists.                                                                                                   │
└──────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────┘

---

4. COMPLETED tasks

A. Code and configuration

#: A1
Item: HSN consistency check (website vs Zoho). Report-only: it never pushes to Zoho and guesses no value. It reports a
difference, or a one-sided empty value.
Task ID: HU item 6, MF-054
Evidence: zoho_item_sync.py, sync_zoho_items.py, zoho_product_sync.py. 2 new tests in test_zoho_item_sync.py (61 passed

with the sync-task tests).
────────────────────────────────────────
#: A2
Item: GoDaddy SMTP configuration. Settings now come from the environment, and the default stays the console backend. A
new command check_email_config connects, starts TLS and authenticates. It never sends mail and never prints the
password.
Task ID: HU item 10, MF-079 (in progress)
Evidence: config/settings/base.py, check_email_config.py, test_email_config_check.py (4 passed). My first version
called
smtp.login, which an identity-boundary guard forbids. I fixed it with Django's get_connection().open() and did not
weaken the guard.
────────────────────────────────────────
#: A3
Item: Product list collection filter (manual and automated collections)
Task ID: PRD-007
Evidence: queries.py, catalogue_views.py; tested
────────────────────────────────────────
#: A4
Item: Product list "Category / type" column
Task ID: PRD-011
Evidence: products.html; tested
────────────────────────────────────────
#: A5
Item: Saved product views: private to the staff member, allow-listed keys, audited
Task ID: PRD-013
Evidence: catalogue_views.py, urls.py; tested
────────────────────────────────────────
#: A6
Item: Product sort by newest created and recently updated
Task ID: PRD-101
Evidence: queries.py; tested
────────────────────────────────────────
#: A7
Item: Bulk add/remove of selected products to a manual collection, audited, with per-product skip reporting
Task ID: PRD-095
Evidence: product_bulk_collection; tested
────────────────────────────────────────
#: A8
Item: Order list payable-amount range filter, kept in saved views and exports; bad input returns 400
Task ID: ORD-019
Evidence: ops_views.py, staff_view.py; tested
────────────────────────────────────────
#: A9
Item: Admin order link to the customer tracking page
Task ID: ORD-143
Evidence: order_detail.html; tested
────────────────────────────────────────
#: A10
Item: Rendering test confirming the customer-record link and the "first order / order N of M" line already work
Task ID: ORD-041, ORD-045
Evidence: test_product_list_filters.py
────────────────────────────────────────
#: A11
Item: Product-list query budget raised 25 → 27. The two extra queries are constant (collection options, saved views).
The test is about not growing with row count.
Task ID: –
Evidence: test_admin_ux.py
────────────────────────────────────────
#: A12
Item: Local end-to-end acceptance test: two products (ACC-A ×1, ACC-B ×2) under an issued TESTCODE.
Task ID: AD-10
Evidence: tests/test_local_acceptance.py; passes; local stubs only

The steps in the acceptance test (A12):
- Zoho down: payment kept, order PAYMENT_CONFIRMED, nothing dispatchable.
- Three failed attempts reach ZOHO_SYNC_FAILED, with nothing duplicated.
- The Admin retry confirms exactly once, and a repeat is idempotent.
- With the payment flipped to failed there is no shipment. Restored, exactly one shipment goes out the next day.
- A read-only testcode_report changes no records.

B. Evidence and verification (no content changed)

Outbox: the five old tasks (HU item 17). I queried the development database read-only. All five were closed DONE at
2026-10-17 16:34:56 UTC by the worker's idempotency branch ("already confirmed"). No Zoho or Shiprocket call occurred.

┌──────┬──────────────┬────────────────────┬─────────────────────────┬───────────┬───────────────┬────────────────┐
│      │              │                    │                         │   Real    │               │                │
│ Task │     Kind     │       Order        │    What "DONE" meant    │ sandbox   │ Sandbox path  │     Action     │
│      │              │                    │                         │   call    │               │                │
├──────┼──────────────┼────────────────────┼─────────────────────────┼───────────┼───────────────┼────────────────┤
│      │              │ 15                 │ The stub had already    │           │ Yes for new   │ Retain; the    │
│ 11   │ ZOHO_CONFIRM │ (EKI-1026-1600018) │ confirmed it (simulated │ No        │ orders        │ order is not   │
│      │              │                    │  event)                 │           │               │ re-synced      │
├──────┼──────────────┼────────────────────┼─────────────────────────┼───────────┼───────────────┼────────────────┤
│ 15   │ ZOHO_CONFIRM │ 16                 │ Same                    │ No        │ Yes           │ Retain         │
│      │              │ (EKI-1026-1700004) │                         │           │               │                │
├──────┼──────────────┼────────────────────┼─────────────────────────┼───────────┼───────────────┼────────────────┤
│      │              │                    │ The shipment was        │           │ No            │                │
│ 12   │ SHIPMENT     │ 5                  │ already created by the  │ No        │ (Shiprocket   │ Retain the     │
│      │              │ (EKI-1026-0900001) │ local stub              │           │ deferred)     │ stub           │
│      │              │                    │ (LOCAL-AWB-…)           │           │               │                │
├──────┼──────────────┼────────────────────┼─────────────────────────┼───────────┼───────────────┼────────────────┤
│ 13   │ SHIPMENT     │ 6                  │ Same                    │ No        │ No            │ Retain         │
│      │              │ (EKI-1026-0900002) │                         │           │               │                │
├──────┼──────────────┼────────────────────┼─────────────────────────┼───────────┼───────────────┼────────────────┤
│ 14   │ SHIPMENT     │ 8                  │ Same                    │ No        │ No            │ Retain         │
│      │              │ (EKI-1026-1400002) │                         │           │               │                │
└──────┴──────────────┴────────────────────┴─────────────────────────┴───────────┴───────────────┴────────────────┘

All five orders carry LOCAL-ZOHO-… references and simulated trails. The four real sandbox Sales Orders belong to orders
18–21 only.

Provider reads (sandbox only)
- Scopes. check_zoho_access reported "Missing required scopes: none". The token holds contacts.CREATE/READ,
  items.CREATE/READ, salesorders.CREATE/READ/UPDATE and settings.READ. The older handover's proposed items.CREATE,
  contacts.CREATE, salesorders.CREATE and salesorders.UPDATE are already granted. They match what the code calls: POST
  /items, /contacts, /salesorders, confirm, and void/cancel.
- Sales Order read-back. SO-00002 to SO-00005 (orders 18–21) read back as confirmed, not invoiced, unpaid, shipment
  pending, 0 invoices, 0 packages, total 195.00. Order 17 has no Sales Order (ZOHO_SYNC_FAILED, free-text test
  address).
- Environment (presence and length only). The Zoho Payments and Inventory credentials and keys are present. The sandbox
  flags are on, and the Payments API base is the sandbox host. ZOHO_SYNC_ENABLED and
  ZOHO_SALES_ORDER_WRITES_AUTHORIZED are off. The Payments return URL still names www.effyklean.in; that is a
  sandbox-time value in the go-live removal register (T7).

Content and parity evidence

#: B1
Item: Tools Required exists only on the Shopify description of EK-HHLD-FCR and EK-BLP-000004: a table of "Bucket with
capacity of 5 litres or more ×1" and "1 litre measuring cylinder ×1". It is missing from EffyKlean revisions v1 and
v2, so it does not show on effyklean.in or in Admin.
Evidence: docs/content/TOOLS_REQUIRED_EVIDENCE_2026-10-18.html, tools_required_shopify_source_2026-10-18.png (the
Shopify section highlighted), storefront_EK-HHLD-FCR_no_tools_section_2026-10-18.png (the live page)
────────────────────────────────────────
#: B2
Item: Dilution check on the 15 products, against "makes N litres, dilute with about N litres". See the table below. Ten

products show no detectable conflict.
Evidence: docs/content/DILUTION_CONSISTENCY_CHECK_2026-10-18.md
────────────────────────────────────────
#: B3
Item: Home-page parity, .com vs local (desktop and mobile screenshots). Branding, hero and Smart solutions block are
close. Differences: no Blogs menu and no floating WhatsApp button locally, and a different menu order. Local adds
Subscribe and Track order. Only the home page was compared.
Evidence: docs/discovery/VISUAL_PARITY_HOME_2026-10-18.md, docs/content/parity_2026-10-18/
────────────────────────────────────────
#: B4
Item: Distributor enquiry (MF-008). The .com page says "fill the form below", but the form is script-injected and not
in
the static HTML. EffyKlean has its own application flow.
Evidence: same file
────────────────────────────────────────
#: B5
Item: Dry-run cleanup report. 17 development orders: 12 pure local stubs (orders 5–16), order 17 (the recovery test),
and orders 18–21 carrying real sandbox Sales Orders. Orders, payments and integration events are protected by foreign
keys and never offered for deletion. Candidates to clean when you authorize it: the Zoho sandbox Sales Orders SO-00002
 to 5 and the sandbox contacts and items created by tests (the code can only void or mark inactive, never delete),
plus 6 pending and 2 permanent ZohoSyncTask rows. Nothing was deleted.
Evidence: RUN_RECORD_2026-10-18.md section 8
────────────────────────────────────────
#: B6
Item: Verified already implemented, not rebuilt: saved-address retention (reset after delivery, active-order
protection,
purge command); the Director/Admin capability model; HTTPS redirect, HSTS (1 year) and secure cookies; the outbox and
Zoho handoff; NO PAYMENT → NO DISPATCH.
Evidence: Test results in section 5
────────────────────────────────────────
#: B7
Item: Three hidden draft blog posts imported into the development database. Nothing published.
Evidence: import_blog_source

Dilution findings (from the Shopify descriptions):

┌───────────────┬───────────────────────────────────────────────────────────────────────┐
│      SKU      │                                Finding                                │
├───────────────┼───────────────────────────────────────────────────────────────────────┤
│ EK-HHLD-FCR   │ Makes 1 L but the directions add 5 L; pours 100 ml from a 200 ml pack │
├───────────────┼───────────────────────────────────────────────────────────────────────┤
│ EK-HHLD-GC    │ Makes 1 L but the directions add 5 L                                  │
├───────────────┼───────────────────────────────────────────────────────────────────────┤
│ EK-HHLD-FCP   │ The text says both 1 and 5 L                                          │
├───────────────┼───────────────────────────────────────────────────────────────────────┤
│ EK-BLP-000004 │ Pours 100 ml; the pack is 200 ml                                      │
├───────────────┼───────────────────────────────────────────────────────────────────────┤
│ EK-BLP-000008 │ Pours 200 ml; the pack is 100 ml                                      │
└───────────────┴───────────────────────────────────────────────────────────────────────┘

Email: who sends what. Zoho sends order, invoice and delay messages by email and WhatsApp (your established workflow,
not duplicated). Shiprocket sends shipping and tracking WhatsApp messages (kept enabled). The website sends only the
Subscribe verification email today. The website events N1, N3 and N6–N9 are unsent and need your wording approval, plus
a decision on whether Zoho already covers N1.

C. Reconciliation and records

597 activities (docs/discovery/RECONCILED_597_STATUS_2026-10-18.csv). All original IDs are kept, along with the
2026-10-17 columns, plus two new columns. Final distribution:

┌────────────────────────────────────────────────────────────────────────────────────────────────────────┬──────┐
│                                                 Status                                                 │ Rows │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Implemented, area tests passed (keyword-level mapping, not row assertions)                             │ 156  │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Implemented, code/route evidence                                                                       │ 72   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Implemented and verified (earlier)                                                                     │ 33   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Implemented, other evidence (e.g. real sandbox evidence, tested today, retained SEO drafts)            │ 10   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Closed, Zoho-owned, not built                                                                          │ 15   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Deferred / excluded / not authorized                                                                   │ 148  │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Proposal only, pending HU+DI naming                                                                    │ 66   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Awaiting HU+DI decision                                                                                │ 58   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Needs reconciliation                                                                                   │ 11   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Implemented but not fully validated                                                                    │ 13   │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Direction recorded (Admin enters values later)                                                         │ 3    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Blocked: conflicts with frozen SPEC (customer deletion)                                                │ 3    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Blocked: cart notice (MF-027)                                                                          │ 1    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Partial: GST and invoicing verification (MF-054), parity (MF-007), blog drafts (MF-086), SMTP (MF-079) │ 4    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Observed: MF-008, MF-094                                                                               │ 2    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Deferred Shiprocket (MF-070); separate transition (MF-092)                                             │ 2    │
├────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────┤
│ Total                                                                                                  │ 597  │
└────────────────────────────────────────────────────────────────────────────────────────────────────────┴──────┘

"Implemented" here means the screen or function exists and the area tests pass. It does not mean accepted. Batch 1 and
the 122-row map remain not accepted. The 139 acceptance criteria are a separate measure and were not used to shrink the
597.

122 audit rows (classified in ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md):

┌───────────────────────────────────────────────────┬──────┐
│                       Class                       │ Rows │
├───────────────────────────────────────────────────┼──────┤
│ A: already decided, excluded                      │ 17   │
├───────────────────────────────────────────────────┼──────┤
│ B: nothing to implement                           │ 1    │
├───────────────────────────────────────────────────┼──────┤
│ C: superseded by HU 18-Oct (Zoho owns inventory)  │ 18   │
├───────────────────────────────────────────────────┼──────┤
│ D: implemented, referenced by ID                  │ 13   │
├───────────────────────────────────────────────────┼──────┤
│ E: derivable YES, implementation not traced by ID │ 73   │
└───────────────────────────────────────────────────┴──────┘

No row of the 122 needs a new HU decision. A second pass checked each class E row against the code:
- Built: category/type/use-case filters, descriptions and dilution fields, product history, primary-image upload,
  automated collections with SEO and image fields, the order-list figures strip, the "mark delivered" action, theworker and mapping views, staff sign-in history, recent activity, business figures and the responsive shell.
- Implemented this session: PRD-007, PRD-011 and ORD-143.
- Superseded because Zoho owns them: PRD-008, PRD-010, PRD-034, PRD-035 and ORD-130.
- Not applicable (one channel): PRD-012 and COL-008.
- Not built (Shopify-only constructs): PRD-043, PRD-044 and PRD-046.
- Blocked by frozen design: PRD-052, PRD-053 and PRD-063.

Records updated: RUN_RECORD_2026-10-18.md (sections 1–12), PROJECT_LOG.md, the Delta status register, the CLAUDE.md state paragraph, and README.md.
D. Settled by your rulings (closed, not built)
- 15 Zoho-owned rows, including MF-078, MF-083, MF-101, MA-ORD-039, MA-ORD-090 and the stock and low-stock rows.
- 18 inventory rows (INV-001 to INV-024), superseded.- MF-070 (Zoho-managed Shiprocket), deferred.
- MF-074 and MA-PRD-036/037 (weights and dimensions), entered by Admin later.

---

5. Tests and checks run

┌───────────────────────────────────────────────────────────────────────────────┬──────────────────────────────────┐
│                                      Run                                      │              Result              │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Saved shipping and business accounts                                          │ 43 passed                        │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Journey, payment, outbox and Zoho handoff set (test_e2e_prototype,            │                                  │
│ test_outbox, test_f05_checkout, test_phase1_payments, test_zoho_payments,     │ 234 passed                       │
│ test_zoho_inventory, test_sales_order_safeguards,                             │                                  │
│ test_payment_reconciliation, test_order_operations)                           │                                  │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Item sync and sync tasks                                                      │ 61 passed                        │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Email, contact form and subscribe                                             │ 77 passed                        │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Settings, CSP and request security                                            │ 89 passed                        │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Orders list, order tools and product filters                                  │ 81 passed                        │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Cart, checkout and storefront parity (including the reverted change)          │ 246 passed                       │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Re-run of files that had failed                                               │ 247 passed                       │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│                                                                               │ 2340 passed, 1 failed (my SMTP   │
│ Full suite, 1st                                                               │ check vs an identity-boundary    │
│                                                                               │ guard; fixed)                    │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│                                                                               │ 2347 passed, 3 failed (my cart   │
│ Full suite, 2nd                                                               │ notice broke two guards; the     │
│                                                                               │ query budget was exceeded)       │
├───────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────┤
│ Full suite, final tree                                                        │ 2351 passed, 0 failed (30m11s)   │
└───────────────────────────────────────────────────────────────────────────────┴──────────────────────────────────┘

What these do not show
- The sandbox evidence was reused from 2026-10-17, not repeated. No new real-sandbox payment or Sales Order was created
  this session; only reads were made.
- The "area tests passed" rows are a keyword mapping to passing test files, not per-row assertions.
- The ORD-019 and PRD-007/013/095 tests exercise the code through the test database, not the live Admin in a browser.
- CI was not run.

---

6. UNDONE tasks

Category 1: Third-party integration

#: 1.1
Undone task: Zoho Payments webhook (MF-043/051 follow-up)
Reason: Not registered. The sandbox token gets 401 on /webhooks and lacks ZohoPay.settings.*.
Needed: Register the tunnel URL in the portal, or re-grant the scope.
────────────────────────────────────────
#: 1.2
Undone task: Seven Zoho Inventory scopes you authorized
Reason: items.UPDATE, contacts.UPDATE, invoices.READ, customerpayments.READ, packages.READ, shipmentorders.READ and
inventoryadjustments.CREATE are not on the token. Nothing in the code needs them yet, but I cannot read invoices,
payments or packages, and the price-update leg cannot run.
Needed: Re-grant the Self Client token.
────────────────────────────────────────
#: 1.3
Undone task: Invoice automation in the sandbox org
Reason: The sandbox Sales Orders stay not invoiced and unpaid. I built no invoice logic, as you directed. Whether the
Zoho Flow runs there is unverified.
Needed: Check the Flow in the sandbox org.
────────────────────────────────────────
#: 1.4
Undone task: Shipment trigger
Reason: Whether Zoho starts Shiprocket when a Sales Order is confirmed is untested. You deferred it.
Needed: Later testing phase.
────────────────────────────────────────
#: 1.5
Undone task: Shiprocket sandbox and real status (INT-006)
Reason: Never contacted; stub only.
Needed: Deferred by you.
────────────────────────────────────────
#: 1.6
Undone task: Real stock behaviour
Reason: The sandbox has zero stock. Earlier tests forced 999, so availability, reservation and decrement are not
evidenced.
Needed: Real stock in a Zoho org.
────────────────────────────────────────
#: 1.7
Undone task: GoDaddy mailbox (MF-079)
Reason: check_email_config has not been run against GoDaddy. Authentication and delivery are unverified.
Needed: Mailbox credentials in the server environment.
────────────────────────────────────────
#: 1.8
Undone task: Refund execution and assisted payments (MF-060, MF-064, MA-ORD-070)
Reason: DC-15 and DC-22 are undecided.
Needed: Decisions, then a sandbox test.
────────────────────────────────────────
#: 1.9
Undone task: Zoho price mismatch and production SKU codes
Reason: Two SKUs (EK-HHLD-AR and EK-HHLD-FCP) differ on price against pre-existing sandbox items. The production SKU
codes are unconfirmed.
Needed: Confirm production Zoho items.
────────────────────────────────────────
#: 1.10
Undone task: Zoho Inventory credential rotation
Reason: Your own follow-up.
Needed: Rotation.
────────────────────────────────────────
#: 1.11
Undone task: DigitalOcean Spaces and real media migration
Reason: Not provisioned. The migration was only tested against an in-memory bucket. Duplicate video folders (14
matching
hashes), 13 missing posters and 3 unreferenced images are retained until a verified copy exists.
Needed: Authorize and provision.
────────────────────────────────────────
#: 1.12
Undone task: Hosting and operations: App Platform plus Managed PostgreSQL, a stable webhook URL, scheduler, process
supervision (MF-109), observability (MF-111), secrets management (MF-110), performance baseline on hosting (MF-114),
production migrations plan (MF-113).
Reason: No hosting exists. Phase 2 needs its own authorization.
Needed: Authorize.
────────────────────────────────────────
#: 1.13
Undone task: CI
Reason: Not run this session.
Needed: Push or trigger.
────────────────────────────────────────
#: 1.14
Undone task: WhatsApp floating button (MF-094)
Reason: It exists on .com and not locally.
Needed: HU+DI decision.
────────────────────────────────────────
#: 1.15
Undone task: effyklean.com redirect and Shopify account
Reason: A separate transition phase.
Needed: Later.
────────────────────────────────────────
#: 1.16
Undone task: Scheduled report delivery (MA-ANA-018)
Reason: Needs email.
Needed: Item 1.7.

Category 2: HU approval or response

#: 2.1
Undone task: Customer deletion (CR-010), MA-CUS-009/041/050
Reason: HU item 18 wants Admin to delete Distributor/Bulk customer records without escalation. Frozen CR-009 / AC-9.6
gives removal of a suspended role to the Director alone. Deletion is Director-only. The code refuses any account
holding a business role, and an active Distributor cannot be removed at all. Implementing it would silently override a
 frozen change. I need a controlled change on who may delete a business customer record.
────────────────────────────────────────
#: 2.2
Undone task: Dilution values for the five flagged SKUs
Reason: No per-SKU source data. I will not invent it.
────────────────────────────────────────
#: 2.3
Undone task: Tools Required
Reason: Decide whether to add it to the two floor-cleaner products.
────────────────────────────────────────
#: 2.4
Undone task: Email wording
Reason: N1, N3 and N6–N9 are unapproved, and Zoho's overlap with N1 is undecided.
────────────────────────────────────────
#: 2.5
Undone task: Privacy, terms and cookie wording (MF-084/089/093)
Reason: Needs your approved legal text. Retention is also open.
────────────────────────────────────────
#: 2.6
Undone task: 15 SEO drafts and 3 blog drafts
Reason: Need Director review and your claim checks before any publication.
────────────────────────────────────────
#: 2.7
Undone task: HSN 3402 default
Reason: The accountant should review it. The production Zoho HSN mapping is unconfirmed.
────────────────────────────────────────
#: 2.8
Undone task: Weights, dimensions, barcodes, prices
Reason: You will enter these as Admin.
────────────────────────────────────────
#: 2.9
Undone task: Schema and scope decisions
Reason: The nine new SKU fields vs SPEC 13.9 / AC-13.6, PRD-043/044/046, price per litre (PRD-028), the pack-size
selector (MF-024), related products (MF-026), wishlist/reviews (MF-033), cart across devices (MF-050), customer
mapping to Zoho contacts (MF-055), free-shipping bar wording (MF-045).
────────────────────────────────────────
#: 2.10
Undone task: Draft orders, manual payment and notifications
Reason: MA-DRF-001 to 021, DC-22, MA-ORD-077, MA-SET-007, DC-21 templates and toggles, abandoned checkouts (MA-ORD-110
to 112), MA-ORD-095 and MA-ORD-089.
────────────────────────────────────────
#: 2.11
Undone task: Batch 1 items
Reason: T41 scheduled publication, T35 rejected-delivery log, T38 slug edit (PRD-063).
────────────────────────────────────────
#: 2.12
Undone task: Frozen-design changes
Reason: PRD-052/053: withdrawing or unlisting a published product conflicts with F-07A "no withdrawal". MF-027: the
added-to-cart notice needs a cookie or a changed redirect, which frozen guard tests forbid. I tried it and reverted
it.
────────────────────────────────────────
#: 2.13
Undone task: CSP enforcement
Reason: Needs your browser check of Pay now, return and failure, then a soak period.
────────────────────────────────────────
#: 2.14
Undone task: Acceptance and commits
Reason: Batch 1 and the 122-row map are not accepted. Committing this session's 31 paths and pushing the 3 local
commits
need your approval.
────────────────────────────────────────
#: 2.15
Undone task: Backup retention periods
Reason: Deferred by you.
────────────────────────────────────────
#: 2.16
Undone task: 66 "proposal only" and 58 "awaiting HU+DI decision" rows
Reason: Mostly features never named by HU+DI, such as traffic analytics, channels, languages, segments, command
palette,
PO number, map view and source attribution.

Category 3: Blockers due to dependencies, and work I did not do

┌──────┬──────────────────────────────────┬────────────────────────────────────────────────────────────────────────┐
│  #   │           Undone task            │                          Dependency or reason                          │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│      │ Per-row validation of the 597    │ No external dependency. This is work I did not complete. About 156     │
│ 3.1  │ activities and the 73 class E    │ rows rest on keyword-level coverage, and the 73 are evidenced by route │
│      │ rows                             │  and code, not by per-row assertions.                                  │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.2  │ Visual parity beyond the home    │ More browser passes. The catalogue is loaded, so this is doable.       │
│      │ page (MF-007)                    │                                                                        │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.3  │ Add-to-cart notice (MF-027)      │ Blocked by the frozen cart contract (item 2.12).                       │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.4  │ Release acceptance gate (MF-115) │ Depends on MF-043, MF-052, MF-053, MF-054 and MF-107 to 113.           │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.5  │ Committed-tree proof (MF-004)    │ Depends on the baseline commit decision (MF-002). The 2351 passes are  │
│      │                                  │ on the uncommitted tree.                                               │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.6  │ Customer-facing website emails   │ Depend on 1.7 (credentials) and 2.4 (wording).                         │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.7  │ Process supervision, performance │ Depend on hosting (1.12).                                              │
│      │  baseline and migrations plan    │                                                                        │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.8  │ Admin price-update leg to Zoho   │ Depends on items.UPDATE (1.2).                                         │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.9  │ Blog publication and the Blogs   │ Depend on Director review (2.6).                                       │
│      │ menu                             │                                                                        │
├──────┼──────────────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ 3.10 │ Schema-dependent product         │ Depend on 2.9.                                                         │
│      │ features                         │                                                                        │
└──────┴──────────────────────────────────┴────────────────────────────────────────────────────────────────────────┘

---

7. Provider status

┌──────────────────────┬───────────────────────────────────────────────────────────────────────────────────────────┐
│       Provider       │                                          Status                                           │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ Zoho Inventory       │ Reads verified this session. Writes verified earlier (2026-10-17), not repeated.          │
│ (sandbox)            │                                                                                           │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ Zoho Payments        │ Credentials and flags present. The 2026-10-17 real payment is reused as evidence. The     │
│ (sandbox)            │ webhook is not registered.                                                                │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ Shiprocket           │ Never contacted. Stub only.                                                               │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ GoDaddy SMTP         │ Not contacted. No credentials.                                                            │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ Zoho Flow /          │ Not evidenced.                                                                            │
│ invoicing            │                                                                                           │
├──────────────────────┼───────────────────────────────────────────────────────────────────────────────────────────┤
│ Production           │ Untouched.                                                                                │
└──────────────────────┴───────────────────────────────────────────────────────────────────────────────────────────┘

8. Safety, scope and honest corrections

- Not done: no commits, staging, push, deployment, DNS change, provider write, paid service or deletion.
- Preserved: the home-page link rearrangement files were not modified. config/settings/local.py had an earlier
  uncommitted edit and I left it. Secrets were checked for presence and length only.
- Reverted: the add-to-cart notice, which violated two frozen guard tests.
- Test budget raised: the product-list query budget, 25 to 27, with the reason recorded.
- My earlier overstatements, corrected:
  - My first report implied the whole 597-row and 122-row queues had reached a terminal state. They had not.
  - I presented the area-tested rows as validated when they were keyword-level.
  - I had not done a fresh end-to-end flow, and I had no real screenshots; both were added later.
  - Several rows I called "proposal only" were in fact already implemented, because the old status file was stale. That
    is now corrected.

9. Changed paths

Modified
- CLAUDE.md, README.md, PROJECT_LOG.md
- config/settings/base.py
- modules/backoffice/ files:
  - catalogue_views.py, ops_views.py, queries.py, urls.py
  - zoho_item_sync.py, zoho_product_sync.py
  - management/commands/sync_zoho_items.py
  - templates/backoffice/order_detail.html, templates/backoffice/products.html
- modules/orders/staff_view.py
- tests/test_zoho_item_sync.py, tests/test_admin_ux.py
- The Delta status register and docs/foundation/ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md
- config/settings/local.py was already modified before the session and I left it as it was.

New
- modules/backoffice/management/commands/check_email_config.py
- tests/test_email_config_check.py, tests/test_product_list_filters.py, tests/test_local_acceptance.py
- docs/foundation/RUN_RECORD_2026-10-18.md
- docs/discovery/RECONCILED_597_STATUS_2026-10-18.csv, docs/discovery/VISUAL_PARITY_HOME_2026-10-18.md
- Under docs/content/: the dilution check, the Tools Required HTML and two screenshots, and parity_2026-10-18/ with four screenshots

10. Quick wins for you

1. Give the dilution values for the five SKUs (2.2) and a yes/no on Tools Required (2.3).
2. Register the webhook and re-grant the Zoho scopes (1.1, 1.2).
3. Put the GoDaddy credentials in the environment (1.7). After that I can run check_email_config against GoDaddy.
4. Approve committing this session's work and decide the push (2.14).
5. Say yes or no to the cart notice (2.12). The simplest answer is to drop it.
6. Check the Zoho Flow in the sandbox org (1.3).

11. Next checkpoint

1. You send decisions and actions from section 10, or new instructions for the rest.
2. You approve the commit, so the committed-tree proof (MF-004) can follow.
3. After the webhook registration and the Zoho scopes, I would run one real sandbox journey with webhook delivery. I would not repeat the local suites.  