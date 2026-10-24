# Agent Response — DigitalOcean Hosting — 24 October 2026, 23:27

The local staging configuration is finished and committed in two checkpoints. All of it was checked locally only. Nothing was pushed or deployed, and I changed nothing in DigitalOcean, DNS, the database or network, or any provider.

Start and end: the start was `2a35f4e`, which was present as expected, and the worktree had the reported 210 unrelated files. The end is `5c45f31`. The 210 unrelated files are untouched, and no commit has a co-author trailer.

| Commit | Message | Paths |
|---|---|---|
| `b965d2b` | staging uses the in-memory email backend; delivery-dependent email features refused | `config/settings/staging.py`, `tests/test_staging_settings.py` |
| `5c45f31` | staging database CA via path or PEM, build/run commands and environment names documented | `config/settings/staging.py`, `tests/test_staging_settings.py`, `deploy/staging.env.example` (new), `docs/foundation/STAGING_PROFILE_2026-10-24.md`, `PROJECT_LOG.md` (only my added line) |

## Requirements

- **Email: DONE (verified).**
  - `EMAIL_BACKEND` is fixed to Django's in-memory backend, and any other value in the environment is refused.
  - I also made staging refuse `NOTIFICATIONS_ENABLED`, `REPORT_EMAIL_ENABLED` and `CAMPAIGN_SENDING_ENABLED`, because with an in-memory backend they would record messages as sent when nothing was delivered. This goes slightly beyond your list, so please confirm you want it.

- **Media: DONE (verified).** Local disk is accepted only with `STAGING_EPHEMERAL_MEDIA_ACK=1`. Without it, startup fails. Tests cover both cases.

- **Database: DONE (verified).**
  - TLS is required, and `doadmin` is refused.
  - The CA certificate can be given as a file path (`DB_SSLROOTCERT`) or as certificate text (`DB_SSLROOTCERT_PEM`). The text is written once to a private temp file.
  - With a CA and no `DB_SSLMODE`, the mode defaults to `verify-full`.
  - Bad combinations are refused (tested).

- **Proxy, hosts, gate, static, health: DONE (verified locally).** I booted the run command with 2 gunicorn workers and sent requests, using a placeholder Host `staging.example.test`:
  - Plain HTTP to `/` returned 301 to HTTPS.
  - HTTPS via the proxy header to `/` and `/assets/effyklean-logo.jpg` returned 403 without a staff cookie.
  - `/healthz` with an allowed Host was not redirected. It returned 503 only because I pointed it at an unreachable database.
  - `/healthz` with an unknown Host returned 400.
  - `collectstatic` exit 0, 9 files.

- **Build and run: PARTIAL.** The repository evidence is `pyproject.toml` (Python 3.14, gunicorn), `uv.lock` and `.python-version`. There is no Dockerfile or Procfile, and I did not invent one. I could not verify that DigitalOcean's buildpack installs from `uv.lock` on Python 3.14. If it can't, a Dockerfile using uv is needed, which is your decision.

- **Checks: DONE.** `test_staging_settings`, `test_settings`, `test_deploy_readiness` and `test_build152_deploy_artifacts` gave 119 passed against a throwaway local PostgreSQL. I did not run the full suite, so the staging-settings and gate tests were not re-run against the real hosted setup.

## Exact commands

(Set `DJANGO_SETTINGS_MODULE=config.settings.staging` for both build and run scopes.)

- **Build:** `python manage.py collectstatic --noinput`
- **Pre-deploy:** `python manage.py migrate --noinput`. This needs DDL rights for `effyklean_app`, which is untested.
- **Run:** `gunicorn --worker-tmp-dir /dev/shm --bind 0.0.0.0:${PORT:-8080} --workers 2 --access-logfile - config.wsgi:application`

## Values only the DigitalOcean UI can supply

(The names are in `deploy/staging.env.example`.)

- The app domain.
- The health probe's actual Host, to add to `ALLOWED_HOSTS`.
- The database host and port, the CA certificate text, and the `effyklean_app` password and privileges.
- The trusted-source or VPC attachment choice.
- The fix for the database-attachment form that didn't populate.
- `SECRET_KEY` and the other secrets.
- `CSRF_TRUSTED_ORIGINS` and `TRUST_FORWARDED_PROTO=1`.

## Shortcuts and out-of-scope changes

None beyond the email-feature refusals above. There are no stubs, TODOs, weakened tests or swallowed errors. In-memory email accumulates in process memory until a restart, which I documented. I did not touch the existing `deploy/app-spec.staging.example.yaml`. It is untracked work from another session and still names the production settings module, so correct it before using it.

I stopped and deleted the temporary local PostgreSQL I used for the checks.
