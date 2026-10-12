# EffyKlean Functionality Audit and Implementation Roadmap

**Status:** Working audit record — HU+DI review pending  
**Audit date:** 12 October 2026  
**Repository:** `Di-Eval-Effyklean`  
**Scope:** Functionality, operational capability, integrations, and storefront experience  
**Governance:** HU+DI

## 1. Purpose

Maintain one consolidated, evidence-linked record comparing the existing reference platforms with EffyKlean Admin and EffyKlean.in. Identify genuine gaps, distinguish implementation from verification, reconcile conflicting evidence, record HU+DI decisions, and produce a prioritised implementation roadmap after the audit stages are complete.

This document is the working decision and roadmap record. The detailed comparison documents and source evidence remain the supporting evidence; they should not be unnecessarily duplicated.

## 2. Audit sequence

The audit must proceed in this order.

### Stage 1 — Shopify Admin vs EffyKlean Admin
Compare relevant administrative functionality, business operations, permissions, reporting, content management, and integration management. Identify gaps and conflicts against the frozen EffyKlean specification and architecture.

### Stage 2 — BRMChemicals.com vs EffyKlean.in
Compare customer-facing business functionality and functional flows, identifying relevant differences and gaps without assuming that every competitor feature is required.

### Stage 3 — effyklean.com vs effyklean.in
Compare storefront functional flows, product presentation, media, CSS, HTML, responsive behaviour, and UI/UX.

**Stage gate:** Complete the current stage's evidence review and HU+DI scope decisions before beginning the next stage. Do not jump ahead or combine the three comparisons into one undifferentiated review.

## 3. Governance and decision rules

1. The frozen EffyKlean specification, approved architecture, architecture decisions, and recorded HU+DI decisions remain authoritative.
2. A capability present in Shopify or another reference website is not automatically an EffyKlean requirement.
3. A comparison report's recommendation is not an approval.
4. Preserve existing decisions accurately. In particular, DEFER is not REJECT.
5. Do not classify a feature as missing solely because an inventory or readiness register says it is missing. Check implementation and decision evidence.
6. Distinguish a user interface, backend implementation, simulated provider, successful local test, provider sandbox proof, and production proof. These are different evidence levels.
7. Do not treat static code inspection as equivalent to an end-to-end test.
8. Do not implement audit findings while the audit and scope decisions are in progress unless HU+DI explicitly authorises that work.
9. Do not modify frozen requirements or architecture implicitly while resolving gaps.
10. Record unresolved contradictions explicitly rather than resolving them by assumption.

**Decision protocol:** STOP → REPORT → HU+DI DECIDE whenever evidence reveals a material conflict, an ambiguous requirement, an architectural deviation, or a decision that requires approval.

## 4. Evidence sources

The following existing documents are the initial evidence base.

1. `COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md`
2. `COMPARISON_2_BRMCHEMICALS_VS_EFFYKLEAN_2026-10-12.md`
3. `COMPARISON_3_EFFYKLEAN_COM_VS_IN_2026-10-12.md`
4. `COMPARISON_4_CONSOLIDATED_GAP_REGISTER_2026-10-12.md`
5. `EffyKlean_Master_Functionality_Comparison_Evidence_Consolidation12102026-1800Hr.md`
6. Frozen specification, architecture decisions, decision records, implementation records, and applicable test evidence in the EffyKlean project repository.

Evidence documents are supporting records, not substitutes for the frozen specification or explicit HU+DI decisions.

## 5. Finding status and evidence standards

Each finding must distinguish the following dimensions.

### 5.1 Implementation status
- Implemented
- Partially implemented
- Missing
- Simulated or stubbed
- Blocked by an existing decision
- Uncertain

### 5.2 Evidence status
- Current end-to-end evidence
- Current automated-test evidence
- Current static code or route evidence
- Historical browser or test evidence
- Provider sandbox evidence
- Production evidence
- Not verified

Do not collapse implementation status and evidence status into one label.

