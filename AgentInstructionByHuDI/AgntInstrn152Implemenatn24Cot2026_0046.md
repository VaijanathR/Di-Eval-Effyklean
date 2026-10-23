# EffyKlean — Implementation Mandate for the 152 Reconciled BUILD Items

## 1. Mission and exact scope
Implement and verify all 152 authorized BUILD records: the 141 BUILD IDs in the 245-item ledger plus MF-070, MF-071, MF-074, MF-078, MF-092, MF-107, MF-109, MF-114, MA-ORD-068, MA-DSC-023 and MA-SET-061 from the 597-row register. This 152-item scope supersedes the older 245-record mandate's scope count; use that mandate for standards, not to expand this assignment. Exclude Implemented, LATER, EXCLUDE and INVESTIGATE records unless an authoritative correction explicitly places one of these 152 IDs in scope. Do not change dispositions to improve totals.

## 2. First mandate — read the authoritative records
Before changing anything, read and apply the following in full, including relevant linked source records, corrections and later HU clarifications:
- [Full implementation mandate](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/AgntInstImplementation-FINAL%20and%20Updated%2022Oct2026_2249.md).
- [Mandatory SSD completion-audit requirement](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md). It applies from the beginning; reread before final reporting.
- [597-row disposition register](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv), [245-item BUILD ledger](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/BUILD245_LEDGER_2026-10-22.csv), reconciled decision ledger, decision reconciliation, recovered HU responses, genuine unresolved-decision shortlist, current 597 status reconciliation, disposition corrections, HU-response reconciliation, [implementation plan and item DoDs](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/ImplementationPlanOCT22-26-2026.md), and [implementation summary](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/IMPLEMENTATION_SUmmary_22Oct26_1250.md).
- Also read the HU+DI disposition decision log, INVESTIGATE-10 reconciliation, frozen SPEC v0.8, approved architecture, ADRs, authorization gate, canonical 122-capability decision master, original decision ledger, applicable Delta plan/status register, relevant project logs, README, CLAUDE.md, later HU clarifications, application code, migrations, dependencies and tests. Locate and read authoritative copies. The public repository is a continuity mirror and may differ from the private application repository/current worktree.
- The older BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md is superseded; do not use it as a question queue.

## 3. Record-by-record implementation
Use the reconciled 597 register for dispositions and the 245 ledger plus the 11 additional IDs above for this 152-record scope. For every record preserve original ID, wording, scope and traceability. Read its individual DoD, HU decision/response, plan mapping, dependencies, existing code and evidence before changes. Identify genuinely implemented work and avoid needless rebuilds; implement all missing authorized behavior.

Keep overlapping/composite records separately traceable. Map each DoD criterion to implementation and evidence; do not merge IDs, omit subrequirements or treat one feature/test as proof of unrelated criteria. An answered HU decision does not prove implementation, testing, provider configuration, legal compliance or release readiness. Do not ask Hu to repeat recorded answers or reopen settled decisions merely because validation remains pending.

## 4. Execution, frozen rules and authorization
Complete all safe, authorized, independently actionable work; do not substitute another plan, broad reassessment, recommendations or a convenient subset for implementation. A blocker on one item must not stop independent work. Resolve routine technical details within approved constraints without unnecessary questions.

Preserve frozen specifications, architecture, ADRs, security controls, integrations and approved business decisions:
- Modular-monolith Django/Python/PostgreSQL; Python 3.14, Django 5.2 LTS, PostgreSQL 17, uv, pytest-django, Ruff and GitHub Actions. No SQLite substitution.
- DigitalOcean App Platform with Managed PostgreSQL preferred; AWS excluded. Hosting, deployment and paid resources retain separate authorization boundaries.
- **NO PAYMENT → NO DISPATCH.** No COD, no partial payment on delivery and no Razorpay fallback.
- Zoho owns the recorded inventory, GST/tax, invoicing and related provider-managed workflows. Preserve the existing Zoho-managed Shiprocket workflow.
- Treat Zoho Payments sandbox as working and Zoho Inventory–Shiprocket sandbox integration as completed/known per Hu's recorded reports. Do not repeat completed setup unnecessarily or treat sandbox evidence as production readiness or proof of the full application lifecycle.
- Preserve recorded pricing, GST, order, stock, shipment, refund, customer-data, access-control, audit, retention and consent rules. Apply MF-089 privacy/retention requirements and MF-105 sign-in-assistance/data-export safeguards according to their DoDs and decisions.
- Keep optional analytics/marketing tracking disabled until recorded consent conditions permit it. Preserve the HU-approved homepage-link rearrangement and other approved existing changes.
- Do not invent shipment states, cancellation cutoffs, retry rules, customer promises, permissions, financial/tax behavior, defaults or data fallbacks where an authoritative decision is missing.

