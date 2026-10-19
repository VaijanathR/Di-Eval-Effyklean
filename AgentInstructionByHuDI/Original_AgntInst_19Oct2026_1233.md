# EffyKlean — Final Consolidated Implementation Continuation, Project Reconciliation and Mandatory Honest Audit

**Date:** 19 October 2026  
**Authority:** HU+DI  
**Mode:** Continue authorized implementation, independently verify actual state, close actionable gaps, and report honestly.  
**Primary objective:** Deliver the approved EffyKlean website and its required integrations in accordance with the complete authoritative project scope—not merely make code changes or produce a green test report.

---

## 0. FIRST MANDATE — READ AND FOLLOW THE PUBLIC SSD AUDIT REQUIREMENT

Before beginning implementation or making substantive changes, read the complete mandatory audit requirement:

https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md

This is your first mandatory execution and reporting requirement. Apply it throughout the task, not merely when preparing your final report.

You must re-read the audit requirement before issuing your final report and verify that every applicable requirement has been satisfied.

Do not issue premature completion messages. Do not hide unfinished work behind test counts, summaries, assumptions, mocks, previous reports, or deferred-task labels.

If you could have completed an item using the tools, information and permissions already available, acknowledge that fact and complete it if it remains authorized.

An accurate PARTIAL or NOT DONE report is preferable to a false, misleading or unsupported DONE claim.

This instruction does not grant additional permissions, override safety requirements, supersede frozen specifications, or bypass HU+DI decisions. When an item genuinely requires a decision or authorization, stop only that affected item, report the evidence and options, and continue independent authorized work.

## 1. RECONSTRUCT THE ORIGINAL TASK AND COMPLETE SCOPE

Start with the original task instruction:

https://github.com/VaijanathR/Di-Eval-Effyklean/blob/main/AgentInstructionByHuDI/AgntInst_18Oct2026_1958.md

Retrieve and read the complete current authoritative implementation plan and every relevant linked or referenced project artifact. Do not rely on this prompt alone as the complete scope definition.

Inspect the actual repository and applicable records, including:

- The frozen SPEC v0.8 and all applicable amendments.
- The approved architecture, ADRs, authorization gates and governance rules.
- The complete implementation plan, task ledger, acceptance criteria and dependency records.
- HU+DI decisions, change requests, decision-evidence mappings and unresolved decision records.
- `PROJECT_LOG.md`, `CLAUDE.md`, `README.md` and the current status register.
- The 597-activity inventory, including the approximately 228 keyword/route-only rows previously identified.
- The 73 class-E rows and the 122-row decision-evidence map.
- Historical implementation, test, audit, provider-setup and handover evidence.
- Relevant Git history, existing code, migrations, configuration, tests and working-tree changes.

Use the actual current files and repository state. Do not assume a filename, commit, status, test result or earlier report remains accurate without checking it.

If a required record is missing or inaccessible, report precisely which record could not be retrieved, what was attempted, and what evidence is still available. Do not silently substitute a summary for an unavailable authoritative source.

### Required scope inventory

Before broad implementation, create or update a complete requirement-to-evidence ledger covering every applicable task and acceptance criterion.

For each item, record:

1. A unique identifier and authoritative source.
2. The requirement and its acceptance criteria.
3. Applicable dependencies and prerequisite decisions.
4. Current implementation status.
5. Exact implementation location or relevant artifact.
6. Evidence supporting the reported status.
7. Required validation and its actual result.
8. Remaining gaps, risks or blockers.
9. The next action and whether it is already authorized.

Use these status distinctions consistently:

- **DONE — VERIFIED:** Acceptance criteria are satisfied by appropriate evidence.
- **PARTIAL:** Some work is complete, but a requirement, acceptance criterion or verification remains outstanding.
- **NOT DONE:** Applicable work remains outstanding.
- **BLOCKED:** A specific, evidenced obstacle prevents the next action.
- **DEFERRED — AUTHORIZED:** An identifiable authority or approved decision explicitly permits deferral.
- **NOT APPLICABLE — JUSTIFIED:** The item is outside the applicable scope for a documented, evidence-based reason.

A code file, passing test, status-register entry, prior agent assertion or successful configuration step is not automatically proof that a requirement is complete.

The inventory must include implementation, testing, security, integration, operational readiness, documentation, evidence collection and required acceptance work. The named priorities in this prompt are not an exhaustive task list.

