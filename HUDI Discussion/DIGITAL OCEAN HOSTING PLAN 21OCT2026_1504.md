# DIGITAL OCEAN HOSTING PLAN 21OCT2026_1504

**Project:** EffyKlean.in  
**Prepared by:** HU+DI  
**Date:** 21 October 2026  
**Purpose:** Consolidated hosting plan, shipment-workflow investigation plan, recommendations, and Definitions of Done accepted by Hu.

## 1. Purpose and governing position

Hu confirms that the Definitions of Done listed in this plan are correct and should be documented alongside Di's recommendations and plan. This confirms acceptance of the completion criteria; it does **not** mean the work described below has already been performed or verified.

The immediate next step is a fresh, read-only repository checkpoint. No implementation, provider writes, cloud-resource creation, deployment, DNS change, production action, or launch is authorized by this document alone. Each remains subject to the existing authorization gates and any explicit later HU+DI decision.

## 2. Existing architecture and constraints

- Target website: effyklean.in; reference storefront: effyklean.com.
- Local repository path: /mnt/d/effykleanproject.
- Public discussion and governance records: https://github.com/VaijanathR/Di-Eval-Effyklean
- Private implementation repository: https://github.com/VaijanathR/EffyKleanProject
- Frozen SPEC v0.8: commit 8601602, containing 139 acceptance criteria.
- Architecture baseline: commit a45a033.
- ADR baseline: commit 4fe5767.
- Foundation Authorization Gate: commit 94df6e3.
- Claude governance sync: commit 93222e3.

The approved architecture is a Django/Python/PostgreSQL modular monolith. DigitalOcean App Platform with Managed PostgreSQL is the preferred hosting direction. Droplets require a documented justification; AWS is excluded; GoDaddy is the fallback. The intended stack is Python 3.14, Django 5.2 LTS, PostgreSQL 17, uv, pytest-django, Ruff, and GitHub Actions. SQLite is not permitted.

Relevant frozen decisions include:
- **AD-10:** NO PAYMENT → NO DISPATCH.
- **AD-11:** no stale catalogue.
- **AD-16:** secret hygiene.

The DigitalOcean Managed PostgreSQL resource effyklean-db in BLR1, PostgreSQL 17, was previously reported online with a 1 GB RAM / 10 GiB disk configuration. This is a historical checkpoint and must be rechecked before any deployment decision. Historical cost estimates were approximately USD 10/month for the app and USD 15.15/month for the database; reconfirm current pricing before committing to spend.

## 3. Recommended execution order

1. Establish a fresh, read-only repository checkpoint.
2. Verify the actual Zoho-managed shipment workflow using authorized read-only evidence.
3. Confirm the website-to-Zoho-to-Shiprocket integration boundary.
4. Preserve and verify payment, dispatch, cancellation, edit-cutoff, staff-hold, and handover rules.
5. Resolve the shipment state model against the frozen specification and architecture.
6. Select and document a safe Zoho-to-website synchronization method.
7. Define idempotency, ordering, reconciliation, and exception handling.
8. Only after explicit HU authorization, implement the agreed focused changes and tests.
9. Separately pass the DigitalOcean hosting readiness gate before creating or changing hosting resources.
10. Run the controlled sandbox end-to-end gate, update continuity records, and request the next HU+DI decision.

Do not combine these gates into a single implied authorization.

## 4. Section 1 — Fresh read-only repository checkpoint

**Recommendation:** Begin here. Previous report details are historical, not proof of current state.

Inspect the current branch and HEAD, upstream relationship/divergence, modified and untracked file inventory, and the relevant source/specification files. Identify changes made during inspection and distinguish previously approved work from unexplained changes.

Historical agent checkpoint: branch main, HEAD 625e210, reported three commits ahead of origin, 89 modified files and 24 untracked files. The working tree reportedly changed during investigation. These figures must not be reused as current facts without a fresh check.

