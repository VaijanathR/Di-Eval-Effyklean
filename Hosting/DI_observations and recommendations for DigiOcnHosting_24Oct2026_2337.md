# DI Observations and Recommendations — DigitalOcean Hosting
**Date:** 24 October 2026, 23:37 IST  
**Reviewed report:** `Hosting/AgntResp_DigiOcnHosting_24102026_2327.md`

## Overall assessment

The local staging-settings checkpoint is useful progress, and the agent supplied concrete test results rather than claiming that hosting itself was verified. The work is **not yet ready to treat as a completed DigitalOcean staging deployment**. The current evidence establishes local configuration and focused-test behaviour only; it does not establish that DigitalOcean can build, start, connect securely to the existing database, run migrations, or enforce the staff-only gate in the hosted environment.

Keep the approved scope: staff-only staging first, public launch only after explicit HU+DI approval. Do not deploy, change DNS/network/database/provider state, or create chargeable resources as part of this review.

## Observations and recommendations

### 1. Local commits and repository state

- The agent reports checkpoints `b965d2b` and `5c45f31`, starting from `2a35f4e`, with 210 unrelated worktree files left untouched.
- The report says the changes were committed locally, not pushed.
- **Recommendation:** verify the exact commit ancestry, changed paths, and current remote `main` before pushing. Push only the intended hosting commits and paths; never use `git add -A`. Do not rewrite history or force-push. Stop and report evidence if remote history diverges or unrelated changes would be included.
- Keep the hosting application repository distinct from the public documentation/records repository. Uploading this review to the records repository does not push application code.

### 2. Email restrictions — HU+DI decision needed

- Fixing staging to Django's in-memory email backend matches the approved initial staging approach; it avoids accidental real email delivery.
- The agent additionally refuses `NOTIFICATIONS_ENABLED`, `REPORT_EMAIL_ENABLED`, and `CAMPAIGN_SENDING_ENABLED`. The agent explicitly identifies these as going beyond the requested list.
- **Recommendation:** do not silently broaden or remove these restrictions. Treat the three extra refusals as a decision point for HU+DI. Until decided, keep real outbound delivery disabled and do not represent email/notification delivery as tested. Confirm that in-memory messages are not being mistaken for delivered messages.

### 3. Ephemeral media

- Requiring `STAGING_EPHEMERAL_MEDIA_ACK=1` before local-disk media is accepted is consistent with the approved temporary staging choice.
- **Recommendation:** preserve the explicit acknowledgement and document that files can disappear on restart/redeployment. Do not use staging for durable customer uploads or treat local media as production-ready. Defer Spaces or another durable media service to a separate decision.

### 4. Database TLS, identity and privileges

- Requiring TLS, refusing `doadmin`, supporting CA path or PEM text, and defaulting to `verify-full` when the CA is supplied are appropriate safeguards according to the report.
- Local tests do not prove the hosted CA value, hostname verification, connectivity, or role privileges are correct. The migration command needs DDL rights for `effyklean_app`, and this remains untested.
- **Recommendation:** use the existing `effyklean-db` cluster and `defaultdb` as previously decided; do not create a duplicate database. Verify the dedicated `effyklean_app` role and minimum required privileges through the approved database/UI workflow. Validate CA/hostname verification and connection only when the required values are available. Do not use `doadmin` as the application account and do not weaken certificate verification to get a connection working.

### 5. Buildpack and Python 3.14 — unresolved deployment blocker

- The report identifies `pyproject.toml`, `uv.lock`, and `.python-version`, but it does not verify that DigitalOcean's selected buildpack installs the project correctly from this configuration. No Dockerfile or Procfile is present.
- **Recommendation:** resolve the build route before relying on the app deployment. First verify the actual DigitalOcean buildpack behaviour and logs. If it cannot support the repository's Python/uv setup, stop and bring the Dockerfile/build-route choice to HU+DI; do not invent or introduce a Dockerfile without the decision. Keep `DJANGO_SETTINGS_MODULE=config.settings.staging` explicit for build and run.

### 6. Host, proxy, staff-only access and health checks