Do not stop after producing the inventory. Use it to guide execution and continue updating it as evidence changes.

## 2. RECONSTRUCT PROJECT HISTORY AND DECISION AUTHORITY

Reconstruct the relevant project direction chronologically, using authoritative records and actual evidence.

Determine:

- The original business objective and approved implementation direction.
- The sequence of specifications, architecture decisions, ADRs, change requests and explicit HU+DI approvals.
- Which decisions remain authoritative and which have been superseded, narrowed, expanded or reversed.
- Which historical statements were binding decisions versus proposals, suggestions, assumptions or unverified claims.
- What work was authorized, what was actually implemented and what was only reported.
- Which completion claims were subsequently corrected or contradicted.
- Which known defects, omissions, regressions, shortcuts and deferred tasks remain unresolved.
- Whether the current implementation plan and status register accurately represent that history.

Do not assume the latest document automatically overrides a frozen specification or explicit HU+DI decision. Resolve authority using the governing project rules and documented approvals.

If the history contains conflicting directions, identify the exact conflicting sources and explain the impact. Do not silently choose whichever interpretation makes implementation easier.

Follow the established governance rule:

**STOP → REPORT → HU+DI DECIDE**

Use it when a genuine business, architecture, security, scope or authorization decision is required. Stop only the affected work; continue other authorized and independent tasks.

### Reconcile recorded status against reality

The status register, project logs, earlier audit reports and agent handovers are records to verify, not independent proof of correctness.

Compare each applicable status with actual implementation and evidence. Identify discrepancies, stale entries, missing acceptance evidence, contradictory decisions, omitted requirements and unjustified deferrals.

Do not mark a historical discrepancy resolved simply because the status register has been edited. Resolve the underlying work or clearly document its remaining status.

## 3. PRESERVE THE REPOSITORY AND ALL APPROVED WORK

Inspect the real repository before making changes.

Establish and record:

- Repository root, current branch and HEAD commit.
- Relationship between the local branch and its configured upstream.
- Current working-tree status, including staged, unstaged and untracked files.
- Relevant diffs, recent commits and existing stashes.
- Existing modifications and untracked artifacts that could be overwritten or confused with your changes.

Preserve the approved homepage link rearrangement in `modules/storefront/site.py` and `tests/test_storefront_shell.py`. These changes were explicitly approved by HU; do not treat them as unexplained or unauthorized work.

Preserve `config/settings/local.py` and all other existing approved or unrelated changes. Do not overwrite, discard, reset, clean, or conflate them with new implementation work.

Previously reported Git state and file counts may be stale. Verify the current state rather than assuming an earlier report remains correct.

### Git and publication boundaries

Unless HU explicitly authorizes a change to these boundaries:

- Do not stage files.
- Do not commit.
- Do not push or publish.
- Do not deploy.
- Do not rewrite Git history.
- Do not discard existing work.
- Never use `git add -A`.
- Never perform broad cleanup that could delete unrelated or test evidence.

Use explicit file paths for any Git operations that become authorized later. Keep work logically separated so HU can review it safely.

No implementation instruction in this prompt implicitly authorizes publication or deployment.

## 4. GOVERNING ARCHITECTURE AND TECHNICAL BASELINE

Respect the approved architecture and frozen project decisions.

The established baseline includes:

- Modular Monolith using Django/Python and PostgreSQL.
- Python 3.14, Django 5.2 LTS and PostgreSQL 17.
- `uv`, `pytest-django`, Ruff and GitHub Actions.
- No SQLite substitution.
- The approved deployment direction and its constraints; AWS is excluded by the current architecture decision, DigitalOcean App Platform with Managed PostgreSQL is preferred, Droplets require justification, and GoDaddy remains the fallback.
- Existing security and authorization gates.
- AD-10: **NO PAYMENT → NO DISPATCH**.
- AD-11: do not publish stale catalogue content.
- AD-16: preserve the applicable security gate.

Verify the exact current authoritative records before relying on these summaries where detailed interpretation matters.

Do not silently replace the architecture, framework, database, authorization model or integration design to simplify implementation.

Do not treat a local test environment as proof that production deployment is ready.

## 5. IMPLEMENT ALL REMAINING AUTHORIZED WORK

Use the complete scope ledger and implementation plan to determine the full workload. The following priorities identify known workstreams; they do not limit your responsibilities.

### Priority A — Known implementation work