**STOP → REPORT → HU+DI DECIDE** only for a genuine new business decision, frozen-rule conflict, material security/privacy/financial/tax/data-integrity risk or missing authorization. State evidence, conflict, options/risks and exact decision/action needed. Park only the affected item and continue independent work.

Without separate required authorization, do not deploy; perform live/production-provider writes; send external communications; create paid resources; change DNS/cut over; perform destructive data/recovery actions; commit, push, rewrite history, reset, discard or broadly stage repository changes; or perform other restricted external actions. Use explicit Git paths; never use git add -A. No commit co-author trailers. Preserve pre-existing/user-approved changes. Keep credentials, tokens, secrets, customer-sensitive data and private agent/session logs out of Git and reports. This mandate does not grant permissions beyond these boundaries.

## 5. Evidence standard — no false DONE
Each record's DoD is its acceptance contract. Never weaken, reinterpret away or omit criteria because they are difficult, costly, inconvenient or untested. A record is not DONE merely because code/model/UI exists; a test was added/collected/passed without exercising the claimed behavior; a mock, stub, fixture, hardcoded value or simulated provider response works; an earlier agent claimed completion; a command was attempted, failed or was not run; documentation describes unimplemented behavior; a composite requirement is only partly met; or a test passes after a meaningful assertion, validation, permission check or coverage was weakened/removed.

Never invent command output, test history, file content, line numbers, provider results, screenshots or validation evidence. Distinguish direct evidence freshly executed/observed during this task, applicable prior evidence for unchanged code/configuration, historical/other-agent evidence not independently checked, and inference/assumption/unverified behavior. Label mocks, stubs, sandbox checks and provider simulations honestly; state what each test establishes and does not establish. **No adequate evidence means no DONE (verified).**

## 6. Mandatory status ledger for all 152
Assign exactly one primary status per ID:
- **DONE (verified):** all applicable DoD criteria are met and adequately evidenced.
- **PARTIAL:** meaningful work exists but one or more criteria/validations remain incomplete.
- **NOT DONE:** required work remains unmet without a justified, approved deferral.
- **DEFERRED:** paused for a specific evidenced blocker, dependency, safety boundary, authorization requirement or HU+DI decision.

For every record include original ID/requirement, traceable DoD criteria and criterion-level outcome, implementation paths and precise line references where available, actual validation/command/exit code/result, evidence/environment type, limitations and next action. For each non-DONE record state the exact unmet criterion, work attempted, actual evidence/results, why incomplete, whether the cause is genuine/external or avoidable/investigation/validation still outstanding, whether safe completion was possible, and next action/owner. Add a reason category where applicable: BLOCKED, DECISION REQUIRED, VALIDATION PENDING or DEPENDENCY NOT MET. These categories do not replace the primary status. No convenience deferrals, hidden omissions or unsupported blocker claims.

## 7. Mandatory SSD shortcut, integrity and timeline audit
Inspect changed files and relevant surrounding code/tests; searches are only a starting point. Check:
- TODO/FIXME/XXX/HACK/NotImplemented, bare pass, empty functions and placeholders.
- Mocks/stubs/fakes/fixtures, hardcoded/sample/dummy/fabricated values, fallbacks, skips/xfails, disabled checks and temporary workarounds.
- Swallowed exceptions, broad handlers, ignored return values/failures, bypasses, relaxed validation and silent-failure paths.
- Tests/assertions added, removed, skipped, disabled, weakened or rewritten; coverage lost; false positives, untested branches, weak assertions and mocks masking real behavior.
- New business defaults, permissions, state transitions, security assumptions, data fallbacks, migrations/data-integrity risks; financial/payment/tax/order/dispatch/stock/shipment/refund/customer-data behavior; provider calls, external writes, emails, shipments and production actions.
- Items labelled out of scope/later phase or otherwise deferred while the original requirement remains actionable.

For each relevant finding give exact path/line or search evidence, impact on acceptance, and whether pre-existing or introduced. Explain justified test changes and how original protections remain covered. Passing tests do not make a shortcut harmless.

Audit the available task timeline, including intermediate messages/status claims. List every completion-like claim and what was actually complete, unfinished, deferred or unverified at that time. Admit premature claims plainly; later work does not retroactively justify earlier claims.