- The agent's local checks are useful: HTTP redirect, 403 for the root and static asset without a staff cookie, allowed-host health endpoint bypassing redirect, and 400 for an unknown host.
- These checks used placeholder host `staging.example.test`; they do not verify the actual DigitalOcean app domain, health-probe Host, proxy headers, or hosted access controls.
- **Recommendation:** obtain the real app domain and actual health-probe Host from DigitalOcean before setting `ALLOWED_HOSTS`. Configure `CSRF_TRUSTED_ORIGINS` for the exact staging origin only. Enable `TRUST_FORWARDED_PROTO=1` only for the intended DigitalOcean proxy and verify the observed request scheme. Do not use wildcard hosts.
- Preserve staff-only staging: only the existing active Admin and Director accounts after MFA; do not create new staff accounts. Verify the gate in the hosted environment before allowing any wider access.
- The reported `/healthz` 503 was caused by the deliberately unreachable test database. It confirms the failure path, not a healthy hosted database connection.

### 7. Static assets and collectstatic

- `collectstatic` exited successfully and collected 9 files; the static asset request was denied without a staff cookie, as intended by the gate.
- **Recommendation:** retain the static-asset check as a separate staging verification. Once hosted, confirm the expected asset is served for an authorized staff session and is not exposed contrary to the intended gate. Do not infer full static delivery readiness from the local collection count alone.

### 8. Migrations and test coverage

- The report records 119 passing focused tests across `test_staging_settings`, `test_settings`, `test_deploy_readiness`, and `test_build152_deploy_artifacts`, using throwaway local PostgreSQL. This is useful focused evidence; it is not a full-suite result or hosted validation.
- **Recommendation:** do not rerun the full suite merely as paperwork. Before staging is relied upon, run the minimum necessary checks at the relevant gate: confirm build/start, database TLS and connectivity, migration permissions and result, health endpoint, and staff-only access. Record exact command output and outcome. Do not claim the migration is verified until it has actually run successfully in the intended environment with the dedicated role.

### 9. Existing app-spec example

- The report flags `deploy/app-spec.staging.example.yaml` as untracked work from another session and says it still references production settings.
- **Recommendation:** do not use that example to create or update an app in its current state. Inspect and correct it only as a scoped hosting change, preserving unrelated work and explicitly selecting `config.settings.staging`. Do not stage unrelated files while doing so.

### 10. DigitalOcean UI and network configuration

The report still needs values/actions available only in the DigitalOcean UI: app domain, health-probe Host, database endpoint and CA, dedicated-role password/privileges, trusted-source or VPC choice, the database-attachment form issue, secrets, CSRF origin and proxy configuration.

- **Recommendation:** follow the existing decision record: use the existing EffyKlean / Production project and `effyklean-web`; auto-deploy on push remains disabled. Preserve legitimate existing database access while choosing and verifying a safe trusted-source/VPC configuration—do not guess IPs or broadly expose the database. Resolve the database-attachment form issue before finalizing the app's database connection.
- Set secrets through the intended secret configuration, not committed files. Never place credentials, private keys, or certificate secrets in the public records repository.
- No DNS change, public launch, live provider write, order/dispatch operation, or chargeable infrastructure change is authorized by this review.

## Recommended order of work

1. Verify local branch, remote `main`, ancestry and intended commit paths; push only the approved hosting commit sequence if it is a safe fast-forward.
2. Resolve the three additional email-feature refusals through HU+DI decision; keep outbound delivery disabled meanwhile.
3. Resolve the DigitalOcean buildpack/Python 3.14/uv uncertainty. Bring a Dockerfile/build-route choice back to HU+DI if needed.
4. In the DigitalOcean UI, resolve the database-attachment issue and obtain the actual app/health-probe host values. Configure exact allowed hosts, CSRF origin and intended proxy behaviour.
5. Configure the existing database endpoint and CA with `verify-full`; confirm `effyklean_app` privileges without using `doadmin`. Run migrations only after the role and target are verified.
6. Verify hosted health, static assets and staff-only access with existing authorized staff accounts. Keep the app staff-only and auto-deploy disabled.
7. Report each item as **DONE (verified) / PARTIAL / NOT DONE / DEFERRED**, with command output, relevant file/line evidence or DigitalOcean UI evidence. List any shortcuts, stubs, placeholders, TODOs, weakened tests, swallowed errors and out-of-scope changes. Do not claim a check was performed if it was not.

## Bottom line

The staging configuration work is a solid local checkpoint, but the remaining build-route, UI-provided values, database-role/migration, and hosted security checks are real gates. Continue with the smallest evidence-based steps, preserve unrelated work, and stop for HU+DI decisions where the build approach or expanded email restrictions require a choice.
