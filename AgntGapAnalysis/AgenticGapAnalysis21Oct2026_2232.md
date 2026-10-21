# EFFYKLEAN — EXHAUSTIVE READ-ONLY PROJECT ASSESSMENT, GAP ANALYSIS AND PHASED IMPLEMENTATION PLAN

## 1. PRIMARY MANDATE

Conduct a comprehensive, independent, evidence-based assessment of the entire EffyKlean project.

Your objectives are to establish:

1. What the project was originally intended to deliver.
2. What requirements, functionality, business rules, architecture constraints and operational capabilities were subsequently agreed or amended.
3. What each previous agent was instructed to do.
4. What each previous agent actually achieved, as established by evidence rather than claims.
5. What is complete and correct, partially implemented, incomplete, missing, incorrect, inadequately tested, deferred, blocked or unverified.
6. What defects, omissions, inconsistencies, risks and hidden dependencies remain.
7. What work is still required to achieve the agreed project outcomes.
8. How that remaining work should be organised into a phased, dependency-aware implementation plan.
9. What precise, objectively verifiable Definition of Done (DoD) must apply to every proposed implementation task.
10. Which decisions and authorisations must be referred to HU+DI before implementation can proceed.

Do not limit the investigation to existing checklists, known issues, selected documents, recent agent reports or files that appear important from their names.

Independently reconstruct the intended scope, examine the actual implementation, investigate additional issues, reconcile conflicting evidence, and account for every discovered requirement and outstanding task.

**This is strictly a READ-ONLY assessment and planning assignment. You are not authorised to implement, fix, modify, create, delete or otherwise change anything.**

Thoroughness and evidence quality take priority over speed, report brevity and the appearance of completion.

## 2. MANDATORY SOURCE DISCOVERY: LOCAL REPOSITORY AND PUBLIC GITHUB

You must examine both the local EffyKlean project and the public GitHub repository independently, then reconcile their contents.

Do not ask Hu to identify specific documents or provide a curated list of files. Discover the relevant material yourself.

### 2.1 Local repository

The local repository path is:

`/mnt/d/effykleanproject`

Inspect the actual local repository and its current state, including relevant directories, files, working-tree changes, branches, commits and available history.

Examine all relevant project materials, including:

- Application source code and module structure.
- Models, views, services, business logic, validation and error handling.
- Tests, fixtures, test utilities, test configuration and CI-related files.
- Specifications, acceptance criteria, architecture documents and ADRs.
- Implementation plans, task breakdowns, agent instructions, reports and handoffs.
- README, CLAUDE.md, project logs, status registers and other project records.
- Dependencies, lockfiles, build configuration, quality tools and CI workflows.
- Environment templates, settings, migrations and configuration.
- Integration implementations, mocks, stubs, scripts and provider-specific code.
- Deployment instructions, infrastructure configuration and operational procedures.
- Relevant tracked, untracked, modified and ignored project materials where safely accessible.
- Git history, relevant branches, diffs and remote-tracking information.
- Any other material needed to establish the intended scope or actual implementation state.

Establish the repository baseline, including current branch, current commit, working-tree status, uncommitted changes, untracked files and relevant divergence from remote history.

Do not assume the checkout is current, complete or clean.

If the specified path is unavailable, do not silently substitute a different directory. Report the exact access problem and what is required to continue.

### 2.2 Public GitHub repository

Inspect the public repository:

`https://github.com/VaijanathR/Di-Eval-Effyklean`

Discover and examine the relevant contents across the repository rather than opening only the latest document or a few obvious files.

Review, where applicable:

- Specifications and acceptance criteria.
- Architecture, ADRs and approved decisions.
- Agent instructions and task-specific requirements.
- Implementation plans, definitions of done and work breakdowns.
- Project logs, status registers, reports and handoffs.
- Historical discussions and implementation records stored in files.
- Relevant source files or supporting artifacts present in the repository.
- Commit history and changes needed to understand the evolution of the project.
- Referenced documents, linked files and cross-referenced records.

Follow relevant references until the intended requirement, decision or work item can be understood in context.

Do not assume that the latest document supersedes all earlier material. Establish which records apply, which were superseded, and what evidence supports that conclusion.

If files or historical records cannot be accessed, identify them and disclose the limitation. Never claim to have reviewed inaccessible content.

