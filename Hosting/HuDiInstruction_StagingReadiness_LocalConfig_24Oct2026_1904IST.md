# HU+DI Instruction — Finish Staging Readiness Configuration
**Date:** 24 October 2026  
**Priority:** Get staff-only staging running quickly; keep the work narrow and evidence-based.

## Task
Continue from the agent's local application commit `2a35f4e` and complete the remaining **local repository** configuration needed for a safe DigitalOcean staff-only staging deployment. Read the latest public HU+DI hosting decision record first, especially Sections 9–10, and use `Hosting/STAGING_PROFILE_2026-10-24.md` as the current profile. Do not ask Hu to repeat recorded decisions.

## Decisions to implement
- Settings module: `config.settings.staging`; do not modify `production.py`.
- Staff-only mode stays fixed ON. Only existing active Admin/Director accounts that completed MFA are allowed; do not create accounts.
- Initial staging email backend: Django in-memory backend; no outbound email delivery.
- Initial staging media: temporary local/ephemeral storage is accepted only with `STAGING_EPHEMERAL_MEDIA_ACK=1`; document uploads are disposable. Defer Spaces.
- Database target: existing `effyklean-db` / `defaultdb`, dedicated least-privilege `effyklean_app`, never `doadmin`. Require TLS; support correct CA verification. Do not guess trusted-source IPs or make cloud/database changes.
- Use `TRUST_FORWARDED_PROTO=1` only for the intended DigitalOcean proxy setup. No wildcard hosts. Health probe Host must be explicitly allowed once its actual value is known.
- Keep Zoho Payments and Zoho Inventory/Shiprocket in sandbox. Preserve the Zoho-owned shipment workflow. Exact signed Zoho Payments webhook exemption only.
- Keep auto-deploy disabled; no public launch.

## Constraints
- Local repository changes and local tests only. **Do not push, deploy, change DigitalOcean/database/network/DNS settings, create resources, change provider settings, or enable live integrations.** Those actions require separate explicit HU+DI authorization.
- Work in the existing local checkout and preserve the reported local commit/worktree. Do not reset, clean, stash, or overwrite the 210 reported unrelated modified/untracked files. Do not stage broadly; use explicit paths only. No `git add -A`. No commit co-author trailer.
- Do not modify frozen architecture/specs or weaken security/tests. Do not add stubs, placeholders, TODOs, swallowed errors, or unrelated refactors.
- Do not run the full suite automatically; run focused tests for changed behavior and relevant deployment-readiness checks.

## Required work
1. Verify current local HEAD and worktree first; confirm commit `2a35f4e` is present. If not, stop and report rather than guessing or overwriting.
2. Implement/document the in-memory email backend and acknowledged ephemeral-media setting for staging, with fail-closed behavior when required.
3. Verify the startup/build route and exact build/run commands from the repository's actual dependency and deployment configuration; configure `DJANGO_SETTINGS_MODULE=config.settings.staging` for the correct scopes. Do not invent a Dockerfile or change build strategy without evidence.
4. Check the proxy/HTTPS configuration, `ALLOWED_HOSTS`, CSRF origins, staff-only gate, `/healthz`, static collection/serving, database TLS and least-privilege checks. Clearly distinguish settings that can be safely completed in code from values that must come from the DigitalOcean UI.
5. Run focused tests and relevant Django/deployment checks. Avoid an expensive full suite unless a concrete finding makes it necessary.
6. Commit regularly at each coherent, verified checkpoint (for example, staging email/media settings; then build/startup configuration; then any distinct security/readiness fix). Run the focused checks for that checkpoint before committing. Use a clear, scoped commit message and explicitly stage only intended paths/hunks. Preserve unrelated work. Do not push. Avoid both premature commits of failing/incomplete changes and one oversized end-of-task commit.

## Completion report — mandatory
For each requirement above, mark **DONE (verified) / PARTIAL / NOT DONE / DEFERRED** and provide command output or file/line evidence. Include:
- exact starting and ending commit hashes; each checkpoint commit hash and message, with the paths included in each commit;
- exact changed paths and focused test/check commands with results;
- the exact build and run commands, supported by repository evidence;
- every value still requiring DigitalOcean UI input (including actual health-check Host and trusted-source/network choices);
- any shortcuts, stubs, placeholders, TODO/pass, weakened tests, swallowed exceptions, or out-of-scope changes (state “none” only after checking);
- explicit confirmation that nothing was pushed, deployed, or changed in DigitalOcean, DNS, database/network settings, or providers.

Stop and report if the worktree state, frozen requirements, or a security/business decision conflicts with this instruction. Do not make a new decision on Hu's behalf.
