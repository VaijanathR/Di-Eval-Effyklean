# EffyKlean SSD — Agent Task Audit Requirement
**Status:** Mandatory governing instruction  
**Owner:** HU+DI  
**Effective:** 19 October 2026  
**Applies to:** Every EffyKlean implementation task, continuation, investigation, validation, handoff, and completion report.

## 0. FIRST MANDATE — READ, APPLY, AND VERIFY THIS REQUIREMENT

Before doing implementation work, read this entire document and apply it throughout the task. This is the first mandatory audit instruction, not optional end-of-task advice. Before presenting any final report, re-read this document, cross-check every requirement against the actual task and repository state, and take all safe, authorized actions needed to close gaps.

Do not optimize for a high completion percentage, a quick finish, a reassuring report, or the appearance of progress. Optimize for truthful status, complete authorized work, reliable evidence, and early disclosure of problems.

Do not claim completion while authorized, independently actionable work remains. Do not use a report, handoff, test count, or completion notification as a substitute for finishing work.

This requirement does not grant permission to perform an otherwise unauthorized, destructive, external, financial, production, or business-decision action. Preserve existing HU+DI governance: for a genuine frozen-specification/architecture conflict, new business decision, material security/data-integrity risk, or action requiring authorization, STOP → REPORT → HU+DI DECIDE. Park only the affected item and continue independent authorized work.

## 1. RECONSTRUCT THE ORIGINAL TASK — DO NOT AUDIT ONLY YOUR OWN CHECKLIST

Read the original task prompt, all referenced instructions and artifacts, applicable frozen specifications, architecture/ADRs, approved HU decisions, task inventories, and relevant follow-up corrections. Identify explicit and implied deliverables, constraints, prohibitions, required validations, and reporting obligations.

Create an item-by-item ledger covering every original task and acceptance criterion. Preserve original IDs and wording where available. Do not silently omit inconvenient, lengthy, difficult, or overlooked items. Do not replace the original task with a narrower checklist of work you chose to perform.

For each item, use exactly one primary status:
- **DONE (verified):** The requirement is met and direct evidence demonstrates the intended acceptance criterion.
- **PARTIAL:** Some work exists, but the requirement is incomplete, the result is not sufficiently verified, or material limitations remain.
- **NOT DONE:** The requirement remains unmet and no genuine approved reason justifies deferral.
- **DEFERRED:** Work is intentionally paused for a specific, evidenced blocker, dependency, safety boundary, or HU+DI decision.

A test passing is not sufficient by itself to mark a criterion DONE. An implementation attempt is not completion. Missing evidence means the item is not verified.

## 2. EVIDENCE FOR EVERY DONE CLAIM

For every DONE item, provide the exact acceptance criterion and evidence that proves it. Include, as applicable:
- Exact command executed, exit code, and actual output.
- Test name and the meaningful assertion or behavior exercised.
- File path and relevant line range showing the implementation.
- Browser or UI action actually performed and observed result.
- Provider/environment used and whether it was sandbox, stubbed, mocked, or live.
- Relevant Git diff or repository evidence.

Clearly distinguish:
1. Directly executed and observed by you in this task.
2. Existing evidence that remains applicable because the relevant code/configuration has not changed.
3. Evidence reported by another agent or historical report but not independently checked by you.
4. Inference, assumption, or unverified behavior.

Do not invent output, imply a command ran when it did not, or present a paraphrase as raw output. A test name, test count, code presence, mock response, screenshot file, or successful syntax check does not prove more than it actually exercises.

Mocks and stubs can be appropriate for local tests, but label their evidence honestly. Do not claim real-provider integration, browser behavior, end-to-end behavior, production readiness, security, or business acceptance from tests that do not exercise those claims.

## 3. HONEST COMPLETION CLAIMS AND TIMELINE AUDIT

Review the full task timeline, including your own intermediate messages, notifications, status summaries, and any completion message. List every point where you said or implied the task was complete or substantially complete. For each, state what was actually complete at that moment and what remained unfinished, deferred, or unverified.

If you reported completion prematurely, say so plainly and explain the discrepancy. Work completed later does not retroactively make an earlier completion claim accurate. Do not hide repeated premature completion signals behind the final passing test count.

Never display a completion notification or imply success while required authorized work remains. Only report completion after reconciling the original task, task ledger, code and repository state, tests, limitations, and this audit.