### 2.3 Reconcile the two sources

Use the local repository to establish what is actually present and implemented. Use the public repository and other available project records to reconstruct the intended scope, authorisations, plans and historical progress.

Compare the two sources for:

- Missing, divergent, outdated or conflicting documentation.
- Local implementation changes not reflected in public records.
- Publicly documented requirements missing from the local implementation.
- Uncommitted or untracked work relevant to project progress.
- Differences between agent claims and repository evidence.
- Inconsistencies between code, tests, specifications, plans and status reports.
- Requirements or decisions that were lost, misunderstood or omitted in later work.
- Missing evidence needed to establish completion.

Do not synchronise, publish, upload, download into the repository, or otherwise modify either source as part of the assessment.

## 3. RECONSTRUCT THE COMPLETE INTENDED PROJECT SCOPE

Before judging completion, establish what EffyKlean was supposed to deliver.

Do not assume that one specification, plan, status register, audit instruction or agent report contains the entire project scope.

Inspect and reconcile all relevant available:

- Frozen specifications and individual acceptance criteria.
- Architecture documents and architectural decision records.
- Foundation, governance, security and authorisation requirements.
- Implementation plans, phase plans, delta plans and task breakdowns.
- Agent instructions, follow-up instructions and definitions of done.
- HU+DI decisions, approved changes and subsequent clarifications.
- Project logs, status registers, README, CLAUDE.md and handoff documents.
- Git history, commits and relevant change records.
- Test plans, validation requirements and quality gates.
- Deployment, integration and operational requirements.
- Explicit deferrals, unresolved questions, blockers and dependencies.

Reconstruct the timeline where necessary. Distinguish:

- Original commitments.
- Subsequently approved scope changes.
- Superseded instructions and decisions.
- Requirements that remain binding.
- Explicitly deferred work.
- Decisions that remain unresolved.
- Agent assumptions or changes that were never authorised.

Preserve traceability to the original records.

Break broad objectives into individually assessable requirements and deliverables. Do not merge distinct obligations in a way that hides incomplete work.

Do not silently discard requirements because they are inconvenient, difficult to locate, absent from a later summary or not included in an existing audit checklist.

### Existing audit requirement

Locate and examine `AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement` and follow its applicable governance requirements.

However, that document is not an exhaustive inventory of EffyKlean, a limit on the investigation or a substitute for independently reconstructing the project.

Discover and investigate requirements, gaps, risks and obligations beyond those explicitly listed in that document.

## 4. REVIEW EVERY RELEVANT PREVIOUS AGENT'S WORK

Reconstruct the available work history of previous agents from their instructions, reports, repository changes, commits, tests and other relevant evidence.

For each identifiable task or work package, establish:

1. What the agent was instructed to accomplish.
2. What constraints, decisions and acceptance conditions applied.
3. What the agent claimed to have completed.
4. What files, code, tests, documentation or configuration actually changed.
5. What validation was performed and what evidence exists.
6. Which obligations were genuinely completed and correctly implemented.
7. Which obligations were partially completed, omitted, incorrectly implemented or insufficiently validated.
8. Whether the required documentation and handoff were completed.
9. Whether regressions, contradictions, duplication or new risks were introduced.
10. Whether the agent exceeded its authorisation or made unsupported completion claims.
11. What remains necessary to close the task.

Compare each agent's work against both the instruction that applied at the time and the requirements that remain authoritative now.

Investigate shortcuts and suspicious patterns, including:

- Stubs, placeholders and incomplete implementations.
- TODOs and unexplained `pass` statements.
- Skipped tests or weakened assertions.
- Swallowed exceptions and incomplete error handling.
- Misleading mocks or hard-coded assumptions.
- Disconnected functionality and unimplemented integration paths.
- Missing failure-path and boundary-condition coverage.
- Tests that pass without establishing the required outcome.
- Unsupported statements that a feature or phase is complete.
- Documentation that claims more than the evidence demonstrates.

Do not assume every occurrence is a defect. Examine the surrounding context and establish its practical effect.

Do not accept an agent's report as proof of completion. Verify claims against the underlying evidence wherever possible.

## 5. INVESTIGATE THE IMPLEMENTATION END TO END

Do not limit the assessment to reviewing isolated files or checking whether functions and classes exist.