Investigate, reconcile and complete the applicable remaining work for:

1. **T41 — Scheduled publication.** Verify the intended scheduling requirements, publication permissions, timezone behavior, failure handling and acceptance criteria. Implement and test the authorized behavior. Do not publish content without approval.
2. **T35 — Rejected webhook-delivery logging.** Inspect the relevant webhook handling and `orders.0025` migration context. Ensure rejected delivery attempts have the required auditable logging without incorrectly changing provider response semantics or introducing security-sensitive data into logs.
3. **T38 / PRD-063 — Slug editing.** Verify the exact product requirement, editing permissions, uniqueness constraints, collision behavior, URL compatibility and acceptance criteria. Implement only the approved behavior.
4. **Remaining Delta implementation work.** Reconcile the current plan and actual code for Admin, storefront, security, email configuration and operations. Do not presume any category is complete merely because it appears in a previous report.
5. **Site parity and storefront completeness.** Continue beyond the reviewed homepage using authorized Shopify/reference catalogue evidence and the applicable specification. Do not invent product data, content, prices, images, dilution instructions or approval status.
6. **Requirement-level evidence gaps.** Reconcile the 597-activity inventory, 73 class-E rows, 122-row decision-evidence map and all 139 original frozen acceptance criteria, including applicable amendments. Resolve actionable gaps rather than merely recounting them.
7. **Customer-record deletion.** Reconcile CR-009, AC-9.6, CR-010 and the exact HU requirement. Determine whether authorized Distributor/Bulk customer-record deletion is distinct from role removal. Preserve orders, payments, audit records and approved published revisions. Do not widen deletion or role-removal permissions without the required decision.
8. **Two-product end-to-end journey.** Implement and validate a meaningful local journey using two products and appropriate Razorpay and Shiprocket stubs where required by the approved test plan. Prove the intended workflow and business rules, and clearly distinguish stubbed behavior from real provider verification.

These items must be verified against the actual plan. Their presence here does not prove that all other work has been listed.

### Priority B — Previously identified audit concerns

Investigate these items against current code and evidence. Do not assume the earlier observations are still accurate; do not ignore them if they remain unresolved.

- The reported claim that only one code path can mark an order Delivered, associated with AC-12.9.
- The independent audit-event requirement associated with AC-26.2.
- The previously pending application of orders migration `0027`; verify the current migration graph, dependencies and authorization. Do not apply it merely because it was mentioned in a prior report.
- The reported broad GST fallback in the Zoho Inventory Sales Order adapter, where certain non-authentication/non-rate-limit HTTP 4xx responses on GST-bearing orders may retry as consumer orders. Inspect the exact implementation and narrow any fallback to explicitly understood, justified and tested GST-specific rejection cases. Do not silently convert unrelated errors into consumer orders.
- Previously reported assumptions or defaults around callback hours, date windows, order-value bands, country/state selectors and PIN-to-region mappings. Verify whether each is authorized, correctly represented and sufficiently validated; do not expand business rules by assumption.
- Monthly order-value display and the interpretation of “10,000 and above.” Reconcile against the exact approved business meaning.
- Remaining tax-inclusive/GST display conflicts involving AC-7.4, AC-9.8 and AC-10.8.
- Razorpay-specific acceptance criteria such as AC-12.7, AC-12.8 and AC-15.1. Reconcile them with the approved Zoho Payments direction without assuming that provider-specific behavior is equivalent.
- Refund execution requirements, including AC-16.5, and the existing staff/provider-dashboard process.
- Content parity, legal/privacy/terms/cookie approvals, contact-form decisions, email-provider setup, media storage, catalogue values and any remaining external-provider prerequisites.
- Any outstanding CI, browser, sandbox or integration validation that was previously omitted, misreported or deferred.

For each concern, report the current finding, exact evidence, impact, disposition and next action. If a concern is no longer valid, show why. If it is valid and actionable, resolve it when authorized.

### Priority C — Requirements, decisions and operational dependencies

Inspect the complete implementation plan for other required work that is not listed above.

Distinguish between:

- Work that can be implemented now.
- Work that can be tested locally or with mocks.
- Work requiring an existing sandbox.
- Work requiring external configuration or provider evidence.
- Work requiring business approval or an HU+DI decision.
- Work that is truly outside the approved scope.

Do not confuse “waiting for an external dependency” with “nothing else can be done.” Complete the independent work that remains available.