Preserve all work. Do not reset, clean, stash, or discard changes. Do not use git add -A. The previously HU-approved homepage link rearrangement in modules/storefront/site.py and tests/test_storefront_shell.py must be preserved and kept separate from unrelated work. Approval to make those edits is not approval to stage, commit, or push them.

### Definition of Done — Section 1

- [ ] Current branch, HEAD SHA, upstream and divergence are recorded from fresh command output.
- [ ] Modified and untracked files are inventoried without changing them.
- [ ] Relevant current source, tests, specification, architecture, ADR and hosting-plan files are identified.
- [ ] Previously HU-approved changes are distinguished from other changes.
- [ ] Any changes occurring during inspection are reported.
- [ ] No working-tree changes are discarded, staged, committed or pushed.
- [ ] The checkpoint clearly distinguishes verified current facts from historical reports and unknowns.

## 5. Section 2 — Verify the real Zoho-managed shipment workflow

The intended operational model is that Zoho owns shipment creation and its existing Shiprocket carrier workflow. The website must not create shipments directly with Shiprocket.

A previous report identified this suspected website path:
**request_shipment → SHIPMENT outbox → _run_shipment → _attempt_fulfilment → zoho.request_fulfilment**

The report stated that the real Zoho adapter raises ZohoNotSupportedError, while a stub can mask this by pretending to create a shipment. This is a reported finding that needs fresh source verification; do not treat it as a newly verified fact.

Hu has stated that Zoho Inventory sandbox is integrated with Shiprocket sandbox and that this integration should be treated as completed/known. Do not reopen provider setup or infer that the integration is broken solely because a prior sample or code path did not demonstrate the full lifecycle.

Use authorized read-only methods to inspect an existing sandbox Sales Order and its Zoho-created shipment/package details, carrier, tracking identifier, statuses and available timestamps. Do not create or alter provider records merely to obtain evidence unless Hu explicitly authorizes that write.

### Definition of Done — Section 2

- [ ] Current website shipment path is traced from request/outbox through the actual adapter, with source-file and line evidence.
- [ ] Real adapter behavior is distinguished from stub/mock behavior.
- [ ] An authorized read-only sandbox example demonstrates what Zoho exposes for an existing Sales Order and its shipment/package lifecycle, or the precise evidence limitation is documented.
- [ ] Available shipment IDs, carrier/tracking data, status fields and timestamps are recorded without inventing missing values.
- [ ] Existing Zoho Inventory–Shiprocket sandbox integration is treated as a known completed setup unless contrary evidence is found.
- [ ] No unauthorized provider writes, cleanup, or test-record deletion occurs.
- [ ] Findings and remaining unknowns are reported separately.

## 6. Section 3 — Preserve the integration boundary

**Recommendation:** Keep the responsibility boundary explicit:

1. The website receives the order and enforces the existing payment and order gates.
2. The website submits the required sales-order information to Zoho.
3. Zoho owns shipment creation and its existing Shiprocket carrier workflow.
4. Shipment, tracking and delivery updates flow from Shiprocket to Zoho and then to EffyKlean.in.
5. EffyKlean.in presents the approved customer-facing status and retains the internal evidence needed for operations and reconciliation.

Do not implement direct website-to-Shiprocket shipment creation. Do not assume that an unsupported Zoho operation works merely because a stub passes.

### Definition of Done — Section 3

- [ ] The actual integration path matches the Zoho-owned shipment model or deviations are reported.
- [ ] No website code independently creates a Shiprocket shipment.
- [ ] Real provider behavior is not represented as successful by a stub in the end-to-end evidence.
- [ ] Ownership of order submission, shipment creation, carrier execution, status synchronization and customer display is documented.
- [ ] Any proposed architecture/specification change is stopped and brought to HU+DI before implementation.

## 7. Section 4 — Order handover, payment and dispatch gates

