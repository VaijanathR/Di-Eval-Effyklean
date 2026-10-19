# EffyKlean — DigitalOcean Staging Readiness: Focused Follow-up

## 1. Governing instructions

Follow the consolidated HU+DI agent instructions exactly as published:

https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/Original_AgntInst_19Oct2026_1233.md

Also comply with the mandatory SSD audit requirement referenced by those instructions.

Treat this task strictly as a **read-only investigation and recommendation exercise**. The existing DigitalOcean investigation report is the starting point:

https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentImplementationRecords/AgentREsp_DIgitalOceanSetup_18Oct26_1708.md

Do not repeat the entire previous investigation unnecessarily. Verify the specific unresolved points below against the current repository and current DigitalOcean documentation.

## 2. Absolute boundaries

- Do not modify repository files.
- Do not create, edit, delete, or resize DigitalOcean resources.
- Do not create databases, database users, App Platform apps, components, jobs, Spaces, or other paid resources.
- Do not deploy, publish, push, commit, stage, or alter DNS.
- Do not enable auto-deploy or trigger a build/deployment.
- Do not use live payment, inventory, shipping, email, or other provider operations.
- Do not reveal, copy, print, or include secret values in the report. Inspect only what is necessary and report configuration presence/status, not credentials.
- Do not change `.env`, repository settings, account settings, or provider configuration.
- Do not run potentially destructive commands or checks that create real provider-side records.
- Do not run the full test suite merely for reassurance. Use existing evidence and narrowly targeted, non-destructive checks only when necessary.
- Preserve all existing changes, including the previously HU-approved home-page link rearrangement. Do not stage or commit anything.
- Do not delegate this task to another agent.

If a frozen architecture/specification, security guard, provider workflow, business rule, or existing configuration conflicts with a proposed solution, STOP → REPORT → HU+DI DECIDE. Do not resolve it by assumption.

## 3. Verify the current repository evidence

Inspect the actual checked-out repository and establish:

1. Current branch, HEAD, working-tree status, and divergence from the configured remote, without modifying anything.
2. Whether the current GitHub branch contains the required deployment files and implementation. Distinguish local-only commits and uncommitted changes from what App Platform could actually build.
3. The actual dependency/build files: `pyproject.toml`, `uv.lock`, `.python-version`, any `requirements.txt`, and any Dockerfile or deployment configuration.
4. The actual Django WSGI/ASGI module, installed production server dependency, and correct working directory.
5. Existing production and development settings, provider guards, media storage, email configuration, health/readiness checks, and migrations.
6. The precise existing protections against accidental live Zoho Payments, Zoho Inventory, Shiprocket, email, or other external side effects.

Report file paths and line references or exact command output that supports each material conclusion. Do not infer repository facts from an earlier report when they can be verified read-only.

## 4. Resolve the DigitalOcean Python build/run uncertainty

Consult the current official DigitalOcean App Platform Python buildpack documentation and compare it with the actual repository.

Official reference:
https://docs.digitalocean.com/products/app-platform/reference/buildpacks/python/

Determine, based on evidence:

- Whether the current repository root can be detected and built using the documented Python buildpack.
- How the documented `uv` support relates to the buildpack’s root-file detection requirements.
- Whether a Dockerfile is genuinely necessary, or whether a simpler supported build configuration is sufficient.
- The exact proposed build command, if one is required.
- The exact proposed run command, including the correct Django WSGI module, Gunicorn dependency, port binding, and any documented temporary-directory workaround.
- The appropriate health-check path and whether it exists and is safe to call without triggering external side effects.

Do not edit dependency files or add a marker file just to make detection work. Do not guess. If current documentation and repository evidence do not establish a reliable answer, report the uncertainty and the smallest safe verification needed.

## 5. Recommend the minimum safe staging configuration

Inspect existing settings and propose a minimal staging-settings design, likely under `config/settings/staging.py` if that fits the existing structure.

This is a design recommendation only; do not create the file.

The proposal must address:

- `DEBUG=False`, explicit allowed hosts, HTTPS-aware settings, secure cookies, and appropriate CSRF trusted origins.
- Clear separation between staging and production settings.
- Explicit sandbox-only Zoho Payments configuration.
- The Zoho Inventory sandbox → Shiprocket sandbox workflow Hu has reported as integrated; preserve it and do not switch it to live mode.
- Explicit refusal of live provider credentials/configuration in staging where technically feasible. Do not rely on credentials alone as the safety control.
- No real payment capture, shipment creation, inventory mutation, customer notification, or other external write unless separately reviewed and expressly authorized.
- Safe email behavior that does not accidentally send customer-facing messages. Do not assume an existing email readiness check is harmless if it contacts SMTP.
- `TESTCODE` and local provider stubs must remain rejected/disabled in the staging web configuration where required by the project’s frozen rules.
- Media storage limitations if Spaces remains deferred.
- A safe health check and a safe, deployment-time migration approach.

Identify any conflict with frozen specifications or existing production guards. Do not weaken production protections to accommodate staging.

## 6. Database and resource recommendation

Use the existing reported DigitalOcean Managed PostgreSQL cluster as the starting point for cost-conscious planning. Do not create or change anything.

Recommend whether staging should use a separate logical database and separate database role on the existing cluster. Address:

- Private connectivity and TLS.
- Least-privilege database permissions.
- Keeping local automated tests off the DigitalOcean database.
- Separation from production data and credentials.
- The fact that sharing a cluster also shares the underlying infrastructure and backup/failure domain.

Do not assume that an existing database or user is suitable without evidence. Do not print database credentials or connection strings.

## 7. Background jobs and migrations

Classify these existing management commands based on their actual code and available evidence:

- `run_outbox`
- `run_scheduled`
- `retry_integrations`
- `reconcile_payment_attempts`
- `suspend_inactive_business_roles`

For each, state whether it appears to be a continuous worker, scheduled job, on-demand maintenance command, or not yet safe to classify.

Check evidence for idempotency, locking, retry behavior, external side effects, and sandbox safety. If evidence is missing, state that explicitly.

Recommend the minimum initial background-processing setup. Do not create jobs or assume every command should be enabled.

Recommend a deployment-time migration job rather than running migrations independently in each web process, subject to confirmation against the project’s existing deployment and database design.

Official DigitalOcean reference:
https://docs.digitalocean.com/products/app-platform/how-to/manage-jobs/

## 8. Costs and remaining decisions

Provide a concise estimate of the expected incremental monthly cost for the smallest plausible staging setup, separating:

- Existing resources and their already-reported costs.
- Proposed App Platform web component.
- Any optional worker or scheduled-job costs.
- Deferred Spaces or other optional services.

Use current official pricing where available. Clearly distinguish estimates from confirmed account-specific prices. Do not create anything to obtain a price.

List only genuine decisions that require HU+DI approval. Avoid adding optional infrastructure or complexity without a demonstrated need.

## 9. Required report format

Return one concise, evidence-based report with:

1. Executive conclusion: ready for the next planning step, or blockers remain.
2. Verified repository and GitHub deployment-source status.
3. Build/run/health-check recommendation.
4. Minimum staging configuration recommendation.
5. Database isolation recommendation.
6. Background-job and migration recommendations.
7. Cost estimate and deferred items.
8. Blockers, uncertainty, and explicit HU+DI decisions needed.
9. Exact files/lines, commands, and official documentation supporting conclusions.
10. Final audit confirming that no files, repository state, credentials, provider settings, DigitalOcean resources, DNS, deployments, or charges were changed.

Clearly label each important statement as one of:
- **Verified fact**
- **Recommendation**
- **Unresolved / requires evidence**
- **HU+DI decision required**

Do not claim a check passed unless it was actually run and its result is available.

## 10. Stop condition

Finish after delivering the report. Do not implement the recommendations or begin another task. Wait for HU+DI review and explicit authorization before making any changes.

The objective is to establish the smallest safe, evidence-backed path to a sandbox staging deployment while preserving the frozen architecture, existing resources, provider sandbox workflow, and all project governance rules.
