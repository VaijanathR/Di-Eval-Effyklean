# EffyKlean — Final DigitalOcean Implementation & Hosting Plan
**Document:** FinalDigitalOCeanImplementationHostingPlan19Oct2026_1424.md  
**Date:** 19 October 2026  
**Status:** HU+DI working plan — strategy agreed; technical evidence gates remain open  
**Repository:** https://github.com/VaijanathR/Di-Eval-Effyklean  
**Scope:** DigitalOcean hosting, restricted production testing, sandbox integrations, test-data cleanup, controlled live-order validation, and public launch.

---

## 1. Executive decision

The agreed direction is to host the real EffyKlean website on DigitalOcean in a **restricted-access phase**, initially available only to approved team members. During end-to-end testing, all third-party integrations must use their supported **sandbox/test environments**, not live production environments.

After testing is satisfactory, test-created data will be identified, reconciled, and cleaned up through a reviewed procedure. The team will then deliberately transition third-party integrations to production, place one controlled live order by an authorized team member, reconcile the full result, and seek HU+DI approval before making the website publicly accessible.

This plan does not authorize immediate resource creation, deployment, DNS changes, repository publication, provider writes, or database deletion. Each requires its own review and explicit authorization where applicable.

## 2. Agreed lifecycle

### Phase A — Readiness investigation and source review

Before creating an App Platform app:

1. Resolve the DigitalOcean Python buildpack detection uncertainty or obtain an authoritative support answer.
2. Review local repository changes against GitHub `main`. The readiness report found local HEAD `625e210`, three commits ahead of `origin/main`, with 84 modified and 24 untracked files at the time of that report. Reverify current state before acting.
3. Preserve the previously HU-approved home-page link rearrangement in `modules/storefront/site.py` and `tests/test_storefront_shell.py`. Approval of the changes is not authorization to stage, commit, or push them.
4. Classify all changed and untracked files into required deployment work, approved work, unrelated work, and unexplained work.
5. Design the restricted/sandbox settings strategy and tests without weakening existing production safeguards.
6. Resolve the specific outbox and scheduled-command questions in Sections 7 and 8.
7. Confirm the minimum safe DigitalOcean resource design and current costs.

No code or cloud resources should be changed during a read-only investigation.

### Phase B — Restricted hosted website with sandbox integrations

1. Host the actual EffyKlean website on DigitalOcean App Platform using production-grade security settings.
2. Allow access only to explicitly approved team members. Protect all relevant pages and business actions with real authentication and authorization; a hard-to-guess URL or search-engine exclusion is not access control.
3. Keep all third-party integrations in their supported sandbox/test environments:
   - Zoho Payments sandbox.
   - Zoho Inventory sandbox organisation.
   - The existing Zoho-managed Shiprocket workflow, using its sandbox/test configuration where supported.
   - Safe email/notification behavior that cannot unintentionally contact real customers.
4. Do not enable live payment, live inventory writes, live customer notifications, or live fulfilment during this phase.
5. Preserve the existing architecture: the website hands relevant order/inventory work to Zoho; Zoho's own Shiprocket integration handles shipping. Do not add a direct website-to-Shiprocket shipment-creation integration.
6. Use a separate logical staging database and least-privilege role on the existing Managed PostgreSQL cluster if isolation, TLS, permissions, capacity, and operational risk checks pass.
7. Initially run no continuously running worker or scheduled jobs until their actual behavior and side effects are reviewed. Enable only the minimum task processing necessary for the approved end-to-end test, after safety is established.
8. Keep DNS and public launch deferred unless separately approved.

### Phase C — End-to-end testing

Test the deployed website—not only the local development environment—using sandbox integrations.

The risk-based test plan should cover, as applicable:

- Approved-member authentication, authorization, session behavior, and denial of anonymous access.
- Catalogue visibility and correctness, product title, quantity, final diluted volume, and current approved catalogue content.
- Checkout validation and the intended GST/customer-invoice behavior, as supported by the sandbox.
- Sandbox payment success, failure, cancellation, duplicate/callback behavior, webhook handling, and order/payment state reconciliation.
- Website order creation and Zoho Inventory sandbox synchronization.
- The established Zoho-managed Shiprocket handoff and its resulting status.
- Outbox enqueueing, processing, retries, terminal states, and recovery from expected failures.
- Safe email and notifications.
- Health checks, database connectivity/TLS, application logs, and recovery procedures.
- Security settings, host/origin validation, HTTPS/proxy behavior, and safe handling of configuration errors.

