## Current status reconciliation — 23 October 2026 (supersedes prior totals)

The 245-row BUILD ledger has 83 unique items marked `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. All 83 DONE rows are mapped to Implemented in the 597-item primary disposition because the implementation and test evidence is recorded for each. External/provider/legal/operational follow-ups remain explicitly recorded as gates; they are not misrepresented as completed. In particular, MF-089's code and tests are implemented, but the host still must schedule the contact-retention job and HU legal review of wording remains outstanding. Therefore MF-089 is counted as Implemented at code/feature level, not as operationally scheduled or legally approved.

**Current 597-item primary-disposition totals: 340 Implemented + 160 BUILD + 10 LATER + 9 INVESTIGATE + 78 EXCLUDE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; MA-ORD-103 and MA-ORD-105 remain DEFERRED as implementation items but are EXCLUDE from current scope, leaving 160 active BUILD items (62 PARTIAL + 98 DEFERRED). The 83 reviewed DONE rows and their recorded evidence, limitations, and follow-ups are mapped in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv). The 22-Oct primary register and 18-Oct snapshot remain historical records; apply the current reconciliation overlay for future counts. This does not authorize production writes, deployment, provider actions, or implementation of deferred rows.

---

## Current status reconciliation — 23 October 2026 (supersedes 22-Oct totals)

The per-item BUILD ledger contains 245 unique IDs: 83 are `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. Reconciliation against the 597-item primary-disposition register promotes all 83 verified-DONE BUILD rows to `Implemented`. MF-089 is counted as `Implemented` at code/feature level; the host must still schedule the contact-retention job and HU legal review of wording remains outstanding. These external gates are not claimed complete. No item was promoted based on aggregate arithmetic alone; each promotion is listed in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv) with its row-level implementation, resolved-path, validation, evidence and limits.

**Current 597-item primary-disposition totals: 340 Implemented + 160 BUILD + 10 LATER + 9 INVESTIGATE + 78 EXCLUDE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; MA-ORD-103 and MA-ORD-105 remain DEFERRED as implementation items but are EXCLUDE from current scope, leaving 160 active BUILD items (62 PARTIAL + 98 DEFERRED). This is the current count to use in future queries. The 22-Oct 597-row register and the 18-Oct source snapshot remain preserved as historical evidence; apply the 23-Oct reconciliation overlay for the current status. This does not authorize production writes, deployment, provider actions or work on deferred rows.

---

# EffyKlean — HU+DI reconciliation of ten INVESTIGATE records

Date: 2026-10-22



HU submitted responses for all ten records on 2026-10-22. This reconciliation records the directions and resulting handling. It does not authorize implementation, delegation, deployment, production/provider writes, paid resources, or changes to external systems.

| Record | Reconciled status / handling | HU direction and constraints |
|---|---|---|
| MF-002 | INVESTIGATE — identify exact local working-tree evidence | HU asked what the reported “28 paths” are. The category labels alone are insufficient. Obtain exact local Git status and changed-path evidence before explaining/classifying them. Preserve the tree; no stage, commit, reset, stash, clean, or delegation. Preserve the HU-approved homepage-link rearrangement and keep unrelated changes separate. |
| MF-004 | VALIDATION PENDING — dependent on MF-002 baseline identification | HU selected “Validate after baseline established.” First identify committed baseline versus uncommitted changes; then choose proportionate validation. Do not claim the prior uncommitted-tree run proves the committed baseline. |
| MF-005 | REMOTE PERMISSION CHECK — no remote action authorized | HU selected “Identify exact remote permission if needed.” Identify the precise repository/workflow permission and intended change. Do not modify remote workflow/repository settings without explicit authorization. |
| MF-006 | INVESTIGATE — audit existing evidence first; no automatic re-observation | HU challenged why re-observation is required and who requested it. Compare existing Shopify Admin observations and the 12-Oct decision ledger against the specific unanswered question. Re-observe only if a concrete material evidence gap or staleness is demonstrated and the required signed-in session is available. Request provenance is not established by the register row; do not attribute it to a person/agent without evidence. |
| MF-007 | VALIDATION PENDING — relevant-page comparison | HU selected “Complete relevant-page comparison.” Compare relevant rendered pages on desktop/mobile and accessibility/functional parity, record concrete differences, and distinguish defects from Shopify-only features. Respect existing scope and dependencies. |
| MF-008 | HU CONFIRMED IMPLEMENTED — primary disposition corrected in working register | HU states the EffyKlean distributor enquiry is already implemented and is a form. Do not ask again whether it is a form. This is HU confirmation; independent code/runtime verification has not been performed in this reconciliation. Preserve the ID and correct the stale/misframed status when the working register can be safely updated. |
| MF-009 | EVIDENCE ONLY — no implementation absent an established requirement | HU selected evidence-only. Competitor/reference observations do not create scope. Implement only if evidence identifies a requirement already present in the frozen SPEC or an authoritative existing project decision; stop for HU+DI if a genuine conflict arises. |
| MF-050 | INVESTIGATE — specific behavior only | HU selected “Investigate before disposition.” Investigate signed-in cross-device cart persistence against existing account decisions, reference behavior, and frozen architecture. Do not reopen the general customer-account scope decision; present a recommendation only if a real unresolved behavior decision remains. |
| MA-ORD-037 | INVESTIGATE — continuation confirmed; no BUILD authorization | HU reaffirmed “Continue INVESTIGATE.” Existing 22-Oct direction is retained. Resolve evidence/policy questions before proposing a disposition; investigation is not implementation approval. |
| MA-USR-020 | RECONCILE AGAINST EXISTING LEDGER — composite row, no blanket new question | HU asked what the row is and who is asking. Map its components against ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md (Staff users section). Existing direction says active staff list is covered; POS-app-only and Requests-tab functions were excluded. Preserve the source ID; separate/trace components and ask no broad repeat question. Register-row provenance does not establish a specific author. |

### Cross-cutting reconciliation rules

- An INVESTIGATE count is not a count of new HU questions. Separate scope decisions from evidence, validation, access, and authorization tasks.
- Do not attribute a request to a named person or agent unless the source record proves provenance.
- Do not repeat questions answered by the canonical 122-capability master or the 12-Oct HU+DI decision ledger.
- The working CSV has now been updated and re-fetched. Commit `a5ecf972ee5a291557b5bf223b916d7e89e3a616`. Verified: 597 data rows, 22 columns, 597 unique IDs, each of the ten target IDs appears once, no non-target rows changed, and all ten original source columns are unchanged. MF-008 is now primary disposition Implemented based on HU confirmation; code/runtime verification remains separate. 22-Oct primary counts were 257 Implemented, 245 BUILD, 10 LATER, 9 INVESTIGATE, 76 EXCLUDE; current 23-Oct counts are 340 Implemented, 162 BUILD, 10 LATER, 9 INVESTIGATE, 76 EXCLUDE. The immutable 18-Oct snapshot is unchanged.
- No code, local working tree, external system, or provider state was changed. No agent was delegated.

