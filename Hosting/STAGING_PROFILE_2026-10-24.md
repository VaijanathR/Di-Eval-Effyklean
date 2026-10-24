# Staging settings profile and staff-only gate (2026-10-24)

Implements HU+DI decision section 9 (`Di-Eval-Effyklean/Hosting/Hosting_DigitalOcean_HUDI_Decisions_24Oct2026_1200IST.md`).
Local only: nothing pushed, deployed, or changed in DigitalOcean; `production.py` is unchanged.

* `config/settings/staging.py` — `DJANGO_SETTINGS_MODULE=config.settings.staging`. DEBUG off; `STAFF_ONLY_MODE` is fixed
  True (not an environment value). Fails closed on: SECRET_KEY under 50 chars, wildcard hosts, non-HTTPS CSRF origins,
  DB TLS weaker than `require` (`DB_SSLMODE`, `DB_SSLROOTCERT` for verify-ca/full), the `doadmin` DB user, local/payment
  stubs, `TESTCODE_ACTIVE`, Zoho Payments credentials without `ZOHO_PAYMENTS_SANDBOX=1`, Zoho Inventory org/sync/write
  flags without `ZOHO_INVENTORY_SANDBOX=1`, `CAMPAIGN_SENDING_ENABLED`, non-S3 media unless
  `STAGING_EPHEMERAL_MEDIA_ACK=1`. HTTPS redirect, secure cookies, HSTS 3600 s default (no subdomains/preload).
  `TRUST_FORWARDED_PROTO=1` is required behind the DigitalOcean proxy (same convention as production), else the HTTPS
  redirect loops.
* `modules/backoffice/staff_only_gate.py` — middleware. Every request is refused (403, noindex) unless the browser holds a
  signed `effyklean_staff_access` cookie. A signed-in, MFA-verified staff member gets it from
  `/EKIAdmin2026/staging-access` (POST "open"; "end" removes it). Re-checked per request against the active staff account
  and its password hash; any fault refuses. Exempt: Admin paths (own auth), exact `/healthz`, `/payments/zoho/webhook`
  (signature-verified). The Director's storefront password page is separate and unchanged.
* Tests: `tests/test_staging_settings.py`.
* Open (HU+DI): media store for staging (Spaces vs acknowledged throw-away disk); DB trusted sources/verify-full;
  who counts as "authorized staff" (currently any active, MFA-verified staff account); webhook exemption; DO health-check
  `Host` must be in `ALLOWED_HOSTS`; the build's `collectstatic` step (staticfiles is not installed, so the command
  does not exist; see the report).
