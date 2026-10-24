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

### HU+DI decision — dedicated application database user (24 October 2026)

- Hu approved creating a dedicated application database user rather than using the administrative `doadmin` account for routine app traffic.
- Proposed username: `effyklean_app`. This is a proposed name only; **the user has not yet been created**.
- Reuse the existing `effyklean-db` cluster and `defaultdb`; do not create a duplicate database.
- Before creating the user, inspect the DigitalOcean creation form and establish what privilege/access options it exposes. Grant only the access needed by the Django application; do not assume that creating a username alone establishes suitable permissions.
- Keep `doadmin` and `defaultdb` unchanged. Do not record the new user's password or any secret-bearing connection string in this public file.
- Hu accepts that the dedicated user can be changed or removed later if required, but only after updating the app's connection configuration and verifying that no dependency still uses that account.
- In the App Platform database-attachment form, the only listed choices observed were `defaultdb` and `doadmin`; clicking either option closed the dropdown without visibly populating the field. The cause is unknown. Do not assume the blank fields automatically select those defaults; resolve the UI/attachment behaviour before finalizing the app.
- This records a decision and plan, not a completed database change. No database user has been created and no database/app configuration has been changed as part of recording this decision.

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
- Current screen selection: `apps-s-1vcpu-0.5gb`, displayed at **$5.00/month** (512 MB RAM, 1 shared vCPU, 50 GB bandwidth); this is only the current selection, not a finalized resource or incurred charge.
- Autoscaling: Off; one container
- Project: EffyKlean / Production
- **Chosen app name: `effyklean-web`** (Hu confirmed this choice on 24 October 2026).

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

### Confirmed HU+DI decision: staff-only application mode

Hu approved an **application-level staff-only mode**, controlled by a deployment setting, as the access rule for initial final testing:

- Only authenticated and authorized staff may access the storefront during final testing.
- Ordinary visitors must not be able to browse the storefront or place orders during this phase.
- The restriction stays enabled until HU+DI explicitly approves public launch.
- Payment and fulfilment remain in sandbox/test mode during staff testing.
- Health checks must continue to work without exposing customer or business data.
- Prefer this approach over creating another service or changing DNS solely to restrict access.
- This is a confirmed policy decision, **not a claim that the feature is already implemented**. Before deployment, verify the existing Django architecture and implement/test the control in a compatible way. Do not interfere with the coding agent's active work; coordinate after its work reaches a safe point.

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
4. Implement and test the approved application-level staff-only mode before any staff-facing deployment; keep it enabled until explicit HU+DI public-launch approval.
5. Settle database connectivity, TLS verification, trusted sources, and least-privilege database access before connecting the app; create the HU+DI-approved dedicated user `effyklean_app` only after reviewing the creation form and required privileges, then resolve the App Platform dropdown behavior.
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


## 9. HU+DI decision — dedicated Django staging settings profile (24 October 2026)

**Decision: use `config.settings.staging` for hosted, staff-only final testing. Do not use `local.py` or weaken/change `production.py` to fit this testing phase.**

### Why this is the selected option

- The DigitalOcean resource belongs in the existing **EffyKlean / Production project**, but that project label does not require the Django `production` settings module or mean the site is publicly launched.
- `local.py` is for local development: it enables `DEBUG`, local provider stubs and local-host assumptions, so it is not suitable for the hosted DigitalOcean staff-testing environment.
- `production.py` is intentionally fail-closed for the live environment. As currently written, it requires production configuration such as S3-compatible media and non-console email, requires the Zoho credentials/tax configuration, and rejects Inventory sandbox mode and payment stubs. Those checks must not be weakened just to support staff testing.
- A dedicated `staging.py` expresses the approved intermediate phase explicitly and keeps the live-production safeguards separate.

### Required staging-profile boundaries

The new profile does **not yet exist** and this decision records policy, not completed implementation. When implemented and verified, it must:

- Keep `DEBUG=False`, require a strong secret key, use the hosted domain/CSRF configuration, HTTPS-aware proxy handling and secure cookies.
- Work only with the approved application-level staff-only access gate: authenticated, authorized staff may test; ordinary visitors must not browse or place orders. Keep this restriction enabled until explicit HU+DI approval for public launch. Health checks must remain usable without exposing business/customer data.
- Allow only the intended sandbox/test integrations. Do not permit real payments, live provider writes, live orders or real dispatch during staff testing. Preserve the Zoho-owned shipment workflow; do not add direct website-to-Shiprocket shipment creation.
- Fail closed against accidental local provider stubs, payment stubs or live-provider mode being enabled by mistake.
- Use the approved hosted PostgreSQL configuration and least-privilege application credentials; do not embed secrets in source or public records. Database identity/isolation and network/TLS prerequisites remain governed by the existing decisions and must be verified rather than assumed.
- Use an explicitly chosen safe email behaviour and persistent media-storage approach suitable for hosted testing; neither is settled merely by selecting this settings module.
- Preserve and verify the `/healthz` behaviour and deployment startup/build configuration.

### Immediate configuration consequence

The current DigitalOcean build failed at `collectstatic` because `DJANGO_SETTINGS_MODULE` was unset. Do **not** set it to `config.settings.production` or `config.settings.local` as a workaround. After `config/settings/staging.py` has been implemented and tested, configure `DJANGO_SETTINGS_MODULE=config.settings.staging` for the required build/run scope and retry deployment.

### Current status and authorization boundary

- The DigitalOcean app `effyklean-web` has since been created in the existing EffyKlean / Production project; the initial deployments failed with the Django settings-module/build error described above. This supersedes the earlier statements in sections 2 and 4 that no app had been created or finalized.
- No claim is made here that `staging.py`, the staff-only gate, or the remaining staging safeguards have been implemented or verified.
- This decision authorizes recording the settings-profile choice only. It does not by itself authorize editing application code, changing cloud configuration, deploying, changing DNS, enabling live integrations or launching publicly. Those actions remain subject to the applicable HU+DI authorization and safety gates.