Use unique, traceable test markers for every test run and all website-owned records where the schema supports it. Example pattern: `TESTCODE-<run-id>-<scenario>`. Confirm how markers are represented and queried before testing. Do not assume the marker automatically propagates into Zoho or Shiprocket; track external sandbox records separately.

All test cases and created records must be traceable to a test run. Do not use test helpers that contain known test passwords as production bootstrap procedures; in particular, never run `seed_hu_admin_test`. Staff/admin setup must use the reviewed production-safe process and required MFA.

### Phase D — Test-data reconciliation and cleanup

When testing is satisfactory:

1. Freeze new test activity and capture the final test-run inventory.
2. Identify all website-owned test records by the approved markers and trace related objects/dependencies.
3. Reconcile sandbox payments, orders, inventory effects, invoices, webhooks, and shipment/fulfilment records. External systems may require separate cleanup or cancellation; deleting a website record does not reverse an external side effect.
4. Produce a dry-run cleanup report listing the exact record categories/counts, dependencies, and proposed actions.
5. Verify that the cleanup scope excludes required configuration, approved catalogue data, staff accounts, security/audit evidence, and records required for reconciliation or legal/operational retention.
6. Obtain explicit HU+DI approval for the precise cleanup scope.
7. Back up the relevant database state and execute a controlled, tested cleanup procedure only after authorization.
8. Verify the results: no unintended test business records remain, referential integrity is intact, system configuration remains correct, and evidence needed for audit/reconciliation is retained.

Do not indiscriminately delete all orders or all records. Do not delete provider-side records or execute destructive cleanup without explicit authorization. Keep an audit record of what was removed, what was retained, and why.

### Phase E — Controlled transition to live integrations

This is a separate authorization gate, not an automatic consequence of passing sandbox tests.

Before switching any provider to production:

- Verify production credentials and environment selection without exposing secrets in reports.
- Confirm live endpoints are intentional and sandbox endpoints are no longer selected.
- Verify payment webhook registration and the stable HTTPS endpoint required by the provider.
- Review production payment and inventory write guards and required permissions.
- Confirm email/notification delivery behavior and intended recipients.
- Confirm backups, recovery, logging, alerting, and a rollback/containment plan.
- Confirm inventory/order/invoice and fulfilment reconciliation procedures.
- Ensure no test-only configuration or stub mode can accidentally run in production.
- Change one integration at a time where practical; verify configuration and health before proceeding.
- Obtain explicit HU+DI authorization for the live integration changes and any live provider writes.

The production configuration must not be weakened merely to make sandbox mode work. Design an explicit, tested configuration strategy for restricted hosted testing while preserving production safeguards.

### Phase F — One controlled live order

After sandbox testing and cleanup, one authorized team member places a real order using production integrations.

Before the order, decide and document whether it will be fulfilled/shipped normally or held at a controlled point for HU+DI review. The choice affects payment, stock, invoice, shipment, cancellation, and refund handling.

For the live order:

1. Record the approved order/test identifier in the internal audit record. Do not assume sandbox TESTCODE rules should be enabled in production; the live validation order should be identifiable through an approved controlled-validation marker or reference that does not bypass production guards.
2. Ensure the team member understands that a real charge and real operational consequences may occur.
3. Verify payment result and provider reference, website order state, Zoho Inventory records, stock effects, invoice behavior, and the intended Zoho-managed Shiprocket handoff.
4. Verify webhooks and reconciliation, and check that no duplicate order/payment/inventory action occurred.
5. If cancellation or refund is needed, use the authorized provider/business procedure. Deleting the local record is not a reversal.
6. Capture evidence and reconcile all local and external records.
7. Review the outcome with HU+DI before opening the website to the public.

### Phase G — Public launch

Public access is a separate explicit HU+DI decision. Before launch:

- Confirm the restricted-access control can be removed safely without weakening other authorization checks.
- Confirm production integrations and webhooks are correctly configured.
- Confirm the live order is reconciled and its intended fulfilment outcome is understood.
- Confirm backup/recovery, monitoring, incident response, support routing, and access to administrative accounts.
- Confirm catalogue, pricing, tax/invoice behavior, inventory, and customer communications.
- Confirm the final production deployment source and rollback path.
- Obtain explicit HU+DI authorization to change public access/DNS or any other launch-related settings.

## 3. Hosting architecture and resource principles

### Web application

DigitalOcean App Platform remains the preferred hosting direction. The existing Managed PostgreSQL cluster `effyklean-db` was reported as online in BLR1, PostgreSQL 17, primary only, 1 GiB RAM / 10 GiB disk, approximately US$15.15/month. Reconfirm current resource details and pricing before relying on these figures.

The readiness report identified `/healthz` at `config/urls.py:29-49` as a GET/HEAD-only health endpoint performing a simple `SELECT 1`, returning 200 or 503 according to database health, and not contacting providers or writing business data. It has not yet been executed as part of the reported investigation; verify it safely before deployment.

The report proposed this candidate run command, subject to confirmation against the final deployment source and DigitalOcean's documented requirements:

```sh
gunicorn --worker-tmp-dir /dev/shm --bind 0.0.0.0:${PORT:-8080} --workers 2 --access-logfile - config.wsgi:application
```

The Gunicorn temporary-directory workaround was identified in DigitalOcean's Python buildpack documentation. Verify that the selected runtime supports it and that the final settings are supplied explicitly, including `DJANGO_SETTINGS_MODULE`.

### Build route uncertainty

The report found that DigitalOcean's Python buildpack documentation describes classic root-level detection files (`requirements.txt`, `Pipfile`, or `setup.py`) while also documenting uv support when `pyproject.toml`, `uv.lock`, and `.python-version` are present. The repository has the uv files but none of the classic detection files. Whether this exact repository is detected and whether `.python-version = 3.14` resolves on the selected stack remain unverified.

Preferred next step: obtain an authoritative DigitalOcean support answer or further official-documentation evidence. Do not create a throwaway app to find out. Do not add a Dockerfile or `requirements.txt` merely as a guess; each is a repository change requiring review and approval.

Official documentation cited by the investigation:
- Python buildpack: https://docs.digitalocean.com/products/app-platform/reference/buildpacks/python/
- App Platform jobs: https://docs.digitalocean.com/products/app-platform/how-to/manage-jobs/
- App Platform pricing: https://docs.digitalocean.com/products/app-platform/details/pricing/

### Database isolation and TLS

Preferred initial design, subject to verification: a separate logical database and role on the existing Managed PostgreSQL cluster, rather than reusing `defaultdb`/`doadmin`.

Requirements:
- Least-privilege role scoped to its own database; no superuser or CREATEDB.
- Use the private VPC endpoint, TLS required, and narrowly scoped trusted sources.
- Confirm the actual Django connection configuration enforces TLS; the report says `database_config()` did not visibly specify an `sslmode` option.
- Never point local pytest/test database creation at the DigitalOcean cluster; pytest-django can create/drop a test database.
- Keep test and live business data isolated. Before the live integration phase, make a deliberate database/data-transition decision rather than assuming test data can be converted to production data.
- Accept explicitly that two logical databases on the same cluster share hardware, backups, and a failure domain. A separate cluster offers stronger isolation but may cost more.

No database, role, firewall/trusted-source change, or other resource should be created until HU+DI authorizes the concrete plan.

### Static files and media

The report says Django staticfiles is excluded, no static directory or WhiteNoise was found, and the candidate build may not require a static collection step. Confirm against the final deployment source rather than assuming no static assets can ever be added.

Production settings require S3-compatible media; DigitalOcean Spaces is deferred. If the restricted test phase requires uploads, HU+DI must choose between:
- Temporary local-disk media with an explicit warning that uploaded files may be lost on redeploy/replacement; or
- Waiting until a persistent object-storage plan is approved.

Do not add Spaces or incur additional charges without authorization.

### Access restriction