### 5.3 HU+DI disposition
- Accept existing behaviour
- Implement
- Fix
- Defer
- Reject
- Validate further
- Block pending an existing decision or prerequisite

A proposed disposition remains a recommendation until HU+DI decides it. Existing explicit decisions must be preserved and referenced.

## 6. Stage 1 — Shopify Admin vs EffyKlean Admin

**Status:** Evidence reconciliation and HU+DI review pending.

### 6.1 Initial corrections to the comparison record

The master evidence consolidation identifies the following corrections to earlier classifications. These must be reflected in the working audit analysis.

- **ORD-007:** Order-list sorting was reported as implemented. Do not retain sorting as a missing capability without contrary evidence.
- **ORD-008:** Item-count column was reported as implemented.
- **ORD-009:** “Fulfil by” date was reported as implemented.
- **ORD-012:** Delivery-status column was reported as implemented at the Admin/UI or data-model level. This does not establish that live shipment status is received from Shiprocket.
- **CG-014:** Separate the implemented sorting capability from the remaining product, amount, and tag-filter questions.
- **ORD-010 and ORD-011:** Preserve their recorded DEFER status. Do not convert them to REJECT based on an inventory recommendation.
- **Blog Admin editor:** The editor reportedly supports pages of kind `BLOG`. The storefront `/blog/` returning 404 is a separate unresolved issue.
- **Order editing:** An order-edit route reportedly exists even though line-item and price editing are recorded as excluded. Inspect the actual behaviour and permitted fields before determining whether a conflict exists.
- **Assisted orders and bank-transfer/UPI verification:** The master consolidation cites SPEC §27.3 and §12.11 as relevant requirements. Do not reject these capabilities merely because they resemble Shopify draft orders.
- **Bulk customer savings:** The master consolidation flags customer-visible cumulative savings under SPEC §28.2. Distinguish the customer-facing requirement from internal reporting or analytics.
- **Related products:** Related-product links reportedly render, while register E-09 records them as out of scope. Reconcile the code, specification, and decision evidence before deciding the intended behaviour.
- **Outbox:** Backend outbox/worker functionality reportedly exists, but a dedicated Admin outbox-list page was not found. Distinguish backend processing from operational visibility.
- **Provider verification:** An Admin screen or mocked integration is not proof of a working external provider integration.

These are evidence-reconciliation items, not blanket implementation approvals.

### 6.2 Stage 1 findings register

Use one unique finding ID per material gap or contradiction. Link multiple capability IDs to a single finding when they describe the same underlying issue.

For each finding, record:

- Finding ID
- Capability IDs and affected Admin area
- Shopify capability and source evidence
- EffyKlean Admin behaviour and source evidence
- Implementation status
- Evidence/verification status
- Gap, parity, or conflict description
- Frozen specification, architecture, or decision reference
- Confidence and evidence limitations
- Proposed disposition and rationale
- HU+DI decision required
- Final decision, decision date, and supporting record once agreed

No final decision should be recorded until HU+DI has reviewed it, unless an existing decision record already establishes the outcome.

### 6.3 Initial Stage 1 review queue

The following items require evidence reconciliation or HU+DI review. Their inclusion does not mean they are all approved for implementation.

| Review item | Initial issue to resolve |
|---|---|
| Order-list controls | Confirm implemented sorting and separately assess product, amount, and tag filters. |
| Order export | Confirm whether export is required, its fields, and applicable data-access controls. |
| Staff comments and order timeline | Distinguish existing timeline/history from the ability to add attributed staff comments. |
| Assisted orders and bank-transfer/UPI verification | Reconcile the recorded blocker with the cited frozen-spec requirements. |
| Order editing | Establish what the existing edit route actually permits and whether it violates an explicit exclusion. |
| Bulk customer-visible savings | Establish the required calculation and customer-facing presentation under the cited specification section. |
| Related products | Reconcile the rendered links with register E-09 and the authoritative requirement/decision records. |
| Outbox visibility | Establish whether operational monitoring and retry visibility are required in Admin. |
| Staff creation/invitation and MFA reset | Preserve D-F2 and determine the permitted scope before proposing a change. |
| Provider integrations | Separate UI/backend implementation from stub, sandbox, and production verification. |
| Blog | Investigate the Admin editor and storefront `/blog/` 404 as separate capabilities. |
| Reporting and customer management | Reconcile each reported gap against current code, earlier acceptance evidence, and explicit requirements. |
| Stale inventory statuses | Recheck classifications based on historical browser walks or incomplete validation before deciding scope. |

