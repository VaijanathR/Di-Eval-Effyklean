## Authoritative row-level status correction — 23 October 2026

This note supersedes any conflicting aggregate totals or “unreconciled” claims elsewhere in this file. The current fetched source files have been compared by unique ID.

- **597-ID register:** 597 rows / 597 unique IDs. Current dispositions: **340 Implemented, 152 BUILD, 74 EXCLUDE, 17 LATER, 14 INVESTIGATE** (597 total).
- **245-ID implementation ledger:** 245 rows / 245 unique IDs. Implementation outcomes: **83 DONE (verified), 62 PARTIAL, 100 DEFERRED** (245 total). Current dispositions within those 245 IDs: **83 Implemented, 141 BUILD, 13 LATER, 8 EXCLUDE** (245 total).
- All 83 verified DONE rows remain promoted to Implemented. Exact-ID comparison: every one of the 245 ledger IDs exists in the 597 register; **zero disposition mismatches**. The 597 response crosswalk also matches the 597 register by ID and current disposition.
- The earlier “163 pending” figure is not current: 62 PARTIAL + 100 DEFERRED = **162**. Of these, **141 are current BUILD** (61 PARTIAL + 80 DEFERRED); **21 are not BUILD** (1 PARTIAL and 12 DEFERRED are LATER; 8 DEFERRED are EXCLUDE).
- **Coverage gap before implementation handoff:** 11 additional IDs are marked BUILD in the 597 register but are not in the 245-row implementation ledger: MF-070, MF-071, MF-074, MF-078, MF-092, MF-107, MF-109, MF-114, MA-ORD-068, MA-DSC-023 and MA-SET-061. They need explicit ledger coverage; do not assume implementation status or evidence.
- MF-055 policy is approved and recorded; it remains PARTIAL / BUILD pending implementation and scoped sandbox validation. MF-084 legal wording still needs Hu/legal confirmation; MF-094 needs source/spec parity investigation before any narrow question; MF-115 is a release evidence gate, not a new policy question. These are distinct from the 83 already implemented.

Historical totals below are retained only as historical record and must not be used as current status.

---

## Current status reconciliation — 23 October 2026 (supersedes prior totals)

The 245-row BUILD ledger has 83 unique items marked `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. All 83 DONE rows are mapped to Implemented in the 597-item primary disposition because the implementation and test evidence is recorded for each. External/provider/legal/operational follow-ups remain explicitly recorded as gates; they are not misrepresented as completed. In particular, MF-089's code and tests are implemented, but the host still must schedule the contact-retention job and HU legal review of wording remains outstanding. Therefore MF-089 is counted as Implemented at code/feature level, not as operationally scheduled or legally approved.

**Current 597-item primary-disposition totals: 340 Implemented + 152 BUILD + 74 EXCLUDE + 17 LATER + 14 INVESTIGATE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; its current dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE. The 11 additional BUILD IDs outside that ledger are listed in the authoritative status correction above and need per-ID ledger coverage before implementation handoff. This does not authorize production writes, deployment, or provider actions.

---

## Current status reconciliation — 23 October 2026 (supersedes 22-Oct totals)

The per-item BUILD ledger contains 245 unique IDs: 83 are `DONE (verified)`, 62 `PARTIAL`, and 100 `DEFERRED`. Reconciliation against the 597-item primary-disposition register promotes all 83 verified-DONE BUILD rows to `Implemented`. MF-089 is counted as `Implemented` at code/feature level; the host must still schedule the contact-retention job and HU legal review of wording remains outstanding. These external gates are not claimed complete. No item was promoted based on aggregate arithmetic alone; each promotion is listed in [CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv](./CURRENT_597_STATUS_RECONCILIATION_2026-10-23.csv) with its row-level implementation, resolved-path, validation, evidence and limits.

**Current 597-item primary-disposition totals: 340 Implemented + 152 BUILD + 74 EXCLUDE + 17 LATER + 14 INVESTIGATE = 597.** The 245-row implementation ledger remains 83 DONE (verified), 62 PARTIAL and 100 DEFERRED; its current dispositions are 83 Implemented, 141 BUILD, 13 LATER and 8 EXCLUDE. The 11 additional BUILD IDs outside that ledger are listed in the authoritative status correction above and need per-ID ledger coverage before implementation handoff. This does not authorize production writes, deployment, or provider actions.

---


❯ where is this file BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md?                                                                                                                                                 
  Ran 1 shell command

● The file is at:

  /mnt/d/effykleanproject/docs/foundation/BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md

  It is 429 lines (about 20 KB) and is committed in the repository, so it is also on GitHub under docs/foundation/. Its contents are the decisions and inputs that the 62 PARTIAL and 100 DEFERRED records are
  waiting on.

  One caveat: I generated it on 22-Oct, before I changed the ledger counts to 83 DONE / 62 PARTIAL / 100 DEFERRED. The record-by-record ledger, BUILD245_LEDGER_2026-10-22.csv in the same folder, is current. If
  you want the two to agree, I can regenerate the decisions file from the ledger.

✻ Crunched for 10s · done 9:20 AM

❯ where is the per item build ledger? is it in .md file?                                                                                                                                                           
  Listed 1 directory

● The per-item ledger is a CSV file, not a Markdown file:

  /mnt/d/effykleanproject/docs/foundation/BUILD245_LEDGER_2026-10-22.csv

  It has 245 rows, one per BUILD record, plus a header row. It is about 165 KB and is committed and pushed. Open it in Excel or LibreOffice. These are its columns:

  - id
  - domain
  - requirement
  - primary_status, which is DONE (verified), PARTIAL or DEFERRED
  - reason_category
  - work_package
  - implemented_behaviour
  - code_paths
  - validation_executed
  - evidence_type
  - unmet_or_limits
  - next_action
  - code_paths_resolved

  I used CSV because 245 rows with 13 columns can be filtered and sorted there. The same folder holds two Markdown companions: BUILD245_IMPLEMENTATION_RECORD_2026-10-22.md for the summary, and
  BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md for the decisions. If you'd prefer a readable per-item .md version of the ledger, I can generate one from the CSV.

✻ Crunched for 10s · done 9:27 AM
                                                                                                                                                                           ✔ Update installed · Restart to update
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────❯ o