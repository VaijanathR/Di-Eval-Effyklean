Current DigitalOcean setup:

  Database: effyklean-db, PostgreSQL 17, Bangalore (BLR1), $15.15/month.

  Planned App Platform app: effyklean-web, $10/month; not yet created.

  Database: defaultdb, user doadmin, VPC default-blr1.

  Auto-deploy disabled.

  Spaces and DNS changes deferred.

  Inspect the current repository and determine the exact Build command and Run command to enter when creating the DigitalOcean App Platform app.

  Identify any environment variables or other settings that must be configured before app creation.

  Verify your recommendations against the actual repository files and report the relevant evidence and any blockers.

  Do not change repository files or DigitalOcean settings. Do not create the app or deploy. Report findings for HU+DI review.

  Ran 6 shell commands

Checking that production settings load with dummy values, and how request security uses the host.

  Ran 1 shell command

DigitalOcean App Platform: build and run settings for effyklean-web (HU+DI review)

Nothing was changed, created or deployed. I read the repository only. I did not run manage.py check against the production settings, because Django isn't installed in this shell.

Recommended commands

The repository has no requirements.txt, Procfile, Dockerfile or app spec. It has pyproject.toml, uv.lock and .python-version (3.14). gunicorn>=26.2.0 is a dependency, and config/wsgi.py exposes application.

┌────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────┐
│    Setting     │                                            Value                                             │
├────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────┤
│ Source         │ GitHub repo, branch main, auto-deploy off                                                    │
├────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────┤
│ Run command    │ gunicorn config.wsgi:application --bind 0.0.0.0:${PORT:-8080} --workers 2 --access-logfile - │
├────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────┤
│ HTTP port      │ 8080                                                                                         │
├────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────┤
│ Health check   │ HTTP path /healthz                                                                           │
├────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────┤
│ Pre-deploy job │ python manage.py migrate --noinput                                                           │
└────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────┘

- Build command: I can't confirm what to enter.
  - Why none is needed: the app has no static files (no staticfiles app, no WhiteNoise, no collectstatic), so nothing needs building.
  - Dependencies: the Python buildpack installs them automatically.
  - Open question: I haven't verified that the DigitalOcean Python buildpack reads uv.lock or supports Python 3.14. That is the first blocker below.
- Run command: gunicorn is in pyproject.toml, and config/wsgi.py refuses to start unless DJANGO_SETTINGS_MODULE is set.
- Health check: the /healthz view in config/urls.py returns 200 after running SELECT 1, and 503 if the database is down. The SECURE_REDIRECT_EXEMPT = [r"^healthz$"] line in config/settings/production.py keeps it from being redirected to HTTPS.
- Pre-deploy job: migrate must run as a job. It can't be put in the run command, because the app will have more than one process or instance over time. The older readiness plan (docs/foundation/DIGITALOCEAN_DEPLOYMENT_READINESS_PLAN_2026-10-16.md) also recommends a single-run job. That plan is partly stale: it says there is no gunicorn and no /healthz, and both now exist.

Environment variables needed before the app is created

config/settings/production.py raises ImproperlyConfigured and refuses to start unless these are set. Mark the secrets as encrypted.

Core
- DJANGO_SETTINGS_MODULE=config.settings.production
- SECRET_KEY (secret)
- ALLOWED_HOSTS (the *.ondigitalocean.app host, plus www.effyklean.in later)
- TRUST_FORWARDED_PROTO=1. Without it, the HTTPS redirect loops behind the App Platform proxy.
- PUBLIC_BASE_URL (the https app URL, used for email links)
- SECURE_HSTS_SECONDS (optional). The default is one year; I suggest a low value such as 300 for the first rollout.