Preserve the frozen AD-10 rule: **NO PAYMENT → NO DISPATCH**. The shipment workflow must also preserve the approved same-day rules, staff holds, cancellation and order-edit cutoffs, and the defined operational handover point.

The handover point must be stated precisely: which confirmed order state permits sending the sales order to Zoho, which state permits shipment processing, and what happens if an order is cancelled, edited, held, or otherwise becomes ineligible before handover. Do not invent new cutoffs or states; reconcile them with the frozen specification and existing decisions.

### Definition of Done — Section 4

- [ ] Payment-before-dispatch is traced and verified across the relevant code and tests.
- [ ] Same-day rules, staff holds, cancellation cutoff, edit cutoff and handover point are traced to approved requirements.
- [ ] Failure, retry and delayed-processing cases cannot bypass the payment gate.
- [ ] The website does not request or permit dispatch for an ineligible order.
- [ ] Any ambiguity in a frozen requirement is reported for HU+DI decision rather than silently resolved.
- [ ] Focused tests cover the relevant gates and failure paths.

## 8. Section 5 — Shipment states and customer-facing statuses

Resolve the implementation against the frozen specification, especially SPEC.md sections 15.4, 16.2, 15.5, 18.6, 18.9, 12.14 and 15.7, and the relevant architecture text. The following customer-facing status set is the existing stated requirement:

- Order Confirmed
- Processing
- Shipped
- Out for Delivery
- Delivered
- Delivery Unsuccessful

NDR, RTO and reattempt details are internal and should not be exposed as customer-facing statuses. Pickup and in-transit details are internal. Architecture wording around Shiprocket/retries may require reconciliation; specification sections that defer mechanics must not be silently expanded into new requirements.

Do not add an unapproved state, field, event log or database migration. If the specification and architecture genuinely conflict, STOP → REPORT → HU+DI DECIDE.

### Definition of Done — Section 5

- [ ] Each implemented state and transition maps to an approved specification requirement.
- [ ] Customer-visible statuses use only the approved set and wording.
- [ ] Internal carrier states remain internal unless HU+DI explicitly approves otherwise.
- [ ] State transitions, including terminal and unsuccessful outcomes, are documented with evidence.
- [ ] Architecture/specification conflicts and deferred mechanics are identified, not silently decided.
- [ ] No new field, state, event-log design or migration is introduced without authorization.

## 9. Section 6 — Zoho-to-website synchronization method

**Recommendation to evaluate, not yet an approved design decision:** polling may be the simplest first option, but select it only after checking which data the existing Zoho Inventory Sales Order GET and packages[] responses actually expose. Those responses may not contain all carrier status and event details needed by the website.

A 15-minute polling interval is a possible candidate, not an approved service-level or business-latency commitment. Assess required freshness, API limits, reliability, hosting/runtime implications and reconciliation behavior before choosing a frequency.

Consider a webhook only if Zoho Inventory webhook authentication, payload semantics, delivery/retry behavior and the relevant API capabilities are verified. A Zoho Payments webhook signature must not be treated as authenticating Zoho Inventory events.

### Definition of Done — Section 6

- [ ] The relevant Zoho read endpoints and actual response fields are verified from authoritative evidence or an authorized sandbox read.
- [ ] The data is sufficient to support the required website status transitions, or gaps are explicitly listed.
- [ ] Polling and webhook options are compared against freshness, reliability, rate limits, authentication and operational complexity.
- [ ] Any proposed interval, including 15 minutes, is explicitly identified as a proposal until HU+DI approves it.
- [ ] No webhook is trusted without verified Inventory-specific authentication and semantics.
- [ ] A recommended method, rationale, limitations and operational implications are presented for HU+DI decision.

## 10. Section 7 — Idempotency, ordering and exceptions

The design must tolerate duplicate, delayed and out-of-order updates. It must not move an order backwards through its approved lifecycle merely because an older event arrives later. Unknown events must be retained or made visible for review rather than silently discarded. Unmatched records must be visible for reconciliation. Carrier/tracking conflicts must be flagged. Timestamps must come from actual evidence; never invent them.