## 6. PRESERVE THE APPROVED PROVIDER DIRECTION AND EXTERNAL-SYSTEM SAFETY

### Zoho Payments

Hu has confirmed the Zoho Payments sandbox direction is working. Preserve that direction. Do not revert to Razorpay or reopen the provider choice without a concrete, evidenced defect or explicit HU+DI decision.

Earlier environment audits found that only some required Zoho Payments environment variables were present, the sandbox flag was absent, and production India defaults could apply. A Django development server had also been started before a token was updated.

Treat these as historical findings to reconcile with the current implementation and authorized evidence. Do not assume that a refresh token alone proves the adapter is fully configured.

Inspect environment variable names, configuration paths, safe redacted diagnostics and application behavior as appropriate. Never print or expose secrets.

Do not perform live provider writes, real payment operations, production credential changes or production webhook registrations without explicit authorization.

### Zoho Inventory and Shiprocket

Preserve the established Zoho Inventory and Shiprocket setup and Zoho-managed workflow. Hu has confirmed the sandbox handoff setup is complete and the existing workflow is intentional.

Investigate only specific outstanding acceptance gaps or concrete defects, such as inbound delivery-status evidence, scope validation or integration behavior. Do not redesign or replace the workflow simply because another approach seems easier.

Hu explicitly instructed that the Zoho Inventory OAuth helper token file be left in place and that its copied token not be rechecked. Do not inspect, verify, delete or suggest deleting that helper token file unless Hu subsequently asks.

Never reveal credentials, tokens, signing keys, webhook secrets or sensitive environment values in logs, reports or commits.

### External side effects

Without explicit authorization, do not:

- Create or modify real payment, shipment, customer or financial records.
- Send real customer emails, WhatsApp messages or other communications.
- Perform live provider writes or irreversible external operations.
- Delete real provider, financial or business records.
- Change provider configuration in production.
- Publish catalogue content, blog posts, SEO drafts or scheduled content.

Sandbox or mock work must use the appropriate safe environment and be labelled accurately.

## 7. BUSINESS RULES AND UNRESOLVED DECISIONS

Respect the current approved business rules, including:

- GST-inclusive pricing as approved, while reconciling unresolved calculation/display conflicts through the proper decision process.
- GST Number plus Name handling for applicable invoice treatment.
- Product titles, quantities and final diluted volume.
- Combo discount behavior: the first item receives no discount; subsequent items receive the applicable discount; if the first item is deleted, the next item becomes the first.
- No COD baseline unless explicitly changed by an approved decision.
- The established refund/replacement limitations and approval boundaries.
- Email and WhatsApp rather than SMS for the approved communication direction.
- The existing marketing roles and budget permissions.
- The distinction between preserving order/payment/audit history and deleting eligible customer records.
- The no-payment/no-dispatch rule and the prohibition on stale catalogue content.

Verify exact wording and applicability in authoritative records before implementing nuanced rules.

Do not invent or infer missing:

- Product dilution values or instructions.
- GST calculations, HSN codes or tax interpretations.
- Product weights or dimensions.
- Catalogue descriptions, prices, images or approval status.
- Legal, privacy, retention or consent wording.
- Contact-form retention/deletion policies.
- Customer deletion or role-removal authority.
- Order-value interpretation or other business defaults.

Known unresolved decisions include GST/invoice behavior, inventory mapping evidence, transactional email, contact-form policy, customer deletion/role-removal conflicts, and applicable legal/privacy approvals. Verify their current status in the decision register rather than treating this list as complete.

Keep the 15 SEO drafts and three blog drafts unpublished unless the applicable content and publication approvals have been obtained. Do not invent “Tools Required” content where the required product decision remains unresolved.

## 8. SECURITY, DATA INTEGRITY AND TEST-DATA SAFEGUARDS

Apply security and data-integrity requirements throughout development.

- Preserve authorization boundaries, CSRF protections, authentication requirements, validation and auditability.
- Do not swallow errors or convert unknown failures into successful outcomes.
- Do not log secrets, payment credentials, sensitive personal information or unnecessary provider payloads.
- Do not broaden permissions to make a workflow pass.
- Do not silently bypass security checks for testing or production behavior.
- Preserve payment/order consistency and the no-payment/no-dispatch invariant.
- Do not delete or overwrite historical business evidence merely to simplify tests.
- Use unique TESTCODE or correlation markers for test-created records.
- Use safe cleanup for test-created records only, after identifying them precisely.
- Never delete real financial/provider records without explicit authorization.
- Verify that error paths, retries, idempotency and duplicate-event behavior preserve data integrity.

