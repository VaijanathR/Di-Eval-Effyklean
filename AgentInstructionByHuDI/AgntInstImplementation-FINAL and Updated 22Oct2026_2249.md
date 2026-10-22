# EffyKlean — Full BUILD Implementation Mandate and Mandatory Completion Audit

**Authority:** HU+DI  
**Scope:** All 245 records currently classified BUILD in the 22 October 2026 reconciled 597-row disposition register  
**Priority:** Complete all safely implementable, authorized work. No fabricated completion, silent omissions, or unauthorized decisions.

## 1. FIRST MANDATE — READ THE AUTHORITATIVE RECORDS

Before changing anything, read and apply the following public records in full, including relevant linked source records and corrections:

1. Implementation summary: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/IMPLEMENTATION_SUmmary_22Oct26_1250.md
2. Reconciled 597-row register: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv
3. Consolidated implementation plan and task-specific DoDs: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/ImplementationPlanOCT22-26-2026.md
4. HU+DI disposition decision log: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/HUDI_DISPOSITION_DECISIONS_2026-10-22.md
5. Ten-record HU+DI reconciliation: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/INVESTIGATE_10_HU_DI_RECONCILIATION_2026-10-22.md
6. Mandatory audit requirement: https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md
7. Frozen SPEC v0.8, approved architecture, ADRs, authorization gate, canonical 122-capability decision master, original decision ledger, applicable Delta implementation plan/status register, and relevant later HU clarifications.
8. Relevant project logs, README, CLAUDE.md, existing tests, migrations, and current implementation instructions.

The SSD audit requirement is mandatory from the beginning of work through the final report. Re-read it before issuing the final report and verify compliance.

The public repository is a decision/continuity mirror. Do not assume it is identical to the private application repository or current working tree.

## 2. IMPLEMENT ALL 245 BUILD RECORDS

The assignment is to implement the complete set of 245 BUILD records, not merely prepare another plan, perform an audit, implement a convenient subset, or report recommendations.

Use the reconciled CSV as the row-level scope inventory and its **individual DoD and validation-evidence method for every record** as the acceptance baseline. Use the consolidated plan to resolve task dependencies and related implementation work.

For every BUILD record:

- Preserve its original record ID, source wording, scope, and traceability.
- Read its own DoD and applicable HU decisions before implementation.
- Identify the related implementation-plan task(s), dependencies, existing code, current evidence, relevant paths, and required validation.
- Determine what is genuinely implemented already and what remains; do not rebuild completed features unnecessarily.
- Implement the missing authorized behavior and meet the original DoD.
- Validate the actual acceptance outcomes and record evidence against that specific record.
- Keep overlapping or composite records separately traceable. Do not merge IDs, silently lose subrequirements, or count one implementation as proof of unrelated criteria without evidence.
- Reconcile all 245 records at completion, including records already satisfied by existing implementation.

**A BUILD classification establishes scope; it does not override a frozen rule, authorize an external action, or resolve an outstanding business decision.** Hu has authorized this full implementation assignment. Do not seek repetitive batch approvals for ordinary, clearly specified work within this mandate. Continue in dependency-aware batches, but stop for HU+DI decisions wherever the rules below require them.

## 3. NO FAKE COMPLETION — THE DoD IS THE ACCEPTANCE CONTRACT

The DoD for each individual record is mandatory. Do not weaken, replace, reinterpret away, or omit any criterion because it is difficult, expensive, inconvenient, or not currently tested.

For each criterion, determine whether it is met and collect evidence that demonstrates the intended behavior.

A record must not be marked complete merely because:

- Code or a model exists.
- A UI element is present.
- A test was added, collected, or passed without testing the claimed behavior.
- A mock, stub, fixture, hardcoded value, or simulated provider response works.
- An earlier agent claimed completion.
- A command was attempted but failed or was never executed.
- Documentation describes behavior that has not been implemented.
- One part of a composite requirement works while other parts remain missing.
- A test passes only after an assertion, validation, permission check, or meaningful coverage was weakened or removed.

Do not invent test output, execution history, file contents, line numbers, provider results, screenshots, or validation evidence. Never describe an inference as an observation or historical evidence as a fresh test run.

Distinguish direct validation performed during this assignment from applicable prior evidence, another agent's unverified claims, and assumptions. State the limits of each item of evidence.

**No adequate evidence means no DONE (verified) status.**

