# EffyKlean — Implementation Continuation (18 Oct 2026)

Continue implementation in the existing repository using the frozen SPEC v0.8, approved architecture, Delta plan, HU decisions, task inventory, status register and historical evidence. **Implement remaining authorized work; do not repeat completed reviews.**

## Execute

1. Preserve the working tree, approved homepage changes, `config/settings/local.py`, the reported three commits ahead of `origin/main`, and all unrelated changes. Inspect current Git status before editing. No reset, discard, broad staging, commit, push, publication, deployment or destructive cleanup.

2. Complete remaining authorized tasks in dependency order, prioritizing:
   - T41 — scheduled publication.
   - T35 — rejected-delivery log.
   - T38 / PRD-063 — slug editing.
   - Remaining authorized Delta-plan work across Admin, storefront, security, email configuration and operations.
   - Website parity beyond the already-reviewed homepage, using existing Shopify comparison and catalogue evidence.

3. Complete outstanding requirement-level evidence for the 597 activities, 73 class-E rows, 122-row evidence map and 139 frozen acceptance criteria. Preserve original IDs and history. Reuse valid evidence; never equate an area test with acceptance of every related requirement.

4. Resolve customer deletion correctly: compare CR-009 / AC-9.6 with HU’s recorded requirement. Implement authorized Distributor/Bulk customer-record deletion if distinct from business-role removal. Preserve orders, payments and audit records. Stop only if an actual frozen-spec conflict remains.

5. **Zoho Payments:** HU confirms the sandbox works. Preserve the integration and successful evidence. Continue only outstanding authorized acceptance work; do not repeat successful tests or classify it as awaiting Zoho Support.

6. **Zoho Inventory + Shiprocket:** HU confirms the Shiprocket integration through Zoho Inventory sandbox is complete. Preserve the existing Zoho-managed workflow and evidence. Do not reopen integration design or repeat successful provider tests. Complete only specific remaining acceptance gaps.

7. Keep local end-to-end acceptance using the existing two-product, TESTCODE journey and `tests/test_local_acceptance.py`. Enforce **NO PAYMENT → NO DISPATCH**. Use local stubs where appropriate and label stub evidence accurately. No unapproved provider writes, stock changes, shipments, live transactions or production operations.

8. Continue independent work despite blocked tasks. Preserve existing decisions and data: do not invent product/dilution/tax/HSN/weight/dimension values; keep 15 SEO drafts and three blog drafts unpublished; do not add “Tools Required” without the outstanding content decision; do not send real emails without authorization and credentials; no paid hosting/media provisioning.

## Validation and governance

- Use Python 3.14, Django 5.2 LTS, PostgreSQL 17, `uv`, pytest-django, Ruff and GitHub Actions. No SQLite.
- Run targeted tests for narrow changes and broader/full suites at meaningful integration gates. Reuse valid results when relevant code is unchanged. Never claim a test or CI run that did not occur.
- Preserve TESTCODE/audit mechanisms and the dry-run cleanup report. Do not delete real provider records.
- Follow existing decisions. For a genuine frozen-spec/architecture conflict, new business decision, material security/data-integrity risk or unauthorized external/destructive operation: STOP → REPORT → HU+DI DECIDE. Park only the affected task and continue independent work.
- Do not stage or commit. Never use `git add -A`.

## Finish

Update existing `PROJECT_LOG.md`, `CLAUDE.md`, `README.md`, Delta status register, 597-activity inventory, 122-row evidence map and relevant evidence records. Keep the private Claude session log out of Git.

Provide **one final evidence-based report** listing:
- Completed task IDs, changed paths and validation evidence.
- Implemented but unvalidated work.
- Every outstanding task, its exact blocker/dependency and next action.
- Tests run and results, reused evidence and limitations.
- Separate Zoho Payments, Zoho Inventory, Shiprocket and email status.
- Actual Git/working-tree state and continuity updates.
- The next actionable implementation milestone.

Do not claim completion while authorized, independently actionable tasks remain. At the end, display one Windows completion message and play one system sound if supported; report any limitation honestly.

**Start implementing from the current state. Preserve completed sandbox integrations, avoid redundant work, and finish with one consolidated report.**