Trace important functionality through its relevant workflow, including entry points, business logic, data models, persistence, validation, permissions, integrations, failure handling and user-visible outcomes.

Investigate, where applicable:

- Whether implemented behaviour matches the specification.
- Whether business rules are enforced consistently.
- Whether data integrity and transaction boundaries are adequate.
- Whether permissions and security controls are correctly applied.
- Whether duplicate processing, retries or concurrent operations create risks.
- Whether external-service failures are handled safely.
- Whether recovery, observability and operational procedures are adequate.
- Whether dependencies, configuration and deployment prerequisites are complete.
- Whether tests establish actual outcomes or merely execute code.
- Whether integration behaviour is real, mocked, stubbed, sandbox-tested or production-verified.
- Whether documentation accurately reflects implementation and readiness.
- Whether features are complete individually but disconnected from the end-to-end workflow.
- Whether new risks emerge from interactions between otherwise reasonable components.

Examine the relevant negative, boundary and failure paths, not only the expected success path.

Investigate additional defects, missing requirements and risks independently, even when previous agents, tests, plans and existing audits never identified them.

Use the agreed specification and architecture as the governing constraints unless reliable evidence establishes that a particular decision was formally superseded.

Do not silently redesign the project or make new business decisions.

## 6. MANDATORY COMPLETION AND INVESTIGATION-DEPTH REQUIREMENTS

### 6.1 Complete every applicable instruction

Every applicable investigation, verification, reconciliation and reporting obligation in this instruction set must be addressed.

Do not selectively perform the easy or quick tasks while omitting work that requires extensive inspection, historical reconstruction, cross-referencing or deeper analysis.

Do not decide independently that a task is unnecessary, too time-consuming, repetitive or adequately covered by a superficial check.

If an instruction is genuinely inapplicable, explain why. If it cannot be completed safely or because access or evidence is unavailable, identify the exact limitation and what remains outstanding.

An attempted check is not a completed check. A generated report is not proof that the required investigation was completed.

### 6.2 Thoroughness takes priority over speed

There is no requirement to finish quickly. Take the time needed to investigate the project thoroughly.

Do not:

- Read only the opening lines of a document and assume its remaining contents.
- Inspect a few representative files and generalise to the entire project.
- Rely on filenames, search snippets, previews or summaries instead of examining relevant source content.
- Assume that a test exists and therefore the tested requirement is satisfied.
- Review only the latest commit when earlier history is relevant.
- Stop after finding a few obvious gaps.
- Omit complex modules, lengthy documents or difficult workflows.
- Replace individual requirement analysis with a high-level summary.
- Skip tasks merely because they are time-consuming.
- Prioritise report appearance or rapid delivery over investigation quality.

Searches may be used to discover relevant material, but inspect the underlying content needed to support the conclusion.

Read relevant documents in sufficient context, including continuation sections, appendices, referenced materials and qualifications.

For large files or documents, inspect them systematically in manageable sections until the relevant content is covered. Do not mistake truncated output or a partial preview for the full source.

### 6.3 No fabricated or unsupported completion claims

Never invent:

- Requirements, facts or findings.
- File contents, paths or line numbers.
- Commits, changes or historical events.
- Command output or test results.
- Agent actions or verification evidence.
- External-system outcomes.
- Completion status or coverage statistics.

Never claim to have read, executed, tested or verified something that you did not actually inspect or perform.

Distinguish observed facts, reasoned conclusions, hypotheses and unverified claims.

When evidence is contradictory, incomplete, truncated or ambiguous, investigate further. If uncertainty cannot be resolved safely, disclose it explicitly.

Do not mark an item DONE (verified) merely because an agent claimed completion, a file exists, a test was added or a command was reportedly run.

### 6.4 Maintain an investigation checklist

Before starting, break this instruction set into a systematic checklist of source inspection, scope reconstruction, verification, gap analysis, planning and final reporting obligations.

Track each obligation throughout the assessment so that nothing is silently omitted.

Before submission, record one operational outcome for each obligation:

- Completed with evidence.
- Partially completed, with outstanding work identified.
- Not completed, with reason and next step.
- Not applicable, with explanation.
- Blocked, with the specific blocker and required evidence or access.

These are investigation-progress outcomes. They do not replace the required project statuses defined in Section 7.

Do not mark an investigation obligation complete merely because you attempted it.