## 4. MANDATORY ITEM-BY-ITEM STATUS LEDGER

Maintain an auditable ledger covering every one of the 245 BUILD records and every associated DoD criterion. Preserve the source ID and enough original wording to trace the result to the register.

Use exactly one primary completion status per record:

- **DONE (verified):** All applicable DoD criteria are met and supported by adequate evidence.
- **PARTIAL:** Meaningful work is complete, but one or more DoD criteria or required validations remain incomplete.
- **NOT DONE:** Required work remains incomplete and no justified, approved deferral applies.
- **DEFERRED:** Work is paused for a specific, evidenced blocker, dependency, safety boundary, authorization requirement, or HU+DI decision.

For each PARTIAL, NOT DONE, or DEFERRED record, additionally identify the reason category, including **BLOCKED**, **DECISION REQUIRED**, **VALIDATION PENDING**, or **DEPENDENCY NOT MET**, where applicable. These are explanatory categories, not substitutes for the mandatory primary status.

For every DONE record, report:

1. Original record ID and requirement.
2. Exact DoD criteria and outcome against each criterion.
3. Relevant implementation paths and precise line references where available.
4. Tests or other validations actually executed, including commands, exit codes, and meaningful results.
5. The behavior each test establishes and any material behavior it does not establish.
6. Environment and evidence type: local, PostgreSQL-backed, mocked, sandbox, browser-observed, or other applicable context.
7. Any residual limitations or separate acceptance gates.

Do not hide partial acceptance criteria behind an overall passing test count.

## 5. BLOCKED, DEFERRED, AND INCOMPLETE WORK — EXPLAIN AND CONTINUE

For every record that is not DONE (verified), state:

- The exact unmet DoD criterion or remaining work.
- Why it remains incomplete.
- The evidence supporting the claimed blocker.
- The exact checks, commands, tests, investigations, or safe remediation attempts performed and their actual results.
- Whether the blocker is genuinely external or authorization-dependent, or instead reflects avoidable uncertainty, incomplete investigation, missing validation, or work not yet done.
- Whether it could have been completed safely with available tools, information, permissions, and dependencies.
- The specific next action, prerequisite, or decision required, and who must provide it.

Do not use “time,” “complexity,” “large scope,” “tool unavailable,” or “dependency missing” as an unsupported blanket excuse. Verify tool availability and dependencies before claiming they are unavailable.

If one record is blocked, **park only that affected record and continue all independent, authorized work**. Do not stop the entire 245-record assignment because a subset requires a decision.

Do not silently move BUILD records to LATER or EXCLUDE. Do not treat missing evidence as evidence of exclusion. Do not hide incomplete work in a later phase, omit it from totals, or change its disposition to improve the completion percentage.

Where a genuine business or architecture decision is required, provide the precise conflict, source evidence, viable options, risks, and a recommended resolution for HU+DI. Do not implement the unresolved behavior by guessing.

## 6. FROZEN ARCHITECTURE AND BUSINESS RULES

Preserve the approved EffyKlean architecture and authoritative decisions:

- Modular-monolith Django/Python/PostgreSQL architecture.
- Python 3.14, Django 5.2 LTS, PostgreSQL 17, uv, pytest-django, Ruff, and GitHub Actions.
- No SQLite substitution.
- DigitalOcean App Platform with Managed PostgreSQL remains preferred; AWS is excluded. Hosting, paid resources, and deployment have separate authorization boundaries.
- **NO PAYMENT → NO DISPATCH.** No COD and no partial payment on delivery. Do not reintroduce COD or a Razorpay fallback.
- Zoho remains the owner of the applicable inventory, GST/tax, invoicing, and related provider-managed functions as recorded in authoritative decisions.
- Treat Zoho Payments sandbox as working and Zoho Inventory–Shiprocket sandbox integration as completed/known according to Hu's recorded reports. Do not repeat completed setup unnecessarily. Do not misrepresent those facts as proof of complete EffyKlean application lifecycle or production readiness.
- Preserve the existing Zoho-managed Shiprocket workflow. Do not invent shipment states, cancellation cutoffs, customer promises, retry rules, or staff permissions where an authoritative decision is missing.
- Preserve approved price, GST, order, customer-data, access-control, retention, audit, and consent rules. Apply the MF-089 operational privacy/retention baseline and MF-105 sign-in-assistance/data-export safeguards according to their recorded DoDs and decisions.
- Keep optional analytics/marketing tracking disabled until the recorded consent conditions permit it.
- Preserve the HU-approved homepage-link rearrangement and other identified pre-existing approved changes.
- Never expose secrets or place credentials, tokens, private logs, or sensitive customer data in Git, reports, tests, or generated artifacts.