Restricting access is an application/security requirement, not a substitute for sandbox integrations or a separate test database. Enforce authentication and authorization at every protected route and action. Prevent unauthenticated access to business data. Search-engine blocking may be an additional precaution but is not access control.

Use explicit allowed hosts, HTTPS redirection, secure cookies, correct CSRF trusted origins, and trusted-proxy configuration appropriate to App Platform. Test these settings against the actual deployment. Do not assume that the current production settings can be reused unchanged when they reject sandbox configuration.

## 4. Settings strategy

The investigation found no `config/settings/staging.py`. Existing `production.py` rejects sandbox-related settings such as `ZOHO_INVENTORY_SANDBOX`, test/stub modes, and local provider stubs, and requires production-shaped Zoho and S3 media configuration. It also does not visibly guard `ZOHO_PAYMENTS_SANDBOX`.

Required design work:

- Create a separately reviewed restricted-testing configuration only after HU+DI approves implementation.
- Reuse common settings without importing production-only guards that immediately reject sandbox configuration. Do not simply use `from .production import *` if import-time raises make that unsafe.
- Keep `DEBUG=False`, explicit hosts, secure cookies, HTTPS/proxy protections, and environment-driven CSRF origins.
- Require explicit sandbox configuration for Zoho Payments and reject the live checkout base URL/default in restricted testing.
- Require the Zoho Inventory sandbox organisation; keep `ZOHO_SYNC_ENABLED` and `ZOHO_SALES_ORDER_WRITES_AUTHORIZED` disabled until their exact intended test use is separately authorized.
- Continue refusing unsafe local stubs and test-only flags in any configuration where the frozen requirements prohibit them. Determine how legitimate sandbox test markers should work without bypassing production safeguards.
- Use a discard-only email backend or other expressly approved safe test delivery.
- Ensure no live credentials/endpoints are silently inherited by the restricted environment.
- Add focused tests proving invalid/live-shaped configuration fails closed and that the restricted configuration remains secure.
- Do not run `check_email_config` casually: the report says it opens an SMTP connection and authenticates even though it sends no message.

All code changes require a reviewed diff and explicit approval before staging/commit/push.

## 5. Outbox, fulfilment and background jobs

The website's architecture must preserve the existing Zoho-managed shipping workflow. The site should not create shipments directly with Shiprocket.

The investigation reported:
- Checkout can enqueue a `SHIPMENT` outbox task.
- `integrations/zoho_inventory.py` reports shipment creation as unsupported because shipping is handled by Zoho's own Shiprocket integration.
- The actual behavior when the outbox task is processed against the real Zoho adapter has not been fully traced.

This does **not** mean the Zoho–Shiprocket integration is assumed broken. The narrow question is whether the website's task correctly implements the intended Zoho handoff, no-op, or state transition, or whether it falls into an unintended exception/retry/failure loop.

Before enabling outbox processing, trace enqueue → dispatch → adapter call → success/exception handling → retries/terminal status. Confirm impact on checkout/order completion and ensure no direct Shiprocket shipment creation is added.

The report classified commands as follows, with some behavior still unverified:
- `run_outbox`: one pass or continuous loop; tasks use row locks/skip-locked, with three total attempts; also scheduled every minute.
- `run_scheduled <job>`: scheduled wrapper with per-job PostgreSQL advisory lock; invokes several operational jobs.
- `retry_integrations`: on-demand; docstring says outbox worker supersedes it; no lock identified.
- `reconcile_payment_attempts`: scheduled every ten minutes; provider calls and idempotency/locking behavior need tracing.
- `suspend_inactive_business_roles`: daily; idempotency behavior needs tracing.

No continuous worker or scheduled jobs should be enabled initially until each required command is reviewed. Do not run provider-contacting commands merely to investigate. Migrations should be a controlled pre-deploy job, not automatically executed by each web process, after repeatability and target-database safety are verified. Never run `seed_hu_admin_test`; use the reviewed staff-creation process with MFA.

## 6. Test records and cleanup rules