## 8. Repository, tools, blockers and final-state validation
Reconcile the actual application repository, not just the public continuity mirror: starting/ending repository, branch, HEAD, remote relationship, staged/unstaged/untracked paths, relevant full diffs, recent commits, stashes/cherry-picks/resets/merges/restores/recovery where relevant, and application code/tests/migrations/configuration/dependency/documentation changes. Reconcile file lists/counts against Git. State whether anything was staged, committed, pushed, discarded or otherwise altered and the authorization for each. Preserve unrelated/approved work; investigate discrepancies rather than selecting the most favorable report.

For claims that a browser, command, credential, permission, service, dependency or tool is unavailable, provide the exact check and actual output plus alternatives investigated. Distinguish unavailable/unauthorized, available but not investigated, available but not used, configuration failure, and not needed for the evidence level. Do not treat the first failed attempt as proof of unavailability; verify dependencies before claiming they are missing.

Run targeted tests after narrow changes and broader suites/linters at meaningful integration gates. Avoid redundant expensive reruns after genuinely narrow fixes, but validate the final relevant code state. Report exact commands, exit codes, actual output, pass/fail/skip counts, warnings, retries, exclusions, failures and duration where available; tests/linters not run and why; environment limits (database/browser/provider/CI); and whether CI actually ran. Identify reused evidence and why still valid. Disclose code changed after last test and assess/rerun relevant checks. Never infer CI success from local results or claim all tests pass when required checks were not run or failures remain.

## 9. Deliverables and continuity
Save locally in the application repository using the actual creation timestamp in Asia/Kolkata (IST, UTC+05:30), 24-hour format. Never use placeholder timestamps or overwrite timestamped artifacts:
- docs/ImplementationPlan/AgentReports/BUILD152_IMPLEMENTATION_REPORT_YYYY-MM-DD_HHMMSS.md
- docs/ImplementationPlan/AgentReports/BUILD152_ITEM_LEDGER_YYYY-MM-DD_HHMMSS.csv

Update applicable PROJECT_LOG.md, CLAUDE.md, README and relevant status register using established filenames; preserve history. Keep private session logs out of Git. Do not push these changes to the public repository without separate authorization. Report any continuity file not updated, why, and exact remaining action.

## 10. Mandatory final report
The saved report and final chat report must agree. Include:
1. Overall status and totals for all 152 across DONE (verified), PARTIAL, NOT DONE and DEFERRED; plus criterion totals met, partial, unmet and unverified. Claim completion only if every authorized actionable item is DONE (verified).
2. Complete item ledger: every original ID/requirement, traceable DoDs, criterion outcomes, paths/lines, actual validation/evidence type, limitations and next actions.
3. Completion-claim timeline and candid disclosure of premature/inaccurate claims.
4. Shortcut/integrity findings, test changes and impact, and security/architecture/business-rule/data-integrity audit.
5. Exact commands, exit codes, outputs/results, failures, skips, warnings, retries, exclusions, unrun checks and environment/CI/provider limits.
6. Repository reconciliation: starting/ending branch and HEAD, remote relationship, worktree/staged/unstaged/untracked state, relevant diffs, recovery operations and authorization for mutations.
7. Every unfinished item with evidence, reason category, whether safely actionable, and next action/owner; assumptions and unverified behavior.
8. Highest risks/discrepancies, exact deliverable paths, continuity updates, and self-audit against this instruction, the full implementation mandate and every section of the SSD audit requirement.

Do not report only aggregate counts, bury serious failures, omit awkward findings or describe self-reported evidence as independently verified.

## 11. Skeptical final self-challenge
Before finalizing, reread the full implementation mandate and SSD audit requirement. Compare every in-scope ID and criterion against the ledger; search for omissions/contradictions; challenge every DONE claim; test for false positives, untested branches, weak assertions, mocks and code changed after tests; reconcile changed files/test counts against Git and command outputs; check whether blocked work was independently actionable; verify completion timeline and continuity updates.

Perform safe, authorized corrective work before reporting. Explain every unmet instruction and remaining gap. Finish all independent authorized work before finalizing; do not issue routine progress updates during the long task. Never claim completion while authorized, independently actionable work remains. A blocked item is not complete; an attempted command is not validation; a passing test proves only what it actually exercises. Honest PARTIAL/NOT DONE is better than an unsupported reassuring claim.

**Governing principle: do the work, satisfy each record's actual DoD, validate the result and prove the claim. Never fabricate, conceal, silently drop or falsely mark work complete.**