Do not rely on an old agent report or historical test count as a current repository fact. Verify the relevant state before acting.

## 7. STOP → REPORT → HU+DI DECIDE

Stop changes to the affected record and report the evidence when any of the following occurs:

- A genuine conflict with frozen SPEC, architecture, an ADR, or an authoritative HU decision.
- A new business rule or materially ambiguous customer-facing behavior is required.
- Material security, privacy, financial, tax, authorization, or data-integrity risk is discovered.
- The action requires separate authorization, including production/provider writes, external communications, paid-resource creation, DNS/cutover, deployment, or another restricted external change.
- A proposed migration, permission change, state transition, deletion, or recovery operation risks existing data or unrelated work and lacks the necessary authorization.

Do not independently decide to defer the entire project or abandon the affected requirement. Record the blocker, request the necessary HU+DI decision, and continue independent authorized work.

No production deployment, live payment operation, production/provider write, DNS/cutover, paid provisioning, external communication, destructive data operation, Git push, commit, history rewrite, reset, discard, or broad staging is authorized merely by this instruction. Existing explicit authorizations apply only within their documented boundaries. Ask before an action that needs separate authorization.

## 8. REPOSITORY SAFETY AND CHANGE CONTROL

Before implementation:

1. Establish the actual application repository and working directory.
2. Record branch, HEAD commit, remote relationship, and full Git status.
3. Capture staged, unstaged, and untracked paths and relevant diffs.
4. Identify pre-existing and HU-approved changes; explicitly protect them.
5. Inspect migrations, model relationships, local environment, and current test configuration before selecting changes.

Do not assume the public decision mirror is the application repo. Do not overwrite, discard, stage, or conflate unrelated existing changes.

Throughout the task:

- Use explicit paths; never use `git add -A`.
- Do not stage, commit, push, reset, stash, clean, rewrite history, or discard work without explicit authorization.
- Do not add commit co-author trailers.
- Do not run destructive cleanup or delete provider/test records without explicit authorization.
- Keep test records clearly identified by unique TESTCODE/correlation marker, with documented and reviewed cleanup.
- Do not run tests against a production or shared provider/database target inadvertently.
- Keep `.claude` session logs and other private working records out of Git.
- At completion, reconcile the actual final Git state and every changed/untracked path. Report exactly what changed and whether any repository mutation occurred.

If the starting tree differs from historical reports, record the real state and preserve it; do not manufacture a clean baseline to match an old report.

## 9. TESTING AND VALIDATION

Choose validation proportional to risk and the affected DoD. Do not automatically rerun an expensive full suite after every narrow fix, but run the required focused tests and the meaningful integration/full-suite gates at appropriate milestones.

Where applicable, validate:

- DoD-specific unit and regression behavior.
- PostgreSQL-backed behavior and migrations against the approved environment.
- Django system checks, security checks, Ruff/lint/format, and relevant static validation.
- Permissions, audit events, failure paths, retries, idempotency, replay, concurrency, and data integrity.
- Actual browser/UI behavior and desktop/mobile parity where required.
- Provider sandbox behavior only where access and authorization exist.
- End-to-end and cross-system behavior where the DoD requires it and the environment safely supports it.

Report the exact command, target commit/state, exit code, actual pass/fail/skip counts, and duration where available. Explain failures and skipped tests. Do not report an unavailable or unexecuted test as passed.

Never weaken or delete a test simply to make the suite green. If a test change is genuinely necessary, explain the old behavior, the change, the reason, and how the original protection remains covered.

Do not claim sandbox, provider, end-to-end, security, browser, or production acceptance based solely on mocked or structural tests.

## 10. MANDATORY SHORTCUT AND MISLEADING-CLAIM AUDIT

Inspect modified code and relevant surrounding code for:

- TODO, FIXME, XXX, HACK, NotImplemented, bare `pass`, empty functions, and placeholders.
- Stubs, mocks, fakes, fixtures, dummy/sample values, hardcoded defaults, temporary workarounds, and fake integrations.
- Swallowed exceptions, overly broad exception handlers, ignored return values, silent failure paths, bypasses, and relaxed validation.
- Added, removed, skipped, disabled, weakened, or rewritten tests and assertions.
- Unjustified permission changes, security assumptions, state transitions, fallbacks, or business defaults.
- Claims that work is out of scope, a later phase, or complete despite unmet acceptance criteria.