### Definition of Done — Section 7

- [ ] Duplicate events/observations do not create duplicate business effects.
- [ ] Delayed and out-of-order updates cannot incorrectly regress an order.
- [ ] Unknown events are retained or visibly surfaced for review.
- [ ] Unmatched provider records are visible and reconcilable.
- [ ] Conflicting carrier or tracking identifiers are flagged rather than silently overwritten.
- [ ] Missing timestamps remain missing/unknown; none are fabricated.
- [ ] Failure and reconciliation behavior is tested and documented.

## 11. Section 8 — Implementation and test gate

Implementation starts only after Hu explicitly authorizes the agreed scope. Use focused tests for the changed behavior, then perform a real sandbox end-to-end test with one or two controlled products. Stub-only tests are insufficient to prove the provider lifecycle. Run broader regression tests at a meaningful gate, not automatically after every narrow correction.

Every test record should use a unique TESTCODE/correlation marker and have a reviewed cleanup plan. Do not delete production/provider records or financial records without explicit authorization.

### Definition of Done — Section 8

- [ ] HU+DI has explicitly authorized the implementation scope before coding/delegation.
- [ ] Each agreed requirement is marked DONE (verified), PARTIAL, NOT DONE or DEFERRED with command output or file/line evidence.
- [ ] Focused tests cover changed behavior and relevant failure cases.
- [ ] A controlled sandbox end-to-end run proves the real Zoho-managed shipment path, not just a stub.
- [ ] Test records use unique TESTCODE/correlation markers and documented cleanup.
- [ ] No production/provider or financial records are deleted without explicit approval.
- [ ] Test results, known gaps, shortcuts/placeholders/TODOs, pass stubs, weakened tests, swallowed errors and out-of-scope claims are explicitly reported.
- [ ] Full regression is run at an agreed meaningful gate and not needlessly repeated after every narrow fix.

## 12. Section 9 — DigitalOcean hosting readiness and deployment gates

Hosting is a separate authorization track. Before creating an App Platform app or changing resources, resolve and verify the readiness questions, including:

- A distinct staging settings module, such as staging.py, with explicit staging-only safety controls.
- Buildpack detection and build route for the repository's pyproject.toml, uv.lock and .python-version; do not assume Python buildpack detection will work without a verified supported configuration.
- The app start command and health check.
- Database naming, role/least privilege, TLS and sslmode configuration.
- Email discard/sandbox behavior.
- Media storage choice (local storage versus DigitalOcean Spaces) and its implications.
- Explicit allowed hosts and CSRF origins, HTTPS, secure cookies, DEBUG=False, HSTS and other appropriate production-like safeguards.
- Access restrictions for staging; ALLOWED_HOSTS and noindex alone are not access control.
- No live provider endpoints or live credentials in staging.
- Secret handling and environment separation.
- Current hosting costs and resource limits.

A previously suggested start command was:

    gunicorn --worker-tmp-dir /dev/shm --bind 0.0.0.0:${PORT:-8080} --workers 2 --access-logfile - config.wsgi:application

A previously suggested health check was /healthz with GET/HEAD and a database SELECT 1. These are proposals to verify against the current code and platform, not proof that configuration exists or is ready. The production settings reportedly reject staging needs; confirm the current settings before deciding how to separate staging.

Required staged gates:
1. Readiness review.
2. Restricted hosted sandbox environment.
3. Sandbox end-to-end validation.
4. Reviewed, dependency-aware test-data cleanup.
5. Live integration review and one controlled live order, only after explicit authorization.
6. Public launch, separately authorized.

Do not run pytest against the DigitalOcean database. Do not create cloud resources, deploy, change DNS, make live provider writes, clean a database, or launch publicly without explicit authorization.

### Definition of Done — Section 9

