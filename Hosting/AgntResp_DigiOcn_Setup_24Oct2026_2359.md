# DigitalOcean Setup — Agent Response

**Recorded:** 24 October 2026, 23:59  
**Source:** Agent response supplied by Hu  
**Scope:** Local staging configuration and preparation for DigitalOcean hosting  
**Important boundary:** The agent reports that nothing has been verified or changed on DigitalOcean.

## Overall result

The local hosting config is complete and pushed to `origin/main` as a fast-forward. Local HEAD and remote HEAD are both `5cd21ad8ddd29f4ee94284c4ced5abb314655c9a` (confirmed with `git ls-remote origin refs/heads/main`). Nothing is verified on DigitalOcean.

Important finding: before pushing, I checked out the commits cleanly. The earlier `2a35f4e–5c45f31` commits were broken on their own: 17 staging tests failed, because `staging.py` read three email-feature flags that exist only in your uncommitted `base.py` edits. Pushing them as they were would have crashed staging at startup. I fixed this before pushing.

## Repository reconciliation

- Branch `main`; `origin/main` was still `ad69d92`, with 0 commits behind and 3 ahead, so the push was a safe fast-forward.
- Pushed commits, in order:
  - `2a35f4e` — Staging profile, staff-only gate, staticfiles.
  - `b965d2b` — In-memory email backend.
  - `5c45f31` — Database CA support, build/run documentation.
  - `e7b2164` — Fix for the clean-checkout failure, plus the timestamped app-spec template and renamed env example. Changes `staging.py`, `tests/test_staging_settings.py` and two files under `deploy/`.
  - `5cd21ad` — Staging profile doc and a single `PROJECT_LOG.md` line.
- The 210 unrelated worktree files are untouched and still present. I used no `git add -A`, no co-author trailers, and no force-push.

## Checklist

- **Reconcile ancestry and remote — DONE (verified):** as above.
- **Staging settings, startup, PORT, static, health, hosts, proxy — DONE (verified locally):** staging and settings tests pass in a clean checkout of `5cd21ad`. Gunicorn booted earlier.
- **Staff-only gate (Admin and Director with MFA) — DONE (verified locally):** `test_staging_settings` and `test_admin_auth`: 165 passed in a clean checkout. No accounts created.
- **Build route — PARTIAL:** DigitalOcean's Python buildpack documentation says `uv` is supported with `pyproject.toml`, `uv.lock` and `.python-version`, and the repository matches. The docs list Python 3.14.0–3.14.3, and `.python-version` is 3.14. The build log must confirm the resolved patch version. No Dockerfile is needed on this evidence, and none was created.
- **Database TLS and role — PARTIAL:** `verify-full` is the default when a CA is supplied, and `doadmin` is refused (tested). The hosted CA, hostname verification, role and connectivity are unverified.
- **Migration readiness — PARTIAL:** in a clean checkout, `makemigrations --check` reported no changes, and `migrate` on an empty throwaway PostgreSQL ran clean. The committed migrations contain no extensions or raw SQL. `effyklean_app` privileges on DigitalOcean are unverified, and PostgreSQL 15+ does not grant `CREATE` on `public` by default. Nothing was granted or guessed.
- **In-memory email — DONE (verified):** fixed in code, and any other `EMAIL_BACKEND` is refused.
- **Ephemeral media — DONE (verified):** refused without `STAGING_EPHEMERAL_MEDIA_ACK=1`; documented as disposable. Spaces deferred.
- **`deploy/app-spec.staging.example.yaml` — DONE:** marked UNUSABLE in its header. It is untracked and was not committed.
- **New app-spec — DONE, as a template:** `deploy/app-spec_staging_2026-10-24_2350.yaml`. It has angle-bracket placeholders, so it is invalid until filled in. Staging settings, auto-deploy off, no worker, no jobs, no migrate job. A test covers it.
- **Hosted health-probe Host in `ALLOWED_HOSTS` — NOT DONE:** the actual value is unknown until DigitalOcean shows it. Wildcards are refused.
- **Hosted HTTPS, deployment, database connection, hosted gate — NOT DONE:** not authorized or not possible from here.

## Tests run

- Main tree: `test_staging_settings`, `test_settings`, `test_deploy_readiness` and `test_build152_deploy_artifacts`: 121 passed.
- Clean checkout: the same files plus `test_admin_auth` (without `test_build152_deploy_artifacts`, which exists only untracked): 165 passed. At exact `5cd21ad`, staging, settings and deploy-readiness: 114 passed.
- All used a throwaway local PostgreSQL, which I stopped and deleted afterwards.
- Not run: the full suite, because no specific finding required it.

## Shortcuts and out-of-scope changes

None reported. No stubs, TODOs, weakened tests or swallowed errors. The one test changed (the middleware-order assertion) is reported as stricter, not weaker. In-memory email accumulates in process memory until a restart. The agent did not update the Di-Eval-Effyklean records repository, so the profile and log can be mirrored there if desired.

## Confirmation and boundaries

The agent did not deploy anything. Nothing was changed in DigitalOcean, DNS, the database or network, or any provider. The only push was `ad69d92..5cd21ad` to the application repository.

## Decisions needed from HU+DI

1. Keep or drop the three extra refusals (`NOTIFICATIONS_ENABLED`, `REPORT_EMAIL_ENABLED`, `CAMPAIGN_SENDING_ENABLED`). They stay refused until Hu decides.
2. Decide whether `effyklean_app` gets `CREATE` rights on the schema it migrates, and who runs the first migration.

## Agent's proposed next steps

1. Hu: in the DigitalOcean UI, fix the database-attachment form, then get the app domain and database host, port and CA text. Choose the VPC or trusted-source option.
2. Hu: create `effyklean_app` with the privileges from decision 2, and enter the secrets as encrypted values.
3. Hu: fill the `deploy/staging_env_2026-10-24_2350.example` names into the app. Set `DJANGO_SETTINGS_MODULE=config.settings.staging` for build and run, with auto-deploy off.
4. First build: read the log to confirm `uv` installs and Python 3.14 resolves, and that `collectstatic` passes.
5. Read the health probe's Host from the first requests and add it to `ALLOWED_HOSTS`. Set `CSRF_TRUSTED_ORIGINS` and `TRUST_FORWARDED_PROTO=1`.
6. Run `migrate` only after steps 1–3 are confirmed. Then check `/healthz`, the staff-only gate with an existing MFA account, and `/assets/…`.

---

## HU+DI review status

This file records the agent's report; it is not independent verification of the claims above. HU+DI review and the safe next-action recommendation are to be recorded separately after reviewing the report against the repository's committed files and current DigitalOcean state.