Inspect all changed code and relevant surrounding paths for security implications and regressions.

## 9. REQUIRED TESTING AND EVIDENCE STANDARD

Use the approved stack: Python 3.14, Django 5.2 LTS, PostgreSQL 17, `uv`, `pytest-django`, Ruff and GitHub Actions. Do not substitute SQLite.

Choose testing according to risk and change scope:

1. Run targeted tests for each meaningful implementation change.
2. Run the appropriate integration tests for cross-module behavior.
3. Validate migrations, Django system checks, linting and formatting as applicable.
4. Use browser checks for requirements that depend on rendered behavior or user interaction.
5. Run the broader suite at meaningful integration or release-readiness checkpoints.
6. Re-run relevant validation after corrections.
7. Verify CI using actual evidence when CI is required; do not claim CI passed if the workflow has not run.

Do not automatically repeat an expensive full suite after every narrow change. Equally, do not use narrow tests as a substitute for the broader validation required at an integration checkpoint.

For every validation claim, report:

- Exact command or procedure.
- Environment and relevant constraints.
- Actual exit code or result.
- Pass/fail/skip counts where available.
- Material warnings, failures and limitations.
- Whether the result is current, historical, mocked, local, sandbox or production evidence.

Do not fabricate or reconstruct command output. Do not present a previous run as if it were run on the current commit.

A mock proves only the behavior exercised by the mock. A local test does not prove provider interoperability. A sandbox test does not prove production readiness. State these distinctions explicitly.

### Test integrity audit

Inspect for:

- Skipped, disabled, xfailed or weakened tests.
- Modified assertions that reduce the required acceptance criteria.
- Mocks or stubs substituted for real required behavior without authorization.
- Hardcoded values that conceal missing implementation.
- Broad exception handling and swallowed errors.
- Bypassed security, validation or provider checks.
- Tests that pass without actually exercising the intended path.
- TODO/FIXME/XXX/HACK markers, `NotImplemented`, bare `pass` and incomplete branches.

For each finding, determine whether it is legitimate and authorized, whether it affects acceptance, and what action is required. Fix actionable deficiencies when authorized.

## 10. NO FALSE BLOCKERS, NO SILENT SCOPE REDUCTION

Before declaring any item blocked or unavailable, investigate the relevant tools, repository files, configurations, commands, logs and permitted evidence.

Report what you attempted, the actual result, the specific missing prerequisite and what would unblock the item. Never claim that a browser, command, integration, file or capability is unavailable without checking it where checking is permitted and practical.

Do not omit work because it is inconvenient, old, difficult, time-consuming, absent from this prompt's priority list or missing from a previous agent report.

Do not mark work deferred merely to finish the task. Do not convert a required implementation into documentation alone, or replace a required integration with a mock, unless the approved requirement explicitly permits it.

If a prerequisite is genuinely unavailable, complete all independent authorized work and document the precise residual gap.

## 11. INDEPENDENT FINAL AUDIT — REQUIRED BEFORE COMPLETION

The final audit is an active verification and correction phase, not a writing exercise.

Before issuing a final completion report:

1. Re-read the complete public SSD Audit Requirement and this consolidated instruction.
2. Reconstruct the complete original task scope and authoritative implementation plan.
3. Reconcile every applicable requirement against the current requirement-to-evidence ledger.
4. Reconcile project history, decisions, specifications, change requests, status register and actual repository state.
5. Verify every DONE claim against its acceptance criteria and appropriate evidence.
6. Inspect changed files and relevant surrounding code for defects, regressions, shortcuts and security issues.
7. Review all unresolved dependencies, business decisions, provider requirements and evidence gaps.
8. Identify and complete any remaining safe, authorized, independently actionable work discovered by the audit.
9. Run the appropriate validation after any corrections and record actual results.
10. Update the required continuity records and status/evidence registers without staging or committing them.
11. Recheck Git state and ensure that no unauthorized publication or destructive action occurred.
12. Ensure the final report agrees with the actual repository and evidence—not with the outcome you hoped to achieve.

Do not declare the overall task complete if any applicable requirement remains incomplete, if required verification remains outstanding, or if a mandatory decision is unresolved. Report the overall outcome as PARTIAL when that is the truthful result.