- Use unique test-run/scenario markers on website-owned test records wherever supported.
- Maintain a mapping from each test scenario to the local records and sandbox-side records it created.
- Do not assume every external system supports the same marker or that local markers automatically propagate.
- Reconcile sandbox-side payments, invoices, inventory movements, and shipment records separately.
- Use a dry-run cleanup report, backup, dependency checks, explicit HU+DI authorization, controlled cleanup, and post-cleanup verification.
- Do not remove configuration, approved catalogue data, staff/admin accounts, audit evidence, or records required for reconciliation/retention.
- No bulk deletion or destructive cleanup without explicit authorization.

## 7. Cost and resource approval

The earlier estimate was approximately US$10/month for a fixed 1-vCPU/1-GiB App Platform web component, plus the reported existing Managed PostgreSQL cost of approximately US$15.15/month. These are estimates from the prior investigation, not account-specific quotes; reconfirm current pricing and billing before resource creation.

A separate worker may add roughly US$5–10/month depending on size and use. It is not recommended initially. Scheduled/pre-deploy jobs are billed while running according to the cited pricing model; Spaces is deferred and must not be created without approval.

Do not create any resources or accept charges until the exact resource plan, monthly cost, database design, trusted-source configuration, and rollback/cleanup plan are presented for explicit HU+DI authorization.

## 8. Outstanding evidence and decisions

### Technical evidence still required

1. Buildpack detection and Python 3.14 resolution for the actual uv-only repository.
2. Current local/GitHub source divergence and exact changed-file inventory.
3. Shipment outbox execution and terminal-state behavior against the intended Zoho-managed workflow, without provider calls.
4. Payment reconciliation and scheduled-command idempotency/side-effect analysis.
5. Actual TLS configuration and a safe way to verify health-check behavior.
6. Migration repeatability and safe pre-deploy job design.
7. Test-marker coverage and cleanup queries/dependencies.
8. Zoho sandbox-to-Shiprocket sandbox behavior as reported by HU; repository inspection alone cannot prove the Zoho-side configuration.
9. Zoho Payments sandbox webhook requirements and stable HTTPS URL needs.

### HU+DI decisions required before implementation/resources

- Approve the proposed restricted/sandbox settings implementation and focused tests.
- Approve the exact local changes to publish after change inventory and review.
- Choose temporary local media versus deferring upload testing until persistent storage is approved.
- Approve the separate logical database/role design on the existing cluster, or choose a separate cluster.
- Approve the build route if official evidence cannot resolve buildpack detection.
- Approve the discard-only email approach.
- Approve any worker, scheduled job, provider write, resource creation, paid service, DNS change, cleanup, live-integration switch, first live order, and public launch separately as appropriate.
- Before the first live order, decide whether fulfilment proceeds normally or is held at a controlled point for review.

## 9. Governance and stop conditions

- Follow the frozen architecture/specification and existing HU+DI governance.
- Any conflict or unresolved business/architecture ambiguity: STOP → REPORT → HU+DI DECIDE.
- Read-only investigation must not modify repository files, stage/commit/push, deploy, create resources, change DNS, inspect/print secrets, change `.env`, or call/write to providers.
- Preserve approved work. Never use `git add -A`.
- Keep private Claude/session logs out of Git until the website is online.
- Update `PROJECT_LOG.md`, `CLAUDE.md`, `README`, and the status register at appropriate safe checkpoints before clearing a session.
- Do not claim a test, health check, TLS connection, provider flow, or cloud configuration has been verified unless evidence shows it was actually executed.
- Stop after each evidence report and wait for HU+DI review before taking the next authorized action.

## 10. Immediate next steps

1. Complete the focused read-only evidence pass covering the outstanding items above.
2. Review the evidence and change inventory with HU+DI.
3. Approve the smallest necessary implementation batch.
4. Implement and test the restricted/sandbox configuration locally, preserving unrelated approved work.
5. Review the exact diff and approve publication of the required deployment source.
6. Approve the minimum DigitalOcean resource plan and cost.
7. Create the restricted hosted environment only after the above gates pass.
8. Execute sandbox end-to-end testing, reviewed cleanup, live-integration authorization, one controlled live order, and the separate public-launch decision.

**Current status:** Strategy agreed; not yet authorized for cloud resource creation, deployment, repository publication, provider writes, database cleanup, live-order testing, or public launch.