- [ ] Hosting prerequisites and unresolved decisions are listed with evidence.
- [ ] Staging settings and runtime/build assumptions are verified against the current repository and supported platform behavior.
- [ ] Health endpoint and start command are tested or clearly marked unverified.
- [ ] Database TLS, least privilege, environment separation and secret handling are defined.
- [ ] Access restriction and safe email/media behavior are defined for staging.
- [ ] DEBUG is off and HTTPS/host/CSRF/cookie/security settings are explicitly reviewed before public exposure.
- [ ] Current costs and resource configuration are reconfirmed before spend/resource changes.
- [ ] Readiness, hosted sandbox, sandbox E2E, live integration and public launch remain separate gates.
- [ ] No cloud-resource creation, deployment, DNS change, live provider write, database cleanup or launch occurs without explicit authorization.

## 13. Section 10 — Project records and continuity

At the appropriate checkpoint, update PROJECT_LOG.md, CLAUDE.md, README and the status register so the current state, evidence, decisions, blockers and next authorized action agree. Keep the private Claude session log out of Git until the site is online, as previously directed.

Agent instructions should remain concise and task-focused. The completion audit must be strict: every plan/spec item must be reported as DONE (verified), PARTIAL, NOT DONE or DEFERRED, with command output or file/line evidence. The report must call out shortcuts, stubs/placeholders, TODOs, pass, test weakening, swallowed errors and out-of-scope claims. Stop for HU+DI decisions where frozen architecture/specification, risk or business ambiguity is encountered.

### Definition of Done — Section 10

- [ ] Required continuity records are updated consistently at the appropriate checkpoint.
- [ ] The private Claude session log remains out of Git until the stated condition is met.
- [ ] Completion audit includes every applicable plan/spec item and evidence for claimed completion.
- [ ] Shortcuts and quality risks are listed explicitly.
- [ ] Decisions, blockers, deferred work and next authorized action are clear.
- [ ] No authorization is inferred from documentation updates or an agent's recommendation.

## 14. Section 11 — Final HU+DI authorization gate

After the read-only checkpoint and evidence gathering, Di presents the findings and options. Hu and Di decide the unresolved business and architecture questions together. Only then may Hu explicitly authorize implementation or a specific hosting action.

Use **STOP → REPORT → HU+DI DECIDE** for conflicts with frozen architecture/specification, new decisions, risk, or business ambiguity. Do not delegate to a coding agent unless Hu explicitly authorizes delegation.

### Definition of Done — Section 11

- [ ] Read-only findings are presented with evidence and uncertainty clearly labelled.
- [ ] Unresolved business, architecture, operational and hosting decisions are listed.
- [ ] Each decision has a recommendation, alternatives where useful, and consequences.
- [ ] HU+DI explicitly decides the next implementation/hosting scope.
- [ ] Any coding-agent delegation is explicitly authorized by Hu.
- [ ] No implementation or hosting action is treated as authorized merely because this plan or its DoD is accepted.

## 15. Status vocabulary

Use these statuses in implementation and completion reports:

- **DONE (verified):** evidence demonstrates the requirement is met.
- **PARTIAL:** some work is complete, but the requirement is not fully demonstrated.
- **NOT DONE:** not implemented or not met.
- **BLOCKED:** cannot proceed until a named dependency, evidence item or decision is resolved.
- **DEFERRED:** deliberately postponed by an explicit decision.

Accepting the Definitions of Done means the criteria themselves are approved as the basis for review. It does not pre-mark any work item as DONE.

## 16. Immediate next action

Start with **Section 1 — Fresh read-only repository checkpoint**. Preserve the working tree and return the current branch/HEAD/upstream/divergence, modified and untracked inventory, relevant current files, and any concurrency changes. Do not implement, stage, commit, push, run provider writes, or change hosting resources as part of that checkpoint.

After reviewing the checkpoint, HU+DI will decide whether and how to proceed with read-only shipment verification and the subsequent gates.
