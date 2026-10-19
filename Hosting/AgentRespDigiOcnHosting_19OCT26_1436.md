# DigitalOcean Restricted-Production Readiness — Final Evidence Pass
**Date:** 19 October 2026  
**Report status:** Read-only investigation  
**Labels:** VF = Verified Fact; REC = Recommendation; UNR = Unresolved; DEC = HU+DI Decision Required.

## Overall conclusion

Not ready to build. Four findings change the earlier plan:
- The real Zoho adapter makes every shipment attempt fail (§2).
- No code restricts the site to approved people (§5).
- TESTCODE is blocked in production settings, but the plan depends on it (§5, §7).
- App Platform scheduled jobs run at most every 15 minutes (§3).

The buildpack question is mostly resolved (§4). Nothing was changed, staged, committed, pushed or contacted.

## 1. Repository reconciliation

- VF: HEAD is 625e210, 3 commits ahead of origin/main (513fc98). Nothing is staged, there are no stashes, and the 3 unpushed commits are docs and one fix (02aeb80, 7a13cf8, 625e210).
- VF: The home-page link rearrangement is already on origin/main. It was committed in f48cda5, and git merge-base --is-ancestor f48cda5 origin/main confirmed it. No uncommitted home-page logic exists.
- VF: The tree now shows 89 modified and 24 untracked files (2,021 insertions and 227 deletions across the modified files), against 84 and 24 in my previous report. I did not touch them. CLAUDE.md changed on disk at 08:08 UTC and records an audit pass dated 19 Oct (2487 tests passed, nothing committed). Another actor is editing this tree, so the working tree is not a stable deployment source.
- VF, by purpose:

| Group | Files | Needed for restricted deployment? |
|---|---|---|
| Tests | 45 modified, plus 5 new test files | No, but they travel with the code |
| Webhook rejection log | modules/orders/models.py (+40), payment_flow.py, storefront/views.py, new migration 0025_rejected_webhook_deliveries.py | Yes, the model and its migration must ship together |
| Enquiry and contact forms | new enquiry_form.py, migrations 0026 and 0027, bulk_*, distributor_*, contact_pages.py | Yes, the models need their migrations |
| Zoho adapter edits | integrations/zoho_inventory.py (+40) and zoho.py | Yes, if the sandbox sales-order handoff is wanted |
| Settings | base.py (SMTP), local.py | Yes for email settings, with the DEC in §8 |
| Admin | catalogue_views.py and others | No |
| Docs and records | CLAUDE.md, PROJECT_LOG.md, 13 docs and audit files, screenshots | No |

- REC: The 3 migrations (0025, 0026, 0027) are untracked. Pushing the model changes without them would break migrate on a clean database. The batch has to go up in one approved commit set.

## 2. The SHIPMENT outbox task

- VF, creation: request_shipment (modules/orders/checkout.py:757-788) requires ORDER_READY, a succeeded payment, an earlier IST day, and no staff hold. It moves the order to SHIPMENT_PENDING, creates a Shipment (REQUESTED) and enqueues a SHIPMENT task. Only dispatch_ready_orders (:916-929, called by dispatch_orders) and the admin retry (order_actions.py:256) trigger it.
- VF, execution: outbox.run_due claims a task with a row lock and a 5-minute lease (outbox.py:190-205) and runs it through _run_shipment (:125-151). The task calls zoho.request_fulfilment inside _attempt_fulfilment (checkout.py:791-850).
- VF, the problem: The real adapter's request_fulfilment always raises ZohoNotSupportedError (integrations/zoho_inventory.py:736-740: "EffyKlean does not create shipments"). _attempt_fulfilment catches every exception as a failed attempt (:801-805).
- VF, consequence: Each shipment attempt fails. After 3 failures the order moves to SHIPMENT_FAILED with an ACTION_REQUIRED log entry saying "The shipment was not created". Retries use the delays at outbox.py:34.
- Verdict (VF): With the real adapter, the code does not represent the Zoho-managed handoff. Every dispatched order would end in SHIPMENT_FAILED. The stub passes only because it pretends to create shipments.
- VF, safe state today: Nothing enqueues SHIPMENT except request_shipment. If the dispatch job and the admin shipment retry are not used, the path stays dormant and EffyKlean's part ends at ORDER_READY after Zoho confirms.
- UNR: After a Sales Order is confirmed, how does EffyKlean learn about shipping and tracking? models.py:6-13 says the post-shipment order states were never approved, and I found no inbound path from Zoho or Shiprocket.
- DEC: Choose how ORDER_READY, SHIPMENT_PENDING and SHIPMENT_FAILED should represent a Zoho-managed handoff. This touches approved order states, so I did not resolve it.

## 3. Payment reconciliation and scheduled commands

- VF, reconcile_payment_attempts:
  - It calls reconcile_attempt for each CREATED attempt older than 30 minutes (payment_flow.py:124-226).
  - It asks the provider (gateway.fetch_order_state, a read) and acts only on the answer: it places the order if the full amount was captured, releases the attempt on a confirmed failure, and otherwise leaves the hold.
  - It writes local records, so it is not provider-side-effect-free. place_order is described as idempotent. The command has no lock, so overlap safety rests on place_order.
  - UNR: I did not trace place_order idempotency or the Zoho Payments fetch_order_state implementation.