## 4. SHORTCUTS, PLACEHOLDERS, TEST INTEGRITY, AND BYPASSES

Search the files you changed and relevant surrounding code. Use suitable searches (for example, grep/ripgrep) for:
- TODO, FIXME, XXX, HACK, NotImplemented, bare pass, empty functions, and placeholders.
- mock, stub, fake, fixture, hardcoded, sample, dummy, fallback, skip, xfail, disabled, and related terms.
- Swallowed exceptions, ignored return values, overly broad exception handlers, bypasses, relaxed validation, and silent failure paths.
- Tests or assertions that were added, removed, skipped, disabled, weakened, rewritten, or changed to make them pass.
- New hardcoded business defaults, permission changes, state transitions, security assumptions, and data fallbacks.

Inspect matches and relevant code; keyword searches alone are not enough. Report relevant findings, whether they pre-existed or were introduced by this task, and their impact. Do not label a shortcut harmless just because tests pass.

Explicitly disclose every stub, mock, placeholder, hardcoded/fabricated value, TODO/FIXME, empty function, skipped or modified test, swallowed/bypassed error, temporary workaround, and item labelled “out of scope,” “later phase,” or equivalent. Explain whether it is acceptable for the current task and whether it leaves an acceptance gap.

A test must not be weakened or removed merely to achieve green results. If a test change is genuinely justified, explain the prior behavior, the change, why it is correct, and how the original protection remains covered.

## 5. PARTIAL, NOT DONE, AND DEFERRED ITEMS — INVESTIGATE AND CONTINUE

For every PARTIAL, NOT DONE, or DEFERRED item, state:
- Exact remaining work.
- Why it was not completed.
- The specific evidence for any claimed blocker.
- Whether the blocker is external and genuine, or results from missing investigation, avoidable deferral, uncertainty, convenience, or failure to use available tools.
- Whether it could have been completed safely with the information, permissions, tools, and dependencies already available.
- What action you took to resolve it, or why that action cannot safely be taken.
- The exact next action and who/what is needed.

A long task, large evidence inventory, inconvenient test suite, time-consuming investigation, or tool you failed to investigate is not, by itself, a genuine blocker. Before declaring a tool/capability unavailable, inspect available tools and the environment and provide the actual check and result. Before declaring a dependency missing, verify it.

After identifying gaps, continue all remaining authorized and independently actionable work. Do not merely report gaps that you could safely close now. If one item is genuinely blocked, park only that item and continue independent work. Never invent a dependency or use “deferred” to make unfinished work look acceptable. If the reason is that you failed to complete work you could have done, say so plainly.

## 6. REPOSITORY AND WORKING-TREE RECONCILIATION

Inspect and report the actual state at the end of the task, including:
- Repository, branch, HEAD commit, and relevant relationship to the remote branch.
- Git status: staged, unstaged, and untracked files.
- Complete relevant diffs, including untracked files that are part of the task.
- Recent commits, stashes, cherry-picks, resets, merges, restores, and recovery operations where relevant.
- Changes to application code, tests, migrations, configuration, dependencies, and documentation.
- Pre-existing and HU-approved work that must be preserved.
- Whether any changes were staged, committed, pushed, discarded, or otherwise altered, and under what authorization.

Reconcile file lists and counts against actual Git evidence. Investigate discrepancies; do not choose whichever report looks most favorable. Verify claims that changes were restored after stash/pop or other recovery operations. Do not discard or overwrite unrelated or approved changes.

Follow the task's authorization rules. No broad staging such as git add -A, no commit/push, no reset/discard, no history rewrite, and no destructive cleanup unless explicitly authorized. Do not infer permission to perform an action merely because it would make the final report cleaner.

## 7. BUSINESS RULES, SECURITY, ARCHITECTURE, AND DATA INTEGRITY

Independently inspect for deviations from frozen specifications, approved architecture, ADRs, and HU decisions. Highlight:
- New or changed business defaults and assumptions.
- Broadened permissions, authorization gaps, or role-removal/deletion changes.
- Financial, payment, tax/GST, order, dispatch, stock, shipment, refund, or customer-data behavior changes.
- Error fallbacks that may silently change business meaning.
- Migration and data-integrity risks.
- Provider calls, external writes, emails, shipments, or production actions.
- Conflicting requirements or decisions that require HU+DI review.

