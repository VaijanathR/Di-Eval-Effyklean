# HU+DI DigitalOcean Decisions and Setup Handover — 24 October 2026

**Record timestamp:** 24 October 2026, approximately 12:00 IST  
**Purpose:** Durable decision record for the active DigitalOcean setup. Read this before asking Hu to repeat decisions or continuing setup in another chat.

## 1. Confirmed hosting and launch decision

- DigitalOcean is the selected initial hosting provider. The intention is to observe performance and cost for 3–6 months after go-live, optimize within DigitalOcean first, and reconsider migration only if evidence justifies it.
- Use the existing **EffyKlean Production project** in DigitalOcean. Hu explicitly corrected the earlier suggestion to create/use a separate staging project.
- Deploy the actual EffyKlean storefront into the Production project for **staff-only final testing first**.
- Keep the site restricted to authorized staff during final testing. Do not expose it as a public storefront until the issues are resolved and integrations have been tested.
- Open the storefront to the public only after the readiness criteria are satisfied and public launch is explicitly approved.
- “Production project” does **not** mean public access or live payment/fulfilment is enabled during staff testing.
- Keep Auto-deploy on push disabled during setup/testing so coding-agent pushes do not automatically trigger deployments.
- Documentation and this record do not themselves authorize app creation, chargeable resources, database configuration changes, deployment, DNS changes, live provider writes, or public launch.

## 2. Current DigitalOcean resources (confirmed during this session)

The EffyKlean project currently shows one resource:

- Database cluster: `effyklean-db`
- Region/engine: BLR1 / PostgreSQL 17
- Status: Online
- Plan: primary-only, 1 GB RAM / 10 GiB disk
- No App Platform app was listed before starting this setup.

Do not create a duplicate database without a specific, reviewed reason. Reuse the existing database only after confirming the application connection, access-control, TLS, database-role and data-safety requirements.

## 3. Database network and TLS observations

Hu inspected the database's Network Access and connection parameters:

- Public and VPC/private connection endpoints are shown.
- Connection parameters show `sslmode=require`; the `verify-full` option is OFF.
- The Network Access page states that no trusted sources are currently configured and that the database is open to all incoming connections.

**Required before app connectivity is enabled:** establish and apply a safe trusted-source/network plan, preserve any legitimate existing access, prefer supported private connectivity when correctly configured, and configure proper server-certificate verification where supported. Do not guess IPs or prematurely add broad access rules. Do not share passwords or secret-bearing connection strings in public records.

A dedicated least-privilege application database user should be considered instead of using the administrative `doadmin` account for routine application traffic. Do not change database users or network rules until the plan is clear and the action is authorized.

## 4. App Platform screen reached — not finalized

Hu selected the following in the App Platform flow:

- GitHub repository: `VaijanathR/EffyKleanProject`
- Branch: `main`
- Auto-deploy on push: Disabled
- Resource type: Web Service
- DigitalOcean detected a Python build.
- Current build strategy displayed: Buildpack
- Build command: none defined
- Run command: none defined
- Public HTTP port: 8080
- Environment variables: none added
- Region: BLR1
- Proposed instance: `apps-s-1vcpu-1gb-fixed`, displayed at **$10.00/month**
- Autoscaling: Off; one container
- Project: EffyKlean / Production
- App name was shown as `effklean-web`; use a clear name such as `effyklean-web` if the name is still editable and available.

**Important:** Hu has not finalized/created this app as of this record. Do not assume a deployment exists or that the displayed price has been incurred.

## 5. Build and startup strategy — still needs verification

- EffyKlean uses `uv` for Python dependency management. `uv` is free and open-source; no replacement of it is intended.
- A Dockerfile that explicitly uses `uv` was recommended as a possible reliable DigitalOcean build route because buildpack detection requirements may not match the repository's files. This is not recorded as an implemented repository change.
- The current DigitalOcean screen still shows Buildpack and has no build or run command. Do not finalize or deploy until the repository's actual build files, Python version, dependencies, Django settings module and startup command have been safely verified.
- Do not interfere with the coding agent's active work or edit its working tree while it is running. Re-check the repository at a safe point before deciding whether to use Buildpack or Dockerfile.
- The historical proposed startup command was:
  `gunicorn --worker-tmp-dir /dev/shm --bind 0.0.0.0:${PORT:-8080} --workers 2 --access-logfile - config.wsgi:application`
  Treat this as a proposal only; verify it against the current repository and the selected settings module before use.

## 6. Staff-only testing and safe integration boundary

Before staff testing, confirm genuine access control for authorized staff. Do not rely solely on `ALLOWED_HOSTS`, obscurity, or search-engine no-indexing. Configure environment secrets safely, HTTPS and secure cookies, appropriate allowed hosts/CSRF origins, DEBUG disabled, safe email behavior, health checks, and a reviewed media-storage approach.

- Keep payment and fulfilment integrations on sandbox/test configuration during final staff testing.
- Zoho Payments sandbox has been tested and is working.
- Hu has confirmed Zoho Inventory sandbox integration with Shiprocket sandbox is completed/known; do not reopen setup merely because an older audit could not verify the Zoho-side link.
- Preserve the established workflow: website sends order data to Zoho; Zoho owns shipment creation/carrier workflow; shipment status/tracking returns through Zoho to the website. Do not add direct website-to-Shiprocket shipment creation.
- No real payment, live provider write, real shipment/dispatch, or live order should occur during sandbox testing.

## 7. Recommended next actions

1. Keep the current App Platform flow unfinalized until deployment configuration is ready.
2. Safely verify repository build files and current Django settings after the coding agent's active work is finished; do not repeat checks Hu has already confirmed.
3. Decide the supported build route and define the correct build/run commands.
4. Choose and implement the staff-only access-control approach before any staff-facing deployment.
5. Settle database connectivity, TLS verification, trusted sources, and least-privilege database access before connecting the app.
6. Decide safe email and media behavior for the hosted test environment.
7. Review expected total monthly cost and account credits before creating chargeable resources.
8. Create/configure the App Platform app only when prerequisites are ready and the action is explicitly authorized.
9. Complete staff-only sandbox end-to-end testing. Resolve issues and test integrations.
10. Keep public launch as a separate HU+DI approval gate.

## 8. Working rules for future continuation

- Read this file and the existing Hosting decision/implementation-plan records before asking Hu to repeat information or making a new recommendation.
- Preserve Hu's explicit decision: **Production project, staff-only final testing first, public storefront only after issues are resolved and integrations tested**. Do not silently substitute a separate staging project.
- Distinguish decisions, proposed configuration, verified state, and completed actions. Never describe an uncreated app as deployed.
- Do not incur charges or perform cloud/database/DNS/provider changes without the relevant explicit authorization.
- When blocked, investigate practical alternatives and report the smallest decision needed; do not simply defer without analysis.
