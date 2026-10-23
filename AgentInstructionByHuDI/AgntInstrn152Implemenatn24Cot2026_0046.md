# EffyKlean — Implement the 152 Reconciled BUILD Items

## 1. Mission and scope

Implement all 152 authorized BUILD items in the existing EffyKlean application repository.

- 141 items from the 245-item ledger.
- 11 additional items from the 597-item register: `MF-070, MF-071, MF-074, MF-078, MF-092, MF-107, MF-109, MF-114, MA-ORD-068, MA-DSC-023, MA-SET-061`.

Total: **152 items.**

Do not add already implemented, LATER, EXCLUDE or INVESTIGATE items to this scope. Preserve the reconciled classifications.

## 2. Mandatory project context

Read and follow these existing records before implementation:

1. [HU+DI Golden Rules](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/HU_DI_GOLDEN_RULES.md)
2. [SSD completion-audit requirement](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md)
3. [Existing implementation mandate](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/AgntInstImplementation-FINAL%20and%20Updated%2022Oct2026_2249.md)
4. [Reconciled 597-ID register](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv)
5. [245-item ledger](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/BUILD245_LEDGER_2026-10-22.csv)
6. [Reconciled decision ledger](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/BUILD245_DECISIONS_RECONCILED_LEDGER_2026-10-23.csv)
7. [Decision reconciliation](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/BUILD245_HUDI_DECISIONS_RECONCILIATION_2026-10-23.md)
8. [Recovered HU responses](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/HU_RESPONSES_RECOVERED_REGISTER_2026-10-23.md)
9. [Genuine unresolved decisions shortlist](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md)
10. [Current 597 status reconciliation](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv)
11. [Disposition corrections](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv)
12. [HU response reconciliation](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/HU_RESPONSE_RECONCILIATION_597_2026-10-23.csv)
13. [Implementation plan](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/ImplementationPlanOCT22-26-2026.md)
14. [Implementation summary](https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/docs/ImplementationPlan/IMPLEMENTATION_SUmmary_22Oct26_1250.md)

Consult the frozen specifications, architecture, ADRs and authorization records where relevant to a task. Do not conduct unrelated reviews. The old `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md` is superseded and must not be used as a question queue.

## 3. Implement without repeating settled work

- Use existing decisions, responses, project history and verified evidence. Do not reopen settled questions, repeat completed assessments or ask Hu to repeat recorded answers.
- Implement the approved acceptance criteria using the existing architecture and business rules. Resolve routine technical details within those constraints.
- Do not launch another broad gap analysis, planning exercise or decision questionnaire.
- Investigate only specific gaps, contradictions, failures or risks that materially affect implementation or verification.
- Work through all 152 items. A blocker on one item must not stop independent, authorized work on the others.
- Never invent requirements, silently change scope, weaken acceptance criteria or claim completion without evidence.

## 4. Authorization and repository safety

Preserve frozen specifications, architecture, ADRs, business rules, security controls and existing integrations.

Do not deploy, publish, perform production or live-provider writes, send external communications, incur paid resources, change DNS, perform destructive operations, or stage, commit or push changes without the required separate authorization.

Use explicit paths for Git staging; never use `git add -A`. Do not add commit co-author trailers. Keep secrets and private agent/session logs out of Git. Preserve existing user changes.

Apply **STOP → REPORT → HU+DI DECIDE** only when a genuine unresolved business decision, frozen-specification conflict, material risk or authorization gap prevents safe progress. Document the evidence and precise decision required, isolate the blocker, and continue independent work.

## 5. Verification and item status

Verify each item against its actual acceptance criteria. Use targeted tests for narrow changes and broader suites at meaningful integration gates. Avoid redundant expensive test runs.

Record actual commands, exit codes and relevant output. Distinguish local tests, mocks, sandbox checks and production evidence. Never fabricate results, weaken tests to pass, or swallow errors.

Give every item exactly one status:

- `DONE (verified)` — criteria met with evidence.
- `PARTIAL` — some implementation completed; criteria or verification remain outstanding.
- `NOT DONE` — implementation remains incomplete.
- `DEFERRED` — a specific decision, authorization, risk or dependency prevents safe progress.

For each of the 152 IDs, record its criteria, status, changed-file paths and relevant lines, verification evidence, limitations and next action. For every non-DONE item, state the exact blocker, evidence, work attempted and responsible next step. Do not defer work for convenience.

## 6. Completion audit

After implementation, perform the required SSD completion audit against the actual changes and evidence. Do not use it as an excuse to restart the project-wide assessment.

Check relevant stubs, placeholders, TODOs, unjustified `pass` statements, weakened or bypassed tests, swallowed exceptions, missing controls, incomplete criteria and unsupported completion claims. Distinguish pre-existing findings from changes introduced during this work. Do not silently make out-of-scope changes or unauthorized decisions.

## 7. Timestamped reports and continuity records

Save these two deliverables in the local application repository:

- `docs/ImplementationPlan/AgentReports/BUILD152_IMPLEMENTATION_REPORT_YYYY-MM-DD_HHMMSS.md`
- `docs/ImplementationPlan/AgentReports/BUILD152_ITEM_LEDGER_YYYY-MM-DD_HHMMSS.csv`

**Timestamp rule:** Every report and supporting artifact created or saved for this assignment—including audits, evidence records, summaries and handovers—must use its actual creation date and time in the filename, format `YYYY-MM-DD_HHMMSS`, using `Asia/Kolkata` (IST, UTC+05:30) and 24-hour time. Never use placeholder timestamps in actual filenames or overwrite an existing timestamped artifact. Use a shared run timestamp for related files where practical. Record actual timestamps and timezone inside each report.

Update applicable canonical continuity records (`PROJECT_LOG.md`, `CLAUDE.md`, README and the relevant status register) under their established filenames, preserving history. Include these updates in the final report. Keep reports local; do not push them without separate authorization.

## 8. Final report and completion requirements

Complete all independent, authorized work before finalizing. Do not send routine progress updates or stop overall work because one item is blocked.

Provide the substantive final report in the agent's final chat response and save it locally. The chat and saved report must agree. Include:

1. Overall outcome and counts across all 152 items by status.
2. Item-by-item criteria, outcomes and implementation/verification evidence.
3. Commands, exit codes, relevant outputs and test limitations.
4. Changed files, relevant line references and continuity-record updates.
5. Completion-audit findings, including shortcuts or unsupported claims.
6. All unresolved items, with exact blockers, evidence and next actions.
7. Security, architecture, business-rule, migration and data-integrity risks.
8. Starting and ending branch, HEAD, working-tree state and repository mutations.
9. Exact timestamped paths of all requested deliverables and supporting artifacts.
10. Final self-audit against this instruction and the applicable mandates.

Never claim full completion unless every authorized actionable item is implemented and verified. Report incomplete work honestly; do not omit or fabricate evidence.