A blocker or authorized deferral must be reported honestly; it must never be disguised as completion.

## 12. PROJECT CONTINUITY AND REQUIRED RECORD UPDATES

Maintain continuity so the next session can resume without reconstructing everything from chat history.

Update the applicable records, including:

- `PROJECT_LOG.md`
- `CLAUDE.md`
- `README.md`
- The Delta status register.
- The 597-activity inventory.
- The 122-row decision-evidence map.
- Relevant requirement-to-evidence records and acceptance evidence.
- Other authoritative project records identified during scope reconstruction.

Record actual changes, validation performed, results, unresolved issues, decision dependencies, relevant repository state and the next authorized milestone.

Do not overwrite historical evidence or falsely rewrite history to make the latest status look cleaner.

Keep private Claude session logs private and out of Git until the website is online, in accordance with the project rules.

Do not stage or commit continuity updates. Do not clear or discard session context before the records needed for continuity have been safely preserved.

At a safe checkpoint, report whether the working environment has become unnecessarily resource-intensive and whether closing unused test browsers, zrok processes or unused Django/PostgreSQL/Docker windows would help. Do not interrupt active work or terminate processes without checking their purpose and obtaining any required authorization.

## 13. REQUIRED FINAL REPORT

Provide one consolidated, evidence-based report with these sections:

### A. Overall status
State DONE or PARTIAL honestly. Explain the basis for that status.

### B. Complete requirement ledger
Provide the complete item-by-item implementation-plan and acceptance-criteria reconciliation, or an accessible, directly identified project artifact containing the complete ledger. Include all applicable items, not just the priority list in this prompt.

### C. Historical and decision reconciliation
Summarize the project direction reconstructed, applicable authoritative decisions, status-register discrepancies, superseded decisions and unresolved conflicts.

### D. Implemented changes
List exact changed paths and explain the behavior implemented. Separate new implementation from pre-existing and HU-approved work.

### E. Validation and test integrity
Report actual commands, exit codes, test counts, warnings, failures, skipped tests and environment limitations. Separate current results from historical results and mocks from real sandbox or production verification.

### F. Shortcuts, defects and regressions
Report findings concerning stubs, mocks, hardcoded values, TODOs, incomplete branches, swallowed exceptions, weakened tests, security bypasses and other implementation gaps. State their disposition and evidence.

### G. Completion-claim reconciliation
Identify material prior completion claims that were verified, corrected or found unsupported. Explain discrepancies without concealing errors or making unsupported claims about intent.

### H. Blockers and unresolved decisions
For each item, state the evidence, what was attempted, what remains blocked, who or what must unblock it, and the next action. Distinguish genuine blockers from work that can still proceed.

### I. Provider and operational readiness
Report Zoho Payments, Zoho Inventory, Shiprocket, email and other relevant integration status separately. Clearly distinguish configuration, code implementation, local tests, sandbox verification and production verification.

### J. Repository state and authorization compliance
Report branch, HEAD, working-tree state, relevant changed/staged/untracked files and any other material repository observations. Confirm only what was actually verified. Report any unexpected state or authorization concern.

### K. Continuity records
List the records updated, what was preserved and where the next session should resume.

### L. Remaining risk and next authorized milestone
Identify the highest-risk unresolved requirements and recommend the next actionable step. Do not disguise outstanding work behind a long list of successful tests.

The report must make it possible for HU+DI to independently verify what is complete, what remains incomplete, what evidence supports each claim and what decision or action is needed next.

---

## 14. FINAL GOVERNANCE RULE

The objective is not to produce a favorable report, maximize the number of passing tests, or finish this prompt's listed items while overlooking the actual project scope.

The objective is to implement the approved EffyKlean requirements correctly, preserve the governing architecture and business decisions, validate the result with appropriate evidence, and maintain an accurate project record.

Be proactive within your authority. Investigate before reporting blockers. Complete safe and authorized work. Preserve unrelated and approved changes. Escalate genuine decisions through HU+DI governance. Never invent facts, approvals, test results or completion.

**Do not ask HU to repeat information already available in authoritative project records. Do not stop after the first substantial batch. Do not declare completion until the complete applicable scope has been reconciled and the mandatory independent audit has been performed.**

Start with the public SSD Audit Requirement, reconstruct the actual current project state, build the complete scope ledger, and proceed in dependency-aware order.
