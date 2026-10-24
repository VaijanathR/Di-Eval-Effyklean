HU+DI DIRECTIVE — COMPLETE DIGITALOCEAN STAGING READINESS AND CHECKPOINT PUSH — 24 OCT 2026

Continue from the existing repository state and the latest hosting work. Read these records first; do not ask Hu to repeat information already recorded:

1. Hosting/AgntResp_DigiOcnHosting_24102026_2327.md
2. Hosting/DI_observations and recommendations for DigiOcnHosting_24Oct2026_2337.md
3. Hosting/Hosting_DigitalOcean_HUDI_Decisions_24Oct2026_1200IST.md
4. The applicable implementation instructions, current project status register, and existing repository governance.

OBJECTIVE

Finish the remaining authorized DigitalOcean staging-readiness work, preserve all unrelated work, commit verified checkpoints, and push the intended hosting commit sequence to origin/main if it can be done safely as a fast-forward. Produce a complete evidence-based handover so HU+DI can resume without repeating this work.

1. RECONCILE THE REPOSITORY FIRST
- Inspect current branch, HEAD, origin/main, ancestry, git status, staged/unstaged diffs, untracked files, and the complete intended commit sequence.
- Reconcile the existing local hosting checkpoints, including b965d2b and 5c45f31, against their actual ancestry and the current remote. Do not assume these hashes or their order are still valid without verification.
- There are 210 unrelated changed/untracked worktree files reported previously. Recheck the actual count and preserve all unrelated work.
- Do not reset, clean, stash, amend, rebase away work, or use git add -A.
- Stage explicit, reviewed paths only. Do not overwrite another session's work.
- If origin/main has diverged, or intended commits contain unrelated changes, STOP and report the exact evidence and proposed safe resolution. Do not force-push.

2. COMPLETE STAGING READINESS — HOSTING SCOPE ONLY
Use the approved config.settings.staging approach. Do not weaken production.py or modify local.py merely to make staging work.

Resolve and verify, where possible:
- Python 3.14 / uv.lock / DigitalOcean build-route compatibility. Establish the actual supported build method from repository configuration and available evidence. If a Dockerfile is necessary, implement it only if consistent with the existing approved architecture and instructions; otherwise STOP and report the concrete incompatibility and decision required.
- Staging settings, startup command, PORT binding, static files, health endpoint, allowed hosts, proxy HTTPS handling, and staff-only access gate.
- Database connection to the existing effyklean-db PostgreSQL 17 instance in BLR1, using defaultdb and a dedicated effyklean_app role, not doadmin. Enforce certificate-verified TLS (verify-full) with the correct CA. Do not invent a CA path, certificate, IP address, privilege grant, or credential.
- Verify the expected database privileges and migration readiness from available local evidence. Hosted connectivity, role existence, privileges, migrations, and deployment behavior must remain explicitly unverified unless actually tested with authorized access.
- Keep the initial staging email backend in-memory/non-delivering. Do not enable outbound email or campaigns.
- Keep ephemeral media only with STAGING_EPHEMERAL_MEDIA_ACK=1 and clearly document that uploaded media is disposable. Do not introduce Spaces without a separate decision.
- Verify the health probe's actual Host is allowed. No wildcard ALLOWED_HOSTS.
- Preserve the staff-only gate for existing active Admin and Director accounts after MFA. Do not create staff accounts.
- Review deploy/app-spec.staging.example.yaml. The previously reported version referenced production settings; do not use or leave a misleading deployable specification. Correct it only within authorized scope and verify it, or clearly mark it unusable pending the required decision.
- Treat any additional email-feature refusal flags, including NOTIFICATIONS_ENABLED, REPORT_EMAIL_ENABLED and CAMPAIGN_SENDING_ENABLED, as a HU+DI decision point if their behavior exceeds the already approved initial staging scope. Keep outbound delivery disabled; do not silently expand business scope.
- Do not repeat completed sandbox setup. Zoho Payments sandbox is working. Zoho Inventory sandbox integration with Shiprocket sandbox is completed per Hu. Preserve the Zoho-managed shipment workflow; do not add direct website-to-Shiprocket shipment creation.

3. TEST WITH RISK-BASED SCOPE
- Run the relevant focused tests for each changed area and the required Django/system/configuration checks.
- The previous report recorded 119 focused tests passing against a throwaway local PostgreSQL database. Verify the present baseline and rerun only where needed for current changes.
- Do not claim a full-suite pass unless the full suite was actually run. Do not weaken tests, skip required tests to manufacture a pass, or swallow errors.
- Do not perform migrations or writes against the DigitalOcean database, deploy, change cloud settings, create chargeable resources, change DNS/networking, or run live provider operations. HU+DI will handle those steps separately.
- If a required check cannot run, state the exact blocker, command, and evidence. Continue other independent authorized work.

4. CHECKPOINT, COMMIT AND PUSH
- Commit each coherent, verified hosting checkpoint locally with clear messages and no co-author trailers.
- Review each commit's changed paths and diff before committing.
- Push the intended hosting commit sequence to origin/main only if the remote ancestry and reviewed contents confirm a safe fast-forward and no unrelated changes are included. Hu has authorized this intended checkpoint push; this is not deployment authorization.
- After pushing, verify the remote HEAD and that every intended commit is present. Report exact commit SHAs and verification evidence.
- Never use force-push. If safe push cannot be established, STOP before pushing and report the precise reason.

5. REQUIRED COMPLETION AUDIT
For every applicable plan/spec/instruction item, report exactly one status:
DONE (verified) / PARTIAL / NOT DONE / DEFERRED.

For each status, give concise evidence: command and relevant output, test result, commit/path, or file and line reference. Distinguish local verification from actual DigitalOcean-hosted verification.

Explicitly list:
- Remaining blockers and decisions required from HU+DI.
- Any stubs, placeholders, TODO/FIXME, pass-only implementations, weakened tests/assertions, swallowed exceptions, misleading configuration, or out-of-scope changes found or introduced.
- Tests actually run, tests not run, and why.
- Local commits created, intended commits pushed, remote HEAD verification, and anything deliberately left uncommitted.
- Every remaining action needed before HU+DI can safely proceed to the DigitalOcean UI and staging deployment.

6. GOVERNANCE AND HANDOVER
- Update the applicable timestamped hosting status/decision records and project status documents to match the verified result. Every new EffyKlean filename must include a timestamp. Do not create duplicate or untimestamped documents.
- Keep records concise and factual; do not claim deployment, hosted verification, or completion of a task that was only proposed.
- Do not add UTM tracking parameters to GitHub URLs or records.
- Do not send progress popups or interim reports. Finish the authorized work and return one consolidated final report.
- Stop and report rather than make assumptions whenever a frozen architecture/specification, security boundary, business rule, or unresolved HU+DI decision would be changed.

FINAL RESPONSE FORMAT
1. Overall result and exact current local/remote HEADs.
2. DONE (verified) / PARTIAL / NOT DONE / DEFERRED checklist against the applicable plan.
3. Commands and test evidence.
4. Exact commit SHAs and push verification, or why push was safely withheld.
5. Remaining blockers and explicit HU+DI decisions.
6. Short, ordered next-step list for Hu and Di.

Prioritize verified progress and blockers over paperwork. Do not stop merely because a task is inconvenient; stop only for a genuine authorization, safety, ambiguity, or technical blocker. Do not report success without evidence.