### 6.5 Follow material leads and dependencies

When a requirement, finding, instruction, implementation or report points to another relevant file, task, decision, test, commit or workflow, follow that reference as far as reasonably possible.

When a task contains multiple acceptance conditions, assess each condition separately.

When a requirement spans several modules, investigate the relevant end-to-end workflow.

When evidence suggests a defect or contradiction, investigate its scope and implications sufficiently to distinguish the likely cause from a hypothesis.

Do not stop at the first plausible explanation simply because it makes the report easier to finish.

### 6.6 Disclose incomplete investigation

If any required work remains incomplete, report:

- The exact scope not completed.
- What was inspected or attempted.
- What evidence was obtained.
- Why the investigation could not be completed.
- What would be required to finish it.
- How the limitation affects the confidence and completeness of the assessment.

Do not describe the investigation as exhaustive if material areas remain unexamined.

If the response cannot contain the complete report, continue in subsequent responses until all report sections are delivered. Do not omit task-level details merely to shorten the output.

## 7. STATUS EVERY REQUIREMENT AND DELIVERABLE

Assign exactly one of these project statuses to every assessable requirement and deliverable:

- **DONE (verified):** Sufficient direct evidence establishes that the intended outcome is achieved.
- **PARTIAL:** Some work is achieved, but one or more obligations remain incomplete, incorrect or inadequately validated.
- **NOT DONE:** The required work is demonstrably absent or incomplete.
- **DEFERRED:** An identifiable decision or plan explicitly defers the work, and it remains deferred.

Explain blocked, unverified and externally unverified conditions in the supporting notes; do not invent additional project status categories.

For each item, record:

- Unique item ID.
- Requirement or deliverable.
- Source document, identifier or instruction.
- Intended outcome and acceptance conditions.
- Dependencies and relevant decisions.
- Current status.
- Evidence and references.
- Completed elements.
- Outstanding elements.
- Related findings and risks.
- Evidence or work required for closure.

Where a parent task contains several obligations, assess the obligations individually. A parent task must not conceal partial completion of its constituent requirements.

Where a deferred item has subsequently been implemented, assess its current state rather than retaining a historical deferred status automatically.

Where evidence is insufficient, state precisely what remains unverified.

## 8. EVIDENCE AND VERIFICATION STANDARDS

Make every material conclusion traceable to evidence wherever possible.

Use exact file paths, line references, acceptance-criterion IDs, task identifiers, commit references, test names and actual command output as applicable.

For each significant finding, provide:

- Finding ID.
- Severity: Critical, High, Medium or Low.
- Affected requirement, task, module, workflow or decision.
- Expected outcome.
- Actual observed state.
- Evidence and what it establishes.
- Practical impact or risk.
- Verification confidence and limitations.
- Recommended corrective action, without performing it.

Distinguish confirmed findings, partial evidence, reasoned assessments and unresolved hypotheses.

Do not fabricate evidence or imply that a verification occurred when it did not.

Prefer existing test evidence and safe inspection. Do not automatically run expensive test suites merely to make the assessment appear more thorough.

Where checks are executed, report what was run and the actual result. Where checks are not executed, state why and what remains unverified.

For external integrations, distinguish clearly between:

- Implementation present in code.
- Local behaviour tested.
- Mock-based tests passed.
- Sandbox integration tested.
- Production integration verified.

Do not infer production readiness from sandbox success.

Never expose secret values. Report only relevant configuration names, non-sensitive presence or absence, and associated risks.

## 9. COMPREHENSIVE GAP ANALYSIS

Produce a detailed gap analysis reconciling the intended project scope with the verified current state.

Organise it by meaningful project areas, modules, features, end-to-end workflows and operational capabilities.

Include a consolidated gap register. For every gap, provide:

- Gap ID and severity.
- Related requirement, acceptance criterion or planned deliverable.
- Expected functionality or outcome.
- Actual implementation state.
- Exact missing, incorrect or inadequately verified elements.
- Evidence and relevant references.
- Business, technical, security, operational or delivery impact.
- Dependencies and blockers.
- Whether the gap is confirmed or requires further verification.
- Recommended next action.
- Whether HU+DI approval is required.

Distinguish implementation defects from missing evidence, test deficiencies, documentation inconsistencies, external-verification limitations, deferred work and unresolved decisions.