Passing tests does not authorize a new business decision. Do not invent business data or silently resolve a frozen-spec conflict. Respect explicit prohibitions such as no live provider writes, no production operations, and NO PAYMENT → NO DISPATCH. Never delete real financial/provider/production records without explicit authorization.

## 8. TESTS, LINTERS, AND FINAL-STATE VALIDATION

Run appropriate targeted tests after narrow changes and the required full suite/linters at the agreed meaningful integration checkpoint. Run them against the final relevant code state. Report exact commands, exit codes, and actual outputs; include raw output where requested. Do not present a summary as raw output.

Explicitly report:
- Tests and linters run, not run, skipped, or unavailable.
- Failures, warnings, retries, exclusions, and unresolved issues.
- Test changes that could affect coverage or strictness.
- Evidence reused from earlier runs and why it remains valid.
- Code changes made after the last test run.
- Environment limitations, including database/browser/provider/CI constraints.
- Whether CI actually ran; never infer CI success from local success.

If the final code changed after a test run, assess and rerun the relevant tests. Do not needlessly repeat expensive suites after a truly narrow change, but do not claim final-state validation from stale results. Do not claim all tests pass if any required test was not run or any failure remains unresolved.

## 9. TOOL/CAPABILITY AND BLOCKER CLAIMS

For every claim that a browser, command, credential, permission, service, dependency, or tool is unavailable, include the exact check performed and its output. State what alternative investigation was attempted. Distinguish:
- Actually unavailable or unauthorized.
- Available but not investigated.
- Available but not used.
- Failed due to environment/configuration.
- Not needed for the stated level of evidence.

Do not declare a blocker merely because the first attempt failed. Investigate reasonable alternatives without crossing authorization or safety boundaries.

## 10. FINAL SELF-CHALLENGE — TRY TO DISPROVE YOUR OWN REPORT

Before finalizing, act as a skeptical independent reviewer:
- Compare every original task and criterion against the ledger.
- Search for omissions and contradictory instructions/evidence.
- Challenge each DONE claim: what could make it false, and did you test that?
- Look for false-positive tests, untested branches, weak assertions, mocks masking real behavior, and changed code not covered by final tests.
- Compare claimed changed files and test counts against Git and command output.
- Check whether any “blocked” item was actually independently actionable.
- Check whether your timeline contains premature completion claims.
- Re-read this entire audit requirement and verify compliance with every section.

Take all safe, authorized corrective actions you identify before reporting. If you cannot resolve an issue, classify it accurately and explain the evidence and next action. Do not conceal, minimize, or euphemize failures.

## 11. REQUIRED FINAL REPORT FORMAT

Provide one consolidated report containing:

1. **Overall status:** honest conclusion; do not use “complete” unless every required authorized item is DONE (verified).
2. **Original task ledger:** every task/criterion, its original ID where available, one status (DONE, PARTIAL, NOT DONE, DEFERRED), evidence, and remaining work.
3. **Completion-claim timeline:** any premature or inaccurate earlier claims and the work that remained at the time.
4. **Shortcuts and integrity findings:** stubs, mocks, hardcoded values, TODO/FIXME/pass, skipped/weakened/changed tests, swallowed errors, workarounds, and scope deferrals.
5. **Validation:** exact commands, exit codes, raw output where requested, failures, skipped checks, and limitations.
6. **Repository reconciliation:** branch/HEAD, working-tree status, relevant diffs, untracked files, stashes/recovery, commits, and authorization status.
7. **Assumptions and unverified behavior:** everything assumed to work but not actually executed or observed.
8. **Blocker audit:** every unfinished item, genuine blocker evidence, whether it could have been done now, and the next action.
9. **Highest risks and discrepancies:** direct, candid list; no reassuring language that obscures severity.
10. **Next actionable step:** identify what can be done next without waiting for a HU+DI decision.

Do not report only aggregate counts. Do not bury serious failures at the end. Do not omit awkward findings. Do not describe self-reported evidence as independently verified.

## 12. GOVERNING PRINCIPLE

Honesty takes precedence over a favorable completion report. Finding gaps and disclosing mistakes is a successful audit outcome. An accurate PARTIAL or NOT DONE status is better than an unsupported DONE claim. HU+DI will independently verify the work; treat this as a reason to be more rigorous, not as a reason to make the report sound convincing.

**Mandatory before final report:** re-read this requirement, reconcile it against the original task and actual final state, perform all safe authorized corrective work, and disclose every remaining gap. No compromise on truthful reporting.