Inspect matches; a keyword search alone is insufficient. Distinguish legitimate test doubles from production shortcuts. Report pre-existing findings separately from those introduced or modified by this assignment. Explain each material finding and whether it leaves a DoD gap.

A placeholder or stub may be acceptable only where the applicable DoD explicitly allows it; it must be labelled honestly and must not be represented as working functionality.

## 11. REQUIRED FINAL DOCUMENTATION

At the appropriate safe, authorized completion checkpoint, reconcile the current state in the required project records, including `PROJECT_LOG.md`, `CLAUDE.md`, README, and the applicable status register. Preserve historical entries rather than silently rewriting history. Keep the private session log out of Git.

Do not push these changes or modify the public repository unless separately authorized. Report any document that could not be updated, why, and the exact remaining action.

## 12. REQUIRED FINAL REPORT — NO EXCEPTIONS

Do not issue a completion message until the implementation ledger, repository state, tests, shortcut audit, and this mandate have been reconciled.

The final report must contain:

### A. Executive status
- Total BUILD records: 245.
- Counts of DONE (verified), PARTIAL, NOT DONE, and DEFERRED.
- Number of DoD criteria met, partially met, not met, and not verified.
- Clear statement that completion is claimed only for items whose DoDs are adequately evidenced.

### B. Complete 245-record reconciliation
For every original BUILD ID, provide:
- Original ID and requirement.
- Exact DoD or traceable criterion references.
- Primary status and reason category where relevant.
- Implemented behavior and changed file paths/line references.
- Actual validation evidence and results.
- Unmet criteria, limitations, dependencies, and next action where incomplete.

No IDs may be omitted. No totals may be inferred from a subset. Include a machine-readable ledger in the application workspace if appropriate and authorized; the human-readable report must still make the item-level outcomes auditable.

### C. Test and validation evidence
- Exact commands, target commit/state, exit codes, meaningful output, pass/fail/skip counts, and duration where available.
- Tests not run, failed, blocked, or skipped, with reasons.
- Actual environment/provider context and limits of the evidence.
- Regression and integration results, clearly separated from mocks or static checks.

### D. Incomplete-item investigation
For every PARTIAL, NOT DONE, or DEFERRED item, provide the evidence-backed explanation and precise next step required by Section 5. Identify avoidable incompletion honestly.

### E. Shortcut and integrity findings
List relevant stubs, mocks, placeholders, TODOs, hardcoded values, swallowed errors, workarounds, weakened/removed tests, and other bypasses. State whether pre-existing or introduced and whether each affects acceptance.

### F. Security, architecture, and business-rule audit
Report all material deviations, risks, conflicts, unauthorized actions, or discovered inconsistencies. Confirm what was checked and what could not be verified. Do not claim a clean audit without evidence.

### G. Repository and change reconciliation
Report repository, branch, starting and ending HEAD, Git status, changed/untracked path manifest, migration/config/dependency changes, and whether anything was staged, committed, pushed, discarded, or externally modified. Identify the authorization for any action that occurred.

### H. Completion-claim audit
Disclose any earlier message or status that implied completion before it was justified. Explain what was actually complete at that point and what remained. Do not conceal premature claims behind later test results.

### I. Final self-audit
Re-read `AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md` and this entire instruction. Provide a criterion-by-criterion compliance checklist with evidence. Explain every unmet instruction.

Do not call the overall assignment complete while any authorized, independently actionable work remains. If genuine blockers remain, report the assignment as incomplete, explain them, and continue all remaining safe, authorized work before finalizing.

## 13. FINAL PRINCIPLE

**Do the work, satisfy each record's actual DoD, validate the result, and prove the claim. Never optimize for a completion percentage or a reassuring report. Never fabricate, conceal, silently drop, or falsely mark work complete.**

All 245 BUILD records must remain traceable from source ID to implementation, DoD, validation, and final outcome. An explanation is not implementation. An attempted command is not a successful validation. A passing test is not proof of behavior it does not exercise. A blocked item is not complete.

Follow HU+DI governance throughout. Where an item genuinely requires a new decision or separate authorization, stop that item, report the evidence, and continue the remaining authorized work.