- VF, run_scheduled: It takes a per-job Postgres advisory lock (scheduling.py:80-105) and skips an overlapping run.
- REC, locking: A session advisory lock only works over a direct connection. If jobs went through a DigitalOcean connection pool in transaction mode, they would not be reliable. UNR: I did not confirm which port the jobs would use.

| Command | Side effects | Verdict |
|---|---|---|
| run_outbox | Zoho confirm and cancel, shipment; 3 attempts | Worker or pass. Safe only with Zoho sandbox flags |
| reconcile_payment_attempts | Provider read, local order placement | Sandbox-safe if the gateway is the sandbox one |
| dispatch_orders | Hands orders to the shipment path | Do not enable (see §2) |
| suspend_inactive_business_roles | Local role change only | Low risk; idempotency not traced |
| purge_saved_shipping | Local deletion, off unless SAVED_SHIPPING_ENABLED | Leave off |
| archive_orders | Hides delivered orders, audited | "Safe to run repeatedly" per its docstring |

- VF, scheduling limit: DigitalOcean cron jobs run at most every 15 minutes (jobs doc, minimum every 15 minutes), yet scheduling.py defines outbox as every minute and reconcile-payments every 10 minutes. Neither fits as an App Platform job.
- REC: If the outbox is needed, run run_outbox --loop as a worker (a worker costs about as much as a service). Otherwise accept a 15-minute outbox delay.

## 4. DigitalOcean Python buildpack detection

- VF: DigitalOcean's page names Heroku buildpack v322 and lists requirements.txt, Pipfile or setup.py for detection. A "Limits" paragraph says at least one must be in the root. The same page also supports uv with pyproject.toml, uv.lock and .python-version. The page contradicts itself.
- VF: The upstream v322 bin/detect accepts pyproject.toml, uv.lock, .python-version and manage.py, all of which this repo has. It deliberately lists more files than the supported managers so that a build can fail with a helpful message instead.
- VF: The v322 changelog says the Python 3.14 alias resolves to 3.14.1, and DigitalOcean lists 3.14.0–3.14.3.
- Conclusion (VF plus inference): The upstream buildpack should accept this repo, and the "Limits" line is probably stale. That does not prove DigitalOcean's own component-type detection works the same way.
- UNR, question for DigitalOcean support: "For an App Platform GitHub source whose root has only pyproject.toml, uv.lock, .python-version (3.14) and manage.py, and no requirements.txt, Pipfile or setup.py, does the Python buildpack detect and build it with uv, and which Python 3.14 patch version does 3.14 resolve to? Your Python buildpack page lists both requirements."
- REC: No Dockerfile and no marker file are justified yet. I created no test app.

## 5. Secure restricted access with sandbox integrations

- VF, no gate exists: I searched config and modules for an access gate, allowlist or basic-auth mechanism and found none. The only related items are noindex headers (config/security.py:40, site.py:485). The DigitalOcean networking page showed no app-level IP allowlist or basic-auth feature in the text I searched. An app on a *.ondigitalocean.app URL would be public, with only ALLOWED_HOSTS limiting it.
- DEC: Choose the restriction mechanism. Options are a new access-gate middleware (new code), a DigitalOcean-side control if one exists, or another route. This is an architecture-level choice.
- REC for a new settings module (placeholder name config/settings/restricted.py, design only):
  - Keep production hardening: DEBUG=False, HTTPS redirect and HSTS, secure cookies, an explicit ALLOWED_HOSTS, and CSRF_TRUSTED_ORIGINS (not set anywhere today).
  - Keep refusing LOCAL_PROVIDER_STUBS and PAYMENT_STUB_ONLY.
  - Require ZOHO_PAYMENTS_SANDBOX=1 and ZOHO_INVENTORY_SANDBOX=1; refuse otherwise.
  - Allow TESTCODE_ACTIVE, with the DEC below.
  - Force site-wide noindex and a restrictive robots.txt.
  - Use a non-delivering email backend.
  - Leave production.py unchanged. Move shared guards to a function rather than copying them (from .production import * would run its raises).
- VF, conflict with the frozen production guard:
  - production.py:44-46 forbids TESTCODE_ACTIVE, and :118-122 forbids ZOHO_INVENTORY_SANDBOX.
  - testcodes.environment() (:38-52) also refuses TESTCODE unless Zoho Payments is a sandbox or stubs are on.
  - So the agreed strategy ("production-grade, sandbox integrations, identifiable test records") cannot run on config.settings.production without weakening it.
  - DEC: Approve a separate settings module, or amend the guard policy. I did not decide this.
- VF: The Zoho Inventory write gate is writes_allowed (zoho_sync.py:112-120), which needs ZOHO_SYNC_ENABLED plus a sandbox declaration. Keep both off until you instruct otherwise.
- UNR: Whether Zoho's Shiprocket link is sandbox is a Zoho-side setting I cannot see from the repo.