This queue must be expanded using the existing Comparison 1 and master evidence consolidation. Do not repeat the complete discovery exercise merely to reproduce information already documented.

## 7. Stage 1 decision log

Record each substantive HU+DI decision here, including the finding ID, decision, rationale, applicable specification/decision reference, and date.

No new decisions are pre-approved by this document. Existing decisions remain in force until explicitly revised through HU+DI governance.

## 8. Stage 2 — BRMChemicals.com vs EffyKlean.in

**Status:** Not started in this working decision record.

After Stage 1 is reviewed and its scope decisions are complete, record the relevant functional-flow comparisons, supporting evidence, gaps, conflicts, and HU+DI decisions here.

Do not assume that a feature present on BRMChemicals.com is automatically required for EffyKlean.

## 9. Stage 3 — effyklean.com vs effyklean.in

**Status:** Not started in this working decision record.

After Stage 2 is reviewed and its scope decisions are complete, record functional-flow, product/media, CSS/HTML, responsive, and UI/UX comparisons here.

Keep unverified visual observations separate from code-based inference. Record any public availability, TLS, DNS, or empty-catalogue limitations that prevent a valid live comparison.

## 10. Consolidated gap register

After the three stage reviews, maintain one consolidated list of unique gaps.

Each entry must link to:
- Its originating stage and finding ID
- Applicable frozen specification or decision reference
- Existing implementation and evidence
- HU+DI disposition
- Dependencies and prerequisites
- Roadmap item, if approved

Deduplicate repeated symptoms of the same underlying gap. Do not merge distinct requirements merely because they concern the same application area.

## 11. Implementation roadmap

**Status:** Not approved; to be prepared after all three audit stages and scope decisions are complete.

The roadmap must include only work authorised by HU+DI or already required by an applicable frozen requirement and existing authorisation.

For each approved item, specify:
- Priority and business/operational rationale
- Finding and decision IDs
- Scope and acceptance criteria
- Dependencies and blocking decisions
- Implementation and test approach
- Required local, sandbox, and production evidence
- Documentation/checkpoint updates
- Explicit approval boundary

Do not begin implementation merely because a finding is labelled “high priority” in a comparison report.

## 12. Audit limitations and checkpoint discipline

Record material evidence limitations alongside the affected findings, including:
- Historical rather than current Shopify Admin observations
- Static inspection without end-to-end verification
- Stubbed or simulated providers
- Missing sandbox or production proof
- Public-site availability or TLS failures
- Empty catalogue preventing meaningful product-page comparisons
- Visual/responsive/accessibility checks not performed
- Requirements or decision references that have not yet been reconciled

Update the project checkpoint and handover records at meaningful phase boundaries. Preserve private agent/session logs outside Git in accordance with project governance.

## 13. Current checkpoint

As of 12 October 2026:

- The three comparison documents and consolidated gap register exist as supporting evidence.
- The master consolidation reports corrections and conflicts requiring reconciliation.
- Stage 1 is the active review stage.
- Stage 2 and Stage 3 are not authorised to begin before Stage 1 review is complete.
- No new implementation or scope change is approved by this audit record.
- The implementation roadmap remains pending completion of the three stages and HU+DI decisions.

**Next action:** Continue Stage 1 from the existing evidence, reconcile the known misclassifications and specification conflicts, and record HU+DI decisions before progressing to Stage 2.