Database
- DB_NAME=defaultdb, DB_USER=doadmin
- DB_PASSWORD (secret)
- DB_HOST (use the private VPC hostname from the database's connection details)
- DB_PORT (managed databases normally use 25060; confirm in the connection details)
- The database settings (database_config()) have no sslmode option, so the connection defaults to prefer. That is probably acceptable, but verify that the connection really uses TLS.
- Add the app as a trusted source on the database firewall.

Media
- MEDIA_STORAGE_BACKEND=s3
- MEDIA_S3_BUCKET, MEDIA_S3_ENDPOINT_URL, MEDIA_S3_ACCESS_KEY, MEDIA_S3_SECRET_KEY (secret)
- MEDIA_PUBLIC_BASE_URL (must start with https://)

Email
- EMAIL_BACKEND, plus EMAIL_HOST, EMAIL_PORT, EMAIL_HOST_USER, EMAIL_HOST_PASSWORD and DEFAULT_FROM_EMAIL. The console backend is refused in production.

Zoho Payments (live, not sandbox)
- ZOHO_PAYMENTS_ACCOUNT_ID, ZOHO_PAYMENTS_CLIENT_ID, ZOHO_PAYMENTS_CLIENT_SECRET, ZOHO_PAYMENTS_REFRESH_TOKEN, ZOHO_PAYMENTS_SIGNING_KEY, ZOHO_PAYMENTS_WEBHOOK_KEY, ZOHO_PAYMENTS_RETURN_URL

Zoho Inventory (live)
- ZOHO_INVENTORY_ORGANIZATION_ID, ZOHO_INVENTORY_CLIENT_ID, ZOHO_INVENTORY_CLIENT_SECRET, ZOHO_INVENTORY_REFRESH_TOKEN
- ZOHO_INVENTORY_TAX_ID_INTRA_STATE, ZOHO_INVENTORY_TAX_ID_INTER_STATE

Must be unset or empty
- LOCAL_STUB_*, PAYMENT_STUB_ONLY, TESTCODE_ACTIVE and ZOHO_INVENTORY_SANDBOX (each of these stops production from starting).
- Also leave ZOHO_SYNC_ENABLED, ZOHO_SALES_ORDER_WRITES_AUTHORIZED, CONTACT_FORM_ENABLED and SAVED_SHIPPING_ENABLED off, per CLAUDE.md.

Blockers and risks

1. Python version. pyproject.toml pins >=3.14,<3.15. Confirm that App Platform's Python buildpack supports 3.14 and reads uv.lock. If it doesn't, the choices are a Dockerfile (a repo change) or changing the pin, and either needs HU+DI approval.
2. Spaces is deferred, but production requires it. Production refuses to start without S3 media settings, so the app can't boot until Spaces exists. "Spaces deferred" and "app created" can't both hold unless the app is created and left failing. Alternatively, a staging settings module could be added later (a code change). This is the main blocker.
3. Live Zoho credentials are mandatory. Production refuses sandbox Inventory and requires the live Zoho Payments values. Putting live credentials into a staging app conflicts with the sandbox-first rule, and production credentials need their own authorization.
4. Email provider. No provider or credentials are approved. The GoDaddy SMTP configuration is local and uncommitted.
5. Unpushed and uncommitted work. main is 3 commits ahead of origin/main (per my last git rev-list), and the working tree holds uncommitted changes. App Platform builds from GitHub, so none of that would be deployed.
6. Worker and scheduled jobs. A $10 web-only app has no worker. These commands exist but have nothing to run them: run_outbox, run_scheduled, retry_integrations, reconcile_payment_attempts and suspend_inactive_business_roles. Without a worker or scheduled job, the Zoho handoff and the other automation would not run.
7. Webhook URL. The Zoho Payments webhook is not registered. It needs HU to register it, and a stable HTTPS URL. The App Platform URL could serve as that endpoint.
8. First admin account. After the first migrate, someone has to run createstaff (and MFA setup) in a console. seed_hu_admin_test must never be run, because it holds a test password.
9. No static files. I found no static-file handling in config or modules. I didn't check whether the admin pages and the storefront templates depend on served CSS or JS.
10. Data loading. load_policy_pages, load_howto_videos and the catalogue import are not scheduled to run. The catalogue is already in the development database, so production needs a data-load decision.
11. Temporary arrangements. If a staging app uses any sandbox values, add them as rows in docs/foundation/TEMPORARY_ARRANGEMENTS_REMOVE_AT_GO_LIVE.md.

Please run /clear or start a new session before the next task.

✻ Cogitated for 58s · done 11:29 AM

❯ inspect the current repository and report:
  1. Whether a staging settings module already exists.
  2. Which exact production-only checks prevent a sandbox deployment.
  3. The minimum changes that would be needed to support staging, with exact file paths and evidence.
  4. Whether staging can safely use the existing managed database or needs a separate database.
  5. Which existing commands and tests can validate the staging configuration without contacting live providers or creating business records.
     No code changes, migrations, deployment, credential entry, or Git operations should be performed during that investigation.

  Ran 4 shell commands

────────────────────────────────────────────────────────────────────────────────────────────────── 1 new message ──────────────────────────────────────────────────────────────────────────────────────────────────

Staging settings investigation (HU+DI review)

I changed nothing: no code, migrations, deployment, credentials or Git operations. I read the settings, wiring and test files only.

1. Does a staging settings module exist?

No. config/settings/ holds only base.py, local.py, production.py and test.py.
- local.py is unsuitable for staging because it sets DEBUG = True, LOCAL_PROVIDER_STUBS = True, SESSION_COOKIE_SECURE = False and a localhost-only ALLOWED_HOSTS.
- test.py is unsuitable because it generates a throwaway SECRET_KEY and blanks every provider credential.

2. Production-only checks that block a sandbox deployment

All are in config/settings/production.py:

┌──────────────────────────────────────────────────────────────────────────────────┬──────────────────────────────────────────────────────────────────────────────────────┐
│                                      Check                                       │                            Effect on a sandbox deployment                            │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ ZOHO_INVENTORY_SANDBOX set raises (last lines of the file)                       │ Blocks the Zoho Inventory test organisation. This is the decisive one.               │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ _MISSING list: all 7 Zoho Payments values and 6 Zoho Inventory values required   │ Staging needs live-shaped values, so the sandbox credentials would be accepted here. │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ MEDIA_STORAGE_BACKEND != "s3" or any MEDIA_S3_* or MEDIA_PUBLIC_BASE_URL missing │ Blocks staging until a bucket exists. This is the Spaces blocker.                    │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ EMAIL_BACKEND ending in console.EmailBackend                                     │ Blocks staging until an SMTP provider is set.                                        │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ PAYMENT_STUB_ONLY set raises                                                     │ Blocks the stub payment mode.                                                        │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ LOCAL_PROVIDER_STUBS true raises                                                 │ Blocks the stubs.                                                                    │
├──────────────────────────────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────────┤
│ TESTCODE_ACTIVE set raises                                                       │ Blocks TESTCODE mode.                                                                │
└──────────────────────────────────────────────────────────────────────────────────┴──────────────────────────────────────────────────────────────────────────────────────┘

ZOHO_PAYMENTS_SANDBOX is not refused. config/settings/base.py:163 reads it, and modules/orders/testcodes.py:43 and modules/backoffice/insight_views.py:914 use it. Production already accepts the Zoho Payments sandbox, and the live-vs-sandbox choice is made only by which credentials and ZOHO_PAYMENTS_CHECKOUT_BASE are used. It is not a guarded boundary.

Two settings control the sandbox write path, and both are off by default:
- Unsafe default: in production with ZOHO_INVENTORY_SANDBOX unset and a live org id, modules/orders/zoho_sync.py:writes_allowed refuses writes, because the org isn't declared a sandbox.
- Staging behaviour: with ZOHO_INVENTORY_SANDBOX=1, ZOHO_SYNC_ENABLED=1 and ZOHO_SALES_ORDER_WRITES_AUTHORIZED=1, a staging app would write to Zoho's test organisation.

3. Minimum changes for staging

1. New file config/settings/staging.py. It would be production-like (DEBUG off, HTTPS redirect, secure cookies, host list from the environment). Production's guards that don't fit staging are deliberately left out of it:
   - Allow ZOHO_INVENTORY_SANDBOX=1, and conversely require it, so staging can't be pointed at the live org.
   - Keep refusing PAYMENT_STUB_ONLY, LOCAL_PROVIDER_STUBS and TESTCODE_ACTIVE.
   - Either keep the S3 requirement (needs Spaces or a separate bucket) or allow local media, which is lost on every deploy.
   - Keep the SMTP requirement, or allow a labelled non-delivering backend.
   - Optionally require ZOHO_PAYMENTS_SANDBOX=1 and a sandbox checkout base URL, so staging can't take real payments.
   - Safest way to do this: from .production import * can't be used, because production's raise statements run on import. The checks would have to move into a shared function, or the file duplicates the safe parts.
2. config/wsgi.py: no change. It only needs DJANGO_SETTINGS_MODULE=config.settings.staging.
3. Tests: a new test file, in the style of tests/test_settings.py (test_production_*). It would cover staging loading, refusing a missing sandbox flag, and refusing stubs and TESTCODE.
4. Register: add rows to docs/foundation/TEMPORARY_ARRANGEMENTS_REMOVE_AT_GO_LIVE.md.

4. Existing managed database or a separate one?

Use a separate database. Reasons:
- Business records: the checkout path creates orders and customer records. Sandbox payments and Zoho Sales Orders would mix with whatever production later holds in defaultdb.
- Test runs: pytest-django creates and drops a test_<NAME> database. Running tests with DB_NAME=defaultdb as doadmin would create test_defaultdb on the managed server. Do not point the test run at the DigitalOcean database at all.
- Reset: staging data would need to be resettable.

The cheapest option is a second logical database (for example effyklean_staging) on the same effyklean-db cluster, with its own user. That avoids a second $15.15/month cluster, but the two share server load and backups. Production migrations and the backup procedure in docs/foundation/BACKUP_AND_RESTORE.md would then treat them separately. A fully separate cluster is the stricter choice.

5. Validation without live providers or business records

All of these run against local settings with no network:
- manage.py check and manage.py check --deploy, run with DJANGO_SETTINGS_MODULE set to the new staging module and dummy environment values.
- manage.py makemigrations --check --dry-run, which reads the model definitions and writes nothing.
- pytest tests/test_settings.py and tests/test_contact_form.py::test_production_*. These import production settings with monkeypatched environments and need a local PostgreSQL only for the Django test runner (pytest-django), which is a throwaway test database, not DigitalOcean.
- manage.py check_email_config connects to the SMTP server and authenticates but sends nothing. It does contact the mail server, so it is not strictly offline.
- manage.py check_zoho_access does contact Zoho. It is read-only, but it uses the real token, so run it only deliberately against the sandbox organisation.
- show_schedule and showaudit: I did not verify their side effects, so check before use.

