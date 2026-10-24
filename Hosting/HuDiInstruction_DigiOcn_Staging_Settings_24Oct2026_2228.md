# HU+DI Instruction — Resolve Staging Static Assets, Verify and Commit

**Priority: Immediate. Implement → verify → document → commit. Do not return another assessment-only report.**

## Existing project records

Read the existing implementation and decisions; do not repeat previously completed work.

- Application repository: https://github.com/VaijanathR/EffyKleanProject
- HU+DI hosting decisions: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/Hosting/Hosting_DigitalOcean_HUDI_Decisions_24Oct2026_1200IST.md
- Staging profile: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/Hosting/STAGING_PROFILE_2026-10-24.md
- Previous implementation report: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/Hosting/AgntResponses_StagingSettingsImplementation_241026_2141.md

## 1. Implement the fix

Resolve the known failure:

`Unknown command: 'collectstatic'`

The reported cause is that `django.contrib.staticfiles` is absent.

- Implement the smallest safe solution compatible with the existing Django architecture and deployment build.
- Ensure required static assets can be collected and actually served in staging. Do not merely make the command available or silently bypass collection.
- Reuse existing project dependencies and serving mechanisms where suitable. Avoid unnecessary redesign or new infrastructure.
- Preserve `DEBUG=False`, HTTPS/security protections, database TLS protections and all existing staging safeguards.
- Ensure restricted staging access permits **existing active Admin and Director accounts only, authenticated with MFA**. Do not create new staff accounts. Do not rely on a generic `is_staff` check alone.

## 2. Verify the fix

Run only the focused checks needed to establish that the change works:

- Confirm `collectstatic` is available and completes successfully.
- Verify the configured static-serving strategy and the presence/accessibility of collected assets using an appropriate local check.
- Run relevant staging-settings, settings, deployment-readiness and staff-access tests.
- Run relevant Django checks.

Do not rerun the entire test suite unless a specific failure or dependency makes that necessary. Do not claim that hosted HTTPS behavior or DigitalOcean deployment has been verified unless actually tested.

## 3. Update project records

Update the relevant staging profile/documentation and `PROJECT_LOG.md` with the actual changes, verification results and remaining limitations.

Preserve unrelated existing edits. If `PROJECT_LOG.md` already contains unrelated changes, incorporate the entry without overwriting them.

## 4. Commit the completed work — explicitly authorized

After implementation, focused verification and documentation updates:

1. Inspect the complete diff and identify all intended files.
2. Stage **explicit file paths only**. Never use `git add -A`.
3. Include only the staging implementation, static-assets fix, directly relevant tests and documentation/log updates.
4. Preserve all unrelated modified and untracked files. The working tree contains substantial unrelated changes; do not include them in this commit.
5. Commit the verified work on the current branch with a clear, descriptive commit message.
6. Do not add commit co-author trailers.
7. Report the commit hash and exact committed file list.

**Commit is authorized. Push and deployment are not authorized.**

## 5. Strict boundaries

- Do not push, deploy, modify DigitalOcean or DNS, change production configuration, or alter cloud/database/provider settings.
- Do not perform live payment, provider-write, dispatch or other live business operations.
- Do not weaken tests, add stubs/placeholders, suppress errors or make unrelated changes.
- If a genuine frozen-architecture conflict or unresolved security/business decision blocks implementation, stop and report that specific blocker. Otherwise, proceed without asking for another approval.

## 6. Required completion report

For each applicable task, mark **DONE (verified) / PARTIAL / NOT DONE / DEFERRED** and provide concise command output or exact file-and-line evidence.

Report:

- Root cause and fix implemented.
- Exact files changed and why.
- `collectstatic` result and static-serving verification.
- Focused tests and Django check results.
- Admin/Director MFA authorization enforcement and relevant test evidence.
- Documentation and project-log updates.
- Commit hash and exact committed files.
- Remaining staged, unstaged and untracked changes, explicitly distinguishing pre-existing unrelated work.
- Any shortcuts, stubs, placeholders, TODOs, weakened tests, swallowed errors or out-of-scope claims introduced; state **None** if none.
- Confirmation that no push, deployment, cloud/DNS change or live provider operation occurred.

**Proceed now. Implement, verify, document and commit. Do not return another assessment-only report.**