Include previously known gaps and newly discovered ones.

Do not omit minor but legitimate gaps merely because larger defects exist. Prioritise by severity and dependency, but account for the full identified scope.

## 10. PROPOSED PHASED IMPLEMENTATION PLAN

Based on the complete assessment and gap analysis, prepare a detailed, logically ordered implementation plan covering all remaining work required to achieve the agreed project functionality and operational outcomes.

This is a proposal for HU+DI review. It is not permission to implement anything.

Organise the work into logical phases and individually numbered tasks. Derive the phases from actual dependencies, architectural constraints, risks, verification requirements and delivery needs.

### 10.1 Required fields for every task

Every proposed task must include:

1. **Task ID and title:** Unique, stable identifier.
2. **Phase and objective:** The phase to which the task belongs and the intended phase outcome.
3. **Source and traceability:** Relevant requirements, acceptance criteria, previous tasks, decisions and gap IDs.
4. **Current state:** What exists, what is verified and what remains incomplete.
5. **Target outcome:** Precisely what the task must deliver.
6. **Scope:** Relevant functionality, components or files likely to be affected, where known.
7. **Dependencies:** Prerequisite tasks, decisions, integrations or environmental conditions.
8. **Priority and rationale:** Why the task has that priority and where it belongs in the sequence.
9. **Proposed implementation approach:** A concise approach, with unresolved alternatives identified.
10. **Definition of Done:** Specific, objective and testable completion conditions.
11. **Verification requirements:** Tests, commands, expected outcomes, evidence and applicable CI or quality gates.
12. **Documentation and handoff requirements:** Records that would need updating once implementation is authorised.
13. **Risks and constraints:** Relevant architecture, business rules, security and regression concerns.
14. **Approval gate:** Decisions or authorisations required from HU+DI before implementation.

### 10.2 Definition of Done for every task

Every task must have a task-specific DoD derived from its actual requirements.

Avoid vague statements such as "feature complete", "tests pass", "integration works" or "documentation updated" unless the specific expected outcomes and evidence are defined.

Where relevant, include:

- Required functionality and acceptance scenarios.
- Positive, negative, boundary and failure-path conditions.
- Business-rule enforcement and data-integrity expectations.
- Permission and security requirements.
- Integration behaviour, timeouts, errors and recovery behaviour.
- Required automated tests and meaningful assertions.
- Relevant test commands and expected results.
- Required CI, linting, formatting and framework checks.
- Documentation, configuration and operational deliverables.
- Regression checks and evidence needed to establish completion.

Specify what must be demonstrated, not merely what activities must be performed.

A later reviewer must be able to determine objectively whether each task is DONE, PARTIAL or NOT DONE.

Define proportionate testing for individual tasks and broader validation at meaningful integration or release gates. Do not prescribe unnecessarily expensive full-suite runs after every narrow change without justification.

### 10.3 Plan completeness and dependency reconciliation

Every confirmed implementation gap must map to one or more proposed tasks.

If a gap does not require an implementation task, explain whether it requires a decision, additional evidence, external verification, an authorised deferral or another non-implementation action.

Identify:

- Dependencies between tasks.
- Prerequisite decisions.
- Blockers and their resolution requirements.
- Logical implementation sequence.
- Required integration and regression gates.
- Work that must precede deployment or operational use.
- Tasks that cannot proceed until HU+DI authorises a decision.

Separate mandatory work needed to fulfil existing commitments from optional improvements and newly proposed scope.

Do not hide unresolved decisions inside implementation tasks. Do not convert recommendations into authorised requirements.

Do not invent dates, durations or completion percentages without a defensible basis. Explain any estimates and their assumptions.

The plan must be detailed enough for HU+DI to review, amend, prioritise and separately authorise before any implementation agent receives work.

## 11. REQUIRED FINAL REPORT

Deliver the full assessment directly in your final response. Do not create or modify a report file.

Use this structure:

1. Executive assessment and principal conclusions.
2. Local repository baseline, branch, commit and working-tree state.
3. Public GitHub repository baseline and records examined.
4. Local-versus-public discrepancies and limitations.
5. Reconstructed intended project scope and decision history.
6. Complete requirement and deliverable inventory, with individual statuses and evidence.
7. Previous-agent assessment, comparing instructions and claims with actual results.
8. Detailed gap analysis by module, feature, workflow, integration and operational area.
9. Additional defects, risks, overlooked requirements and hidden dependencies.
10. Test, CI, quality, security, business-rule and operational-readiness assessment.
11. Consolidated outstanding-work register.
12. Proposed phased implementation plan, with individually numbered tasks and a complete DoD for every task.
13. Dependencies, blockers, sequencing and proposed verification gates.
14. HU+DI decisions and authorisations required.
15. Inaccessible records, evidence limitations and checks not performed.
16. Final completeness reconciliation against this entire instruction set.

Provide the complete item-by-item inventory and task-level DoDs. Do not substitute aggregate counts, examples or selected highlights for the underlying details.

Summaries may supplement the detailed assessment but must not replace it.

If the complete report requires multiple responses, explicitly continue until every section and its required detail has been delivered. Do not silently omit items to shorten the report.

## 12. ABSOLUTE READ-ONLY RESTRICTIONS

This assignment authorises inspection, analysis, verification within safe limits, gap reporting and preparation of a proposed implementation plan only.

You are NOT authorised to implement, fix, refactor, complete, clean up or modify anything.

Do not:

- Edit, create, delete, rename, move, reformat or regenerate project files or documents.
- Modify source code, tests, dependencies, lockfiles, migrations, configuration or environment files.
- Modify project records, status registers, instructions, plans or documentation.
- Stage, commit, stash, reset, clean, checkout, merge, rebase or push Git changes.
- Synchronise local and public repositories.
- Deploy or change infrastructure, provider settings or external services.
- Create, update, delete or modify records in Zoho, Shiprocket, databases or other integrations.
- Install packages or execute operations with uncertain side effects.
- Delegate the assessment or any proposed implementation to another agent.
- Start implementing a proposed task, even when a defect appears obvious or its fix appears trivial.
- Publish, upload or otherwise distribute assessment results.
- Create a report file as part of this assignment.

Preserve all existing user changes, including uncommitted and untracked work. Do not clean up or reclassify those changes as authorised for staging or commitment.

Avoid any command whose effects on the working tree, persistent state or external systems are uncertain. If a check requires a prohibited write, risky operation or additional authorisation, document the limitation and stop short of that action.

If you discover a serious defect, report the evidence and recommended action. Do not fix it.

For conflicts involving frozen architecture, approved decisions, specifications, business rules or scope authority, follow:

**STOP → REPORT → HU+DI DECIDE**

Do not resolve such conflicts independently.

## 13. FINAL COMPLETENESS AND INTEGRITY AUDIT

Before submitting the report, perform a final reconciliation against the entire instruction set.

Confirm that:

- The local repository has been examined to the extent safely accessible.
- The public GitHub repository has been independently examined to the extent accessible.
- Relevant files, referenced documents and material historical records have been followed.
- Local and public evidence has been reconciled.
- The intended project scope and decision history have been reconstructed from available records.
- Every discovered requirement and deliverable has an explicit project status.
- Previous-agent claims have been compared against underlying evidence wherever possible.
- DONE claims have adequate supporting evidence.
- Partial completion and outstanding subrequirements have not been hidden by parent-task statuses.
- All material gaps, defects, risks and newly discovered issues have been documented.
- Every confirmed implementation gap is accounted for in the proposed plan or explicitly explained.
- Every proposed task has a specific, testable Definition of Done.
- Task dependencies, blockers, deferred work and approval gates are represented.
- Investigation omissions, inaccessible records, unverified claims and unexecuted checks are explicitly disclosed.
- The outstanding-work register reconciles with the detailed gap analysis and proposed plan.
- No completion claim exceeds the work actually performed.
- No files, documents, Git state or external systems have been changed.

If this audit reveals omissions, return to the investigation and address them wherever safely possible before submitting the report.

If something cannot be completed, report it honestly. Do not disguise unfinished investigation as successful completion.

**Success is measured by completeness, accuracy, evidence and the usefulness of the resulting implementation plan—not by speed, brevity, a high completion percentage or a polished-looking report.**

A transparent assessment that clearly identifies genuine limitations is preferable to a seemingly complete report based on partial inspection, unsupported assumptions or fabricated verification.

Stop after delivering the complete read-only assessment, gap analysis and proposed phased implementation plan. Wait for HU+DI to review and explicitly authorise any subsequent action.