## 6. Database, TLS, health check, migrations

- VF: database_config() (config/settings/base.py:23-33) has no OPTIONS, so no sslmode is set. DigitalOcean's database security page recommends strengthening TLS verification with sslmode such as verify-full.
- REC, TLS without a code change (unverified): libpq reads a PGSSLMODE environment variable, so PGSSLMODE=require (or verify-full with the cluster CA) may work. I did not test it. A settings option in the new module is the code-based alternative.
- REC, database: A separate logical database and role on the existing cluster, using the private VPC host and a trusted source on the cluster, and never doadmin or defaultdb. I did not connect to it.
- VF, health check: /healthz (config/urls.py:29-49) runs SELECT 1 only and is exempt from the HTTPS redirect (production.py:31). It was not executed. A new module must keep that exemption.
- REC, migrations: A PRE_DEPLOY job is a documented job kind (the jobs page shows "kind": "PRE_DEPLOY") and can use the same environment. It would also need the PGSSLMODE setting or its equivalent.
- UNR: I did not run migrate, makemigrations --check or manage.py check --deploy. CI (.github/workflows/ci.yml) has no check --deploy step. I do not know if the migrations run cleanly on an empty database.

## 7. Test markers and cleanup

- VF, what is stamped: The TestScenario TESTCODE (models.py:55-72) is a foreign key on only PaymentAttempt and Order (:130, :224). It is set server-side from TESTCODE_ACTIVE (payment_flow.py:271). build_report (testcodes.py:223+) reads one code's attempts and orders. It is read-only and deletes nothing.
- VF, reachable through the order: OutboxTask, Shipment and integration logs.
- VF, not marked: customer accounts and saved addresses (identity/models.py:72,119), enquiry and subscription records, the ZohoSyncTask (models.py:1062) and ZohoContactLink (:1104) rows, and sandbox contacts created in Zoho.
- REC: Add a nullable test-marker column to those record types, defaulting from TESTCODE_ACTIVE (a schema change). Query by the marker, or by order, for cleanup. Never delete by similarity. on_delete=PROTECT on TestScenario means cleanup must go in dependency order.
- VF, external records needing separate reconciliation: Zoho Payments sandbox sessions and payments (IDs on PaymentAttempt.provider_order_id and provider_payment_id); Zoho Inventory sandbox Sales Orders (Order.zoho_order_reference) and contacts (ZohoContactLink.zoho_contact_id, ZohoSyncTask.zoho_id); and any Shiprocket sandbox shipments created by Zoho.
- UNR: I found no Zoho-side marker field or cleanup API in the repo. Whether Zoho sandbox records can be deleted or voided automatically is not established.

## 8. Remaining blockers and decisions

HU+DI decisions:
1. How a Zoho-managed fulfilment handoff should be represented in order states (§2).
2. A separate settings module versus changing production guards (§5).
3. The access-restriction mechanism (§5).
4. Approving the commit and push of the batch, including the 3 migrations (§1).
5. Test-marker schema change (§7).
6. Worker versus 15-minute polling for the outbox (§3).

Unresolved: the support answer on buildpack detection (§4); place_order idempotency; the real TLS behaviour; migrate on an empty database; the Zoho-side Shiprocket sandbox; the Zoho Payments webhook (not registered, needs HU and a stable HTTPS URL).

## 9. Smallest proposed implementation batch

Needs authorization, nothing is started:
1. The new settings module with shared guards and tests (including PGSSLMODE/sslmode).
2. The access-gate middleware, if option 1 in decision 3 is chosen.
3. A guard preventing SHIPMENT creation (and the dispatch job) against the real Zoho adapter, pending decision 1.
4. The test-marker column on the unmarked record types.
5. A runbook for the PRE_DEPLOY job, a worker command and the cleanup procedure.

Risk-based validation:
- Run only the new settings tests and the affected modules first.
- Then manage.py check --deploy under the new module with dummy values.
- Then makemigrations --check.
- Then one full suite at the end. Anything about DigitalOcean behaviour (TLS, detection, the health check, the pre-deploy job) can only be shown on the real platform.

Actions needing explicit authorization:
- Committing, staging or pushing.
- Creating the app, database role, worker or job.
- Using any sandbox credentials.
- Registering the Zoho webhook.
- Provisioning Spaces.
- Any migrate.
- Any test-suite run.

## 10. Final audit

- No files were edited, and nothing was staged, committed, stashed, pushed or discarded. HEAD is 625e210, 0 staged, 0 stashes.
- The modified-file count rose from 84 to 89 during this task through changes I did not make (see §1).
- No secrets were read or printed, and .env was untouched.
- No provider, DigitalOcean or database contact happened. I only fetched public documentation and GitHub files with curl and gh api.
- I ran no tests, manage.py commands or migrations. I created no DNS records, deployments, test apps or resources. I used no sub-agent.
- A runserver on 127.0.0.1:8000 was already running before this task and I left it alone. My temporary documentation files in the scratchpad are removed.

Please /clear before the next task. I'm waiting for your direction.
