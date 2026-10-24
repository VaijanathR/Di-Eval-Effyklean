# Agent Response — Django Staging Settings Implementation

**Recorded:** 24 October 2026, 21:41 IST  
**Application repository:** https://github.com/VaijanathR/EffyKleanProject  
**HU+DI decision record:** https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/Hosting/Hosting_DigitalOcean_HUDI_Decisions_24Oct2026_1200IST.md

## Readiness for HU+DI review

The staging profile and staff-only gate are built and tested, but they are **not committed and not deployed**. One build-step question and several decisions remain open.

## Repository state and change handling

- Branch: `main`
- HEAD before and after the agent's work: `ad69d92`
- The agent did not commit because `CLAUDE.md` principle 6 requires HU's review first.
- Explicitly staged paths:
  - `config/settings/staging.py`
  - `modules/backoffice/staff_only_gate.py`
  - `tests/test_staging_settings.py`
  - `docs/foundation/STAGING_PROFILE_2026-10-24.md`
- The agent appended an entry to `PROJECT_LOG.md` but left it unstaged because that file already contained unrelated uncommitted edits.
- The working tree contained approximately 210 other modified files from earlier sessions.
- When committing, do not add a co-author trailer; `CLAUDE.md` forbids it.
- `config/settings/production.py`, `config/settings/base.py`, and `urls.py` were unchanged.
- No push, deployment, DigitalOcean change, or DNS change was performed.

## Requirement status and evidence

| Requirement | Status | Evidence / qualification |
|---|---|---|
| Staging settings profile | DONE (verified) | Loads with `DEBUG=False`; requires a 50+ character secret key, non-wildcard hosts, HTTPS-only CSRF origins; uses secure-cookie and HTTPS-redirect protections. HSTS defaults to 3600 seconds. |
| Database security | DONE (verified) | Requires TLS; supports `verify-full` and a root certificate; refuses the `doadmin` user. |
| Provider safeguards | DONE (verified) | Refuses local stubs, payment stub, `TESTCODE_ACTIVE`, Zoho Payments or Inventory settings without the corresponding sandbox switch, and campaign sending. Each refusal has a test. |
| Staff-only gate | DONE (verified) | Details below. |
| Health check | DONE (verified) | `/healthz` remains open and returns only `ok`. |
| `production.py` unchanged | DONE (verified) | It does not appear in `git status`. |
| Focused tests | DONE (verified) | `tests/test_staging_settings.py`: 55 passed. |
| Django check with staging settings | DONE (verified) | Output: “no issues (1 silenced)”. |
| `check --deploy` | DONE (verified, with warnings) | Three warnings reported: no Django CSRF middleware (the project uses its own); HSTS subdomains and preload are deliberately off. |
| `collectstatic` with staging settings | NOT DONE | Command failed with “Unknown command: 'collectstatic'”, exit code 1, because `django.contrib.staticfiles` is not installed. The architecture reportedly leaves it out of scope; the DigitalOcean build behavior remains unverified. |
| Full test suite | NOT RUN | Agent reported that the change adds new files only. |
| Email and media | PARTIAL | Decisions remain open below. |

The combined test run for `test_staging_settings`, `test_settings`, `test_deploy_readiness`, and `test_admin_auth` reported **148 passed**. Docker was unavailable, so tests ran against a throwaway PostgreSQL instance in a scratchpad, which the agent stopped and deleted afterward.

## Staff-only gate evidence

The gate is implemented in `modules/backoffice/staff_only_gate.py`, enabled by `STAFF_ONLY_MODE=True` in staging settings, and cannot be disabled through an environment variable.

- Anonymous requests receive HTTP 403 with `noindex`, including `/`, `/products/`, `/cart/`, `/checkout/`, `/api/v1/`, `/robots.txt`, unknown paths, and POST requests such as `/cart/add` and `/checkout/pay`.
- Parametrized tests cover 13 GET paths and 3 POST requests.
- The agent also exercised real requests under `config.settings.staging`: `/`, `/products/`, `/api/v1/`, and a POST to `/cart/add` all returned 403.
- Access is granted only to a signed-in, MFA-verified staff member through a button at `/EKIAdmin2026/staging-access`.
- The access cookie is signed, HttpOnly, Secure, SameSite=Lax, and expires after 8 hours.
- A deactivated account, changed password, or database fault ends access immediately (tested).
- Password-only login without MFA does not grant access.
- Still reachable without the cookie: the Admin sign-in page, exact `/healthz`, and the Zoho Payments webhook, which accepts only a valid signature.
- Not yet exercised: actual HTTPS redirect behavior and the health probe under staging settings against a TLS database, because no hosted database was available.

## Open HU+DI decisions and blockers

1. **Static files / `collectstatic`:** The command is absent. DigitalOcean might skip the step when the command is missing, but this was not verified. Decide whether to skip that build step or approve installing `django.contrib.staticfiles`.
2. **Media:** Staging requires S3-compatible storage. Temporary local disk is accepted only with `STAGING_EPHEMERAL_MEDIA_ACK=1`. Which option to use is for HU+DI; Spaces is not provisioned.
3. **Email:** Console backend is the default, so messages are not delivered. A real mail backend, sender, and provider have not been selected.
4. **Database user:** The app refuses `doadmin`; the `effyklean_app` user needs sufficient privileges for the first migration. This is untested on DigitalOcean.
5. **Authorized staff definition:** Currently any active, MFA-verified staff account qualifies. A narrower role/capability would require a decision.
6. **Zoho Payments webhook exemption:** The gate exempts this webhook so sandbox payments can complete. HU+DI confirmation is requested.
7. **Health probe host:** DigitalOcean's probe Host header must be included in `ALLOWED_HOSTS`, or the existing host check will reject it.
8. **Proxy header:** Set `TRUST_FORWARDED_PROTO=1` behind the proxy to avoid an HTTPS redirect loop.

## Shortcuts, placeholders, and deviations

The agent reported no stubs, TODOs, weakened tests, or swallowed errors. The gate's broad exception handler is intentional fail-closed behavior and logs a warning.

The agent left `deploy/app-spec.staging.example.yaml` and the rest of the working tree untouched.

## Current boundary

This report records the agent's claims and evidence for HU+DI review; it does not itself verify the local working tree. The implementation remains uncommitted and undeployed. Do not treat the staging decision record as proof that the implementation is complete, and do not deploy or enable public access until HU+DI reviews the remaining decisions and authorizes the next step.
