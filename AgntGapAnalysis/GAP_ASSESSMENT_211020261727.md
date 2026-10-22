# EffyKlean — Read-only project assessment, gap analysis and proposed phased implementation plan

**Assessment date:** 2026-10-21 (local time 17:27 at creation; the file name is GAP_ASSESSMENT_DDMMYYYYHHMM)
**Mandate:** the "EFFYKLEAN — EXHAUSTIVE READ-ONLY PROJECT ASSESSMENT, GAP ANALYSIS AND PHASED IMPLEMENTATION PLAN" instruction set (public repo `AgntGapAnalysis/AgenticGapAnalysis21Oct2026_2232.md`), applied together with `AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md`.
**Authorised exception:** HU allowed this one repository document in addition to the full report in chat. Nothing else was created, changed, staged, committed or pushed. This file is untracked.
**Status of this document:** a proposal for HU+DI review. It authorises nothing. Every proposed task needs separate HU+DI approval before an implementation agent receives it.

**Revision 3 (2026-10-22).** HU asked that every remaining document be read and every gap closed. All 105 test files, all `docs/` documents and all public records (except the excluded BRM capture) were read; the test suite was not run (excluded by HU). Added gaps G-69 to G-76, minor findings m17 to m21 and decisions DEC-30 to DEC-32; corrected the statement that three different Delta plan versions exist (they differ only in headers); rewrote §3, §15 and §16 to state exact coverage. **Where revision 3 differs from revisions 1 and 2, revision 3 governs.**

**Revision 2 (full-read pass, 2026-10-21 evening).** HU asked that nothing rest on agent summaries. After the first version the assessor therefore read, directly: all remaining Admin (`modules/backoffice`) views, forms, queries, commands and the template set (templates audited mechanically; see §15), settings, scripts, the migrations that matter, the 104 test bodies attached to the acceptance criteria that had been graded M, all of `ARCHITECTURE.md`, `README.md`, `PROJECT_LOG.md` (all 1,640 lines), the SPEC acceptance criteria and change-control sections in full, 26 of the 101 local `docs/` files in full, and re-cloned and read the principal public records. This revision (a) raises 80 acceptance criteria from evidence grade M to H after reading the named test bodies, (b) moves AC-6.4 from DONE to PARTIAL, (c) adds findings G-51…G-66 (plus the minor items of §8.3), decisions DEC-23…DEC-29 and the plan tasks that carry them, and (d) rewrites §3, §15 and §16 to state exactly what was and was not read. **Where this revision differs from the first version, this revision governs. It is still not a line-by-line review of every file: §15 gives the exact coverage.**

---

## 0. How to read this report

**Project statuses (exactly four):** DONE (verified), PARTIAL, NOT DONE, DEFERRED. Blocked, unverified and externally unverified conditions are explained in the notes, not as extra statuses.

**Confidence column used in the inventory (assessor's own evidence grade):**
- **H** — the assessor read the implementing code and/or the named test body (first pass: code; revision 2: the bodies of 104 tests attached to 80 criteria; revision 3: all 1,790 test functions were read, none run) and found it asserts the acceptance condition. H does not mean the assessor ran it.
- **M** — (after revision 2 only 5 rows: AC-12.20, AC-15.1, AC-22.1, AC-26.1, AC-26.3, each explained in its note) a named test exists but the body read does not establish the whole criterion; pass results are the recorded full-suite runs (see §10), not a run by the assessor.
- **L** — the only evidence is a structural, static or wording test, or an indirect/mis-attributed test. It proves a shape or an absence, not runtime behaviour.

**What "DONE (verified)" means here.** The assessor could not execute the test suite (no Docker daemon, no PostgreSQL; the assessor also chose not to create databases in a read-only assignment). DONE is therefore granted only where code and/or test bodies were read (H), or a named behavioural test exists and no contrary evidence was found (M, now rare), or the evidence is structural and the claim is itself structural (L). **No DONE item has been re-run by the assessor.** All provider evidence is mock, local-stub or (for a few Zoho items) sandbox evidence reported by earlier agents; none is production evidence.

**Evidence classes used when quoting history** (from the SSD requirement §2): (1) executed and observed by the assessor in this task; (2) existing evidence that remains applicable; (3) reported by an agent or record and not independently checked; (4) inference.

---

## 1. Executive assessment and principal conclusions

**Overall status: PARTIAL.** The project is a large, disciplined local build of a Django/PostgreSQL storefront, Admin and integration layer. It is not production-ready and cannot honestly be called complete against the frozen SPEC v0.8 (+ CR-004…CR-009), the frozen ARCHITECTURE, or HU's 18 October direction that all 597 planned activities be accounted for and implemented.

What is genuinely strong (evidence class 1 or 2 unless stated):
1. A coherent B2C journey exists in code: catalogue → cart → checkout → provider payment session → order created only from the provider's own record → outbox-driven Zoho Sales Order → cancellation with 20% charge. Order creation is idempotent and guarded (`modules/orders/payment_flow.py:124-215, 298-365`, read by the assessor).
2. Production settings fail closed (stubs, console e-mail, local media, missing Zoho settings, TESTCODE and sandbox flags all raise at start-up: `config/settings/production.py`, read).
3. The test suite is large and, where read, meaningful: **2,491 tests collected** (assessor ran `pytest --collect-only`, 8.8 s); by AST analysis only 5 of 1,790 test functions contain neither an assert nor a `pytest.raises` (all benign: configuration-loads and migration-smoke tests), and there are no skip/xfail markers and no `assert True`; no skip/xfail markers; no TODO/FIXME/NotImplemented markers in application code; ruff check and ruff format --check pass on 331 files and `manage.py check` reports no issues (all three run by the assessor with no cache writes).
4. No secrets are tracked; no credential-pattern hit in 138 commits other than a fake test value.

The principal problems, in order of severity (details §8–§9):
1. **The Zoho-managed shipment and delivery lifecycle does not work with the real adapter, and every feature that depends on it is dead in production.** `integrations/zoho_inventory.py:737-741` makes `request_fulfilment` always raise; the only writer of delivery status is a stub-only Admin simulation (`modules/backoffice/order_actions.py:345-380`, refuses unless `LOCAL_PROVIDER_STUBS`); no inbound feed exists. Consequences, all verified in code: no shipment/tracking link, no Shipped/Out for Delivery/Delivered, B2C replacement requests impossible (they need `Shipment.delivered_at`), the saved-address reset never fires, and **customer cancellation stays open after Zoho/Shiprocket has really dispatched** because the cutoff is "local Shipment row CREATED". (G-01, G-02)
2. **Frozen-spec conflicts that agents parked but that no CR resolves:** GST (SPEC §7.9/7.10/13.14 versus `modules/orders/tax.py`), HSN/cost master data held locally (SPEC §13.9/AC-13.6), Razorpay-worded criteria (AC-12.7/12.8/15.1), refund execution (AC-16.5), copy-as-is content (AC-23.1). (G-04, G-13, G-14, G-16, G-44)
3. **Spec-required capabilities not built and not formally deferred:** bank-transfer/UPI with Admin verification (SPEC §12.10-12.11), assisted orders (§27.3), rule-based combos and fixed bundles (§21.2-21.4), transactional e-mail (§20.2, AD-14), privacy/terms/cookie consent (§23.2, §26.2), Zoho invoice number/status in Admin (AC-13.8). (G-03, G-05, G-06, G-12, G-15)
4. **Nothing is deployed or provisioned; hosting, staging access gate, scheduler, monitoring, DB TLS and media storage are all open.** (G-07, G-08, G-24, G-38, G-39)
5. **Repository and governance state is fragile:** 113 uncommitted paths (89 modified, 24 untracked, including migrations 0025-0027), HEAD three commits ahead of `origin/main`, and **eight commits already pushed carry a `Co-Authored-By` trailer** in breach of the project's mandatory no-co-author rule. CI has run 12 times (7 success, 5 failure) but never on the current tree, and several records wrongly say CI "never ran". (G-09, G-10)
6. **Security findings (Medium):** guest order lookup/cancel (`/track/`) has no throttle; customer sign-in throttle uses the default per-process cache; no edge rate limiting; no dependency or security-lint scanning in CI. (G-11, G-49)
7. **Documentation drift:** CLAUDE.md/README/PROJECT_LOG carry many contradictory "latest state" paragraphs; the public mirror's status register, AC index and 122-row map copies differ from local; one AC is credited by a parser unit test (AC-9.9). (G-20, G-21)

**Counts (item-level tables follow; these counts are a summary, not a substitute):** 147 SPEC acceptance criteria: 110 DONE (verified) (87 at confidence H, 3 at M, 20 at L), 25 PARTIAL (22 H, 2 L, 1 M), 11 NOT DONE, 1 DEFERRED (revision 2: AC-6.4 moved from DONE to PARTIAL; 80 criteria raised from M to H after the test bodies were read). 597 planned activities (agent reconciliation, mapped to the four statuses in Appendix A): 259 DONE, 25 PARTIAL, 3 NOT DONE, 310 DEFERRED (of which 148 are explicit "do not build" decisions). 60 non-AC deliverables: see §6B.

**Added by revision 2 (principal new findings, all confirmed by direct reading):**
8. **HU's recorded NO on customer-initiated cancellation contradicts the frozen SPEC and the built feature (G-51).** `ORD-064` is NO in the decision ledger, the Delta plan §6 and the reconciliation record ("no customer cancellation or editing after order placement; Admin-only"), while SPEC §16.1-16.3/AC-16.1-16.3 give the B2C customer a 20%-charge cancellation and the build offers it on `/track/`. Two further NO-listed capabilities were built (ORD-019 amount filter; returned-package inspection ORD-076, which SPEC §14.10 itself requires). The governing records say such a conflict must be reported, not resolved by an agent.
9. **No way exists to record fulfilment or tracking in production (G-52).** HU's YES decisions ORD-080/081 (Admin marks fulfilled, adds tracking or leaves it blank for local pickup) are not built, and the only delivery writer is stub-only, so with the real Zoho adapter nothing can ever show tracking or Delivered.
10. **Production never writes products or customers to Zoho, and new customers cannot reach Zoho orders (G-53)**, because the write gate allows only a stub or a declared sandbox and the customer mapping needs an existing Zoho contact.
11. **Every product list, product page, cart and checkout step calls Zoho live, uncached (G-54)**, against Zoho Inventory limits that the project log records as 100 requests a minute for this account and that Zoho's published FAQ (read in the first pass, evidence class 3) sets at 1,000-5,000 calls a day on the lower plans (the account's plan is not recorded); HU's own desired model (change-triggered sync plus hourly reconciliation) is not built.
12. **A test added in the uncommitted tree reads a gitignored file (G-59)** and will fail on every clean checkout/CI run; `media/` is entirely untracked.
13. **Customer accounts can be pre-registered by anyone and then inherit a business role (G-55)**; there is no password reset (G-56).
14. **The 15 published products carry an MRP that was imported from Shopify's compare-at price with an "assume" flag (G-61)**, which AC-6.4 forbids without verification.
**Added by revision 3 (all confirmed by reading):**
15. **Production Zoho item mapping has no sanctioned path (G-69):** development ids are SKU-code placeholders and the only mapping command is sandbox-only.
16. **No owner for sending the GST invoice to customers (G-70), no rule for paid-but-unconfirmed orders (G-71), no recorded decision on disputes/chargebacks (G-74), and order corrections can edit e-mail and GST fields beyond the DC-08 recommendation (G-76).**
17. **Availability, RPO and RTO targets are undefined although AD-17 requires them before production (DEC-30); 99.5% is not an approved SLO.** Address validation is format-only (G-75). The FAQ-with-videos question is closed by HU's 19-Oct 04:51 IST decision.

**Single most valuable next step:** HU+DI decide the Zoho-managed shipment/delivery model (G-01) and the GST rule (G-04), and rule on the customer-cancellation conflict (G-51); each gates large amounts of otherwise finished work.

---

## 2. Local repository baseline (evidence class 1 unless stated)

| Fact | Observed value | How obtained |
|---|---|---|
| Path | `/mnt/d/effykleanproject` (accessible; no substitution) | `ls`, `git` |
| Branch / HEAD | `main` / `625e2102335a3e9b4a094466fb260fd023050fe8` ("docs: backup and restore procedure with a verified local drill, responsive and load check (2026-10-17)") | `git rev-parse` |
| Remote | `origin` = `https://github.com/VaijanathR/EffyKleanProject.git` (private: unauthenticated API returns 404; authenticated `git ls-remote` and `gh` work) | `curl`, `git ls-remote`, `gh` |
| Upstream | `origin/main` = `513fc98` (2026-10-17 18:57 UTC); `git ls-remote origin` returned the same SHA. HEAD is **3 commits ahead, 0 behind** (`02aeb80`, `7a13cf8`, `625e210`) | `git log origin/main..HEAD`, `ls-remote` |
| Working tree | **113 paths: 89 modified, 24 untracked; 0 staged; 0 stashes.** Tracked diff: 89 files, +2,025 / −229 | `git status --short`, `git diff --stat` |
| Untracked (24) | 5 docs/content items, 2 discovery docs, `RECONCILED_597_STATUS_2026-10-18.csv`, 4 foundation docs (`AC_EVIDENCE_PASS`, `AUDIT_LEDGER`, `CONSOLIDATED_REPORT`, `RUN_RECORD`), `modules/backoffice/audit_outbox.py`, `check_email_config.py`, **migrations `orders/0025`, `0026`, `0027`**, `enquiry_form.py`, `contact-us.jpg`, 4 new test files, `test_product_list_filters.py` | `git status` |
| Modified (89) | CLAUDE.md, PROJECT_LOG.md, README.md, `config/settings/base.py`, `local.py`, status register, AC docs, `integrations/zoho.py`, `zoho_inventory.py`, ~30 `modules/*` files, ~45 tests | `git status` |
| Ignored but present | `.env`, `.env.phoenix`, `AI-LLM-conversations/`, `ChatwithCGPT_LLMmd`, `modules/backoffice/management/commands/seed_hu_admin_test.py` (hard-coded local test password), `media/` (1.3 GB). None is tracked (`git ls-files` confirmed) | `git status --ignored`, `du` |
| Commits | 138, all authored `VaijanathR <vaijnath_r09@yahoo.com>`; **8 carry `Co-Authored-By`**: 38175b3, e30d19e, e213b1a, 8601602, a45a033, 4fe5767, 94df6e3, 93222e3 (the frozen SPEC/ARCHITECTURE baselines); the 3 unpushed commits carry none | `git log --grep` |
| Size | 514 tracked files; non-migration Python: backoffice 15,807 lines, orders 8,102, storefront 5,852, catalogue 3,477, integrations 1,919, identity 1,075, config 865, scripts 549; tests 33,473 lines in 106 files | `wc` |
| Migrations | backoffice 3, catalogue 11, identity 5, orders 27 (0025-0027 untracked) | `ls` |
| Stack | Python ≥3.14,<3.15; Django ≥5.2.8,<5.3; psycopg 3; django-otp; boto3/django-storages; gunicorn; dev: pytest, pytest-django, ruff | `pyproject.toml` |
| Tests | 2,491 collected (assessor, `pytest --collect-only`, dummy `DB_*` values on the command line, `.env` untouched) | command run |
| Static checks run by assessor | `ruff check --no-cache` → "All checks passed!"; `ruff format --check --no-cache` → "331 files already formatted"; `manage.py check` (test settings, dummy env) → "no issues (1 silenced)" | commands run |
| Test execution | **Not run.** `docker ps` → cannot connect to `/var/run/docker.sock`; no listener on 5432/55434/8000/8001 at check time | commands run |
| CI | `.github/workflows/ci.yml` runs `scripts/ci.sh` (uv sync --locked, ruff check/format, `manage.py check`, `makemigrations --check --dry-run`, pytest) on PostgreSQL 17. `gh run list`: **12 runs, 7 success, 5 failure** (2026-10-16 → 2026-10-17); last run succeeded on `513fc98`. CI has **never run on the 3 unpushed commits or the working tree**. No `check --deploy`, dependency audit or security-lint step | `gh run list` |
| Dev server | None listening during this assessment (an earlier report said pid 19615 was left on :8000) | `ss` |

The assessor's own state check at the end of the assessment is recorded in §16.

---

## 3. Public GitHub repository baseline (evidence class 1)

`https://github.com/VaijanathR/Di-Eval-Effyklean` is public, default branch `main`, **75 commits**, last push 2026-10-21 17:05 UTC (`83c6efa`, "Add exhaustive read-only EffyKlean gap analysis instructions"). The assessor cloned it into the session scratch directory (outside the project) and read the tree (128 entries, `git/trees?recursive=1`, not truncated). It contains decision/analysis records, agent instructions and responses, hosting plans, saved Shopify checkout HTML (`checkoutCart/`, ~80 asset files), and no application source, SPEC.md, ARCHITECTURE.md or PROJECT_LOG.md.

**Records read by the assessor (revision 2; "full" means every line was read in this assignment).**

*Read in full:* `AgentInstructionByHuDI/EffykleanSSD_Audit_Requirement.md`, `AgntInst_18Oct2026_1958.md`, `Original_AgntInst_19Oct2026_1233.md`, `DigiOcn_InstructionsForAgnt_19Oct25_1306.md`, `Hosting/AgntInstDigiOcnImplmntatn_19OCT2026_1505.md`, `AgntGapAnalysis/AgenticGapAnalysis21Oct2026_2232.md` (this assignment's own instruction text, not a prior analysis); `HUDI Discussion/RESP_18OCT_QA_HU ANSWERS.md` (items 1-20 and the approved corrections), `RESP_18OCT2026_1149.md`, `EffyKlean_Delta_Implementation_Execution_Decisions_ActionPlan_13102026122932.md`, `12 Effyklean HUDI CHAT- Delta Implemenation plan13Oct2026.md`, `13 Effyklean- Hudi - Actual Implementations part 1 - 15OCt2026_1713.md`, `DIGITAL OCEAN HOSTING PLAN 21OCT2026_1504.md`; `HU_DI_DECISIONS_AND_RESUME_CHECKPOINT_2026-10-13.md`, `HU_DI_GOLDEN_RULES.md`, `ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md`, `CONFLICT_RECONCILIATION_ANALYSIS_2026-10-12.md`, `EFFYKLEAN_PHASE_WISE_IMPLEMENTATION_PLAN_DRAFT_2026-10-13.md`, `docs/audit/EFFYKLEAN_FUNCTIONALITY_AUDIT_AND_IMPLEMENTATION_ROADMAP.md`, `security/EffyKlean_Storefront_CSP_Proposal_2026-10-16.md`; `Hosting/FinalDigitalOCeanImplementationHostingPlan19Oct2026_1424.md`, `Hosting/Hosting_Decision_DigitalOcean_Observation.md`, `Hosting/AgentRespDigiOcnHosting_19OCT26_1436.md`; `AgentImplementationRecords/DiReview_AgentResponse18Oct26_1651.md`, `AgentREsp_DIgitalOceanSetup_18Oct26_1708.md`, `19Oct2026/CONSOLIDATED_REPORT_2026-10-19.md` (identical to the local copy).

*Read in revision 3 (previously partial or unread):* `HU_DI_122_CAPABILITY_DECISION_AND_REFINEMENT_MASTER_2026-10-16.md` (sections 1-7 and the amendment register read; its Appendices A, B and C were diffed against the standalone ledger, conflict analysis and evidence map and differ by four lines each, i.e. headings only); `19Oct2026/AgntRespEffyImplmntn19OCT2026_1751.md`, `AgentResponse18oct2026_2210.md` (1,879 lines), `AgentRespDigiOCN_Setup19Oct2026_1925.md`; the 17 Oct HU-DI chat (HTML text extracted, 3,571 lines; the PDF is a byte-identical duplicate); the master comparison transcript and `COMPARISON_1-4` (byte-identical to the local copies, diffed).

*Diffed, not re-read:* the public Delta plan copies (63,016 and 62,106 bytes) against the local reference copy (63,664 bytes): they differ only in provenance headers and a status note (4 and 12 differing lines), so they are one plan. The public status register, AC index and ROW122 copies are older than the local files.

*Excluded by HU instruction (2026-10-22):* the saved Shopify checkout HTML and its ~80 asset files under `checkoutCart/` (static third-party capture).

---

## 4. Local-versus-public discrepancies and limitations

| # | Discrepancy | Evidence | Effect |
|---|---|---|---|
| D-1 | The **private repository holds the governing documents** (SPEC, ARCHITECTURE, PROJECT_LOG, CLAUDE.md, code); the public mirror holds decisions, instructions and copies of reports. An agent reading only the public repo cannot see SPEC or code | tree listing | A recorded blocker ("HU's item-18 text is not on this machine") was avoidable: the text is public and readable by `curl` (G-17) |
| D-2 | Public `AgentImplementationRecords/EffyKlean_Delta_Implementation_Status_Register.md` is 274 lines; the local copy is 362 | `wc`, `cmp` | Public register is older |
| D-3 | Public `docs/foundation/ROW122_DECISION_EVIDENCE_MAP_2026-10-16.md` is the 133-line 16 Oct version; the `19Oct2026/` copy (480 lines) equals the local file | `wc`, `cmp` | Two public versions of one record |
| D-4 | Public `19Oct2026/AC_TEST_INDEX.md` differs from the local (modified) index although both have 165 lines | `cmp` | Index regenerated after publication |
| D-5 | `AUDIT_LEDGER_2026-10-19.md`, `RUN_RECORD_2026-10-18.md`, `RECONCILED_597_STATUS_2026-10-18.csv` and `PROJECT_LOG.md` are **not** published | tree listing | The public record lacks the item-level 597 file and the audit ledger |
| D-6 | Local records say "CI never run / nothing pushed" (CONSOLIDATED_REPORT, AUDIT_LEDGER, status register A-05, PRODUCTION_READINESS_REGISTER A-05 "MISSING") although GitHub shows 12 CI runs, last success 17 Oct on `513fc98` | `gh run list` | Records are wrong; the real gap is that CI has not run on the current tree |
| D-7 | CLAUDE.md's older state paragraphs say `main = origin/main = 162543a`; actual `origin/main` is `513fc98` | CLAUDE.md vs `ls-remote` | Superseded paragraphs remain in the file, flagged "SUPERSEDED IN PART" |
| D-8 | `docs/foundation/DEPLOYMENT_PREREQUISITES_2026-10-17.md` lists product images/evidence as local-disk-only; `modules/catalogue/media.py` and `storefront/site.py:520-535` now read from S3 when `MEDIA_STORAGE_BACKEND=s3` | code | Doc older than code |
| D-9 | The instruction set cites "139 acceptance criteria"; SPEC §33 now holds **147** (139 at the v0.8 freeze plus CR-004…CR-008 additions) | `ac_ids` count | Different baselines; both numbers are legitimate when labelled |

**Limitations of this reconciliation:** the assessor could not see the private repository's GitHub web UI (no browsing of Actions logs or PR history), only `git`, `gh run list` and the clone of the public repo. Remote refs other than `origin/main` do not exist (`git branch -r` shows only `origin/main`).

---

## 5. Reconstructed intended scope and decision history

**Purpose (SPEC §1, CLAUDE.md):** a new, independent EffyKlean e-commerce site for www.effyklean.in, matching and exceeding effyklean.com (Shopify), with EffyKlean as system of record; Zoho as authority for stock, GST, invoicing; Zoho Payments for payment; shipping through Zoho→Shiprocket; Indian market only; B2C, Distributor/B2B and Bulk/Institutional segments.

**Timeline (from PROJECT_LOG headings and the public records):**
1. 2026-10-03: project initiated; Shopify discovery; P0-1…P0-9 and FD-A…FD-C decisions; SPEC v0.1.
2. 2026-10-04: v0.2-v0.4 (FD-D…FD-F), **v0.4 frozen**; CR-001 (Shiprocket lifecycle) then **CR-002: COD removed, all orders prepaid** → v0.7 frozen; architecture decision review AD-01…AD-17.
3. 2026-10-05: CR-003 (SKU model, amount-based combo, slabs, reporting) → **SPEC v0.8 frozen** (`8601602`). 2026-10-06: `ARCHITECTURE.md` frozen (`a45a033`); Foundation Authorization Gate (`94df6e3`).
4. 2026-10-06/07: F-01B…F-07B and I-01…I-04 accepted by HU+Di. CR-004 (catalogue revisions, availability vocabulary), CR-005 (₹500 only with an additional discount).
5. 2026-10-09/11: Razorpay Phase 1 verified once in test mode; large Admin build (Shopify Admin mapping, 494 capabilities); CR-006 (Distributor pricing simplified), **CR-007 (Zoho Payments replaces Razorpay)**, CR-008 (replacement video), CR-009 (Director-only role removal).
6. 2026-10-12/13: three-way comparison; Delta Implementation Plan; HU+DI authorise "controlled local implementation" under the Delta plan (not production, not live providers); sandbox-first sequencing.
7. 2026-10-14…10-17: 55-task Batch 1 (not formally accepted); Zoho Inventory sandbox work (items, contacts, Sales Orders SO-00002…5, all reported evidence); first real Zoho Payments sandbox payment (reported); media storage, own policy pages, Shopify-independence changes; backup drill; CI first runs and pushes (`513fc98`).
8. 2026-10-18: HU answers items 1-20; agent continuation (T35, forms, 597/122 reconciliation).
9. 2026-10-19: HU+DI consolidated instruction and SSD audit requirement; audit pass (GST fallback narrowed, AC-26.2 event); DigitalOcean hosting readiness and Zoho shipment-lifecycle investigations (read-only).
10. 2026-10-21: hosting plan with Definitions of Done accepted by HU; this assessment instruction published.

**Binding today:** frozen SPEC v0.8 + CR-004…CR-009; frozen ARCHITECTURE and AD-01…AD-17 (AD-10 NO PAYMENT → NO DISPATCH, AD-11 no stale catalogue, AD-16 secret hygiene); Foundation gate scope; HU+DI Delta-plan authorisation (local, sandbox; no production); HU answers of 18 Oct; the mandatory no-co-author rule (CLAUDE.md); STOP → REPORT → HU+DI DECIDE.

**Superseded:** Razorpay (CR-007; wording retained historically), COD (CR-002), Distributor slabs/quarterly pricing (CR-006), combo percentage rule (CR-003), prepaid RTO/attempt rules (CR-002).

**Explicitly deferred or excluded by record:** CSP enforcement (report-only), T41 scheduled publication, T38 slug edit, draft orders/duplicate order (ORD-091, DC-22), wishlist/reviews/server cart (register §Excluded), 148 of 597 rows by explicit NO decisions, Shiprocket sandbox testing (HU item 16, "leave for later"), legal pages until HU supplies text, SMS, rewards.

**Unresolved decisions that remain open (non-exhaustive; full list §14):** GST display/arithmetic; DC-22 bank/UPI and assisted orders; DC-33 combo rule model; shipment/delivery model under Zoho; Admin deletion of Distributor/Bulk customers; coupon-versus-combo precedence; related-product links (MF-026); access gate for staging; separate staging settings module.

**Agent assumptions not authorised, or authorised only as working defaults:** extra staff capabilities held by both roles (T12), auto-archive default 7 days, enquiry-form defaults (call hours 9-17 IST, 1-60 day window, India-only country, order-value bands "10,000 and above" read as 10,000-25,000, 36-state/PIN table sampled against India Post for 95 PINs only), the combo-wins-unless-customer-picks-coupon precedence, the Shipping-page sentence about delivery calls, the Admin "(range)" band wording. All are recorded by the agents as awaiting HU.

---

## 6. Complete requirement and deliverable inventory

The inventory has three parts: **6A** every SPEC §33 acceptance criterion (147), **6B** every non-AC deliverable, governance, integration and operational obligation the assessor identified (60), **6C** the 597 planned activities (item level in **Appendix A**). Each item carries one project status. Dependencies and decisions are in the notes and in §11/§14. Related finding IDs (G-nn) are defined in §8-§9.

### 6A. Acceptance criteria (SPEC §33; source: `SPEC.md` lines 1101-1289, index `docs/foundation/AC_TEST_INDEX.md`)

Closure evidence for every item that is not DONE: the criterion's task in §12 (cross-reference in §11). Where the notes say "mock", the behaviour has never been observed against a real Zoho/Shiprocket system.

| ID | Requirement (abridged from SPEC §33) | Status | Conf | Basis |
|---|---|---|---|---|
| AC-1.2 | The platform operates with no runtime dependency on Shopify. | DONE (verified) | H | assessor grep of modules/integrations/config found no Shopify reference; static test |
| AC-2.1 | The platform supports India-only operation in INR with no international payment, tax, currency o | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-5.1 | The business roles are exactly B2C Customer, Distributor, Bulk/Institutional Customer, Admin, Di | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-5.2 | Active specification and customer-facing text use the term Customer Care. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-6.1 | Each commercial size/format (Household 1 L, Bulk 5 L) is a separate product/SKU; one product doe | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-6.2 | Different fragrances of the same product and size are individual SKUs; quantities, prices and di | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-6.3 | Each orderable SKU stores MRP, B2C Sale Price, EffyKlean Product ID and Zoho Item ID/SKU. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_mrp_and_sale_price_stored_as_decimal_two_places`. Decimal(12,2) storage test; the other fields are covered by the catalogue model tests. |
| AC-6.4 | Shopify compare-at price is not used as MRP without product-data verification. | PARTIAL | H | The importer refuses without an explicit acknowledgement (test read), but the 15 published products were imported WITH `--assume-compare-at-as-mrp`; no MRP verification is recorded and no provisional marker exists (G-61). |
| AC-6.5 | A product with no valid Zoho mapping cannot be ordered, is recorded internally as "Unavailable — | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unmapped_sku_is_not_customer_visible_and_needs_no_provider` |
| AC-6.6 | "Unavailable — Zoho mapping missing" and "Out of Stock" remain distinguishable internal states w | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_sku_without_zoho_mapping_cannot_be_ordered`, `test_unmapped_unknown_and_unpublished_are_indistinguishable` |
| AC-6.7 | Any available product can be purchased by B2C, Distributor/B2B and Bulk/Institutional customers; | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_every_customer_type_can_buy_both_product_formats`. Guest, Distributor and Bulk can all add both a household-format and a bulk-format product. |
| AC-6.8 | A product is customer-orderable only if it has a current PUBLISHED catalogue revision and author | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_f06_orderability_requires_a_published_revision`, `test_sku_without_a_current_publication_is_not_orderable` |
| AC-6.9 | Customer-visible availability is exactly one of AVAILABLE (published and authoritatively availab | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_mapped_available_and_unavailable`, `test_unmapped_unknown_and_unpublished_are_indistinguishable` |
| AC-6.10 | Each PUBLISHED catalogue revision is reviewed at least every three calendar months (calendar-mon | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_review_queue_lists_due_and_overdue_reviews` |
| AC-7.1 | A B2C price follows MRP → Sale Price → at most one of Combo/Promo → ₹500 check (only when that a | DONE (verified) | H | assessor read modules/orders/pricing.py and checkout.price_cart |
| AC-7.2 | The displayed B2C price is GST-inclusive and no GST is added after the final payable amount is d | DONE (verified) | H | assessor read modules/orders/tax.py (GST extracted from the tax-inclusive amount, 9+9 or 18) |
| AC-7.3 | No separate shipping charge appears at checkout for any segment. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-7.4 | GST is calculated on the Sale Price and a discount is applied only to the Sale Price component w | NOT DONE | H | tax.py extracts GST from the discounted amount paid; SPEC 7.9/7.10/13.14 keep GST on the undiscounted Sale Price. Frozen-spec conflict, no CR (STOP-REPORT) |
| AC-8.1 | A guest can complete a B2C purchase without creating an account. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_guest_checkout_is_unchanged_and_creates_an_unlinked_order` |
| AC-8.2 | A B2C order to which an additional discount is applied and whose discounted value is below ₹500  | DONE (verified) | H | assessor read modules/orders/pricing.py and checkout.price_cart |
| AC-8.3 | B2C checkout requires email, phone, name, delivery address and payment information. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_contact_and_address_validation_blocks_the_purchase`. Tests block an invalid e-mail, mobile, PIN and address line; the 'payment information' element is satisfied by the payment step, not asserted here. |
| AC-9.1 | A Distributor applicant can be approved, rejected or sent a request for information, and each ac | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_status_changes_are_saved_and_audited_with_a_note` |
| AC-9.2 | A rejected applicant receives no Distributor pricing. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_rejected_or_unapproved_applicant_gets_no_business_account_or_pricing` |
| AC-9.3 | *(CR-006)* A Distributor discount is a percentage above 0 and below 100 that applies overall, to | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_rounding_is_to_the_paisa_half_up`, `test_percentages_outside_the_boundaries_are_refused` |
| AC-9.4 | *(CR-006)* Exactly one rule applies per product (product, else category, else overall); rules ne | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_without_an_active_rule_the_price_is_the_sales_price`, `test_the_most_specific_rule_wins_and_rules_never_stack` |
| AC-9.5 | *(CR-006)* An Admin proposes a rule or a change; a different Director approves it; a proposal ha | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_proposal_changes_no_price_until_it_is_approved`, `test_nobody_approves_their_own_proposal`, `test_a_rejected_proposal_needs_a_reason_and_has_no_effect` |
| AC-9.6 | *(CR-006)* Business pricing applies only to an account whose business role is active; roles are  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_suspended_business_account_is_deleted_only_after_the_role_is_removed` |
| AC-9.7 | Each pricing change records proposer, scope, target, percentage, status, approver, date/time, an | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_business_price_is_shown_everywhere_and_charged_on_the_order`, `test_a_pricing_change_records_who_what_when_and_the_rule_it_replaced`, `test_orders_package_contains_only_authorized_files`. Caveat: the rule applied to each line is kept in the payment-attempt snapshot JSON (`business_rule_id`, `business_percent`), not in an order-line column. The 'Covers AC-9.7' tag on `test_orders_package_contains_only_authorized_files` is incidental (a migration comment) and is not evidence. |
| AC-9.8 | The Distributor sees the final applicable price, GST-exclusive, with the MRP unchanged. | PARTIAL | H | final price shown; prices are tax-inclusive, SPEC requires GST-exclusive display (GST decision open) |
| AC-9.9 | Distributor orders offer no combos, no B2C promotions, no COD and require 100% advance payment. | PARTIAL | L | index credit is spurious: only test_ac_index.py (parser fixture) names it; behaviour partly covered by tests tagged AC-21.5/12.3 |
| AC-9.10 | A Distributor has no website option to cancel; for any cancellation request they are directed to | DONE (verified) | H | assessor read operations.customer_cancellation_status |
| AC-10.1 | A Bulk quotation request accepts products and quantities only and no customer-entered price or d | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_bulk_enquiry_form_has_no_price_field_and_no_cod`, `test_bulk_enquiry_refuses_extra_fields_such_as_a_proposed_price` |
| AC-10.2 | A Bulk proposal is prepared by Admin, approved or rejected by a Director, and accepted by the cu | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_the_customer_sees_and_accepts_their_quote_without_internal_details`, `test_admin_prepares_a_director_approves_and_every_step_is_audited` |
| AC-10.3 | The agreement stores products, agreed quantity, negotiated price/discount and validity period an | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-10.4 | An agreement never generates an order automatically; the customer initiates each recurring order | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_the_customer_sees_and_accepts_their_quote_without_internal_details` |
| AC-10.5 | After expiry there is no automatic extension and the customer buys at the B2C Sale Price. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_validity_is_the_whole_last_day_in_india_time_and_never_extends` |
| AC-10.6 | An order above the agreed quantity still receives the negotiated price; products outside an acti | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_an_order_above_the_agreed_quantity_still_gets_the_negotiated_price` |
| AC-10.7 | The customer sees the B2C Sale Price and the negotiated price, no internal negotiation details,  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_covered_product_takes_the_quote_and_no_rule_a_other_product_takes_the_rule`, `test_cumulative_savings_are_shown_and_a_withdrawn_quote_leaves_orders_unchanged` |
| AC-10.8 | Bulk prices are displayed GST-exclusive; the final payable amount is shown before payment; payme | PARTIAL | H | see AC-9.8 |
| AC-10.9 | A new Bulk/Institutional customer can progress Bulk Enquiry/Application → EffyKlean Review → Acc | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_new_bulk_customer_goes_from_enquiry_to_order_without_a_b2c_account`. A full journey test: enquiry, staff provisioning, set-password, quote, order, with no B2C account at the start. |
| AC-10.10 | A Bulk/Institutional customer has no website option to cancel; for any cancellation request they | DONE (verified) | H | assessor read operations.customer_cancellation_status |
| AC-10.11 | Admin can approve/process a normal Bulk order with no negotiated price or discount arrangement;  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_admin_prepares_a_director_approves_and_every_step_is_audited`, `test_a_normal_bulk_order_needs_no_approval_and_a_rejection_is_audited` |
| AC-10.12 | Orders placed under an active approved negotiated arrangement within its validity period require | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_the_state_machine_and_the_no_self_approval_rule`, `test_cumulative_savings_are_shown_and_a_withdrawn_quote_leaves_orders_unchanged`, `test_a_replacement_arrangement_prices_nothing_until_approved_and_accepted` |
| AC-11.1 | Adding an item to the cart does not reserve stock. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_order_payment_shipment_or_reservation_is_created`, `test_cart_never_calls_the_provider_for_a_quantity_or_reserves` |
| AC-11.2 | Stock is checked at checkout and again immediately before order confirmation. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_stock_unavailable_blocks_before_any_order_or_payment` |
| AC-11.3 | If stock becomes unavailable before confirmation, confirmation is blocked, the customer is told  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_stock_unavailable_means_no_payment_no_order_no_shipment`, `test_stock_unavailable_blocks_before_any_order_or_payment` |
| AC-11.4 | When required Zoho inventory confirmation is unavailable, order confirmation does not proceed an | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_stock_unavailable_at_payment_creates_no_order_and_takes_no_payment` |
| AC-11.5 | The final payable amount is shown before payment. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_review_shows_everything_before_payment` |
| AC-11.6 | An order is not confirmed merely because a payment attempt was initiated. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_order_exists_until_the_payment_is_verified`, `test_a_provider_outage_on_return_keeps_the_hold` |
| AC-12.1 | A B2C customer pays 100% of the order through Razorpay before the order is confirmed; no COD, "2 | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_order_exists_until_the_payment_is_verified`, `test_no_cod_wording_exists_in_customer_facing_rules` |
| AC-12.2 | A B2C order is confirmed only after Razorpay confirms the full payment. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_verified_payment_creates_exactly_one_order`, `test_a_confirmed_payment_webhook_places_exactly_one_order` |
| AC-12.3 | No customer type can pay any part of an order on or after delivery: Distributor/B2B and Bulk/Ins | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_order_exists_until_the_payment_is_verified`, `test_no_cod_wording_exists_in_customer_facing_rules` |
| AC-12.4 | Customer non-availability, inability to receive, failure to coordinate with the courier or to co | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund`. Covered by the single unsuccessful-delivery journey test (no refund, no cancellation, no replacement). |
| AC-12.5 | Distributor/Bulk can pay by Razorpay, bank transfer or UPI. | NOT DONE | H | bank transfer/UPI and PAYMENT_PENDING_VERIFICATION not built; decision DC-22 open; no authorised deferral in SPEC |
| AC-12.6 | A bank-transfer/UPI payment enters PAYMENT_PENDING_VERIFICATION, becomes PAYMENT_CONFIRMED only  | NOT DONE | H | bank transfer/UPI and PAYMENT_PENDING_VERIFICATION not built; decision DC-22 open; no authorised deferral in SPEC |
| AC-12.7 | For each Razorpay payment the platform retains status, amounts, reference, charges, taxes on cha | NOT DONE | H | written for Razorpay settlement/charges; Zoho Payments settlement and charges are not retrieved or shown (order page says so) |
| AC-12.8 | Admin sees Customer Amount Paid → Razorpay Charges/Taxes → Net Amount per order for Razorpay pay | NOT DONE | H | written for Razorpay settlement/charges; Zoho Payments settlement and charges are not retrieved or shown (order page says so) |
| AC-12.9 | Delivery follows the Shiprocket/courier delivery process; the order/shipment is marked DELIVERED | PARTIAL | H | only one writer of delivery status exists (verified) but it is a stub-only Admin simulation; no inbound feed exists |
| AC-12.10 | A courier's physical return of an undelivered prepaid shipment does not by itself create a refun | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund` |
| AC-12.11 | The platform has no COD collection, COD settlement or COD reconciliation requirement or function | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-12.12 | No additional customer charge, refund or forfeiture rule is defined or applied by reason of an u | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund` |
| AC-12.13 | A returned undelivered prepaid shipment is recorded as a physical return event distinct from can | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_only_a_handed_over_shipment_that_is_not_delivered_can_be_recorded` |
| AC-12.14 | EffyKlean neither assumes nor enforces a universal number of delivery attempts for any shipment, | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-12.15 | No refund, forfeiture or payment outcome depends on Shiprocket/courier status or reason data dis | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund` |
| AC-12.16 | *(CR-007)* With Zoho Payments, an order exists only after the provider's own record shows a capt | DONE (verified) | H | assessor read the named test body; asserts the acceptance condition |
| AC-12.17 | *(CR-007)* A payment with no confirmed result keeps the customer's retry on hold with a "do not  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_provider_outage_on_return_keeps_the_hold` |
| AC-12.18 | *(CR-007)* A duplicate or replayed provider event creates no second order, payment or shipment;  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_confirmed_payment_webhook_places_exactly_one_order`, `test_invalid_untrusted_or_unusable_webhooks_are_rejected_and_change_nothing`, `test_unknown_and_unusable_events_are_acknowledged_without_effect` |
| AC-12.19 | *(CR-007)* A partial, mismatched or reversed payment never places an order and stays visible to  | DONE (verified) | H | assessor read the named test body; asserts the acceptance condition |
| AC-12.20 | *(CR-007)* Provider secrets never appear in the repository, logs, screens or errors. | DONE (verified) | M | named test body read (pass 2): test_refused_sign_in_is_an_auth_error_and_never_echoes_secrets, test_secrets_never_reach_the_error_text. Adapter-level tests read (error text never echoes the client secret or refresh token); logs/screens not traced. |
| AC-13.1 | Karnataka intra-state transactions carry CGST 9% + SGST 9%; other Indian states IGST 18%; no tax | DONE (verified) | H | assessor read modules/orders/tax.py (GST extracted from the tax-inclusive amount, 9+9 or 18) |
| AC-13.2 | GSTIN and GST/Company Name entered at checkout are stored on the order and sent to Zoho with all | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_intra_state_uses_the_cgst_sgst_group_and_gst_number_is_sent` |
| AC-13.3 | When no GST details are supplied the order proceeds as a consumer transaction with no GST detail | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_optional_gst_and_company_fields_are_stored`, `test_confirm_creates_a_sales_order_with_the_mapped_payload`. Tests: stored None without GST; adapter sends `gst_treatment: consumer`. |
| AC-13.4 | When Zoho rejects supplied GST details the order proceeds as a consumer transaction with no GST  | PARTIAL | H | named test bodies read in pass 2 (assert the criterion): `test_a_gst_rejection_places_a_consumer_order_and_logs_it_on_the_order`, `test_rejected_gst_details_fall_back_to_a_consumer_order_once`, `test_a_rejection_that_does_not_name_gst_is_not_turned_into_a_consumer_order`. Narrowed 19 Oct: fallback only for a GST-naming rejection; tests: one fallback, an unrelated 4xx not converted, a second rejection fails, INFO event kept. Real Zoho rejection text never observed. |
| AC-13.5 | The platform does not make or override the final GST treatment; invoice generation and numbering | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-13.6 | Product GST/HSN/tax data are read from Zoho and no local authoritative tax master exists. | PARTIAL | H | Sku.hsn_code exists locally (HU 18-Oct: keep fields; report-only comparison with Zoho); SPEC/AC say no local tax master; SPEC not amended |
| AC-13.7 | When required Zoho tax data is unavailable for a Distributor/Bulk order, the final payable amoun | NOT DONE | H | Distributor/Bulk payable amount is computed locally by tax.py; no Zoho tax lookup or guarded unavailable path |
| AC-13.8 | The Admin order view shows the Zoho GST invoice number and invoice status. | NOT DONE | H | needs invoices.READ scope and Zoho invoice automation; not shown in Admin |
| AC-13.9 | The Zoho tax configuration used for EffyKlean orders yields CGST 9% + SGST 9% for Karnataka intr | PARTIAL | H | named test bodies read in pass 2 (assert the criterion): `test_karnataka_delivery_is_cgst_plus_sgst`, `test_other_indian_states_are_igst`, `test_delivery_outside_karnataka_uses_igst_on_the_sales_order` |
| AC-14.1 | Availability displayed is derived from Zoho; no local authoritative stock quantity exists. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_product_aggregate_and_sku_is_unchanged`, `test_availability_reads_item_stock` |
| AC-14.2 | A mapped product with quantity > 0 is internally Available and with quantity 0 is internally Out | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_mapped_available_and_unavailable`, `test_availability_reads_item_stock`. Adapter-level test (stock >= quantity, inactive item unavailable); real Zoho stock unobserved (G-42). |
| AC-14.3 | If payment succeeds but stock confirmation fails, the payment and order are preserved in an expl | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_zoho_outage_after_payment_is_visible_preserved_and_recoverable` |
| AC-14.4 | During a Zoho outage the platform shows no invented availability and preserves already-created/p | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_zoho_outage_after_payment_is_visible_preserved_and_recoverable` |
| AC-14.5 | Orders carry both EffyKlean and Zoho product identifiers. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-14.6 | A package returned to EffyKlean through the delivery process (including an undelivered shipment  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_inspection_decisions` |
| AC-14.7 | A returned product found damaged or otherwise unsuitable for resale is not automatically restore | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_inspection_decisions` |
| AC-15.1 | Every order supports traceability EffyKlean Order → Razorpay Payment → Razorpay Settlement → Zoh | PARTIAL | M | Order, payment, Zoho order shown; settlement, invoice and real shipment links absent |
| AC-15.2 | The Admin order view shows ORDER, RAZORPAY, ZOHO and SHIPROCKET groups and identifies the origin | PARTIAL | H | named test bodies read in pass 2 (assert the criterion): `test_order_page_groups_items_by_the_system_they_come_from` |
| AC-15.3 | Historical order pricing remains unchanged after any price or discount change. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_historical_order_price_survives_catalogue_price_change`, `test_historical_price_is_protected_through_http` |
| AC-15.4 | A paid order whose Zoho sync fails is held in ZOHO_SYNC_PENDING, retried up to 3 times, then mov | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_transient_failure_retries_then_exhausts_after_three_total_attempts`, `test_a_paid_order_creates_exactly_one_sales_order_and_a_repeat_creates_none`, `test_a_withheld_write_gate_sends_nothing_and_keeps_the_paid_order` |
| AC-16.1 | Before Shiprocket handover a B2C customer can cancel; after handover normal customer cancellatio | PARTIAL | H | cutoff keyed to local Shipment.status CREATED; under the real Zoho adapter that never happens (cancellation stays open after real dispatch) |
| AC-16.2 | For a B2C order paid in full, a cancellation before handover deducts 20% of the amount paid and  | DONE (verified) | H | assessor read the named test body; asserts the acceptance condition |
| AC-16.3 | For a B2C order (prepaid in full) the charge equals 20% of the amount actually paid at the time  | DONE (verified) | H | assessor read the named test body; asserts the acceptance condition |
| AC-16.4 | A Distributor/Bulk customer cannot cancel through the website and is directed to Customer Care;  | DONE (verified) | H | assessor read operations.customer_cancellation_status |
| AC-16.5 | For a permitted B2C cancellation the remaining eligible amount is refunded through the original  | PARTIAL | H | refund amount computed and recorded; execution is manual by decision (conflicts with criterion wording) |
| AC-16.6 | Every cancellation decision and charge is present in the order audit trail. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_cancel_post_cancels_records_and_audits` |
| AC-16.7 | No normal return or product refund flow is offered; customer non-availability, failure to collec | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund` |
| AC-16.8 | Customer cancellation, unsuccessful delivery (customer non-availability or failure to receive),  | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unsuccessful_delivery_then_returned_package_inspection_opens_no_refund` |
| AC-16.9 | The pre-handover B2C cancellation rule (AC-16.1–AC-16.6) and the damaged/incorrect-product repla | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_tracking_offers_cancellation_before_handover`, `test_a_replacement_request_within_24_hours_is_received`. Test only shows the cancel offer renders before handover; the real-handover signal is G-02. |
| AC-17.1 | A damaged or incorrect product reported by a B2C, Distributor/B2B or Bulk/Institutional customer | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_customer_request_is_recorded_with_the_product_and_never_auto_approved` |
| AC-17.2 | A B2C, Distributor/B2B or Bulk/Institutional customer can initiate a replacement request through | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_replacement_request_within_24_hours_is_received` |
| AC-17.3 | *(CR-008)* A video of the product at delivery or unpacking is required (photos may support it);  | DONE (verified) | H | assessor read the named test body; asserts the acceptance condition |
| AC-17.4 | The replacement window runs from an actual delivery and does not apply to an unsuccessful delive | PARTIAL | H | window runs from Shipment.delivered_at, which no production path ever sets |
| AC-17.5 | A replacement request received more than 24 hours and up to 72 hours after delivery is decided b | PARTIAL | H | window runs from Shipment.delivered_at, which no production path ever sets |
| AC-17.6 | The customer-facing policy states the 24-hour window and does not present the 24–72 hour excepti | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_after_24_hours_the_customer_is_sent_to_customer_care_without_an_entitlement`, `test_replacement_page_states_24_hours_with_evidence`. The test asserts the 24-hour wording AND 'photos or a video', which conflicts with CR-008 (video required) and SPEC 17.2 (website or Customer Care): see G-63. |
| AC-18.1 | Shipments are created and tracked through Shiprocket, including shipment/AWB reference, shipment | NOT DONE | H | no Shiprocket shipment creation or status feed through the real adapter (request_fulfilment raises) |
| AC-18.2 | If Shiprocket is unavailable the order is retained, fulfilment is marked pending (ORDER_READY →  | PARTIAL | H | works with the labelled local stub; real Zoho-managed handoff has no creation/inbound path |
| AC-18.3 | Only verified/confirmed payments enter fulfilment, and no separate shipping charge is added to a | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_payment_no_dispatch_even_if_a_paid_order_loses_its_successful_payment`, `test_no_payment_no_dispatch_in_the_worker` |
| AC-18.4 | A B2C customer sees the status progression Order Confirmed → Processing → Shipped → Out for Deli | PARTIAL | H | works with the labelled local stub; real Zoho-managed handoff has no creation/inbound path |
| AC-18.5 | Once the shipment is created, the customer receives the relevant Shiprocket tracking details/lin | PARTIAL | H | works with the labelled local stub; real Zoho-managed handoff has no creation/inbound path |
| AC-18.6 | Customer-facing exceptional statuses are simplified (for example Cancelled, Replacement, Deliver | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_customer_facing_status_mapping` |
| AC-18.7 | Normal delivery communication and delivery attempts are handled by Shiprocket/courier; exception | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-18.8 | An order whose delivery is unsuccessful is shown to the customer as "Delivery Unsuccessful"; the | PARTIAL | H | works with the labelled local stub; real Zoho-managed handoff has no creation/inbound path |
| AC-19.1 | B2C account creation is optional and an account provides order history and account information. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_an_order_placed_while_signed_in_is_linked_and_listed` |
| AC-19.2 | No rewards or loyalty feature is present in MVP. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-19.3 | Distributors have order history with tracking; Bulk customers have order history. | PARTIAL | H | works with the labelled local stub; real Zoho-managed handoff has no creation/inbound path |
| AC-20.1 | Email and phone are mandatory at checkout; email is sent for transactional communication. | PARTIAL | H | email and phone mandatory at checkout (done); transactional e-mail is not sent (not built) |
| AC-20.2 | Order processing completes when WhatsApp is unavailable or unconfigured. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_order_processing_completes_when_whatsapp_is_unconfigured` |
| AC-20.3 | No SMS channel is required or used as a mandatory channel. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-20.4 | Transactional and marketing communications are separated. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_no_other_code_selects_active_subscribers_for_sending`, `test_checkout_consent_never_subscribes_anyone`. Static scan plus a checkout-consent test: only the single eligibility gate selects subscribers; checkout consent never subscribes. |
| AC-20.5 | Normal delivery communication (the message and phone call before delivery attempts) is handled b | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-21.1 | A B2C order never carries both a combo discount and a promo/coupon. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_combo_and_coupon_never_stack_and_combo_is_kept_by_default` |
| AC-21.2 | Quantities consumed by one combo rule are not reused by another rule in the same order; rules ar | NOT DONE | H | rule-based qualifying-quantity combos and fixed bundles not built (DC-33); only a per-SKU amount combo exists |
| AC-21.3 | Rule-based combos need no combo SKU; fixed bundles have explicit components. | NOT DONE | H | rule-based qualifying-quantity combos and fixed bundles not built (DC-33); only a per-SKU amount combo exists |
| AC-21.4 | A promo/coupon applies only if its active/inactive status, validity dates, products/categories,  | PARTIAL | H | named test bodies read in pass 2 (assert the criterion): `test_coupon_minimum_order_value_and_the_500_condition`, `test_validity_dates_status_and_usage_limit` |
| AC-21.5 | Combos and promotions are not offered to Distributor/B2B or Bulk/Institutional customers. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_promo_code_does_not_combine_with_business_pricing`. Test shows a promo code is ignored for a business account and the price stays the business price. |
| AC-21.6 | There is no separate Household Combo or Bulk Combo collection. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-21.7 | B2C combo discounts are amount-based and configured per SKU: the first-selected combo SKU line r | DONE (verified) | H | assessor read modules/orders/pricing.py and checkout.price_cart |
| AC-22.1 | Each capability listed in §22.2 is present or explicitly scheduled in the approved architecture/ | DONE (verified) | M | named test body read (pass 2): test_the_implemented_seo_capabilities_are_all_present. Test checks the markers (title, description, canonical, og, JSON-LD, sitemap, robots) only; the SPEC 22.2 list is not exhaustively asserted. |
| AC-22.2 | Discontinued/unavailable products are handled for SEO without producing duplicate content. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_unknown_unpublished_and_malformed_are_the_same_404`, `test_sitemap_lists_public_pages_and_published_products_only` |
| AC-23.1 | Customer-facing content for each area in §23.2 exists and has been reviewed rather than blindly  | PARTIAL | L | content exists; HU approved copying as is on 2026-10-17, criterion says not blindly copied (spec/decision mismatch) |
| AC-23.2 | Contact content shows exactly the details in §4.1. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_the_canonical_contact_details_are_unchanged` |
| AC-23.3 | The customer-facing policy states that all orders are paid in full before fulfilment and COD is  | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-24.1 | No third-party integration beyond those in §24 is introduced without the architecture governance | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-25.1 | No paid order or payment is lost when Razorpay, Zoho or Shiprocket is unavailable. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_zoho_outage_after_payment_is_visible_preserved_and_recoverable`, `test_shiprocket_outage_is_retried_then_visible_then_recoverable_without_duplicates`, `test_a_withheld_write_gate_sends_nothing_and_keeps_the_paid_order`. Zoho and Shiprocket outage journey tests; paid order preserved and recoverable (stub/mock). |
| AC-25.2 | An external operation is retried at most 3 times, after which an explicit failure/exception stat | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_shiprocket_outage_is_retried_then_visible_then_recoverable_without_duplicates`, `test_transient_failure_retries_then_exhausts_after_three_total_attempts`, `test_provider_failure_backs_off_and_stops_at_three_attempts` |
| AC-25.3 | Replayed callbacks/webhooks create no duplicate orders, payments, invoices or shipments. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_a_paid_order_creates_exactly_one_sales_order_and_a_repeat_creates_none`, `test_a_reply_lost_after_the_create_is_recovered_not_duplicated`, `test_after_the_gate_opens_an_operator_retry_creates_exactly_one` |
| AC-25.4 | Each external operation carries a stable correlation ID. | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_correlation_ids_are_stable_unique_and_deterministic` |
| AC-25.5 | Later external status updates attach to the correct EffyKlean order. | PARTIAL | H | only one writer of delivery status exists (verified) but it is a stub-only Admin simulation; no inbound feed exists |
| AC-26.1 | Privileged functions require authenticated access and role-based authorisation; secrets are not  | DONE (verified) | M | named test body read (pass 2): test_secrets_are_not_tracked_in_source_control. Test proves only that `.env` is ignored and untracked; role/authentication enforcement is evidenced by the Admin authentication and permission tests (not named for this AC). |
| AC-26.2 | The events in §26.3 appear in the audit trail with who/what/when. | PARTIAL | H | integration-failure audit event added 19-Oct; bank/UPI and assisted-order events do not exist |
| AC-26.3 | A privacy policy, terms and applicable cookie/analytics consent are present. | DEFERRED | M | privacy, terms, cookie consent withheld until HU supplies approved legal text (recorded rule) |
| AC-27.1 | An assisted order records customer, products, quantities, prices, discounts, GST information, pa | NOT DONE | H | assisted orders not built; DC-22 open |
| AC-27.2 | An Admin override of pricing, GST, inventory or payment rules is explicit and audited; only a Di | PARTIAL | H | Director-only approval of negotiated pricing proven by `test_admin_prepares_a_director_approves_and_every_step_is_audited` (Admin gets 403 on approve/reject); no pricing/GST/inventory/payment override exists (code read). |
| AC-28.1 | Admin business/operational reporting is available; the initial scope is a small generic/core rep | DONE (verified) | H | named test bodies read in pass 2 (assert the criterion): `test_average_order_value_is_sales_over_orders_rounded_to_paise`. Average-order-value test only; the baseline report set is covered by the other report tests. |
| AC-29.1 | No runtime call to Shopify exists in the new platform. | DONE (verified) | H | assessor grep of modules/integrations/config found no Shopify reference; static test |
| AC-29.2 | Only data classes required by approved MVP requirements are migrated; no automatic migration of  | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |
| AC-29.3 | None of the 50 Shopify Unlisted products appears in the new catalogue or is published. | DONE (verified) | L | structural or wording test only; proves shape/absence, not runtime behaviour |

### 6B. Non-AC deliverables, governance, integration and operational obligations

| ID | Requirement / deliverable | Source | Status | Evidence and outstanding work | Findings |
|---|---|---|---|---|---|
| RQ-01 | Foundation baseline: Django/PG/uv/ruff/pytest scaffold, fail-closed settings | Foundation gate `94df6e3`, F-01B | DONE (verified) | `pyproject.toml`, `config/settings/*` read; ruff/check run by assessor. Nothing outstanding | – |
| RQ-02 | F-03 Catalogue SKU master | PROJECT_LOG 2026-10-06 | DONE (verified) | `modules/catalogue/models.py`; M-grade tests. HSN/cost fields added later (see RQ-33) | G-16 |
| RQ-03 | F-04 Staff identity, mandatory MFA, throttle | ARCH §18 | DONE (verified) | `modules/identity/authority.py`, `backoffice/mfa.py`, `throttle.py` read; tests `test_admin_auth`, `test_permissions`. Admin path fixed at `/EKIAdmin2026` (flagged "pending configuration review") | G-26 |
| RQ-04 | F-05 B2C purchase domain on local stubs | PROJECT_LOG | DONE (verified) | `checkout.py`, `payment_flow.py` read. Stub-only for shipments | G-01 |
| RQ-05 | F-06 stateless JSON API | PROJECT_LOG | DONE (verified) | `modules/storefront/views.py`; tests `test_f06_api` (M) | – |
| RQ-06 | F-07B catalogue revision governance (DRAFT→…→PUBLISHED) | SPEC §6.13, CR-004 | DONE (verified) | `modules/catalogue/revisions.py`; tests (M) | – |
| RQ-07 | I-01…I-04 browser increments (page, catalogue, cart, checkout/tracking) | PROJECT_LOG | DONE (verified) | tests (M); guest tracking unthrottled | G-11 |
| RQ-08 | Zoho Payments adapter: session create/retrieve, signed return, webhook, token cache | SPEC §12, CR-007 | PARTIAL | `integrations/zoho_payments.py` (436 lines), ~50 tests (mock). Sandbox session and one payment reported 2026-10-16/17 (class 3). **Webhook not registered** (token 401 on `/webhooks`; needs HU portal action and a stable HTTPS URL). Settlement/charges never read. Production never touched | G-07, G-13 |
| RQ-09 | Zoho Inventory adapter: availability, Sales Order create/confirm/cancel, customers | SPEC §14, §13 | PARTIAL | `integrations/zoho_inventory.py` (809 lines) read in part; mock tests; sandbox Sales Orders SO-00002…5 reported (class 3). Flags `ZOHO_SYNC_ENABLED`, `ZOHO_SALES_ORDER_WRITES_AUTHORIZED` off by default. Real stock decrement unproven (sandbox stock zero). Invoice/payment read-back scopes missing | G-15, G-40, G-41, G-42 |
| RQ-10 | Zoho→Shiprocket shipment creation and status return | SPEC §18.1-18.3, AD-10 | NOT DONE | `request_fulfilment` always raises (`zoho_inventory.py:737-741`); no inbound path. Shiprocket sandbox testing deferred by HU (item 16) | G-01 |
| RQ-11 | Transactional outbox + worker (AD-07), 3 total attempts | ARCH §16-17 | DONE (verified) | `outbox.py`, `run_outbox`; tests (M). Not scheduled on any host | G-24 |
| RQ-12 | Payment reconciliation of unresolved attempts (no timeouts) | SPEC §12.18 | PARTIAL | `reconcile_attempt` read; command exists; unscheduled; `place_order` idempotency read by assessor and found sound | G-24 |
| RQ-13 | Admin: orders, products, revisions, content, collections, coupons, customers, staff, reports, system | SPEC §27, Delta plan | PARTIAL | 15.8k lines; large test set. 25 of the 597 rows PARTIAL (Appendix A) | Appendix A |
| RQ-14 | Distributor and Bulk flows (application, rules, quotes, accounts, suspension) | SPEC §9-10, CR-006/009 | DONE (verified) | tests (M); GST display and bank/UPI gaps tracked under ACs | G-03, G-04 |
| RQ-15 | Optional customer accounts, saved shipping (flag off) | SPEC §19 | DONE (verified) | `customer_accounts.py`; tests (M) | G-11 |
| RQ-16 | SEO baseline: canonical, OG, JSON-LD, sitemap, robots | SPEC §22 | DONE (verified) | `storefront/site.py`, `pages.py` read; `test_storefront_seo` (M). Search Console/analytics parked (OQ-26) | – |
| RQ-17 | Customer policy pages (shipping, cancellation, replacement) | SPEC §23.5 | DONE (verified) | `policy_pages.py`; tests (M). Wording awaits HU review | – |
| RQ-18 | Privacy policy, terms, cookie/analytics consent | SPEC §23.2, §26.2 | DEFERRED | No page exists by recorded rule until HU supplies approved legal text | G-06 |
| RQ-19 | Contact form (fail-closed in production) | SPEC §23 | PARTIAL | `CONTACT_FORM_ENABLED` needs approved privacy text and retention decision (`production.py`); neither exists | G-06 |
| RQ-20 | Subscribe by e-mail with verification (stub mail only) | HU+DI 2026-10-11 | PARTIAL | `modules/orders/subscriptions.py:171` is the **only** `send_mail` call site; no provider, sender domain or consent wording | G-05 |
| RQ-21 | Transactional e-mail (order confirmed, shipped, cancelled, replacement…) | SPEC §20.2, AD-14 | NOT DONE | No sender exists; ownership of each message (website vs Zoho e-mail/WhatsApp) undecided (HU item 10 gives the direction to use GoDaddy `Support@EffyKlean.com` and Zoho channels but no matrix). `DEFAULT_FROM_EMAIL` default is `no-reply@effyklean.invalid`; `check_email_config` refused on the console backend | G-05 |
| RQ-22 | WhatsApp (optional channel); floating WhatsApp button | SPEC §20.3 | DEFERRED | Optional; Admin WhatsApp number setting exists; button decision open (597 file MF row) | – |
| RQ-23 | Media storage in an S3-compatible bucket (DigitalOcean Spaces) | HU 2026-10-17, ARCH §23 | PARTIAL | `media_store.py`, `media.py`; `migrate_media_to_storage` tested with an in-memory bucket only; **Spaces not provisioned; migration unverified**; 1.3 GB local `media/` untracked | G-31 |
| RQ-24 | Production settings guard (fail closed) | ARCH §26 | DONE (verified) | `production.py` read in full. Conflicts with the agreed "production-grade settings with sandbox integrations" staging plan (needs a separate settings module) | G-08 |
| RQ-25 | CI (GitHub Actions) as a quality gate | ARCH, SSD §8 | PARTIAL | Runs and passed on `513fc98`; not run on current tree; five historical failures; no deploy check, dependency audit, or security lint | G-09, G-49 |
| RQ-26 | Backup and restore procedure with drill | HU item 11 | PARTIAL | `docs/foundation/BACKUP_AND_RESTORE.md`; local drill 17 orders/40 revisions reported (class 3); production backups unverified; retention deferred by HU | G-38 |
| RQ-27 | Scheduler for outbox, reconcile, dispatch, suspend-roles, purge | Plan J-03 | NOT DONE | Definitions in `scheduling.py` (advisory-lock guard); nothing scheduled; App Platform jobs run at most every 15 minutes while outbox is defined every minute | G-24 |
| RQ-28 | Operational monitoring/alerting | SPEC §26.1, ARCH §25 | NOT DONE | Console logging config and `/healthz` only | G-39 |
| RQ-29 | Security baseline: headers, HSTS (prod), cookies, origin check, MFA, audit | SPEC §26.1 | DONE (verified) | `config/security.py`, `production.py` read | G-11, G-49 |
| RQ-30 | Storefront CSP enforcement | HU+DI 2026-10-16 | DEFERRED | Report-only by decision; `/videos/` hot-link decision | – |
| RQ-31 | Customer-data privacy: export, deletion, retention, consent records | SPEC §26.2 | PARTIAL | Staff export exists (audited); retention periods undecided; contact-form retention undecided | G-06 |
| RQ-32 | Catalogue content: 15 real products with approved text, images, dilution, HSN, weights | SPEC §6, HU 5/6 | PARTIAL | 15 products reported imported (class 3; dev DB not readable by assessor); five SKUs have conflicting dilution text; "Tools Required" decision open; weights/dimensions/barcodes/HSN values to be entered by Admin later (HU item 5/6) | G-19 |
| RQ-33 | HSN, barcode, cost, weight fields on Sku and Zoho comparison | HU item 6 | PARTIAL | Fields built; report-only HSN comparison; SPEC §13.9/AC-13.6 not amended | G-16 |
| RQ-34 | Shopify independence (no runtime call, own pages, media) | SPEC §29 | DONE (verified) | assessor grep: no Shopify reference in `modules`, `integrations`, `config` (Python and HTML templates) | – |
| RQ-35 | effyklean.com→effyklean.in redirect, Shopify retention, cutover | HU item 15 | DEFERRED | HU keeps Shopify active, redirects at go-live; `OLD_SITE_CLOSURE_CHECKLIST.md`; no DNS work authorised | G-30 |
| RQ-36 | Register of temporary sandbox arrangements to remove at go-live | CLAUDE.md | PARTIAL | `TEMPORARY_ARRANGEMENTS_REMOVE_AT_GO_LIVE.md` exists; items still live (tunnel, `example` return URL, sandbox flags) | G-34 |
| RQ-37 | Mandatory rule: never add a co-author | CLAUDE.md | NOT DONE | 8 pushed commits carry the trailer (verified); rewrite parked for HU+DI | G-10 |
| RQ-38 | Continuity records accurate (CLAUDE.md, README, PROJECT_LOG, registers) | Original_AgntInst §12 | PARTIAL | Records exist and are append-only but contradict each other | G-20 |
| RQ-39 | HU review and acceptance of the local body of work; commit decision | CLAUDE.md principle 6 | NOT DONE | Batch 1 not accepted; 113 uncommitted paths | G-10 |
| RQ-40 | TESTCODE traceability for all test-created records | HU+DI 2026-10-12 | PARTIAL | Stamped on payment attempts and orders only; customers, saved addresses, enquiries, subscriptions, Zoho sync rows unmarked; production refuses TESTCODE | G-08 |
| RQ-41 | Restricted-access staging (approved people only) | HU+DI hosting plan | NOT DONE | No gate in code (assessed by the hosting report and confirmed: no allow-list/basic-auth code found) | G-08 |
| RQ-42 | Zoho Payments webhook registered to a stable HTTPS endpoint | Plan B-02 | NOT DONE | HU portal action; sandbox token lacks settings scopes | G-07 |
| RQ-43 | Seven additional Zoho Inventory scopes + Payments settings scopes | HU item 13 | NOT DONE | Authorised by HU for sandbox 2026-10-18; token not yet re-issued | G-40 |
| RQ-44 | Zoho invoice automation / Flow behaviour observed and no duplicate-order risk | Plan B-16 | NOT DONE | Confirmed Sales Orders remain uninvoiced/unpaid in sandbox; Flow not inspected | G-41 |
| RQ-45 | Production Zoho tax ids and accountant sign-off of GST/HSN | Plan B-07 | NOT DONE | Tax-id env vars unset in production; no certification | G-04, G-15 |
| RQ-46 | Performance baseline / Core Web Vitals | SPEC §30.2 | PARTIAL | Dev-machine server timing only (median 70 ms, p95 228 ms reported); no numeric target in SPEC | G-37 |
| RQ-47 | Responsive/mobile verification | SPEC §22.2 | DONE (verified) | Agent browser runs (115 checks on 17 Oct; 22 storefront + 28 Admin pages at 390/1280 px on 19 Oct; 0 overflow; class 3); not re-run | – |
| RQ-48 | Accessibility assessment | SPEC §30.4 | NOT DONE | None; no target defined | G-37 |
| RQ-49 | Edge rate-limiting / DoS protection (RM-10) | register H-02 | NOT DONE | No edge layer decided | G-11 |
| RQ-50 | Dependency vulnerability and security-lint scanning | SSD §7 | NOT DONE | Not in `ci.sh`; ruff default rules only (noqa comments cite BLE/S rules that are not enabled) | G-49 |
| RQ-51 | Data migration limited to approved classes (catalogue, blog) | SPEC §29 | DONE (verified) | two importers only (structural test + assessor read of command list) | – |
| RQ-52 | T41 scheduled publication | Plan T41 | DEFERRED | HU+DI design decision (publishes on a stored authorisation; ARCH §20) | G-18 |
| RQ-53 | T38 / PRD-063 product slug editing | Plan T38 | DEFERRED | URL-scheme decision; product ID is the URL identity | G-18 |
| RQ-54 | Admin deletion of Distributor/Bulk customer records (CR-010) | HU item 18 | PARTIAL | Director-only deletion exists and is tested; HU said "authorized Admin customer-record deletion is a requirement" | G-17 |
| RQ-55 | Combo-versus-coupon precedence | SPEC §21.1 | DEFERRED | Agent default "combo kept unless customer picks coupon" awaits HU+DI | G-35 |
| RQ-56 | Draft orders / Duplicate order (ORD-091/142) | DC-22 | DEFERRED | "DEFER: with drafts" | – |
| RQ-57 | Notification ownership matrix (website vs Zoho e-mail/WhatsApp) | HU item 10 | NOT DONE | Not written | G-05 |
| RQ-58 | Plan §2.3 122-row decision-evidence audit labels | Plan §2.3 | PARTIAL | Map built (no row accepted); labels (explicit answer / agreed rule / not recovered) still HU+DI review items | G-20 |
| RQ-59 | Per-activity accounting of all 597 planned activities | HU 18-Oct item 12 | PARTIAL | CSV exists with a status per row; 310 rows are not built (decisions/exclusions) | Appendix A |
| RQ-60 | Real-sandbox end-to-end journey (payment → Zoho SO → shipment → delivery) | Plan Phase 3-4, hosting plan | NOT DONE | Never run end to end; shipment half cannot run (RQ-10) | G-01 |

### 6C. The 597 planned activities

The item-level inventory is **Appendix A** (every ID, with the assessor's mapping to the four statuses). Source: `docs/discovery/RECONCILED_597_STATUS_2026-10-18.csv` (untracked, local only). Mapping rule: "implemented…" → DONE; "partial…/in progress" → PARTIAL; "not built" (no NO-ACTION disposition) → NOT DONE; everything else (explicit NO decisions, awaiting HU+DI, proposal-only, blocked, closed as Zoho-owned, parked, observed/evidence-only) → DEFERRED, because an identifiable decision, rule or blocker holds it. The assessor verified mechanically that every one of 819 test names cited in the "implemented" rows' basis text exists in `tests/` (0 dangling); 38 "implemented" rows cite no test and rest on earlier validation levels; row-by-row body reading was done by the earlier agent (class 3) and was only sampled by the assessor.

---

## 7. Previous-agent assessment: instructions and claims versus evidence

The earlier agents were successive Claude Code sessions, not named individuals; the assessor identifies them by work package (WP), from PROJECT_LOG, the status register and the public records. For each WP: the instruction that applied, what was claimed, what the assessor could check, and the verdict. "Verified" means evidence class 1 or confirmed by reading code/tests; "reported" means class 3.

| WP | Dates | Instruction that applied | Claim | What the assessor verified | Verdict / remaining |
|---|---|---|---|---|---|
| WP-1 Foundation and increments (F-01B…F-07B, I-01…I-04) | 3-7 Oct | Foundation gate (`94df6e3`); one controlled increment at a time with HU+Di acceptance | Implemented, accepted, committed | Code present and structurally consistent; 8 of these commits carry a Co-Authored-By trailer | Delivered; **co-author rule breached** (G-10) |
| WP-2 Razorpay Phase 1 and Admin redesign | 9-10 Oct | HU+Di task-by-task | Razorpay verified once in test mode; Admin built | Razorpay superseded; `integrations/razorpay.py` (169 lines) and `LocalRazorpayStub` remain as unwired history and as the local stub class name | Superseded by CR-007; naming residue (G-25) |
| WP-3 Orders Batch 1 and Priorities 1-5 | 10 Oct | Shopify Admin mapping; "implement what HU+DI approve" | ORD-002…012 and discounts, customers, reports, staff implemented | Large Admin code base present; tests (M) | Not formally accepted; ~25 partial rows remain |
| WP-4 Zoho Payments swap, videos, quotes, subscribe | 11 Oct | CR-006…CR-009 | Zoho Payments replaces Razorpay; AD-07 outbox | Adapter, outbox read; tests (M); sandbox evidence reported | Delivered locally; webhook not registered (G-07) |
| WP-5 TESTCODE, real Zoho adapter, three-way comparison | 12 Oct | HU+DI instruction; comparison stages | B1 TESTCODE and adapter (mock), 597-row inventory | `testcodes.py` stamps attempts/orders only | Partial traceability (RQ-40) |
| WP-6 Batch 1 (55 tasks) | 14 Oct | HU "first recommended batch" | Implemented, full suite 2,135 passed | Not formally accepted; T41 blocked, T35/T38 partial then | Superseded by later runs |
| WP-7 Zoho sandbox passes 1-9 | 15 Oct | HU-authorised sandbox reads/writes | Items, contacts, tax ids, Sales Order safeguards, GST rule | `tax.py` read; safeguards tests (M); sandbox writes reported only | GST rule conflicts with frozen SPEC (G-04) |
| WP-8 Sandbox payment journey, media, own policy pages | 16-17 Oct | HU decisions applied | Real Zoho sandbox payment verified; webhook-first; idempotent | Reported only; CI ran and passed on `513fc98` | Webhook still unregistered; storage unprovisioned |
| WP-9 18-Oct continuation | 18 Oct | `AgntInst_18Oct2026_1958.md` | T35, forms, parity, HSN check, SMTP check, 597/122 reconciliation | `DiReview` records 2,351 tests; items reconciled | Superseded by WP-10 |
| WP-10 18-19 Oct continuation | 18-19 Oct | same + HU clarifications | T35 DONE; T41/T38 parked; forms; AC evidence 100→21; 597 file; two defects fixed | See §10 for every checkable claim | PARTIAL, honestly reported; premature "final" messages admitted by the agent |
| WP-11 19-Oct audit pass | 19 Oct | `Original_AgntInst_19Oct2026_1233.md` + SSD requirement | GST fallback narrowed; AC-26.2 audit event; 2,491 tests | Existence of `audit_outbox.py`, `ZohoGstRejectedError`, ledger; suite count (collect-only) matches | Delivered; "CI never run" claim is wrong (D-6) |
| WP-12 DigitalOcean readiness (read-only) | 19 Oct | `DigiOcn_InstructionsForAgnt_19Oct25_1306.md` | Not ready; four findings | Re-verified findings 1 (adapter raises) and 4 (scheduler limit applies); finding 2 (no access gate) consistent with grep | Accurate and useful |
| WP-13 Zoho shipment lifecycle (read-only) | 19 Oct | `AgntInstDigiOcnImplmntatn_19OCT2026_1505` | Design complete, blocked on HU+DI inputs | Verified: no inbound path; four dispatch triggers; `OrderStatus` pinned | Accurate; implementation not authorised |

### 7.1 Completion-claim reconciliation (SSD §3 and §11)

**Claims the assessor verified:**
- 89 modified + 24 untracked, 0 staged, 0 stashes, HEAD 625e210, 3 ahead (CONSOLIDATED_REPORT §9, AUDIT_LEDGER §6): matches `git status`.
- 2,491 tests: matches `pytest --collect-only`. Ruff and `manage.py check` clean: reproduced.
- AC index 128 named / 19 not named / current: `scripts/ac_index.py --check` printed "AC test index is current."; counts match the file.
- Eight pushed co-author commits (CONSOLIDATED_REPORT §8): reproduced with `git log --grep`.
- AC-12.9 "one writer of delivery status": reproduced; and its limitation (stub-only caller) is real.
- T35 `RejectedWebhookDelivery` exists with metadata-only fields; migrations 0025-0027 untracked.
- Real adapter `request_fulfilment` raises (hosting report): reproduced.

**Claims the assessor found wrong or unsupported:**
1. "GitHub Actions CI: NOT DONE, never run" (CONSOLIDATED_REPORT V1, §3, §8; AUDIT_LEDGER §6; status register A-05; PRODUCTION_READINESS_REGISTER A-05 "MISSING"). `gh run list`: 12 runs, 7 succeeded, last success on `513fc98` (2026-10-17). The accurate statement is "CI has not run on the 3 unpushed commits or the working tree".
2. "128 of 147 acceptance criteria are named by a test" overstates by at least one: **AC-9.9 is credited only to `tests/test_ac_index.py`, a parser fixture** (`"""File header cites AC-9.9."""` inside a string). Also AC-1.1 and AC-2.2 are cited by that fixture and are not SPEC criteria.
3. "HU's item-18 text is not on this machine" (CONSOLIDATED_REPORT §1 item 4, §7): the text is in the public repo file `HUDI Discussion/RESP_18OCT_QA_HU ANSWERS.md` (item 18 and the approved corrections), readable with `curl`. The "BLOCKED" was avoidable; the item is better described as a decision on interpretation (is HU, a Director, already able to delete?), not missing text.
4. DEPLOYMENT_PREREQUISITES says product images are "NOT DONE" for object storage; the code now supports S3 for them (D-8).
5. "No browser tool" (earlier status register E-07) was corrected by the agent later; recorded as such.
6. **False evidence link (revision 2):** AC-9.7 carries a `Covers AC-9.7` tag on `tests/test_f05_boundaries.py::test_orders_package_contains_only_authorized_files`; the id appears only in a comment beside a migration name. The real AC-9.7 evidence is in `test_distributor_pricing` and `test_business_accounts` (read).
7. **NO-listed capabilities built without a recorded override (revision 2):** the 18-Oct run record (§10) implements ORD-019 (amount filter) although the decision ledger and Delta plan §6 list it as NO; the 597 file marks both ORD-019 and ORD-064 (customer-initiated cancellation, also NO) as "implemented"; MA-ORD-076 (returned-package inspection, listed NO by plan §3) is still shown there as "awaiting HU+DI decision" although the feature is built. See G-51.
8. **A new test depends on an ignored file (revision 2):** the AC-29.3 structural test reads `media/catalogue_source/source.json`; the pass counts in the records come from a machine that has the file. See G-59.
**Claims the assessor could not verify** (class 3): every full-suite pass count and duration (1,894 … 2,491), sandbox Sales Orders SO-00002…5 and the real Zoho Payments sandbox payment, headless-browser checks (11/11, 115/115, 22+28 pages), the India Post PIN sample (95 PINs), the local restore drill (17 orders), dev-database migration state through `orders.0027`, and "15 products in the dev database".

**Premature completion signals admitted by the earlier agent:** three Windows message boxes (the first sent while work remained), several "final" reports before the consolidated one, stopping early twice, an accidental `git stash` (restored; stash list empty now). The assessor treats these as disclosed and closed.

### 7.2 Shortcut and integrity sweep (SSD §4), current commands

- `TODO|FIXME|XXX|HACK|NotImplemented` in `modules integrations config scripts` (migrations excluded): **one match**, a docstring in `testcode_report.py` ("XXXXXXXX" in a code format). No placeholders.
- `pytest.mark.skip|xfail|skipif|pytest.skip|unittest.skip` in `tests`: **no matches**.
- Bare `pass`: 8 matches, all inside exception-class bodies or deliberate `except InvalidTransitionError: pass` in `checkout.py:726, 847` (a lost race to advance state; the `else` branch records the exhaustion event) and two sitemap `except Exception: pass` in `site.py:710, 719` (the sitemap still lists built-in pages). Read; acceptable.
- `except Exception`: 28 sites (27 under `modules`/`integrations` + `config/urls.py:38`). Read the money/stock ones: `checkout.py:630, 646, 807`, `operations.py:238`, `outbox.py:267`, `zoho_sync.py:174` record a failed attempt or keep the order; `payment_flow.py:401` logs and never alters the webhook answer; `catalogue_views.py:539` and `storefront/pages.py:91` fail safe ("do not claim stock"). `storefront/business_view.py:21,30` swallow lookup errors and show **ordinary prices** (G-22).
- Test functions without an `assert` statement (AST heuristic, 1,790 top-level functions): 7 (5 when `pytest.raises` is also counted as an assertion, which is the figure used in §1 and §10.1); the assessor read all seven: they rely on helper assertions or on an exception being raised (migration drift, `migrate`, config load, model constraints). The weakest is `test_a_complete_sandbox_configuration_is_accepted`, which only constructs a gateway without raising.
- Test weakening: the agents report widening `test_f05_boundaries.py`, `test_f06_boundaries.py`, `test_migrations.py` allow-lists for new files/tables and raising the product-list query budget 25→28. The assessor did not diff these against history (G-50).
- Hard-coded business defaults introduced by agents: see §5 (enquiry-form defaults, auto-archive 7 days, combo-vs-coupon precedence). `seed_hu_admin_test.py` (ignored, untracked) holds a hard-coded local password and must never be deployed (G-33).

---

### 7.3 The assessor's own completion claims (SSD §3)

The first version of this document was delivered with a statement that it was not exhaustive (§15) and with the completion notification HU had requested, while large parts of the code, tests and records were still unread. HU's question that followed ("have you completed all the tasks … gone through all the documents?") exposed that the notification overstated completion. **That signal was premature.** Revision 2 reduces the unread areas considerably (§15) but does not remove them; this revision is likewise not a statement that the project or the review is complete. Work completed later does not make the earlier signal accurate.

## 8. Detailed gap analysis

### 8.1 By area, workflow and integration (what was traced end to end)

**Checkout → payment → order (B2C).** Traced: `price_cart` → `start_payment` (stock check via Zoho, reviewed-total check, open/reuse attempt) → provider session → browser return or webhook → `reconcile_attempt` (provider's own record decides; exact amount and INR required; no timeout releases a hold) → `place_order` (row-locked, idempotent, duplicate payments recorded for a person, outbox task enqueued in the same transaction). Failure paths exist for outage, mismatch, reversal, unknown order, replay and bad signature. This area is sound against SPEC §11-12 and CR-007. **Gaps:** only sandbox/mocks; webhook never registered; settlement/charges unread (G-07, G-13).

**Zoho Inventory handoff.** `submit_to_zoho` and the outbox create one Sales Order per EKI reference, refuse a Zoho total that differs from the amount paid, retry three times, then mark `ZOHO_SYNC_FAILED` with an ACTION_REQUIRED log. GST fallback was narrowed on 19 Oct to GST-naming rejections (names present at `zoho_inventory.py:111, 326, 336, 390, 405`; body not read). **Gaps:** writes are behind two environment flags; real stock, invoice and payment read-back unobserved (G-40…G-42).

**Fulfilment, delivery, cancellation, replacement (the broken chain).** `request_shipment` → SHIPMENT outbox → `_attempt_fulfilment` → `zoho.request_fulfilment`. With the real adapter this raises; three attempts later the order is `SHIPMENT_FAILED`. Delivery status has one writer, `apply_delivery_update`, requiring `Shipment.status == CREATED` and `Order.status == SHIPMENT_PENDING`; its only caller is a stub-only Admin action. Downstream code that reads `Shipment.delivered_at` or `Shipment.status == CREATED`: replacement window (`operations.py:472-520`), customer history and status labels (`customer_view.py`), saved-address reset (`delivered_addresses.py`), returned-package recording (`returns.py:25-38`), and the **cancellation cutoff** (`operations.py:98-118`). SPEC §18.9 customer statuses (Shipped, Out for Delivery, Delivered) and §15.5/15.7 traceability therefore cannot occur in production. ARCHITECTURE §15 explicitly defers "how EffyKlean receives status". (G-01, G-02, G-36)

**Pricing and tax.** B2C combo and coupon arithmetic read in full (`pricing.py`): selection-order amount combo, ₹500 condition, one additional discount, invented precedence flagged by the agent. Business pricing: one rule or accepted quote per product, no stacking. `tax.py` extracts GST from the amount paid (18% total, 9+9 for Karnataka else IGST). **Conflicts with SPEC §7.9/7.10/13.14** (GST on the undiscounted Sale Price; discount does not reduce GST) and with GST-exclusive business display (§9.18, §10.17). (G-04, G-12)

**Catalogue, content, SEO.** Revision workflow, review queue, publication gates and availability vocabulary implemented and tested. Related-product links render although register E-09 says out of scope (G-23). Fifteen SEO drafts and three blog drafts are unpublished by HU decision. Dilution text conflicts for five SKUs; "Tools Required" decision open (G-19).

**Distributor, Bulk, customer accounts.** Implemented, including suspension after three months, Director-only role removal and Director-only record deletion. HU asked (item 18) for **Admin** deletion of Distributor/Bulk records "no questions asked"; only the Director can delete today (G-17). Bank/UPI payment path and assisted orders absent (G-03).

**Admin.** 15.8k lines; MFA, audit, capability model. Extra capabilities were granted to both roles pending HU+DI (G-43). 25 of 597 activity rows remain PARTIAL (Appendix A).

**Security.** Strong boundary middleware (origin/Sec-Fetch-Site checks, admin hardening, HTTPS/HSTS in production). Findings: unthrottled guest lookup/cancel, per-process throttle cache, no edge limiting, no dependency/security scanning, guard asymmetry in production settings (G-11, G-27, G-32, G-49).

**Operations.** No hosting, no staging gate, no scheduler, no monitoring, DB TLS option absent, backups only locally drilled (G-08, G-24, G-38, G-39).

### 8.2 Consolidated gap register

Severity scale: **Critical** blocks the core business flow or breaks a frozen rule in production; **High** blocks launch or breaks a frozen requirement/governance rule; **Medium** degrades a requirement, evidence or safety margin; **Low** minor or cosmetic. "Type" distinguishes: **DEF** implementation defect, **MISS** missing capability, **EVID** missing evidence, **TEST** test deficiency, **DOC** documentation inconsistency, **EXT** external-verification limitation, **DECN** unresolved decision, **DFR** deferred work. "Confirmed" means the assessor verified it in code/commands; "Verify" means it needs further verification.

| ID | Sev | Type | Related requirement | Expected | Actual and exact missing elements | Evidence | Impact | Dependencies / blockers | Confirmed? | Next action | HU+DI approval? |
|---|---|---|---|---|---|---|---|---|---|---|---|
| G-01 | Critical | DEF/MISS | SPEC §15.5, 15.7, 18.1-18.9, 12.9; AC-12.9, 18.1-18.8, 25.5; RQ-10, RQ-60; ARCH §15 | A Zoho-managed shipment appears in EffyKlean with AWB, tracking link and delivery status updates, mapped to customer statuses | `request_fulfilment` always raises; four triggers still call it (`dispatch` job, Admin retry-ship, `retry_integrations` shipment half, outbox SHIPMENT task); no inbound feed; delivery can be set only by a stub-only Admin simulation; every dispatched order would end `SHIPMENT_FAILED` | `zoho_inventory.py:737-741`; `checkout.py:792-850`; `operations.py:430-470`; `order_actions.py:345-380`; hosting report §2 | No shipment status, tracking, Delivered, replacement, returned-package or saved-address reset in production; staff see failed shipments | G-36 decision; Zoho sample/read access; HU item 16 deferred Shiprocket testing | Confirmed | Decide model (G-36), then plan P2 tasks | Yes |
| G-02 | High | DEF | SPEC §16.2, 18.6, 17.4; AC-16.1, 17.4, 17.5 | B2C cancellation closes at real handover; replacement window runs from real delivery | Cutoff = local `Shipment.status == CREATED`, which never happens under the real adapter, so cancellation (20% charge, Zoho SO void) stays open after Zoho/Shiprocket dispatched; replacement window never opens | `operations.py:98-118, 472-520` | Customer can cancel a shipped order; staff must reverse manually; replacement unusable | G-01 | Confirmed | Define "handover" signal from Zoho (P2) | Yes (decision 4 in hosting report) |
| G-03 | High | MISS/DECN | SPEC §12.10-12.11, 27.1, 27.3; AC-12.5, 12.6, 27.1, 27.2; DC-22 | Distributor/Bulk can pay by bank transfer/UPI with Admin verification (PAYMENT_PENDING_VERIFICATION → CONFIRMED); assisted orders audited | Neither is built; criteria worded for Razorpay; no CR defers them | AC index (NONE); register G-03; `modules` grep: no verification state | Business customers can only pay online; Admin cannot create assisted orders | DC-22 decision | Confirmed | Decide scope now or amend SPEC; then P3 | Yes |
| G-04 | High | DECN/DEF | SPEC §7.9, 7.10, 9.18, 10.17, 13.4, 13.14; AC-7.4, 9.8, 10.8, 13.7 | GST on the undiscounted Sale Price, discount applied to the Sale Price component only; business prices GST-exclusive; Zoho authoritative, no guessed amount | `tax.py` extracts GST from the discounted amount paid; business prices are tax-inclusive; payable computed locally even for business customers; no guarded Zoho-unavailable path | `tax.py` read in full; `checkout._price_business_cart` read | Wrong GST arithmetic versus frozen rule on every discounted order; invoice may disagree with order | HU+DI rule; accountant (Zoho is authoritative and may differ) | Confirmed | STOP → REPORT: CR or revert | Yes |
| G-05 | High | MISS | SPEC §20.2; AD-14; AC-20.1; RQ-21, RQ-57 | Order confirmation and status e-mails sent asynchronously, audited; failure never fails an order | No sender except Subscribe verification; `DEFAULT_FROM_EMAIL` defaults to an `.invalid` domain; console backend refused in production; ownership (website vs Zoho e-mail/WhatsApp) undecided; `check_email_config` run only against the console backend | `subscriptions.py:171`; `base.py:241-254`; ledger §7 | A paid customer receives no confirmation from the site | HU credentials + message matrix | Confirmed | Decide ownership matrix; verify GoDaddy SMTP; build async notifier | Yes (wording, ownership) |
| G-06 | High | DFR | SPEC §23.2, 26.2; AC-26.3 | Privacy policy, terms, cookie/analytics consent, retention rules | None exist by rule until HU supplies legal text; contact form fail-closed in production; retention undecided | `production.py:77-84`; `policy_pages.py` header | Cannot launch lawfully; contact form unavailable | HU legal text | Confirmed | HU supplies text; P4 | Yes |
| G-07 | High | EXT | SPEC §12.17-12.19; RQ-08, RQ-42 | Webhook registered and proven end to end on a stable HTTPS URL; production evidence | Webhook never registered (token 401 on `/webhooks`); return URL placeholder; temporary tunnel; only sandbox payments reported | status register, ZOHO_WEBHOOK docs | Payment confirmation depends on browser return only; reconciliation job unscheduled | HU portal action; hosting | Verify (reported, not observable) | HU registers webhook on staging URL; P8 | Yes |
| G-08 | High | MISS | ARCH §23, hosting plan; RQ-23, RQ-24, RQ-41 | Staging/production on DigitalOcean App Platform + Managed PostgreSQL, restricted access during sandbox testing | Nothing deployed; no `Dockerfile`/app spec; no access gate; `production.py` forbids TESTCODE and Inventory-sandbox, so "production-grade settings with sandbox integrations" needs a new settings module; DB `sslmode` unset; pre-deploy migrate not wired | hosting report §5-§6 (class 3), `production.py` read | No place to run the sandbox gate or go live | HU+DI decisions 2-3, cost approval | Confirmed (code); platform facts unverified | P6 | Yes |
| G-09 | Medium | EVID/DOC | SSD §8; RQ-25 | CI evidence on the tree to be accepted; accurate records | CI last passed on `513fc98`; current tree and 3 commits never ran; five historical failures; records say "never ran" | `gh run list` | Local pass counts are not CI evidence | Push/commit approval | Confirmed | Correct records (P0); run CI after approved push | Yes (push) |
| G-10 | High | DOC/GOV | CLAUDE.md co-author rule, principle 6; RQ-37, RQ-39 | No co-author trailers; reviewed commits; reproducible state | 8 pushed commits carry trailers; 113 uncommitted paths; 3 untracked migrations (models in modified files depend on them); nothing accepted | `git log --grep`, `git status` | Loss/ambiguity risk; deploying tracked files without migrations breaks `migrate`; governance breach | HU decision on history rewrite (consequences listed in CONSOLIDATED_REPORT §8) | Confirmed | P0 | Yes |
| G-11 | Medium | DEF | SPEC §26.1; RQ-07, RQ-49 | Brute-force protection on lookups that reveal or change order data | `/track/` (reference + mobile/email) and the cancel flow have no throttle; EKI IDs are sequential per day; no edge limit | `checkout_pages.py:1062-1085`, `customer_view.get_order_view_by_contact` (no limiter found) | Enumeration of order data; unauthorised cancellation with 20% charge by anyone knowing reference+contact | Cache/DB choice | Confirmed (absence of limiter by code reading) | P5 | No (security fix) |
| G-12 | Medium | MISS/DECN | SPEC §21.2-21.4; AC-21.2, 21.3 | Admin-defined qualifying product/quantity rules, no reuse across rules, oldest first; fixed bundles | Only a per-SKU amount applied whenever the cart holds two combo-eligible lines; rule model undefined (DC-33) | `pricing.py` docstring and code | Combo behaviour differs from the SPEC example (10 + 10 units) | DC-33 | Confirmed | Decide model; P3 | Yes |
| G-13 | Medium | DECN/MISS | SPEC §12.9, 12.12, 12.13; AC-12.7, 12.8, 15.1 | Retain and show payment status, charges, taxes on charges, net settled, settlement reference/date | Worded for Razorpay; Zoho Payments settlement is not fetched; Admin says so | order page text, AC index | Finance reconciliation incomplete | Restate AC for Zoho Payments; API availability | Confirmed | Restate then P3 | Yes |
| G-14 | Medium | DECN | SPEC §16.5; AC-16.5; ORD-074/075/076/144, SET-013 | Refund through original mechanism | Refund recorded; staff execute in the provider dashboard (guard test) | `operations.py:140-270`, `test_refund_guard.py` | Manual step with error/audit risk | HU restatement | Confirmed | Restate criterion or build automated refund | Yes |
| G-15 | Medium | MISS/EXT | SPEC §13.10; AC-13.8, 13.9; HU item 20 | Admin shows Zoho invoice number/status; Zoho tax config certified | Not shown; needs `invoices.READ` and automation; HU said do not build Zoho functions unless a frozen criterion requires it (AC-13.8 does) | register D-07 | Staff cannot see invoice status | Scope token, Flow | Confirmed | HU decides whether AC-13.8 stands | Yes |
| G-16 | Medium | DECN | SPEC §13.9; AC-13.6; HU item 6 | No competing local tax master | `Sku.hsn_code`, cost and logistics fields held locally; report-only comparison with Zoho | `test_f07b_boundaries` field list | Spec says no local tax master; HU says keep fields | CR | Confirmed | Amend SPEC/AC via CR | Yes |
| G-17 | Medium | DECN | HU item 18; CR-009; AC-9.6 | Admin can delete a Distributor/Bulk customer record, preserving orders/payments/audit | Director-only deletion (`RECORD_DELETE`) exists and is tested; Admin cannot. Revision 2: `deletion._customer` also refuses any customer who holds a business role, placed an order while signed in, or has quotes; because `Order.customer_account_id` is a plain integer, deleting the record while preserving orders and audit is technically possible, so HU's item-18 requirement (delete a Distributor or Bulk customer, preserving orders/payments/audit) is effectively unmet for every business customer who ever ordered | `authority.py`, `deletion.py`, `test_director_deletion.py` | HU's stated requirement possibly satisfied only for Directors | HU confirms intent | Confirmed | Ask HU one question; adjust | Yes |
| G-18 | Low | DFR | Plan T41, T38 | Scheduled publication; slug edit | Not built; designs in register | register | None for launch | HU+DI designs | Confirmed | Decide later | Yes |
| G-19 | Medium | MISS/EXT | SPEC §6.6, 23; HU items 2, 4, 5 | Approved content and data for all 15 products | Five SKUs with conflicting dilution text; Tools Required undecided; HSN, weights, dimensions, barcodes unentered; 15 SEO and 3 blog drafts unpublished | CONSOLIDATED_REPORT §7 | Content not launch-ready | HU data/decisions | Verify (dev DB unreadable) | P7 | Yes |
| G-20 | Medium | DOC | Original_AgntInst §12; RQ-38 | One accurate current-state record | CLAUDE.md/README/PROJECT_LOG have 20+ stacked "latest state" paragraphs that contradict each other; PRODUCTION_READINESS_REGISTER (12 Oct) stale; public copies stale (D-2…D-4) | files | Reader cannot tell the true state without this assessment | None | Confirmed | P0 reconciliation | No (docs) / push approval |
| G-21 | Medium | TEST | SSD §2, §4; AC-9.9 | An AC "named" only by a real test | AC-9.9 credited to a parser fixture; 20 structural-only ACs; ACs tags are traceability, not acceptance | `test_ac_index.py:36-51` | Coverage figure overstated by ≥1 | – | Confirmed | Add a real AC-9.9 test; mark structural evidence | No |
| G-22 | Low | DEF | SPEC §9.18 | Displayed price equals charged price | `business_view.py` swallows lookup errors and shows ordinary prices while checkout may charge the business price | `business_view.py:14-31` | Possible display/charge mismatch on a transient error | – | Confirmed (by reading) | Fail visibly; add test | No |
| G-23 | Low | DECN | Register E-09, MF-026 | Related-product links only if approved | `related_products` renders on product pages | `customer_view.py:236`, `pages.py:460` | Scope creep versus an "out of scope" label | – | Confirmed | HU+DI decide keep/remove | Yes |
| G-24 | High | MISS | ARCH §16-17; RQ-11, RQ-12, RQ-27 | Outbox, reconciliation, role suspension, purge run on a schedule | No host schedules any job; outbox defined every minute, reconcile every 10 minutes; App Platform cron minimum is 15 minutes (hosting report) | `scheduling.py`, hosting report §3 | Orders never reach Zoho; unresolved payments never reconciled | Hosting decision (worker vs 15-min polling) | Confirmed (no scheduler); platform limit class 3 | P6 | Yes |
| G-25 | Low | DOC | CR-007 | Razorpay wording historical only | `integrations/razorpay.py`, `LocalRazorpayStub`, many docstrings still say Razorpay | grep | Confusion | – | Confirmed | Rename or document | No |
| G-26 | Low | DECN | register H-02 | Admin path decided | `/EKIAdmin2026` hard-coded as "permanently the only entry point", flagged for review | `paths.py` | Obscurity only | – | Confirmed | HU+DI confirm | Yes |
| G-27 | Medium | DEF | SPEC §26.1 | Throttle shared across workers | Customer sign-in throttle uses Django's default cache; no `CACHES` setting, so a per-process in-memory cache; two gunicorn workers halve the protection; resets on restart | `customer_accounts.py:113-126`, settings grep | Weaker protection | – | Confirmed | Use DB or shared cache | No |
| G-28 | Low | DECN | HU item 1, 16 | Zoho owns dispatch timing | Website still enforces "no same-day dispatch" and staff holds in its own dispatch path | `checkout.py:756-790` | Duplicates Zoho; moot if the path is retired (G-01) | G-36 | Confirmed | Resolve in P2 | Yes |
| G-29 | Low | DFR | SPEC §22.3, OQ-26 | Search Console/analytics integration | Parked by governance gate | SPEC §24.4 | None | OQ-26 | Confirmed | Decide later | Yes |
| G-30 | Medium | DFR | HU item 15; RQ-35 | Planned transition: DNS, redirect effyklean.com→.in, Shopify retained | Checklist exists; no plan/dates; DNS not authorised | `OLD_SITE_CLOSURE_CHECKLIST.md` | Cutover risk | Hosting, content approval | Confirmed | P10 | Yes |
| G-31 | Medium | EXT | HU item 9; RQ-23 | Media in Spaces, verified copy, then cleanup | Not provisioned; `migrate_media_to_storage` untested against a real bucket; 1.3 GB local media | status register E-08 | Production refuses to start without it | Cost approval | Confirmed | P6 | Yes (paid) |
| G-32 | Medium | DEF | SPEC §26.1; ARCH §26 | Production refuses unsafe config | `production.py` refuses `ZOHO_INVENTORY_SANDBOX` but **not** `ZOHO_PAYMENTS_SANDBOX` (revision 2: `ZohoPaymentsGateway._check_environment` couples the flag to sandbox hosts and fails closed on a mixed configuration, so the risk is limited to a deliberate sandbox-host plus flag configuration); `PUBLIC_BASE_URL` defaults to `http://127.0.0.1:8000` (used in e-mail links) and is not required; `DEFAULT_FROM_EMAIL` defaults to `.invalid`; `CSRF_TRUSTED_ORIGINS` unset | `production.py`, `base.py:152-163, 252-254`, grep | Misconfiguration could route live traffic to sandbox payments or send localhost links | – | Confirmed | Add guards; P5/P6 | No |
| G-33 | Low | DOC | CLAUDE.md | Test password script never deployed | `seed_hu_admin_test.py` with hard-coded password is untracked/ignored but present in the working copy that a build might upload | status ignored | Credential in a deployable path | – | Confirmed | Exclude from build; keep ignored | No |
| G-34 | Medium | EVID | CLAUDE.md "temporary arrangements" | Every sandbox arrangement cleared at go-live | Register exists; items live (tunnel, sandbox flags, placeholder return URL) | register | Go-live blocker if not cleared | – | Confirmed | Gate in P10 | No |
| G-35 | Low | DECN | SPEC §21.1 | Defined precedence between a qualifying combo and a coupon | Agent default "combo kept unless customer picks coupon" | `pricing.py` docstring | Business-visible behaviour not approved | – | Confirmed | HU+DI decide | Yes |
| G-36 | High | DECN | ARCH §11, §15; hosting report decision 1 | Approved order/shipment state model for Zoho-managed shipping | `OrderStatus` has 9 values; post-shipment states never approved; ARCH defers "how EffyKlean receives status" | `models.py:6-13` (per hosting report), ARCH §15 | Blocks G-01/G-02 | HU+DI | Confirmed | Decide | Yes |
| G-37 | Low | DFR | SPEC §30.4 | Performance/availability/accessibility targets | None approved; dev-machine timings only; no accessibility assessment | J08 doc | Unknown readiness | HU targets | Confirmed | Define | Yes |
| G-38 | Medium | EVID | HU item 11; ARCH §25 | Production backups and a drill | Local drill only; DO Managed DB backups unverified; retention deferred | `BACKUP_AND_RESTORE.md` | Data-loss risk | Hosting | Verify | P6 | Yes (retention) |
| G-39 | Medium | MISS | SPEC §26.1 | Operational monitoring and alerting | Console logs + `/healthz` | `base.py:207-217` | Outages unseen | Hosting | Confirmed | P6 | No |
| G-40 | Medium | EXT | HU item 13 | Seven extra Zoho Inventory scopes and Payments settings scopes | Authorised for sandbox by HU; token not re-issued | register | Invoice, packages and price paths untestable | HU consent action | Verify | P8 | No (already authorised) |
| G-41 | Medium | EXT | Plan B-16; HU item 7 | Zoho Flow/invoice automation shown to work without duplicate Sales Orders | Flow not inspected; Sales Orders stay uninvoiced/unpaid in sandbox | DiReview §5 | Possible duplicate or missing invoices in production | Zoho access | Verify | P8 | No |
| G-42 | Medium | EXT | SPEC §14 | Real stock read and decrement | Sandbox stock zero; earlier forced 999; decrement unproven | DiReview §5 | Overselling risk unknown | Zoho sandbox stock | Verify | P8 | No |
| G-43 | Low | DECN | SPEC §5.4, 27.4 | RBAC matrix approved | Eight new capabilities held by both roles pending HU+DI; Marketing function given to both | `authority.py` comments | Over-broad Admin rights | HU+DI | Confirmed | Approve or narrow | Yes |
| G-44 | Low | DECN | SPEC §23.1; AC-23.1 | "Reviewed, not blindly copied" | HU approved copying effyklean.com content as is (2026-10-17) | CLAUDE.md principle 7 | Criterion contradicts decision | CR | Confirmed | Amend AC | Yes |
| G-45 | Low | TEST | SSD §4 | No silent failure | 28 `except Exception` sites; money-path ones record failure; 5 earlier lacked rationale comments | §7.2 | Low | – | Confirmed | Annotate | No |
| G-46 | Medium | MISS | SPEC §13.13; AC-13.7 | Distributor/Bulk payable amount never guessed when Zoho tax data is unavailable | GST is computed locally, so the scenario cannot arise and no guarded path exists | `tax.py` | Conflicts with Zoho authority | G-04 | Confirmed | Resolve with G-04 | Yes |
| G-47 | Medium | EVID | SSD §2 | Provider behaviour observed in the right environment | Everything external is mock/stub or sandbox-reported; no production and no Shiprocket evidence | records | Production readiness unknown | HU access | Confirmed | P8 gate | No |
| G-48 | Low | TEST | SSD §8 | Browser/E2E checks reproducible | Browser checks were manual agent runs; none in CI | records | Regression exposure for UI | – | Confirmed | Optional P9 | No |
| G-49 | Medium | MISS | SSD §7 | Dependency and security scanning | No `pip-audit`, no `check --deploy`, no ruff security rules in CI; `noqa: S110/BLE001` refer to rules not enabled | `ci.yml`, `pyproject.toml` | Unknown known-vulnerable packages | – | Confirmed | P5 | No |
| G-50 | Low | TEST | SSD §4 | Guard tests not weakened | Guard allow-lists and query budget widened to admit new files/tables | agent reports | Low | – | Verify | Review in P0 | No |
| G-51 | High | DECN/DEF | SPEC §16.1-16.3, 14.10; AC-16.1-16.3, 16.9, 14.6; ledger ORD-064, ORD-019; Delta plan §3.1 and §6; reconciliation record §3, §6; HU_DI_122 master "Governing authority" | The frozen SPEC, HU's recorded NO decisions and the build agree on who may cancel and which Admin capabilities exist | HU's recorded decisions state "no customer cancellation or editing after order placement; Admin may cancel" and list ORD-064 (customer-initiated cancellation) and ORD-019 (amount-range filter) as NO; Plan §3 also lists returned-package inspection (ORD-076) as NO. The frozen SPEC gives a B2C customer a 20%-charge cancellation before handover, and the build implements all three: two-step cancel on `/track/` (`order_pages.py:66-80`, `checkout_pages.py:959-961`, `operations.customer_cancellation_status`), an amount filter on the Admin order list (`ops_views.py:205-327`, `staff_view.py:268-322`; RUN_RECORD §10), returned-package inspection (`returns_views.py`) which SPEC §14.10 requires. The 597 file marks ORD-019/064 "implemented" and ORD-076 "awaiting HU+DI decision" | ledger lines for ORD-064/019; plan §3.1/§6; code files cited | Either a live customer feature contradicts HU's recorded NO, or the plan's NO list contradicts the SPEC HU froze; an agent also built a NO-listed capability (ORD-019) with no recorded override | HU+DI | Confirmed (both sides read) | STOP → REPORT: DEC-23 | Yes |
| G-52 | High | MISS/DEF | Ledger ORD-080/081 YES; Plan §3.1; reconciliation §5.1; SPEC §15.5, 18.1; AC-12.9 | Admin can mark an order fulfilled, add tracking or leave it blank for local pickup (audited; never shown as carrier-confirmed unless it is) | Not built. The only delivery writer is `operations.apply_delivery_update` (needs a CREATED shipment and a SHIPMENT_PENDING order), reachable only from the stub-only Admin simulation (`order_actions.py:345-380`). No fulfil, tracking or pickup action exists | code read | With the real Zoho adapter no one can record a handover, tracking number, pickup or delivery; customers never leave "Order Confirmed"; the approved interim workflow is absent | DEC-28 (and DEC-03 for state names) | Confirmed | P2-06 | Yes |
| G-53 | High | DEF/DECN | Register B-08 (BLOCKED); ARCH §14; HU 18-Oct item 20 | Website products and customers reach the production Zoho organisation in the approved way; a first-time customer's paid order creates a Zoho Sales Order | `zoho_sync.writes_allowed` (`orders/zoho_sync.py:112-120`) allows provider writes only for a stub or `ZOHO_INVENTORY_SANDBOX`, which `production.py` refuses, so product and customer sync tasks can never write to the real organisation. `ZohoInventory._customer_id` (`zoho_inventory.py:544-562`) needs an existing active Zoho contact for the e-mail or `ZOHO_INVENTORY_WEB_CONSUMER_CONTACT_ID` (not required by `production.py`); otherwise `ZohoMappingError`, three attempts, `ZOHO_SYNC_FAILED`. `sales_order_writes` defaults True | code read; `check_zoho_access`/sandbox docs | Every first-time customer's order fails to reach Zoho unless the contact already exists; a shared contact would put all web orders, including GST-registered buyers, on one Zoho customer | DEC-24 | Confirmed | P1-07, P3-07 | Yes |
| G-54 | High | DEF/DECN | ARCH §22 (availability projection deferred); AD-11; AC-6.9, 11.2; HU intent (change-triggered sync plus hourly reconciliation) | Fresh availability without exhausting the Zoho API or taking the catalogue down with it | `catalogue.customer_view._product` calls Zoho `check_availability` for every product on each list, detail (plus up to four related products), cart, checkout review and pay request, with no cache; a Zoho failure returns HTTP 503 "temporarily unavailable" for the page. `tests/test_i03_cart.py::test_cart_never_calls_the_provider_for_a_quantity_or_reserves` asserts the calls happen. PROJECT_LOG records 100 requests per minute for this account; Zoho's published FAQ (first pass, class 3) sets 1,000-5,000 calls a day on lower plans | code and test read | One crawler or a busy hour can exhaust the quota or the minute limit and blank the whole storefront | DEC-25 | Confirmed (code); quota arithmetic needs the account's plan | P1-08, P6-07 | Yes |
| G-55 | Medium | DEF | SPEC §9.6, 19.1; AD-06 | A business role attaches only to an identity the staff verified | Customer registration performs no e-mail verification (README says so) and `business_roles.provision` (`identity/business_roles.py:54-92`) adds the role to an existing consumer account found by e-mail; the Admin message says the holder keeps their current password. Anyone who registered an account with another person's e-mail before provisioning inherits business pricing and quote acceptance; a phone clash can also block provisioning | code read | Account takeover of business pricing; wrong person receives quotes | DEC-27, e-mail channel | Confirmed | P1-10, P5-05 | Yes |
| G-56 | Medium | MISS | SPEC §19.1; README ("no password reset") | A customer who forgets a password can recover the account | No reset flow: `setup_token_for_new_account` refuses accounts that already have a password; no e-mail channel; business set-up links are delivered by hand | code read | Lost accounts; staff workload | G-05, DEC-27 | Confirmed | P5-05 | Yes |
| G-57 | Low | DEF | SPEC §26.1 | Throttles and audit use the real client address behind the DigitalOcean proxy | `REMOTE_ADDR` is the only source (`customer_accounts`/`account_pages.py:46`, `contact_pages.py:114`, `audit.py:142`); behind the App Platform proxy all visitors share one bucket (contact form 10 per hour, customer sign-in 30 failures per 15 minutes) and every Admin audit row records the proxy address | code read | One visitor can lock out others; audit IPs useless | P6-02 topology | Confirmed | P5-06 | No |
| G-58 | Medium | MISS | SPEC §9.1, 10.1, 26.1 | Public enquiry forms are abuse-resistant and staff learn of enquiries | Bulk enquiry and Distributor application forms have no throttle or CAPTCHA (the contact form and subscribe do); staff see enquiries only after Admin login (in-app alerts) because no e-mail exists | code read | Spam floods the review queue; real enquiries unseen | G-05 | Confirmed | P5-06 | No |
| G-59 | Medium | TEST/DEF | SSD §8; AC-29.3; CI | Every test passes on a clean checkout | `tests/test_ac_structural_evidence.py` (untracked) reads `media/catalogue_source/source.json`; `media/` is git-ignored and wholly untracked (`git ls-files media` returns 0), so the test fails on any clean clone and in CI once committed; the AC-26.1 test also shells out to `git ls-files`. The 1.3 GB `media/` tree (images, videos, catalogue source) exists only on this workstation | `git ls-files`, `git check-ignore`, test read | A red CI at the first commit of this tree; media has no source-control backup | P0-01 | Confirmed | P0-06 | Yes (commit) |
| G-60 | Low | DEF | ARCH §17.2 ("non-retryable errors terminate immediately") | A validation/mapping/auth/not-supported Zoho error ends the step at once | `checkout._try_zoho_confirmation` treats every raised error as a failed attempt; Zoho errors with `retryable=False` (`zoho_inventory.py:99-144`) still burn three attempts (the customer/product sync tasks do classify) | code read; register B-15 | Two wasted provider calls and a delayed exception queue entry | – | Confirmed | P2-07 | No |
| G-61 | Medium | DECN/DEF | SPEC §6.4; AC-6.4; Status register decision (3) and D-B1 | MRP is verified product data before customers see it | The 15 published products were imported with `--assume-compare-at-as-mrp` (Shopify compare-at used as MRP); the register records "unverified demonstration value"; MRP lives on the SKU with no provisional marker, so approval and publication expose it; the storefront shows "MRP: ₹…" | ZOHO_INVENTORY_SANDBOX_VALIDATION; status register rows; AC-6.4 test (read) | Possibly wrong MRP shown to customers and used for savings figures | DEC-26 | Confirmed (records); values need HU | P1-09, P7-04 | Yes |
| G-62 | Medium | DEF | ARCH §18, §26; DO plan §3 | The application connects to Managed PostgreSQL over enforced TLS with a deliberate connection policy | `database_config()` (`base.py:23-34`) has no `sslmode` (libpq default `prefer`, which can fall back to plain text) and no `CONN_MAX_AGE`; ARCH §27.1 item 5 (connection strategy/capacity) is open; the advisory-lock jobs also assume a direct connection | code read; DO setup report | Unencrypted DB traffic possible; connection storms on a 1 GiB managed database | hosting | Confirmed | P5-07 | No |
| G-63 | Medium | DEF/DOC | CR-008; SPEC §17.2, 17.3, 23.5(c); AC-17.3, 17.6 | Customer-facing replacement wording states video evidence is required and that a request can be made on the website or through Customer Care | The Replacement policy page and FAQ say "photos or a video" and (FAQ) "through Customer Care" only (`policy_pages.py:115, 176`); `tests/test_storefront_policies.py::test_replacement_page_states_24_hours_with_evidence` asserts "photos or a video"; the tracking-page form itself says a video is needed (`order_pages.py:140`) | code and test read | Customers told photos suffice; staff then refuse; inconsistent policy | DEC-29 | Confirmed | P4-04 | Yes (wording) |
| G-64 | Low | DEF/DOC | SPEC §23.4, 26.3; ledger | Footer policy links resolve and policy text is consistent | The footer always links `/policies/{privacy-policy,refund-policy,terms-of-service,shipping-policy,contact-information}/` (`site.py:93-97`); the pages exist only after `load_policy_pages` is run on the target database (no document schedules it for production); the privacy text still contradicts itself on cookies and uses US/EU rights wording (PRIVACY_POLICY_CHANGES_FOR_HU_REVIEW) | code and docs read | Broken links at launch; legal text unapproved | DEC-11 | Confirmed | P4-04 | Yes |
| G-65 | Low | DEF | SPEC §9, 10 | Business customers can buy in agreed quantities | Cart limits are hard-coded at 100 units per line and 20 lines (`cart_pages.py:35-37`, repeated in the API contracts) and apply to Distributor/Bulk accounts; a Bulk quote with an agreed quantity above 100 cannot be ordered at once | code read | Large Bulk orders need several orders | – | Confirmed | P9-04 | Yes (limits) |
| G-66 | Low | mixed | various | Minor findings closed or accepted | Sixteen small items are listed in §8.3 | see §8.3 | Low individually | – | Confirmed | P9-04 | Some |
| G-67 | Medium | DEF | SPEC §26.1; AD-16; ARCH §18 | Single-use secrets do not appear in logs or Referer headers | Subscribe confirm and unsubscribe tokens, the customer set-password link (`/account/setup/?token=…`) and the business set-up link travel in the URL query string (`customer_admin_views.py:105`, `subscribe_pages.py`); the proposed App Platform run command uses `--access-logfile -`, which logs the full request line, and the documents themselves note the logging gate (SUBSCRIBE_VERIFIED "Production logging note") without a task. A holder of the logs can use a live 72-hour set-up link or verification token | code and docs read | Account set-up takeover or subscription confirmation by anyone with log access | hosting | Confirmed | P5-08 | No |
| G-68 | Medium | EXT | SPEC §12.9, 17.4, 18.9; AC-12.9, 17.4 | EffyKlean can learn that a Zoho/Shiprocket shipment was delivered | Provider evidence (PROVIDER_EVIDENCE_AND_SUBSCRIBE §5.3, class 3): of five Shiprocket shipments in Zoho, two still show "Shipped" months later, status is pulled on demand ("Check Status") rather than pushed, and Shiprocket's own webhook is DISABLED. A scheduled read of Zoho may therefore never see Delivered for some shipments, which the replacement window (SPEC 17.4) and saved-address renewal depend on | docs read | Replacement requests cannot start; addresses never renew | DEC-03; Zoho/Shiprocket support answer | Verify (provider behaviour unobserved by the assessor) | P2-03 (stale-status view) | Yes |
| G-69 | Medium | EXT/MISS | SPEC §11, §13, §14; Zoho authority; AC-6.5 | Production Zoho item mapping is possible by a sanctioned, reviewed path | Development `zoho_item_id_sku` values are SKU-code placeholders (for example `EK-HHLD-X`). `sync_zoho_items --apply`, even mapping-only, requires `ZOHO_INVENTORY_SANDBOX=1`, `--confirm-organization` and a non-live organisation, so it refuses the live organisation. Availability is `GET /items/{item_id}`, so placeholders return 404. Two sandbox SKUs (`EK-HHLD-AR` rate 10, `EK-HHLD-FCP` rate 80) differ from website prices; sandbox stock is zero. Only manual per-product Admin edits remain | `sync_zoho_items`, `zoho_item_sync.py`, CATALOGUE_FIELD_COVERAGE (read) | A production go-live cannot map the 15 products to real Zoho items without an unreviewed manual step | DEC-24 | Confirmed (code and docs) | P1-07 extension, P3-07 | Yes |
| G-70 | Medium | DECN | SPEC §13.10; architecture GF-7; ledger ORD-090 | The customer receives the Zoho GST invoice, and one party is named to send it | Nobody is specified to send it: Zoho-owned, not built, no e-mail provider | `ARCHITECTURE_RECONCILIATION_V0.7` GF-7; ledger | Customers may receive no invoice from either system | DEC-31; G-05 | Confirmed (records) | P4-01 extension | Yes |
| G-71 | Low | DECN | SPEC §14.5; architecture discovery §13 | A written rule for a paid order whose Zoho or stock confirmation never succeeds (fulfil or refund) | Only the exception state exists; no resolution policy or staff runbook | architecture discovery §13; SPEC §14.5 | Staff have no rule; inconsistent handling | DEC-31 | Confirmed (records) | P1-05 extension | Yes |
| G-72 | Low | OPS/EVID | AD-04, AD-17 | App Platform egress IP, provider IP allow-lists, webhook reachability and Tuesday Customer Care closure (replacement 24-hour window) are checked | No record that any of these was checked | capability validation R-13; AD-04 risks | Provider calls may be blocked after deployment | Hosting (P6-02) | Verify | P6-02 extension | No |
| G-73 | Low | DECN | Consolidation readiness §B items 4-5; 2026-10-05 matrix rows 20, 21 | Distributor monthly investment/budget qualification checkpoint and nearest-warehouse selection are built or formally retired | Both were recorded as HU+DI inputs; neither appears in code (no budget field, no warehouse logic) and no later record retires them | grep of `modules/`; `ARCHITECTURE_CONSOLIDATION_READINESS.md` | Recorded decisions with no implementation or retirement | DEC-31 | Confirmed | P1-05 extension | Yes |
| G-74 | Low | DECN | Carry-forward matrix BD-11; inventory ORD-113, ORD-114 | A defined process for payment disputes/chargebacks and post-placement order change requests | SPEC-silent and never decided; only reversed payments (AC-12.19) are handled, with no dispute workflow or runbook | carry-forward matrix §E; inventory | A chargeback has no process | DEC-31 | Confirmed (records) | P1-05 extension | Yes |
| G-75 | Low | DEF/DECN | HU 18-Oct request (valid city, PIN, state, country); `enquiry_form.py` | Only valid city, PIN, state and country are accepted | Validation checks state, six-digit PIN and PIN-to-state prefix only. The PIN-region table is hand-typed and sampled (95 PINs) against India Post, not exhaustively checked. A real PIN with a made-up city passes. Contact-page phone and spelling differ from effyklean.com (+91-843-183-7330, Bhoganahalli) and HU has not chosen. Call hours 9:00-17:00 IST, the 1-60 day window and the 10,000-25,000 band reading are agent defaults | 18-Oct agent transcript (read) | Invalid addresses can be accepted | DEC-31 | Confirmed | P1-05 extension, P5-04 | Yes |
| G-76 | Medium | DECN/DEF | HU+DI mapping D-C1, D-C2; DC-08; SPEC §7.7, §15.8, §16.2 | Editable order fields match DC-08; a guest's cancellation authentication is decided | `EDITABLE_FIELDS` (`modules/orders/operations.py:69-80`) lets staff change customer e-mail, GST number and company name before handover, broader than DC-08 (name, address, phone only; GST not editable because it drives the invoice). A GST correction after Zoho confirmation can desynchronise the invoice (a person-action is queued but not prevented). A guest can cancel from the tracking page with order ID plus contact, the factor that unlocks tracking (D-C2). Neither decision is recorded as answered | `SHOPIFY_ADMIN_FEATURE_MAPPING.md` §11; code | Invoice/order mismatch; cancellation by anyone who knows both values | DEC-32 | Confirmed | P1-06 extension, P2-04 | Yes |

---

### 8.3 Minor findings (Low) found in revision 2

Each is confirmed by reading the cited code; none is individually launch-blocking. All are carried by task P9-04 (G-66).

| # | Finding | Evidence |
|---|---|---|
| m1 | `payment_return` runs `submit_to_zoho` inline in the customer's browser request, and each new-customer sync lists every Zoho contact (up to 50 pages) through `_refuse_conflicting_phone`: latency and API budget on the customer's return page | `checkout_pages.py`, `zoho_sync.py` |
| m2 | The F-06 API orders carry no state or address block, so they cannot be synced to real Zoho (order POST also needs the stubs and returns 503 in production); the guest `GET` order lookup by `X-Customer-Email` is public and unthrottled | `storefront/views.py`, `contracts.py` |
| m3 | The storefront CSP header is report-only with no `report-uri`/`report-to`, so the "review violation data" step of DEC-16 has no data source in production | `config/security.py`, `storefront_csp.py` |
| m4 | Subscribe: the global verification-mail cap (500 per hour) lets a third party mail-bomb a victim's address at one message per cooldown; `consent_text_version` is the draft marker "draft-0" | `subscriptions.py`, `base.py` |
| m5 | Contact messages and enquiries are never e-mailed to staff; they appear only in the Admin after sign-in | `contact.py`, `contact_views.py` |
| m6 | A replacement decision `APPROVED` is terminal; no replacement shipment or order is modelled, so what happens after approval is manual and undocumented | `operations.py`, `replacement_views.py` |
| m7 | The Admin sales report counts cancelled orders in sales totals (shown separately) by documented definition; finance may expect net figures | `staff_view.sales_report` |
| m8 | The Admin to-do "Orders ready to dispatch" and the sidebar count are orders with no CREATED shipment, so under Zoho-owned dispatch they stay non-empty forever | `shell.py:184-195`, `home.py` |
| m9 | Admin sign-in throttle: five failures lock any staff account for the window, so anyone who knows a staff e-mail can lock them out | `backoffice/throttle.py` |
| m10 | Product images are read from the bucket and proxied by the application on every request (immutable cache header, no CDN); only videos get a public CDN URL | `media.py`, `site.py` |
| m11 | `CommercialForm` validates combo ≤ sale price but not MRP ≥ sale price; price changes apply instantly (audited, but not approval-governed; SPEC is silent) | `forms.py:39-80`, `products.py` |
| m12 | Stale wording: the `distributor_views` docstring says approval creates no account although provisioning exists; ARCHITECTURE.md header still says "Implementation NOT AUTHORIZED" and "139 acceptance criteria"; README describes Razorpay Phase 1 as current and "nothing has been pushed" | files cited |
| m13 | Deploy steps that no document schedules for production: `load_policy_pages`, `load_howto_videos` (needs the recovered files in `media/videos`), first staff account via `createstaff`, catalogue data load | management commands |
| m14 | The "no same-day dispatch" rule exists only in PROJECT_LOG (SPEC is silent; the agent noted it); HU says Zoho owns timing, so the website's own rule duplicates Zoho (see G-28) | PROJECT_LOG 2026-10-10 |
| m15 | `scripts/ci.sh` and the CI workflow run no `check --deploy`; the three remaining `check --deploy` warnings (W003, W005, W021) are documented only in agent records | status register |
| m16 | Template audit (mechanical): no `|safe`, no `autoescape off`, no `<script>`, no external URL in any of the 84 Admin templates; CSRF token present in every file that posts (134 POST forms); 9 inline `style=` attributes are permitted by the Admin CSP (`style-src 'unsafe-inline'`). Recorded as a positive finding | `grep` over `templates/backoffice` |
| m17 | Customer cancel and confirm pages (`checkout_pages.py:950`, `order_pages.py:75`) say "Refund to your original payment method: ₹X" while real refunds are manual (staff act in the provider dashboard, MANUAL_REQUIRED) and no e-mail or timeline exists. |
| m18 | Staff password recovery is operator-CLI only (`manage.py changepassword`, `resetstaffmfa`; `createstaff` refuses an existing e-mail); no runbook; the sole Director depends on shell access (ledger USR-003/004 deliberately CLI, decision D-F2 open). |
| m19 | `test_database` pins PostgreSQL major version 17, so DigitalOcean Managed PostgreSQL must match; scheduling advisory locks assume a direct connection (links G-62). |
| m20 | More stale documents: `LOCAL_DEMO.md` (Razorpay, no customer accounts), `VIDEOS_2026-10-11.md` (hot-linked CDN videos, superseded), `STOREFRONT_CONTENT_SOURCES.md` (privacy/terms 404, superseded by `/policies/<slug>/`), `CONVENTIONS.md` (INSTALLED_APPS historical). Plan §3.8 says keep the MARKETING role versus HU 18-Oct (no Marketing role). |
| m21 | `FINAL_ARCHITECTURE_DECISION_GATES.md` and `FINAL_ARCHITECTURE_COST_OPTIMIZATION.md` (read in full) are superseded history: they recommend AWS (excluded by AD-04), SPEC v0.4, Procrastinate, `max_attempts=3` as 3 retries (superseded by 3 total attempts) and a 429-as-deferral rule that remains unapproved; the gate-2 prepaid 'left at address' feasibility question is still unevidenced by any Shiprocket confirmation. |

---

## 9. Additional defects, risks, overlooked requirements and hidden dependencies

Items below were found or sharpened by this assessment (NEW) or were known but are re-stated with the evidence that matters (KNOWN). All are in the register of §8.2.

**Defects and risks**
1. **NEW — one root cause kills five features (G-01/G-02).** The absence of an inbound delivery feed disables, in production: customer status progression, tracking link, replacement requests, returned-package recording, saved-address reset after delivery, and makes the cancellation cutoff wrong. Agents recorded "no inbound path" (register C-02) but not that replacement and cancellation silently depend on it.
2. **NEW — customer cancellation by anyone who knows reference + contact (G-11).** `/track/` and the cancel steps are unthrottled; the reference has a 5-digit daily sequence. A wrong cancellation costs the customer 20% (SPEC §16.3) and voids the Zoho Sales Order.
3. **NEW — production guard asymmetry (G-32).** `ZOHO_PAYMENTS_SANDBOX` is not refused in production while the Inventory sandbox flag is; `PUBLIC_BASE_URL` defaults to localhost; the default From address is an `.invalid` domain; `CSRF_TRUSTED_ORIGINS` is unset.
4. **NEW — CI record error (D-6).** Records say CI never ran; it ran 12 times. The real risk is the opposite of what is recorded: the tree being accepted has no CI evidence.
5. **NEW — spurious AC credit (G-21)** and 20 ACs backed only by structural tests.
6. **NEW — possible display/charge mismatch (G-22)** on a transient lookup error for business customers.
7. **KNOWN — GST rule versus frozen SPEC (G-04)** affects every discounted order and every business order, and the Zoho invoice may then disagree with the amount paid. The Zoho total-equals-amount-paid guard (RQ-09) hides the difference by failing the sync rather than correcting it.
8. **KNOWN — cancellation of an order whose Zoho Sales Order has already progressed** (`cancel_in_zoho` voids it). If Zoho created a package/shipment from the confirmed order, voiding may fail or be refused; no test or evidence exists for that real state (G-01/G-41).
9. **KNOWN — duplicate-payment path ends in a manual refund** in the provider dashboard (log text in `payment_flow.py`). Acceptable by decision (B-13), but there is no reconciliation report that proves every duplicate was refunded.
10. **KNOWN — outbox lock model.** `run_scheduled` uses a Postgres session advisory lock; behind a pooled connection in transaction mode it is unreliable (hosting report §3). Hidden dependency on how the DB connection string is configured.
11. **KNOWN — undelivered-code risk.** Migrations 0025-0027 are untracked. A commit that includes the modified `models.py` but not the migrations breaks `migrate` and CI (`makemigrations --check`).

**Additional defects and risks (revision 2).**
12. **NEW — HU's recorded NO list is not enforced by any check (G-51).** Nothing compares the plan's 50 NO identifiers with the code; ORD-019 and ORD-064 were built and the 597 file calls them "implemented".
13. **NEW — the approved interim fulfilment action does not exist (G-52)**, so even a perfectly configured production site cannot show tracking, pickup or delivery until the inbound feed exists.
14. **NEW — production cannot write to Zoho by design (G-53).** The only authorised write path is sandbox-or-stub, so go-live as the code stands leaves orders in `ZOHO_SYNC_PENDING`/`FAILED` for new customers.
15. **NEW — storefront availability is a live dependency of every page view (G-54).** An outage or quota exhaustion at Zoho blanks the catalogue.
16. **NEW — customer identity is unverified (G-55, G-56)** while business pricing and quote acceptance hang off the same account table.
17. **NEW — the first commit of the working tree would break CI (G-59)**, and the originals of all media exist only on one workstation.
18. **NEW — MRP shown to customers may be Shopify compare-at (G-61)**, contrary to AC-6.4, and it feeds the Bulk savings screen.
19. **NEW — policy wording contradicts CR-008 (G-63)** and its test enshrines the old wording.
20. **KNOWN, CONFIRMED — governance documents carry stacked, partly contradictory state (G-20, m12).**

**Overlooked or under-specified requirements**
1. HU 18-Oct items 15/20: "reproduce the functionality represented by Shopify/effyklean.com and keep its **integrations** working with EffyKlean Admin": there is no inventory of the live Shopify integrations (sales channels, marketing/analytics apps, notification apps) with a keep/replace decision. 597-file rows for "Sales channels" (8) and "Integrations & apps" (15) are DEFERRED.
2. SPEC §14.8 low-stock alerts are left to Zoho (HU item 20); no verification that Zoho is configured to notify.
3. SPEC §6.15 quarterly review exists as an Admin queue; nothing notifies the team (no e-mail channel, G-05).
4. SPEC §10.13 Bulk savings screen was never viewed in a browser (agent admission).
5. SPEC §26.2 cookie/analytics consent has no implementation path while analytics is parked (G-29, G-06).

**Hidden dependencies (deployment and operation)**
- Production start-up needs, in this tree: 13 Zoho variables, an S3 bucket (five values), `ALLOWED_HOSTS`, `SECRET_KEY`, DB variables, an SMTP backend, and `TRUST_FORWARDED_PROTO=1` behind a proxy; and (undeclared) `PUBLIC_BASE_URL`.
- Order creation to Zoho needs `ZOHO_SYNC_ENABLED` and `ZOHO_SALES_ORDER_WRITES_AUTHORIZED` plus tax ids; without them every order sits in ZOHO_SYNC_PENDING.
- The outbox and reconciliation are inert until a worker/scheduler runs them (G-24).
- Zoho Payments return URL and webhook need a stable public HTTPS endpoint (G-07).
- `scripts/ci.sh` expects PostgreSQL 17; local test execution needs Docker or a local server (not available to this assessment).

---

## 10. Test, CI, quality, security, business-rule and operational-readiness assessment

### 10.1 Tests and quality gates

| Dimension | Finding | Evidence class |
|---|---|---|
| Test inventory | 2,491 tests collected; 106 test files; 33.5k lines; strongest areas: payments (`test_zoho_payments`, `test_payment_reconciliation`, `test_phase1_payments`), outbox/safeguards, pricing, replacement evidence, checkout integrity | 1 |
| Pass evidence | Last recorded full run 2,491 passed on the final local tree (2038 s), PostgreSQL 17, mock/local only; earlier runs 1,894…2,490 | 3 (not re-run: no database available to the assessor) |
| Test quality (sampled) | Four bodies read in full (`partial_or_mismatched_amount`, `cancellation_20_percent`, `no_qualifying_video`, `one_sales_order`): meaningful asserts on outcomes, idempotency, state and money | 1 |
| Test integrity | 0 skip/xfail; by AST analysis 5 of 1,790 test functions have neither an assert nor `pytest.raises` (benign smoke tests); no `assert True`; AC-9.9 false credit and the AC-9.7 incidental tag; 20 structural-only ACs; 819 cited names in the 597 file all exist; one new test depends on an ignored file (G-59) | 1 |
| Test quality (revision 2) | 104 test bodies attached to 80 acceptance criteria read in full: they assert outcomes (states, amounts, idempotency, audit rows, response bodies); several run against local stubs or fake transports and say so; two enshrine questionable wording (G-63) or a mis-tag (AC-9.7) | 1 |
| Lint/format/system check | ruff check and format clean (331 files); `manage.py check` clean | 1 |
| Migration drift | `makemigrations --check` is part of `ci.sh` and `test_migrations`; the assessor did not run it (needs a DB handshake) | 3 |
| CI | Exists; 7/12 runs green; last green 17 Oct on `513fc98`; none on the current tree | 1 (`gh`) |
| Browser/E2E | Manual headless-browser runs by agents; none in CI | 3 |
| Load/performance | Dev machine only | 3 |

### 10.2 Integration evidence matrix (SPEC distinction: implementation / local / mock / sandbox / production)

| Integration | Code in EffyKlean | Local tests | Mock tests | Sandbox | Production |
|---|---|---|---|---|---|
| Zoho Payments | Yes (`zoho_payments.py`) | Yes (fake server) | Yes | Session creation, hosted checkout, signed return, failure/replay/tamper cases **reported** 16-17 Oct; **webhook not registered** | None |
| Zoho Inventory | Yes (`zoho_inventory.py`): availability, SO create/confirm/cancel, items, contacts | Yes | Yes | Reads verified; Sales Orders SO-00002…5 created/confirmed/read back **reported**; stock zero; invoices/packages not observed | None |
| Shiprocket (via Zoho) | **None** in EffyKlean (adapter raises by design); local stub only | Stub | – | Not tested (HU deferred) | None |
| E-mail (GoDaddy SMTP) | Config + `check_email_config`; only Subscribe sends | Stub backend | – | None | None |
| WhatsApp | Admin number setting only | – | – | – | – |

### 10.3 Business-rule enforcement (read in code unless marked)

| Rule | Verdict |
|---|---|
| NO PAYMENT → NO DISPATCH (AD-10) | Enforced: order exists only after provider capture; outbox refuses shipment without a succeeded payment (tests M; `place_order`/`request_shipment` read). Holds regardless of G-01 |
| No COD, 100% prepaid | Enforced by absence; tests and wording scan |
| B2C chain, ₹500 only with an additional discount, one additional discount | Enforced (`pricing.py` read) |
| 20% cancellation charge before handover | Enforced for amount; **cutoff wrong under real Zoho** (G-02) |
| Replacement windows 24 h / 24-72 h exception / >72 h auto-reject, video evidence | Enforced in code (`operations.py:472-640` read); unusable in production (G-01) |
| Distributor/Bulk: one percentage, Admin proposes / different Director approves, no stacking, no combos | Enforced (tests M; `_price_business_cart` read) |
| Business role removal Director-only; deletion Director-only | Enforced (`authority.py` read) |
| GST rule | Implemented but conflicts with frozen §7.9/7.10 (G-04) |
| Zoho authoritative for stock/GST/invoice | Stock yes; GST computed locally for payable; invoice not surfaced |
| Idempotency, 3 total attempts, correlation ids | Enforced (read `payment_flow`, `outbox`, `checkout`) |
| Historical price immutability | Order lines snapshot price/MRP (tests M) |
| Customer-initiated cancellation | Built and tested, but contradicts HU's recorded NO (ORD-064; G-51) |
| Admin-only fulfilment/tracking record (ORD-080/081) | Not built (G-52) |
| Verified MRP (AC-6.4) | Not enforced for the 15 published products (G-61) |
### 10.4 Security assessment (code reading; no penetration test)

Strengths: mandatory MFA, per-view CSRF on Admin plus origin/Sec-Fetch-Site checks on every unsafe request, Admin headers (no-store, CSP, frame deny), Host validation, HSTS and secure cookies in production, signed cart cookie holding only id and quantity, server-recomputed totals with a signed review token, HMAC-verified webhooks that cannot place an order by themselves, no raw SQL beyond advisory locks and `SELECT 1`, no `mark_safe` except one admin tag, no secrets tracked. Weaknesses: G-11, G-27, G-32, G-49, G-55 (unverified customer identity attached to business roles), G-56, G-57 (client address behind a proxy), G-58, G-62 (DB TLS), m9 (staff lock-out); storefront CSP is report-only (RQ-30); customer-side CSRF relies on origin headers only (documented ADD-1 design; requests with neither header are allowed); `/EKIAdmin2026` obscurity (documented as not a control).

### 10.5 Operational readiness

Not ready: no hosting, no scheduler, no monitoring, no staging gate, no production backups, no go-live cutover plan, temporary arrangements not cleared, legal pages absent, no outbound e-mail. J-10 release gate re-checked by the agent: "still not releasable". The assessor concurs.

---

## 11. Consolidated outstanding-work register

Every gap of §8.2 is accounted for. "Action type": **Task** = implementation task in §12; **Decision** = HU+DI decision first (§14); **Evidence** = verification only; **Non-impl** = no code (records, external action). Items marked "(if decided)" are conditional on the decision.

| Gap | Sev | Action type | Plan task(s) | Decision(s) | Note |
|---|---|---|---|---|---|
| G-01 | Critical | Decision, Task, Evidence | P1-01, P2-01…P2-05, P8-03 | DEC-03 | core fulfilment chain |
| G-02 | High | Decision, Task | P1-01, P2-04 | DEC-03, DEC-04 | cutoff and replacement signals |
| G-03 | High | Decision, Task (if decided) | P1-04, P3-04 | DEC-06 | |
| G-04 | High | Decision, Task | P1-02, P3-01 | DEC-05 | STOP → REPORT |
| G-05 | High | Decision, Task | P4-01, P4-02 | DEC-10 | |
| G-06 | High | Decision, Task | P4-03 | DEC-11 | HU legal text |
| G-07 | High | Non-impl (HU action), Evidence | P8-01, P6-02 | DEC-18 | |
| G-08 | High | Decision, Task | P6-01, P6-02, P6-06 | DEC-12 | |
| G-09 | Medium | Evidence, Task | P0-01, P0-03, P5-03 | DEC-01 | |
| G-10 | High | Decision, Non-impl | P0-01, P0-02 | DEC-01, DEC-02 | |
| G-11 | Medium | Task | P5-01 | – | |
| G-12 | Medium | Decision, Task (if decided) | P1-04, P3-05 | DEC-07 | |
| G-13 | Medium | Decision, Task | P1-03, P3-02 | DEC-08 | |
| G-14 | Medium | Decision, Task | P1-03, P3-06 | DEC-08 | |
| G-15 | Medium | Decision, Task (if retained) | P1-03, P3-03 | DEC-08 | HU item 20 vs AC-13.8 |
| G-16 | Medium | Decision | P1-03 | DEC-08 | CR to SPEC |
| G-17 | Medium | Decision | P1-05 | DEC-09 | one question |
| G-18 | Low | Decision | P1-05 | DEC-15 | |
| G-19 | Medium | Non-impl (HU data), Task | P7-01, P7-02 | DEC-17 | |
| G-20 | Medium | Non-impl | P0-03 | – | |
| G-21 | Medium | Task (tests) | P0-04 | – | |
| G-22 | Low | Task | P3-01 | – | |
| G-23 | Low | Decision | P1-05 | DEC-14 | |
| G-24 | High | Decision, Task | P6-04 | DEC-12, DEC-13 | |
| G-25 | Low | Task | P5-04 | – | |
| G-26 | Low | Decision | P1-05, P5-04 | DEC-14 | |
| G-27 | Medium | Task | P5-01 | – | |
| G-28 | Low | Decision, Task | P1-01, P2-01 | DEC-03 | |
| G-29 | Low | Decision | P1-05 | DEC-14 | OQ-26 gate |
| G-30 | Medium | Decision, Non-impl | P10-03 | DEC-20 | |
| G-31 | Medium | Decision, Task | P6-03 | DEC-12 | paid service |
| G-32 | Medium | Task | P5-02 | – | |
| G-33 | Low | Task | P5-04 | – | |
| G-34 | Medium | Evidence | P10-03 | – | |
| G-35 | Low | Decision | P1-04 | DEC-07 | |
| G-36 | High | Decision | P1-01 | DEC-03 | |
| G-37 | Low | Decision | P10-01 | DEC-19 | |
| G-38 | Medium | Task, Evidence | P6-05 | DEC-19 | |
| G-39 | Medium | Task | P6-05 | – | |
| G-40 | Medium | Non-impl (HU action) | P8-02 | DEC-18 | already authorised |
| G-41 | Medium | Evidence | P8-02 | – | |
| G-42 | Medium | Evidence | P8-02 | – | |
| G-43 | Low | Decision | P1-05 | DEC-14 | |
| G-44 | Low | Decision | P1-03 | DEC-08 | |
| G-45 | Low | Task | P5-04 | – | |
| G-46 | Medium | Decision, Task | P1-02, P3-01 | DEC-05 | |
| G-47 | Medium | Evidence | P8-03 | – | |
| G-48 | Low | Task (optional) | P9-03 | – | |
| G-49 | Medium | Task | P5-03 | – | |
| G-50 | Low | Evidence | P0-04 | – | |
| G-51 | High | Decision | P1-06 | DEC-23 | STOP → REPORT; HU's recorded NO versus SPEC §16 and the build |
| G-52 | High | Decision, Task | P2-06 | DEC-28, DEC-03 | interim manual fulfilment record |
| G-53 | High | Decision, Task | P1-07, P3-07, P8-02 | DEC-24 | production write path and customer mapping |
| G-54 | High | Decision, Task | P1-08, P6-07 | DEC-25 | availability sync model |
| G-55 | Medium | Decision, Task | P1-10, P5-05 | DEC-27 | verification before business role |
| G-56 | Medium | Decision, Task | P1-10, P5-05 | DEC-27 | needs e-mail channel (P4-02) |
| G-57 | Low | Task | P5-06 | – | trusted proxy setting |
| G-58 | Medium | Task | P5-06 | – | |
| G-59 | Medium | Task | P0-06 | – | blocks a green first commit |
| G-60 | Low | Task | P2-07 | – | |
| G-61 | Medium | Decision, Task | P1-09, P7-04 | DEC-26 | HU supplies MRP values |
| G-62 | Medium | Task | P5-07 | – | needs the managed database (P6-02) |
| G-63 | Medium | Decision, Task | P4-04 | DEC-29 | |
| G-64 | Low | Decision, Task | P4-04 | DEC-11 | |
| G-65 | Low | Decision, Task | P9-04 | DEC-14 | |
| G-66 | Low | Task | P9-04 | – | §8.3 items m1-m16 |
| G-67 | Medium | Task | P5-08 | – | tokens out of URLs or logs |
| G-68 | Medium | Evidence, Task | P2-03, P8-03 | DEC-03 | stale Zoho shipment status |
| G-69 | Medium | Task | P1-07 (extend), P3-07 | DEC-24 | production Zoho item mapping |
| G-70 | Medium | Decision, Task | P4-01 (extend) | DEC-31 | invoice delivery to customers |
| G-71 | Low | Decision | P1-05 (extend) | DEC-31 | paid order with unconfirmed Zoho/stock: fulfil or refund |
| G-72 | Low | Task | P6-02 (extend) | none | egress IP, allow-lists, webhook reachability, Tuesday Customer Care closure |
| G-73 | Low | Decision | P1-05 (extend) | DEC-31 | distributor budget checkpoint; nearest-warehouse selection |
| G-74 | Low | Decision | P1-05 (extend) | DEC-31 | disputes/chargebacks and post-placement order change requests |
| G-75 | Low | Decision, Task | P1-05 (extend), P5-04 | DEC-31 | enquiry-form address data source, defaults, contact details |
| G-76 | Medium | Decision, Task | P1-06 (extend), P2-04 | DEC-32 | editable order fields; guest cancellation authentication |

**Not-built items from the 597 file and the 124 rows awaiting naming** are carried by P9-01/P9-02 (Appendix A lists them).

---

## 12. Proposed phased implementation plan

**This is a proposal. It authorises nothing.** Phases follow real dependencies: baseline and decisions first, then the lifecycle chain, then money/tax, communications and security, then hosting, content and sandbox acceptance, then release. No dates or durations are given: nothing in the record supports a defensible estimate (the only measured quantities are the 31-34 minute local full-suite run and ~9-minute CI run).

**How the 14 required task fields are carried.** Each task states, in order where relevant: source/traceability and current state, target outcome, scope, dependencies, priority, approach, Definition of Done, risks and approval gate. Fields not restated per task are inherited: *phase and objective* from the phase heading; *priority* from phase order (earlier phases are higher unless a task says otherwise); *verification requirements* from the DoD plus clauses C1-C6; *documentation and handoff* from C5; *risks and constraints* default to the frozen SPEC/ARCHITECTURE, NO PAYMENT → NO DISPATCH, regression of the existing local journey and secret hygiene; *approval gate* is the one named in the task, otherwise C4 (no external write, push or spend without approval).

**Common Definition-of-Done clauses (apply to every code task; not repeated):**
- **C1** Targeted tests for the task pass on PostgreSQL 17 with actual command output recorded (`uv run pytest <files> -q`, exit 0); new tests assert outcomes, not execution, and include at least one negative, one boundary and one failure-path case where relevant.
- **C2** `uv run ruff check .`, `uv run ruff format --check .`, `uv run python manage.py check`, `uv run python manage.py makemigrations --check --dry-run` all exit 0.
- **C3** No test is skipped, xfailed, weakened or deleted; any assertion change is justified in the handoff with the original protection shown to remain.
- **C4** No provider write, e-mail, shipment, deployment, push or history change occurs unless the task's approval gate names it; stubs/mocks/sandbox are labelled in evidence.
- **C5** Handoff updates `PROJECT_LOG.md`, the Delta status register and, where relevant, the AC index (`python scripts/ac_index.py`, then `--check` exit 0), without editing frozen SPEC/ARCHITECTURE except through an approved CR.
- **C6** One full-suite run on the final task-set at the phase gate (not after every narrow change); CI result cited only if CI actually ran on that commit.

### PHASE 0 — Governance, baseline and evidence hygiene (objective: a reproducible, accepted, truthfully recorded baseline)

**P0-01 Review, group and commit the working tree; verify on CI.**
- Source: G-09, G-10; RQ-39; CLAUDE.md principle 6; Plan A-02/A-04. Current: 113 uncommitted paths, 3 commits unpushed, migrations 0025-0027 untracked, CI never run on it. Target: reviewed commit groups (docs; migrations with their models; adapters; Admin; tests) created with explicit paths, pushed only if approved, CI green on the resulting head.
- Scope: whole tree; exclude `seed_hu_admin_test.py`, chat exports, session logs. Dependencies: DEC-01. Priority: first; everything else builds on it.
- Approach: produce a file-by-group manifest; HU reviews diffs; commit each group with explicit paths and a message containing no attribution trailer; push; watch CI.
- DoD: manifest lists all 113 paths each assigned to exactly one group; `git status` after commits shows only the approved leftovers; every commit message verified trailer-free with `git log --format=%B`; `git diff origin/main..HEAD --stat` equals the approved set; migrations 0025-0027 are in the same commit set as the models using them; CI run on the head SHA concludes success (link/ID recorded); full local suite recorded 0 failed.
- Verification: `git status`, `git log`, `gh run list`, `uv run pytest` (C6). Docs: PROJECT_LOG entry. Risks: partial commit of models without migrations; accidental `git add -A`. Gate: HU approves each commit and the push.

**P0-02 Co-author trailer remediation (decision, then optional rewrite).**
- Source: G-10, RQ-37. Current: 8 pushed commits carry trailers; public mirror has none. Target: HU+DI-chosen outcome (accept with a documented exception, or rewrite).
- Dependencies: DEC-02, P0-01 (so the rewrite carries final hashes). Approach if approved: rewrite in a separate clone, verify every tree identical, keep a backup branch, move branch, force-push only with explicit approval.
- DoD (rewrite case): `git log --grep='Co-Authored-By'` returns 0 on the rewritten branch; for each of the 138 old commits the tree hash equals the new commit's tree hash (script output attached); backup branch and old SHAs recorded; remote and mirrors updated as approved. (Exception case): HU+DI written decision recorded in PROJECT_LOG and CLAUDE.md.
- Risks: pushed history rewrite, hash changes everywhere (CONSOLIDATED_REPORT §8). Gate: explicit HU approval of rewrite and force-push (never assumed).

**P0-03 Single accurate state record and public mirror sync.**
- Source: G-20, G-09, D-1…D-8. Current: stacked contradictory state paragraphs; wrong "CI never ran" statements; stale public copies.
- Target: CLAUDE.md, README.md, PROJECT_LOG.md carry one current-state section (history preserved by moving old paragraphs under a dated "Superseded states" heading, not deleting); status register and READINESS register corrected; public mirror updated only on approval.
- DoD: each statement of repository state (HEAD, ahead count, file counts, CI facts, test count) in the three files equals fresh command output pasted in the handoff; D-1…D-9 each either corrected or explained; no historical entry removed (diff shows only additions/moves); mirror copies byte-identical to local where published.
- Dependencies: P0-01. Gate: HU approves publication to the public repo.

**P0-04 Test-evidence integrity fixes.**
- Source: G-21, G-50. Target: AC-9.9 backed by a real behavioural test; structural-only ACs labelled; guard-test and budget changes reviewed against history.
- DoD: a new test asserts the AC-9.9 behaviours (no combo, no COD, 100% advance for a business order) and fails when each is broken (mutation shown once); `ac_index.py --check` exit 0 and the Evidence column marks the 20 L-grade ACs "structural"; a written diff review of the widened guard allow-lists (`test_f05_boundaries`, `test_f06_boundaries`, `test_migrations`) concludes each widening is justified or reverts it.
- Gate: none beyond C4.

**P0-05 Independent re-verification run.**
- Source: SSD §8; this assessment's limitation. Target: a database-backed run of the full suite, migration drift check and `check --deploy` (dummy values) on the committed baseline by someone other than the author.
- DoD: command lines, exit codes, pass/fail/skip counts and durations recorded from a fresh environment (Docker/PostgreSQL 17); results compared to the 2,491 figure; any difference explained.
- Dependencies: P0-01. Gate: HU starts Docker/PostgreSQL (or approves a throwaway database).

**P0-06 Make every test independent of ignored and absent files.**
- Source: G-59; AC-29.3 and AC-26.1 tests in `tests/test_ac_structural_evidence.py`. Current: the AC-29.3 test reads the git-ignored `media/catalogue_source/source.json`; `media/` has no tracked file; the AC-26.1 test needs a `.git` directory. Target: the suite passes on a fresh clone of the committed tree.
- Approach: either commit a small non-secret fixture (the 15-product source list, text only, after HU confirms) or assert the property from tracked data; add a guard test that fails when a test references a path matched by `git check-ignore`.
- DoD: cloning the candidate commit into an empty directory and running `uv run pytest tests/test_ac_structural_evidence.py -q` exits 0; the guard test fails on a deliberately added reference to `media/x` and passes after removal; the AC-29.3 assertion stays non-vacuous (changing the fixture to 16 products makes it fail once, shown in the handoff); CI on the commit is green.
- Dependencies: P0-01. Gate: HU confirms any fixture may be committed.

### PHASE 1 — Decisions and controlled spec changes (objective: remove ambiguity that blocks build; documentation only)

**P1-01 Decide the Zoho-managed shipment and delivery model.**
- Source: G-01, G-02, G-28, G-36; ARCH §11, §15; hosting report decisions 1, 4, 5, 6. Current: real adapter cannot create shipments; no inbound feed; order states pinned.
- Target: a recorded HU+DI decision covering: how EffyKlean learns of shipment/delivery (recommended: scheduled read of the Zoho Sales Order's packages plus an optional notification hint), the Shipment sub-states, what "handover" means for the cancellation cutoff, how same-day/staff-hold gates apply once Zoho owns dispatch, and exception display; ARCHITECTURE §11/§15 amended through the controlled-change process.
- DoD: a signed-off decision record answers each of the six hosting-report questions with a choice; amended wording of ARCH §11/§15 and SPEC §15.4/§18 (if needed) is merged as a documented CR; the record names the Zoho field(s) that signal handover and delivery, evidenced by one authorised read-only sandbox sample or a Zoho notification sample.
- Dependencies: HU+DI; optional read-only sandbox sample. Gate: HU+DI decision.

**P1-02 Decide the GST arithmetic and display rule.**
- Source: G-04, G-46; SPEC §7.9, 7.10, 9.18, 10.17, 13.14; `tax.py`; accountant. Target: one rule applied consistently by SPEC, code and Zoho configuration.
- DoD: written decision stating, with a worked example (₹100 + 18; ₹10 discount), the GST amount, payable amount, B2C and business displays, and who computes what (EffyKlean vs Zoho); CR text for SPEC §7.9/7.10/13.14 or a withdrawal of the conflicting decision; accountant sign-off recorded if the rule changes Zoho configuration.
- Gate: HU+DI (STOP → REPORT).

**P1-03 Restate acceptance criteria that conflict with decisions (CR bundle).**
- Source: G-13, G-14, G-15, G-16, G-44; AC-12.7, 12.8, 15.1, 16.5, 13.8, 13.6, 23.1. Target: each criterion restated or withdrawn so SPEC matches decisions (Zoho Payments wording; refund recorded/executed manually; invoice display per HU item 20; local HSN fields; copy-as-is).
- DoD: one CR per criterion group recorded in PROJECT_LOG with source decision IDs; SPEC §33 text updated per the controlled-change rule (no version relabel unless approved); AC index regenerated; no code change in this task.
- Gate: HU+DI approval of each restatement.

**P1-04 Decide DC-22 (bank/UPI, assisted orders) and DC-33 (combo rule model) and coupon precedence.**
- Source: G-03, G-12, G-35. DoD: each is decided as BUILD (with a field-level model: states, actors, audit events, Zoho SO creation point; combo rule fields and evaluation order) or CHANGE SPEC (CR deferring it); the coupon-versus-combo precedence is stated explicitly.
- Gate: HU+DI.

**P1-05 Small outstanding decisions.**
- Source: G-17, G-18, G-23, G-26, G-29, G-43, §5 working defaults. DoD: a decision recorded for each: Admin vs Director deletion of Distributor/Bulk records (asking HU the one question: "does the Director-only delete satisfy your item 18?"), related-product links keep/remove, Admin URL, RBAC matrix (eight capabilities), enquiry-form defaults (call hours, window, bands wording), T41 design (recommended: Director schedules an already-approved revision), T38 slug scheme, analytics/Search Console timing, CSP enforcement.
- Gate: HU+DI.

**P1-06 Decision package: HU's recorded NO decisions versus the SPEC and the build (G-51).**
- Source: G-51. Target: a recorded HU+DI decision for ORD-064 (customer-initiated cancellation), ORD-019 (amount-range filter) and ORD-076/returned-package inspection, with the SPEC consequence of each.
- DoD: a decision paper quoting both sides (ledger, plan §3.1/§6, reconciliation §3/§6 and SPEC §16.1-16.3, §14.10, AC-16.1-16.4, 16.9, 14.6) with options (a) amend the SPEC by CR so cancellation is Admin-only and withdraw the customer page, (b) keep the SPEC and record the NO as superseded, (c) keep both with a recorded exception, and the consequences for the 20% charge flow, `/track/` cancel, Admin cancel, tests and AC rows; the choice is recorded in PROJECT_LOG; CR text is drafted only after approval.
- Gate: HU+DI.

**P1-07 Decide the production Zoho write policy and customer mapping (G-53).**
- DoD: a decision record fixes (1) the policy that replaces "stub or declared sandbox" (for example an explicit enable flag plus an organisation-id allow-list), (2) the customer rule (match by e-mail or phone, else create, or a shared contact; treatment of GST-registered buyers), (3) whether the website creates Zoho items at all (HU: Zoho owns the item master), each with an example payload and the failure behaviour.
- Gate: HU+DI.

**P1-08 Decide the availability and stock-sync model (G-54).**
- DoD: a record stating the freshness requirement (AD-11), the mechanism (short cache for list and detail pages with live checks at cart and checkout, hourly reconciliation, a Zoho change notification only if its authentication is verified), what a page shows when Zoho is unreachable (AC-6.9: never invent), and an API-budget calculation for expected traffic against the plan limits read from the Zoho organisation.
- Gate: HU+DI.

**P1-09 Decide MRP verification (G-61).**
- DoD: "verified" is defined (source, approver, date); HU supplies the 15 MRP values or confirms the imported ones; the decision says whether a provisional marker or publication gate is added.
- Gate: HU.

**P1-10 Decide customer identity controls (G-55, G-56).**
- DoD: a written rule for (a) e-mail verification before an account may hold a business role or have orders linked, (b) provisioning an existing unverified consumer account (refuse or re-verify), (c) password reset by an e-mailed single-use token with the same expiry and throttle pattern as Subscribe.
- Gate: HU+DI; depends on the e-mail channel decision DEC-10.

### PHASE 2 — Zoho-managed fulfilment and delivery lifecycle (objective: shipment, tracking and delivery work with the real adapter)

**P2-01 Retire direct shipment creation against the real adapter.**
- Source: G-01, G-28; hosting report §2. Current: four triggers call `request_fulfilment`. Target: with the real adapter, no trigger attempts creation; the stub keeps simulating for local tests only; orders that Zoho confirms stay ORDER_READY until an inbound signal arrives.
- Scope: `checkout.request_shipment`, `dispatch_ready_orders`, `retry_shipment`, `retry_pending_integrations`, `outbox._run_shipment`, Admin retry-ship, `dispatch_orders` command.
- DoD: with the real adapter configured (fake transport), invoking each of the four triggers creates no `SHIPMENT` outbox task, no `Shipment` row and no `SHIPMENT_FAILED` order; the integrations page labels the path "managed by Zoho"; tests prove each trigger's behaviour for stub (unchanged) and real adapters; NO PAYMENT → NO DISPATCH tests still pass unchanged.
- Dependencies: P1-01. Risk: regressions in stub-based local journey. Gate: HU+DI approval of P1-01 outcome.

**P2-02 Shipment event model and fields.**
- Target: `Shipment` gains the approved sub-state/AWB/carrier/tracking fields and an append-only event log (migration), without changing the 9 `OrderStatus` values unless P1-01 approves.
- DoD: migration applies and reverses on an empty and a populated database; model constraints prevent duplicate events (unique key on provider event id/sequence); `makemigrations --check` clean; tests cover duplicate and out-of-order events.
- Dependencies: P1-01. Gate: migration approval.

**P2-03 Inbound shipment/delivery sync (Phase 1: scheduled read).**
- Target: a scheduled command reads the Zoho Sales Order (packages/shipment info) for orders in ORDER_READY/SHIPMENT states and applies changes idempotently through one writer function; maps to customer statuses (Shipped, Out for Delivery, Delivered, Delivery Unsuccessful) without exposing courier terms.
- DoD: given a fake Zoho response sequence (created, in transit, out for delivery, delivered, unsuccessful, duplicate, out-of-order, 429, 5xx, timeout) the order/shipment ends in the expected state each time with exactly one event per distinct change; a Zoho outage leaves state unchanged and raises an integration-log entry after 3 attempts; DELIVERED is set only from a Zoho-reported delivery; no write to Zoho occurs (read-only scopes `salesorders.READ`); logs contain no secrets or customer addresses; correlation ids present; a shipment whose Zoho status stays "Shipped" beyond a configured age is listed on an Admin exception view instead of silently staying open (provider evidence: two of five historical Shiprocket shipments in Zoho still read Shipped months later; tracking is pulled on demand and Shiprocket's own webhook is disabled), and the replacement window and saved-address renewal are never derived from an assumed delivery date.
- Dependencies: P2-02, P6-04 (host schedule) for production use. Gate: HU+DI approval of the read approach and scope.

**P2-04 Re-key cancellation cutoff, replacement window, returned packages and saved-address reset.**
- Source: G-02; AC-16.1, 17.4, 17.5, 12.13, 14.6. Target: all four read the real signals from P2-02/P2-03.
- DoD: tests prove (a) cancellation is refused once the handover signal exists and allowed before, for B2C only; (b) the replacement window opens at the Zoho-reported delivery time, boundary cases at 24 h, 24 h + 1 s, 72 h, 72 h + 1 s; (c) a returned package can be recorded only after a handed-over, undelivered shipment; (d) saved-address reset happens only after a reported delivery; no behaviour depends on `LOCAL_PROVIDER_STUBS`.
- Gate: none beyond P1-01.

**P2-05 Replace stub-only lifecycle tests and update the integrations page.**
- DoD: every test that previously relied on the stub creating a shipment now has a real-adapter-faithful counterpart; the Admin order page shows "Zoho" as origin for shipment data with last-sync time and any ACTION_REQUIRED entry; `test_e2e_prototype` and `test_local_acceptance` pass unchanged in intent. Dependencies: P2-03. Gate: none beyond C4.

**P2-06 Admin record of fulfilment, tracking or local pickup (G-52).**
- Source: G-52; ORD-080/081; Plan §3.1; DEC-28. Target: an audited Admin action (order-manage capability) on a paid order: mark handed over with carrier and tracking number/URL, or record "local pickup, no tracking" with a reason; marking delivered carries a "reported by Admin" label; it never creates a Shiprocket shipment and never works without a verified payment.
- DoD: tests prove (i) an unpaid or failed-payment order is refused, (ii) the happy path sets the shipment and order states and the customer tracking page shows the link, (iii) blank tracking with the pickup reason is accepted and worded as pickup, (iv) a repeat call is idempotent, (v) an audit event records actor, order, carrier and tracking, (vi) the customer page distinguishes Admin-entered from carrier-confirmed information, (vii) `zoho.request_fulfilment` and every provider call are patched to raise and are never reached, (viii) the action works with the real `ZohoInventory` adapter over a fake transport that asserts zero shipment calls.
- Dependencies: DEC-28 (state names from P1-01). Gate: HU+DI approve the states.

**P2-07 Terminate non-retryable Zoho errors at once in the order outbox (G-60).**
- DoD: a `retryable=False` error (validation, mapping, auth, not supported) ends the ZOHO_CONFIRM task at its first attempt in a terminal state with the safe reason; a transient error still receives three total attempts; tests: validation error gives one provider call and a terminal task, a 500 gives three calls, a mixed sequence behaves accordingly, the Admin retry path is unchanged and the Reconciliation row shows the reason.
- Dependencies: none (ARCHITECTURE §17.2).

### PHASE 3 — Money, tax and commercial completeness (objective: financial rules match the frozen decisions)

**P3-01 Implement the decided GST arithmetic and display.**
- Source: G-04, G-22, G-46; AC-7.4, 9.8, 10.8, 13.7. Dependencies: P1-02.
- Target: GST computed/displayed per the decision for B2C and business orders; if Zoho owns the figure, EffyKlean shows only what Zoho confirms and refuses to guess when unavailable.
- DoD: table-driven tests for Karnataka, other state, with and without discount, B2C and Distributor/Bulk, rounding to the paisa (boundaries ₹0.005), asserting taxable value, CGST/SGST/IGST, payable total; Zoho Sales Order total equals amount paid in every case; Zoho tax unavailable for a business order blocks payment confirmation with data preserved (AC-13.7); business price display error path fails visibly (G-22) with a test; sandbox read-only comparison of the same ₹ example attached (P8).
- Gate: HU+DI (P1-02), accountant sign-off.

**P3-02 Payment settlement and charges (Zoho Payments).**
- Source: G-13; restated AC-12.7/12.8/15.1. DoD: where the Zoho Payments API provides them, per-payment charges, taxes on charges, net and settlement reference/date are fetched read-only, stored without calculating them, and shown on the Admin order page grouped by origin; when the API does not provide them the page states that explicitly and the restated AC says so; tests cover present, absent and error responses.
- Dependencies: P1-03; sandbox evidence (P8-01). Gate: scope check with HU.

**P3-03 Invoice number and status in Admin (only if retained).**
- Source: G-15; AC-13.8. DoD: with `invoices.READ`, the order page shows the Zoho invoice number and status read-only, "not yet invoiced" when none, and an error state when Zoho is unreachable; no invoice logic is created in EffyKlean; tests with fake Zoho for each case.
- Dependencies: P1-03, P8-02. Gate: HU decision on AC-13.8.

**P3-04 Bank-transfer/UPI payment with Admin verification, and assisted orders (only if decided).**
- Source: G-03; AC-12.5, 12.6, 27.1, 27.2. DoD: per the P1-04 model; at minimum: a PAYMENT_PENDING_VERIFICATION state, duplicate-reference idempotency, only Admin-verified payments reach PAYMENT_CONFIRMED and fulfilment, audit event per status change, assisted orders use the same pricing/GST/approval rules with explicit audited overrides, creator and timestamp recorded; negative tests: unverified payment cannot enter fulfilment; Admin cannot silently bypass Distributor/Bulk pricing.
- Gate: HU+DI (DEC-06).

**P3-05 Rule-based combos and fixed bundles (only if decided).**
- Source: G-12; AC-21.2, 21.3. DoD: Admin can define qualifying product/quantity rules and bundles per P1-04; evaluation oldest-first, no reuse of consumed quantities, single additional discount, amount never below zero, per-SKU amount semantics of §21.2A preserved; tests reproduce the §21.2/§21.2A examples exactly (A×3 → B×2 → C×1, removal and re-add) and the 10 + 10 unit example.

**P3-06 Refund handling.**
- Source: G-14. DoD per DEC-08: either (a) criterion restated to "refund recorded; executed by staff" with an Admin checklist and a report listing cancelled-and-unrefunded orders, tested; or (b) an authorised refund API call with idempotency, amount = eligible refund, audit, failure state, sandbox evidence. Duplicate-payment refunds appear in the same report.
- Gate: HU+DI (execution of real refunds is a financial action needing explicit approval).

**P3-07 Production Zoho write path and customer mapping (G-53).**
- Source: G-53; DEC-24. DoD (per the decision): tests over a fake transport prove (a) production-shaped settings with the explicit enable flag match or create the contact once and create exactly one Sales Order, (b) without the flag nothing is sent, the order stays visibly pending and an Admin alert shows, (c) an organisation id outside the allow-list is refused, (d) a first-time customer succeeds end to end, (e) a GST-registered buyer is not merged into a shared contact, (f) `production.py` requires `ZOHO_INVENTORY_WEB_CONSUMER_CONTACT_ID` only if the decision selects a shared contact; the same behaviour is observed once on the sandbox organisation (P8-02).
- Dependencies: P1-07. Gate: HU+DI.

### PHASE 4 — Communications, privacy and legal

**P4-01 Notification ownership matrix and templates.**
- Source: G-05; SPEC §20; HU item 10. DoD: a table of every customer/staff message (order confirmed, payment issue, shipped, delivered, cancelled, refund recorded, replacement decisions, quote/approval notices, role suspension, Subscribe) naming the sending system (website via GoDaddy SMTP, or Zoho e-mail/WhatsApp), trigger, language, and HU-approved wording; no wording invented by an agent.
- Gate: HU supplies/approves wording and ownership.

**P4-02 Asynchronous transactional e-mail.**
- Dependencies: P4-01, SMTP credentials. DoD: messages for the website-owned rows are enqueued through the outbox in the order's transaction, sent by a worker, retried at most 3 total attempts, recorded in the audit/integration log, and **never change order or payment state when they fail**; `check_email_config` against the real mailbox succeeds (no send), then one approved test message reaches an approved test address with SPF/DKIM results noted; production settings require a real backend, `PUBLIC_BASE_URL` (https) and a real From address (P5-02); transactional and marketing paths remain separate (existing guard tests unchanged).
- Gate: HU approves the first real send and credentials.

**P4-03 Privacy policy, terms, cookie/analytics consent, contact-form retention.**
- Source: G-06; AC-26.3. DoD: pages published from HU-approved text through the content review workflow; consent banner only if analytics exists, with a recorded consent state; retention and deletion periods for contact messages, subscribers and enquiries decided and implemented as a purge job with tests; the production start-up guard for the contact form can be satisfied; legal wording is verbatim from HU.
- Gate: HU supplies legal text and retention decisions.

**P4-04 Align policy wording and publication prerequisites (G-63, G-64).**
- DoD: the Replacement page, FAQ and tracking-page form state the same CR-008 rule (a video of the product at delivery or unpacking is required; photos may support it) and both routes (website or Customer Care), each proven by a test that fails on the old wording ("photos or a video", "through Customer Care" only); the footer policy links are either hidden until the page is live or proven live by a test that fails if any of the five slugs is unpublished; the deployment runbook lists `load_policy_pages` and `load_howto_videos` (with the recovered video files) as one-time production data steps; the privacy-policy contradictions (cookies "only those needed" versus analytics/advertising sentences; US/EU rights without an Indian grievance contact) are listed for HU and counsel; no legal text is invented.
- Dependencies: DEC-11, DEC-29. Gate: HU approves wording.

### PHASE 5 — Security and configuration hardening

**P5-01 Throttle guest tracking/cancel and share the customer throttle.**
- Source: G-11, G-27. DoD: failed lookups on `/track/` and the cancel steps are limited per reference and per source (documented thresholds); counters live in a shared store (database or approved cache) so they hold across workers and restarts; tests show the N+1th failure returns the same generic response as a wrong contact (no oracle), a success below the limit is unaffected, and the window slides; behind a proxy the source address comes from the trusted header only when configured.
- Gate: none (security fix), threshold values noted for review.

**P5-02 Production guard additions.**
- Source: G-32. DoD: production settings refuse `ZOHO_PAYMENTS_SANDBOX`, require `PUBLIC_BASE_URL` starting `https://`, a non-`.invalid` `DEFAULT_FROM_EMAIL`, and `CSRF_TRUSTED_ORIGINS`; a settings test per guard proves ImproperlyConfigured on violation and success on a valid set; the staging module of P6-01 keeps explicit, reviewed exceptions.

**P5-03 CI additions.**
- Source: G-49, G-09. DoD: CI runs `manage.py check --deploy` under production settings with dummy values (accepted warnings listed), a dependency vulnerability scan (e.g. `pip-audit` against `uv.lock`), ruff security rules enabled for `modules integrations config` with existing `noqa` entries reconciled; a CI run on the new head is green; any new finding is triaged in writing.
- Gate: approval to add dev dependencies (installing packages was out of scope for this assessment).

**P5-04 Security review and hygiene pass.**
- Source: G-25, G-26, G-33, G-45; RQ-30. DoD: written review of CSRF/origin design, Admin path decision, CSP enforcement readiness (violation reports reviewed), DB TLS option; the 28 `except Exception` sites each carry a reason comment or are narrowed; Razorpay residue renamed or documented as historical; `seed_hu_admin_test.py` is excluded from any build context (documented and checked by a test or CI step); findings list has an owner per item.

**P5-05 Customer account verification and password reset (G-55, G-56).**
- DoD (per DEC-27), each a test: (1) registering with another person's e-mail leaves the account unverified and unusable for business pricing; (2) provisioning a business role for an e-mail that has an unverified consumer account issues a verification or refuses, and never grants pricing first; (3) reset by e-mailed single-use hashed token: expires, single use, throttled, the same response for unknown e-mails, ends every session; (4) the Admin message no longer says the holder keeps their current password unless verified; (5) the mails are sent through the approved backend (`mail.outbox` in tests).
- Dependencies: P4-02, DEC-27.

**P5-06 Real client address and throttles for public forms (G-57, G-58).**
- DoD: a documented trusted-proxy setting makes one `client_ip(request)` helper return the right address only when configured (forged `X-Forwarded-For` ignored by default, proven by test); the customer sign-in throttle, contact form and Admin audit use it; the Bulk enquiry and Distributor application forms get per-source and global hourly caps like the contact form (the N+1th submission is refused with a generic message, a submission below the limit is unaffected); new enquiries raise an Admin alert.
- Dependencies: P6-02 for the proxy topology.

**P5-07 Database TLS and connection policy (G-62).**
- DoD: `database_config()` reads `DB_SSLMODE`; production settings refuse `prefer` and `disable` (settings tests for each); `CONN_MAX_AGE` is decided and set with the managed-database connection limit in mind; advisory-lock jobs use a direct connection (settings test); one observed staging connection shows TLS (`SELECT ssl FROM pg_stat_ssl WHERE pid = pg_backend_pid()` returns true), recorded.
- Dependencies: P6-02.

**P5-08 Keep single-use tokens out of logs and Referer headers (G-67).**
- DoD: the production access-log configuration drops or masks the query string for `/subscribe/confirm/`, `/subscribe/unsubscribe/`, `/account/setup/` and the business set-up path (verified by one staging request whose log line is shown without the token); or the tokens move to the POST body/fragment with a test proving the GET page carries no token in the URL; responses on these pages carry `Referrer-Policy: no-referrer` (test); the emailed/handed-over link still works end to end (test); the runbook states the rule.
- Dependencies: P6-02 (log configuration). Gate: none.

### PHASE 6 — Hosting and operations

**P6-01 Staging settings module and restricted access.**
- Source: G-08, RQ-24, RQ-40, RQ-41; hosting report §5. DoD: a documented `staging` settings module that keeps production hardening, requires sandbox flags, allows TESTCODE, forces noindex and a non-delivering e-mail backend, and cannot be mistaken for production (distinct name checked at start-up); an access gate (mechanism per DEC-12) keeps the site reachable only by approved people, proven by an unauthenticated request receiving the gate response on every route including `/healthz` exceptions as designed; `production.py` is unchanged in behaviour (tests prove it still refuses TESTCODE and sandbox flags).
- Gate: HU+DI approve the module and the gate mechanism.

**P6-02 Provision DigitalOcean App Platform and Managed PostgreSQL (staging first).**
- DoD: app spec stored in the repo (no secrets); PRE_DEPLOY `migrate` job succeeds on a clean database; `DB` connection uses TLS (`sslmode` or `PGSSLMODE`) and a dedicated role (not `doadmin`); `/healthz` returns 200 on the platform and 503 when the DB is down (observed once); HTTPS redirect and `TRUST_FORWARDED_PROTO` verified by a request; cost estimate approved before creation; resources named and listed in the temporary/permanent register.
- Gate: explicit HU approval of spend and creation.

**P6-03 Spaces provisioning and verified media migration.**
- DoD: bucket created and credentials stored only as platform secrets; `migrate_media_to_storage` copies all `media/` objects with checksum verification and a reference check (every DB reference resolves); a dry-run report lists zero unresolved references; the site serves images/videos from the bucket on staging; no local copy is deleted by this task.
- Gate: HU approval of paid provisioning; separate approval for any cleanup.

**P6-04 Scheduler/worker for background jobs.**
- Source: G-24. DoD: `run_outbox`, `reconcile_payment_attempts`, `suspend_inactive_business_roles`, `archive_orders`, `purge_saved_shipping` (only if enabled) and the P2-03 sync run on the chosen mechanism (worker loop or 15-minute jobs per DEC-12/13) with documented intervals; the advisory-lock path uses a direct DB connection (verified by connection settings test); an observed run on staging shows a due outbox task processed and a second concurrent runner skipped; failures alert (P6-05).

**P6-05 Monitoring, alerting, backups and restore drill on the managed database.**
- DoD: error-rate, health and queue-age (oldest due outbox task) alerts reach a named recipient (one test alert observed); managed-DB backups confirmed in the provider console; one restore into a scratch database succeeds and its row counts equal the source (orders, attempts, revisions); retention periods recorded as decided by HU.
- Gate: HU decides retention; spend approval if applicable.
- Added (revision 3): AD-17 requires explicit availability, RPO and RTO targets before production and says 99.5% is NOT an approved SLO (decision register V0.7 section 2A.6); DoD adds the written targets (DEC-30) and a restore time measured against the RTO. DigitalOcean managed PostgreSQL PITR is limited to 7 days and restores into a new cluster (evidence note, section 2A.6).

**P6-06 TESTCODE marker coverage and safe cleanup runbook.**
- Source: RQ-40. DoD: a nullable test-marker column (migration) on customers, saved addresses, enquiries, subscriptions, Zoho sync rows, defaulting from `TESTCODE_ACTIVE`; `testcode_report` lists them; the cleanup runbook deletes only by marker and order, never by similarity, in dependency order (PROTECT respected), proven on a throwaway database with before/after counts; external sandbox records (Zoho sessions, Sales Orders, contacts) are listed for manual reconciliation.
- Gate: migration approval (DEC-12/21).

**P6-07 Availability sync and caching per the decision (G-54).**
- DoD (per DEC-25), measurable: the Zoho call count for a product-list view is zero within the cache lifetime (counted on a fake transport); cart and checkout still verify live before payment (AD-11, AC-11.2); with Zoho failing, list and detail pages behave exactly as the decision states (either the 503 is unchanged or the last known state is shown with the stated limit); a reconciliation job reports drift; twenty concurrent list views cause no more provider calls than the figure in the decision.
- Dependencies: DEC-25, P6-04.

### PHASE 7 — Content and catalogue data

**P7-01 Reconcile catalogue data with HU-supplied values.**
- Source: G-19; HU items 2, 4, 5, 6. DoD: the five SKUs with conflicting dilution text have HU-approved wording or are explicitly left unchanged with a note; the "Tools Required" decision is recorded and, if approved, appears in an approved revision for EK-HHLD-FCR and EK-BLP-000004; HSN, weights, dimensions and barcodes are entered by Admin for all 15 products and the HSN comparison report shows zero mismatches with Zoho; no value is entered by an agent.
- Gate: HU supplies data/decisions.

**P7-02 Review and publish SEO revisions and blog drafts.**
- DoD: each of the 15 SEO revisions and 3 blog posts is reviewed and approved by a different Director (workflow audit shows proposer ≠ approver ≠ publisher where required), then published; `/sitemap.xml` lists them; canonical URLs use the production host on the production build; nothing is published by an agent acting as both submitter and approver.
- Gate: HU acts in the Admin.

**P7-03 Policy wording and content parity sign-off.**
- DoD: HU confirms in writing the Shipping/Cancellation/Replacement wording (including the delivery-call sentence), the Contact details and the FAQ text; AC-23.1 is closed per the CR of P1-03.

**P7-04 MRP verification gate (G-61).**
- DoD (per DEC-26): HU-supplied verified MRP for each of the 15 SKUs is recorded with source and date; a provisional marker or gate exists (test: a SKU whose MRP is unverified cannot have a revision approved or published, or is flagged in the review queue); the importer's `--assume-compare-at-as-mrp` path leaves the marker set; a list of any published product whose MRP differs from the verified value is produced.
- Dependencies: P1-09.

### PHASE 8 — Provider acceptance in sandbox (objective: real evidence for what is currently mock)

**P8-01 Zoho Payments webhook and payment gate.**
- Source: G-07; RQ-42. DoD: HU registers the webhook against the staging HTTPS URL; a real sandbox payment is completed with the browser return **disabled/ignored** and the order is placed by webhook alone (recorded evidence: attempt id, webhook event id, order id, timestamps); replay of the same event creates no second order; a mismatched amount and a failed payment each leave no order; settlement fields recorded per P3-02; all test data carries a TESTCODE.
- Gate: HU registers the webhook and approves test payments.

**P8-02 Zoho Inventory scopes, Flow inspection, stock and invoice observation.**
- Source: G-40…G-42. DoD: the seven approved scopes are present (`check_zoho_access` reports none missing); the Zoho Flow/workflow definition for Sales Orders is inspected read-only and a written note states whether a confirmed EffyKlean Sales Order can trigger a duplicate or invoice; one sandbox item has non-zero stock and a Sales Order reduces availability as expected (before/after readings recorded); invoice number/status read back for one order.
- Gate: HU re-issues the token; each sandbox write needs its authorisation noted in the evidence.

**P8-03 Sandbox end-to-end acceptance gate.**
- Source: G-01, G-47; RQ-60; hosting plan §3 step 10. DoD: one two-product order on staging with a TESTCODE passes payment (P8-01) → Sales Order (confirmed once) → Zoho-managed shipment appears via P2-03 → delivered → replacement request accepted inside the window; separate runs prove: failed payment (no dispatch), duplicate webhook, Zoho outage after payment (preserved, retried ×3, exception visible), cancellation before and after handover, unsuccessful delivery (no refund entitlement); every step lists provider, environment (sandbox), evidence artefact and TESTCODE; a cleanup list is produced; status register rows updated truthfully (DONE only where observed).
- Gate: HU authorises each external write.

### PHASE 9 — Remaining Shopify-parity backlog (scope decided by HU)

**P9-01 Triage the 124 rows awaiting naming.** Source: Appendix A (66 "authorized? NO – proposal only", 58 "awaiting HU+DI decision"). DoD: each row is assigned BUILD, EXCLUDE (explicit NO) or LATER by HU+DI with the criterion or source decision cited; the status register and 597 CSV are updated in place with history preserved; counts reconcile to 597.
- Gate: HU+DI decisions.

**P9-02 Implement the named subset.** For each row named BUILD: acceptance statement taken from the Shopify/effyklean.com reference or frozen SPEC (not invented), tests, evidence entry; template DoD = C1-C6 plus a behaviour test that fails if the feature is removed. The 25 PARTIAL rows (Appendix A.2) each get a closure note (build, accept as is, or exclude).

**P9-03 Optional browser regression suite.** DoD: a small headless-browser suite covering home, product, cart, checkout (stub), track, enquiry forms and Admin sign-in runs in CI and fails on a broken page; no secrets in the repo. Gate: approval to add dev dependencies.

**P9-04 Minor-findings bundle (G-65, G-66, §8.3).**
- DoD: each of m1-m16 and the cart-limit item is closed by a change with a test or accepted in writing by HU+DI; at minimum: cart limits reviewed for business accounts and Bulk quantity above 100 orderable (test), the nav count and to-do wording correct under Zoho-owned dispatch, the Admin lock-out rule decided, the subscribe consent version set when wording is approved, stale docstrings and headers corrected.
- Dependencies: related decisions. Gate: none for pure code items.

### PHASE 10 — Release gate and cutover

**P10-01 Production readiness gate (J-10).** DoD: a checklist of every unmet criterion from the register with evidence per item; numeric performance/availability/accessibility targets defined by HU and measured on staging (response times, Core Web Vitals sample, one keyboard-and-screen-reader pass of checkout); UAT by HU; zero open Critical/High gaps in §8.2.
**P10-02 Production configuration.** DoD: production Zoho organisation ids, tax ids and HSN verified by the accountant; production credentials stored only as platform secrets; sandbox flags absent (start-up guards prove it); first production payment of a minimal amount observed and refunded per approved process; every external write authorised.
**P10-03 Transition and temporary-arrangement clearance.** DoD: `TEMPORARY_ARRANGEMENTS_REMOVE_AT_GO_LIVE.md` has every row cleared with evidence; DNS/redirect plan for effyklean.com → effyklean.in with rollback agreed; Shopify retained per HU; monitoring live; backup restore re-demonstrated on production data; go-live and observation-period dates recorded (3 months minimum per the hosting decision).
- Gate: HU+DI explicit go-live authorisation (production deployment, credentials, DNS, cutover each need their own).

---


**Revision 3 task extensions (no new task numbers).** Each extension adds a Definition of Done line to the named task.
- **P1-05 (small decisions):** DoD adds a written answer to DEC-31 for G-71 (the rule for a paid order whose Zoho or stock confirmation never succeeds: fulfil or refund, with the staff runbook), G-73 (retire or confirm the distributor monthly-budget checkpoint and nearest-warehouse selection), G-74 (dispute/chargeback and post-placement change-request handling) and G-75 (approved PIN/city data source or an explicit statement that format-only validation is accepted; the call-hour window, band wording and which contact phone/spelling to publish).
- **P4-01 (notification ownership matrix):** DoD adds who sends the Zoho GST invoice to the customer (G-70), as a row in the event matrix with owner, channel and failure behaviour.
- **P6-02 (DigitalOcean provisioning):** DoD adds a recorded check that DigitalOcean App Platform egress, provider IP allow-lists and webhook reachability do not block Zoho, Shiprocket or Zoho Payments (G-72), and a note on the Tuesday Customer Care closure against the 24-hour replacement window (website requests timestamped and accepted 24x7).
- **P1-06 (HU's recorded NO decisions) and P2-04:** DoD adds the DEC-32 paper for G-76: the editable-field set (confirm or trim to DC-08) and the guest-cancellation authentication option, each with consequences.
- **P1-07 (production Zoho write policy and customer mapping):** DoD adds the sanctioned production path for Zoho item mapping (G-69), replacing SKU-code placeholders with real item ids without using the sandbox-only sync command, and confirmation of the two sandbox SKU price differences.

## 13. Dependencies, blockers, sequencing and verification gates

**Dependency chain (arrows mean "must precede"):**
`P0-01 → P0-02, P0-03, P0-05, P0-06` · `P1-06…P1-10` (decision papers) are independent of code · `P2-06` needs DEC-28 · `P3-07` needs P1-07 · `P5-05` needs P1-10 and P4-02 · `P5-06`, `P5-07` need P6-02 · `P6-07` needs P1-08 and P6-04 · `P7-04` needs P1-09 · `P0-04` independent · `P1-01 → P2-01 → P2-02 → P2-03 → P2-04 → P2-05` · `P1-02 → P3-01` · `P1-03 → P3-02, P3-03, P3-06` · `P1-04 → P3-04, P3-05` · `P4-01 → P4-02` · `P4-03` independent (needs HU text) · `P5-01…P5-04` independent of P2/P3 · `P6-01 → P6-02 → P6-03, P6-04, P6-05` · `P6-04` also needs P2-03 for the sync job · `P7-*` need HU data but not code · `P8-01` needs P6-02 (stable HTTPS URL) · `P8-02` needs HU token · `P8-03` needs P2-03, P3-01, P6-02, P8-01, P8-02 · `P9-01 → P9-02` · `P10-*` need all Critical/High gaps closed.

**Genuine blockers (evidence in §8.2):** HU+DI decisions DEC-01…DEC-32; HU portal/token actions (webhook, scopes); legal and e-mail wording; spend approval for DigitalOcean and Spaces; a Docker/PostgreSQL environment for independent test runs; Zoho/Shiprocket sample or read access for P1-01.

**Work that can proceed without waiting:** P0-03, P0-04, P0-06 (the test fix, once HU approves committing the fixture), P5-01, P5-02, P5-03, P5-04 (after approval of dev dependencies), P9-03, and all P1 decision papers (writing, not deciding). P0-01/P0-05 need HU to start the database and approve commit groups.

**Verification gates:**
- **Gate A — baseline accepted:** P0-01 and P0-05 done; CI green on the head; records accurate (P0-03).
- **Gate B — decisions closed:** DEC-03…DEC-08 recorded; CRs merged.
- **Gate C — local build complete:** P2-*, P3-* (decided scope), P4-02/03, P5-* done; one full-suite run on PostgreSQL 17 (0 failed) and CI green on that head; AC index current with no Critical/High AC NOT DONE except those formally deferred by CR.
- **Gate D — staging sandbox acceptance:** P6-01…P6-05, P8-01…P8-03 done with TESTCODE evidence; temporary-arrangements register updated.
- **Gate E — release:** P10-01…P10-03 done; HU+DI explicit authorisation for production deployment, credentials, live payments, DNS and cutover (each separately).

**Proportionate testing rule used above:** targeted tests per task; full suite only at Gates A, C and E; the 31-34-minute local run is reserved for gates; CI (about 9 minutes) runs on every push.

---

## 14. HU+DI decisions and authorisations required

| ID | Decision / authorisation | Gaps | Blocks | Recommendation (not a decision) |
|---|---|---|---|---|
| DEC-01 | Review and approve commit groups, and the push of the 3 local commits + working tree; accept or reject Batch 1 | G-09, G-10 | P0-01 | Approve in groups with explicit paths |
| DEC-02 | Rewrite the 8 pushed co-author commits and force-push, or record an exception | G-10 | P0-02 | Decide after P0-01; keep a backup branch |
| DEC-03 | Zoho-managed shipment/delivery model, Shipment sub-states, order-state wording in ARCH §11/§15, retire direct triggers | G-01, G-02, G-28, G-36 | Phase 2 | Scheduled read of the Zoho Sales Order packages first; hint endpoint later |
| DEC-04 | Meaning of "handover" for the cancellation cutoff (Zoho package created? shipment label? courier pickup?) | G-02 | P2-04 | Choose the earliest irreversible Zoho signal |
| DEC-05 | GST arithmetic and display rule; accountant sign-off | G-04, G-46 | P3-01 | STOP → REPORT: either amend SPEC §7.9/7.10/13.14 or change `tax.py` |
| DEC-06 | Bank transfer/UPI and assisted orders: build or defer by CR | G-03 | P3-04 | Decide explicitly; SPEC currently requires both |
| DEC-07 | Combo rule model (DC-33); coupon-versus-combo precedence | G-12, G-35 | P3-05 | Adopt the SPEC §21.2 qualifying-quantity model or amend it |
| DEC-08 | Restate AC-12.7, 12.8, 15.1 (Zoho Payments), AC-16.5 (refund), AC-13.8 (invoice display), AC-13.6 (HSN fields), AC-23.1 (copy as is) | G-13…G-16, G-44 | P1-03, P3-02/03/06 | Restate to match HU's recorded decisions |
| DEC-09 | Admin vs Director deletion of Distributor/Bulk records (does Director-only satisfy item 18?) | G-17 | P1-05 | Ask HU the one question |
| DEC-10 | Notification ownership matrix, wording, SMTP credentials, first real send | G-05 | P4-01/02 | Use GoDaddy `Support@EffyKlean.com` for website messages as HU directed |
| DEC-11 | Privacy policy, terms, cookie consent text; retention periods | G-06 | P4-03 | HU supplies legal text |
| DEC-12 | Hosting: staging settings module, access-gate mechanism, worker vs 15-minute jobs, spend approval for App Platform, Managed DB, Spaces; TESTCODE marker schema | G-08, G-24, G-31 | Phase 6 | Separate `staging` settings module; gate mechanism per DO capabilities |
| DEC-13 | Scheduler intervals for outbox, reconciliation, role suspension | G-24 | P6-04 | Worker for outbox, 15-minute jobs for the rest |
| DEC-14 | Related-product links; Admin URL; RBAC matrix and extra capabilities; enquiry-form defaults; Shipping-page sentence; analytics/Search Console timing; CSP enforcement | G-23, G-26, G-29, G-43 | P1-05, P5-04 | Decide in one sitting |
| DEC-15 | T41 scheduled-publication design; T38 slug scheme | G-18 | optional | Director schedules an already approved revision |
| DEC-16 | CSP enforcement date | RQ-30 | P5-04 | After reviewing report-only data |
| DEC-17 | Catalogue data: dilution values for five SKUs, Tools Required, HSN/weights/dimensions/barcodes; act in Admin to publish SEO and blog drafts | G-19 | Phase 7 | HU supplies; HU publishes |
| DEC-18 | HU actions: register Zoho Payments webhook; re-issue Zoho token with the authorised scopes; allow read-only Flow inspection | G-07, G-40, G-41 | P8 | Do on the staging URL |
| DEC-19 | Performance/availability/accessibility targets; backup retention | G-37, G-38 | P10-01, P6-05 | Define after first staging measurements |
| DEC-20 | Cutover timing, DNS/redirect plan, Shopify transition | G-30 | P10-03 | Plan after Gate D |
| DEC-21 | Test-marker schema change and any migration application to a shared database | RQ-40 | P6-06 | Approve with P6-01 |
| DEC-22 | Scope of the Shopify-parity backlog (124 rows awaiting naming) | Appendix A | Phase 9 | Triage in one pass |
| DEC-23 | HU's recorded NO on customer-initiated cancellation (ORD-064), the amount-range filter (ORD-019) and returned-package inspection (ORD-076) versus frozen SPEC §16.1-16.3 and §14.10 and what was built | G-51 | P1-06 | Keep the SPEC unless HU confirms customers must not cancel; if HU confirms Admin-only, raise a CR and withdraw the customer page; record ORD-019/076 as accepted exceptions or remove them |
| DEC-24 | Production Zoho write policy (replacing "stub or declared sandbox"), customer mapping rule (match/create/shared contact) and whether the website creates Zoho items | G-53 | P1-07, P3-07 | Explicit enable flag plus organisation allow-list; match by e-mail or phone, else create; Zoho owns the item master |
| DEC-25 | Availability and stock-sync model and freshness | G-54 | P1-08, P6-07 | Short cache for list/detail, live check at cart/checkout, hourly reconciliation, per HU's recorded intent |
| DEC-26 | MRP verification and a provisional marker | G-61 | P1-09, P7-04 | HU supplies the 15 MRPs; add a publication gate |
| DEC-27 | Customer e-mail verification, password reset and the business-role provisioning rule | G-55, G-56 | P1-10, P5-05 | Verify before a business role; reset by e-mailed token |
| DEC-28 | Interim Admin fulfilment/tracking action and its states (ORD-080/081) | G-52 | P2-06 | Approve a narrow action now, replaced by the inbound sync later |
| DEC-29 | Replacement wording and channels (video required; website or Customer Care) | G-63 | P4-04 | Align every page to CR-008 and SPEC §17.2 |
| DEC-30 | Availability, RPO and RTO targets (AD-17; 99.5% is not an approved SLO; no document records targets) | G-37, G-38 | P6-05 | Decide numeric targets, retention and incident procedure; record in PROJECT_LOG |
| DEC-31 | Invoice delivery to customers; the paid-but-unconfirmed order rule; distributor budget checkpoint and warehouse selection; dispute/chargeback handling; enquiry-form address data source, defaults and contact details | G-70, G-71, G-73, G-74, G-75 | P4-01, P1-05 | Decide who sends the invoice, the fulfil-or-refund rule, retire or confirm each recorded input, and the address-validation data source |
| DEC-32 | Confirm or trim the editable order fields (e-mail, GST number, GST name) and decide how a guest authenticates to cancel (D-C1, D-C2) | G-76 | P1-06 (extend), P2-04 | Decision paper with both options and consequences |
**Authorisations never implied by this document:** production deployment, production credentials or writes, live customer payments, live provider writes, DNS/cutover, push or history rewrite, paid provisioning, publishing content, sending real e-mail, deleting real provider records.

---

## 15. Inaccessible records, evidence limitations and checks not performed (revision 3, final)

**Coverage statement.** After revision 3 every local document and test listed in the repository was opened and read by the assessor, except the items named below. Nothing was read through another agent's summary where the original could be opened. This is still not a claim that every line of every artefact was verified: reading is not execution, and the exclusions below are real.

**Not accessible / not performed:** the development database `effyklean` (no Docker/PostgreSQL for the assessor), private Actions logs (only run metadata; CI has run 12 times), Zoho Payments, Zoho Inventory, Shiprocket, Zoho Flow and DigitalOcean (no provider contact), the Windows host, the Zoho OAuth helper token file and `.env` (never opened). **Checks not run (by HU instruction on 2026-10-22 and by environment):** the test suite (2,491 tests collected only), `makemigrations --check`, `migrate`, `check --deploy`, browser rendering, penetration testing, DNS/TLS checks. Run in pass 1: `ruff check` (331 files), `ruff format --check`, `manage.py check`, `pytest --collect-only`.

**Read in full by the assessor**
- Local code: `integrations/*`, `modules/backoffice/*`, `modules/orders/*`, `modules/storefront/*`, `modules/identity/*`, `modules/catalogue/*`, `config/*`, `scripts/*`, migrations `orders.0023-0027` (earlier migrations: operation summaries).
- All 105 test files and helpers (1,790 test functions; behaviour assessed, not executed).
- SPEC.md, ARCHITECTURE.md, README.md, PROJECT_LOG.md, the Delta plan and status register, CLAUDE.md.
- All of `docs/foundation/`, `docs/architecture/` (7 documents), `docs/content/` text documents, `docs/requirements/`, `docs/DeltaImplementationPlan/`, `docs/audit/`, `docs/security/`.
- `docs/discovery/`: every document, including COMPARISON_1-4, the benchmark matrix (DC-01 to DC-45), SHOPIFY_ADMIN_FEATURE_MAPPING, FUNCTION_INVENTORY, LIVE_WALK, FLAGGED_ISSUES, DISCOVERY, DISCOVERY_AUDIT, RESTAMP, UI_FIELD_PAGE_FLOW_MAP, REFERENCE_FUNCTIONAL_DISCOVERY, BRM investigation, SPEC_AMENDMENT_PROPOSAL, CARRY_FORWARD matrix, ARCHITECTURE_CONSOLIDATION_READINESS, VISUAL_PARITY, MASTER_FUNCTIONALITY_INVENTORY (the 103 MF rows in full; the 494 MA rows by structured extraction of every row's id, status, disposition and rationale), and RECONCILED_597_STATUS_2026-10-18.csv (all 597 rows by structured extraction; every non-implemented row listed and read; implemented rows' basis columns checked for PARTIAL markers).
- Public repository (HEAD `83c6efa`): all instruction, hosting, Golden Rules, discussion and agent-response records, including `AgentResponse18oct2026_2210.md`, `AgentRespDigiOCN_Setup19Oct2026_1925.md`, `AgntRespEffyImplmntn19OCT2026_1751.md`, the 17-Oct HU-DI chat (text extracted from the HTML; the PDF is byte-identical), the 21-Oct hosting plan and the 122-capability master (whose appendices were diffed against the standalone ledger, conflict analysis and evidence map and differ by four lines each).
- Diffed, not re-read: public COMPARISON_1-4 and the master comparison are identical to local copies; the two public Delta plan copies differ from the local reference copy only in provenance headers and a status note (4 and 12 lines); the public status register and AC index lag the local ones.

**Excluded by HU instruction (2026-10-22):** the saved BRM checkout web page and assets under `checkoutCart/` (static third-party capture) and the test suite.

**Read by extraction rather than line by line:** the 8,897-line master comparison transcript (a verbatim duplicate of MASTER_FUNCTIONALITY_INVENTORY, same content), the MA rows of the master inventory and the 597-row CSV (structured extraction of every row, as above), and large generated files (`AC_TEST_INDEX.md` was read in full).

**Effect on confidence:** Critical/High findings G-01, G-02, G-04, G-10, G-11, G-27, G-32, G-51-G-54 and G-59 are confirmed by direct reading of code, tests and records. Sandbox behaviour, the development database, browser results, historic pass counts and DigitalOcean state rest on earlier agents' records (medium confidence); no test was executed by the assessor. A defect that only manifests at run time, or in a line the assessor read without noticing it, could still exist.

---

## 16. Final completeness reconciliation against the instruction set

### 16.1 Investigation checklist (instruction §6.4) and operational outcome

| # | Obligation | Outcome | Notes |
|---|---|---|---|
| 1 | Local repository examined (§2.1) | Completed with evidence (reading); tests not executed | All application code, all 105 test files and all local documents read (§15) |
| 2 | Public repository examined independently (§2.2) | Completed with evidence, BRM checkout capture excluded by HU | All records read or diffed against local copies (§3, §15) |
| 3 | Reconciliation local vs public (§2.3) | Completed with evidence | §4 |
| 4 | Scope and decision history (§3) | Completed with evidence | §5; SPEC, ARCHITECTURE and PROJECT_LOG read in full |
| 5 | Existing audit requirement located and applied | Completed with evidence | Read in full |
| 6 | Review every previous agent's work (§4) | Completed with evidence for what can be checked without running tests or contacting providers | §7; claims checked against code where possible; pass counts and sandbox evidence unverifiable |
| 7 | End-to-end investigation (§5) | Completed for traced chains | Checkout/payment/order, Zoho handoff, fulfilment/delivery/cancellation/replacement, pricing/tax, Admin and catalogue, identity |
| 8 | Status for every requirement and deliverable (§7) | Completed with evidence | 147 ACs, 60 deliverables, 597 rows (agent-derived with mechanical checks) |
| 9 | Evidence standards (§8) | Completed | grades H/M/L; no secret printed |
| 10 | Gap analysis and register (§9) | Completed with evidence | 76 gaps (§8.2), 21 minor findings (§8.3), §9, §11 |
| 11 | Phased plan with DoD per task (§10) | Completed with evidence | 63 tasks (46 in revision 1 and 17 added in revision 2); revision 3 added gaps G-69 to G-76, minor findings m17-m21 and decisions DEC-30 to DEC-32, absorbed by extending tasks P1-05, P1-06, P1-07, P2-04, P4-01 and P6-02 rather than adding tasks |
| 12 | Every gap maps to a task, decision or evidence action | Completed | §11 |
| 13 | Final report in the 16-section structure | Completed | this document and the chat report |
| 14 | Read-only restrictions | Completed with evidence | §16.2 |
| 15 | Inaccessible records and unexecuted checks disclosed | Completed | §15 |
| 16 | Do not describe the investigation as exhaustive | Completed | It is not exhaustive; §15 lists what remains |

### 16.2 Integrity checks

- **No unsupported completion claim:** DONE is granted at evidence grades H, M and L; the assessor re-ran no tests. The first version's completion signal was premature (§7.3).
- **No file, Git state or external system changed except the one authorised report document.** HEAD `625e2102335a3e9b4a094466fb260fd023050fe8`; 113 pre-existing changed paths unchanged plus this untracked report; 0 staged; 0 stashes; 3 commits ahead of `origin/main`.
- **No provider, database or network write:** reads only; `.env` not opened.
- **No delegation:** no sub-agent used.
- **No commits were made, so no co-author attribution exists anywhere; the project's standing no-co-author rule applies.**
- **Frozen-decision conflicts were reported, not resolved:** G-04, G-13, G-14, G-16, G-44, G-51 and the DECs of §14.

---

## Appendix A — The 597 planned activities (item level)

Source file and mapping rule: §6C. Counts after mapping: **DONE 259, PARTIAL 25, NOT DONE 3, DEFERRED 310** (= 597). "Agent status" is the agent's wording from the 2026-10-18 reconciliation, shortened. The first-listed domain families are Admin/Shopify (Orders 119, Products 87, Customers & B2B 45, Settings 51, Discounts 29, Analytics 27, Content 23, Inventory 18, Staff & security 20, System & search 16, Integrations & apps 15, Draft orders 13, Marketing 11, Collections 10, Sales channels 8, Gift cards 2) and 103 cross-cutting/platform rows.

### A.1 DONE (259 rows)

IDs (agent status "implemented…"; every cited test name exists in `tests/`, 819 names checked, 0 dangling; 38 rows cite no test and rest on the 12-Oct validation level): MF-001, MF-003, MF-004, MF-020, MF-021, MF-023, MF-024, MF-025, MF-026, MF-028, MF-031, MF-040, MF-041, MF-043, MF-046, MF-047, MF-048, MF-049, MF-051, MF-052, MF-053, MF-056, MF-057, MF-058, MF-059, MF-061, MF-062, MF-066, MF-072, MF-073, MF-075, MF-076, MF-077, MF-080, MF-081, MF-082, MF-085, MF-091, MF-095, MF-096, MF-097, MF-098, MF-099, MF-100, MF-103, MF-104, MF-108, MF-111, MF-112, MF-113, MF-117, MF-118, MF-119, MF-120, MF-121, MA-ORD-001, MA-ORD-002, MA-ORD-003, MA-ORD-004, MA-ORD-005, MA-ORD-006, MA-ORD-007, MA-ORD-008, MA-ORD-009, MA-ORD-012, MA-ORD-013, MA-ORD-014, MA-ORD-015, MA-ORD-016, MA-ORD-017, MA-ORD-018, MA-ORD-019, MA-ORD-021, MA-ORD-022, MA-ORD-030, MA-ORD-031, MA-ORD-032, MA-ORD-033, MA-ORD-034, MA-ORD-035, MA-ORD-036, MA-ORD-038, MA-ORD-041, MA-ORD-042, MA-ORD-043, MA-ORD-044, MA-ORD-045, MA-ORD-046, MA-ORD-047, MA-ORD-048, MA-ORD-049, MA-ORD-060, MA-ORD-061, MA-ORD-064, MA-ORD-065, MA-ORD-066, MA-ORD-072, MA-ORD-082, MA-ORD-083, MA-ORD-085, MA-ORD-093, MA-ORD-094, MA-ORD-100, MA-ORD-101, MA-ORD-102, MA-ORD-106, MA-ORD-107, MA-ORD-108, MA-ORD-109, MA-ORD-115, MA-ORD-120, MA-ORD-126, MA-ORD-131, MA-ORD-132, MA-ORD-133, MA-ORD-134, MA-ORD-135, MA-ORD-143, MA-PRD-001, MA-PRD-002, MA-PRD-003, MA-PRD-004, MA-PRD-006, MA-PRD-009, MA-PRD-011, MA-PRD-013, MA-PRD-014, MA-PRD-015, MA-PRD-020, MA-PRD-021, MA-PRD-022, MA-PRD-023, MA-PRD-025, MA-PRD-026, MA-PRD-027, MA-PRD-028, MA-PRD-030, MA-PRD-031, MA-PRD-032, MA-PRD-033, MA-PRD-038, MA-PRD-039, MA-PRD-041, MA-PRD-048, MA-PRD-050, MA-PRD-051, MA-PRD-055, MA-PRD-056, MA-PRD-058, MA-PRD-059, MA-PRD-062, MA-PRD-073, MA-PRD-074, MA-PRD-090, MA-PRD-094, MA-PRD-095, MA-PRD-097, MA-PRD-101, MA-PRD-103, MA-COL-001, MA-COL-002, MA-COL-003, MA-COL-004, MA-COL-005, MA-COL-006, MA-COL-009, MA-COL-010, MA-CUS-001, MA-CUS-002, MA-CUS-003, MA-CUS-004, MA-CUS-005, MA-CUS-007, MA-CUS-008, MA-CUS-010, MA-CUS-011, MA-CUS-013, MA-CUS-016, MA-CUS-019, MA-CUS-026, MA-CUS-029, MA-CUS-030, MA-CUS-031, MA-CUS-032, MA-CUS-033, MA-CUS-040, MA-DSC-001, MA-DSC-002, MA-DSC-003, MA-DSC-004, MA-DSC-005, MA-DSC-006, MA-DSC-008, MA-DSC-009, MA-DSC-010, MA-DSC-013, MA-DSC-015, MA-DSC-016, MA-DSC-017, MA-DSC-018, MA-DSC-019, MA-DSC-022, MA-DSC-025, MA-DSC-027, MA-CNT-001, MA-CNT-002, MA-CNT-003, MA-CNT-005, MA-CNT-006, MA-CNT-007, MA-CNT-009, MA-CNT-010, MA-CNT-012, MA-CNT-013, MA-CNT-017, MA-CNT-018, MA-CNT-040, MA-MKT-005, MA-MKT-010, MA-CHN-001, MA-ANA-001, MA-ANA-002, MA-ANA-003, MA-ANA-004, MA-ANA-005, MA-ANA-006, MA-ANA-007, MA-ANA-008, MA-ANA-009, MA-ANA-010, MA-SET-030, MA-SET-031, MA-SET-033, MA-SET-035, MA-INT-001, MA-INT-002, MA-INT-003, MA-INT-004, MA-INT-005, MA-USR-001, MA-USR-002, MA-USR-005, MA-USR-007, MA-USR-008, MA-USR-009, MA-USR-010, MA-USR-011, MA-USR-013, MA-USR-021, MA-SYS-001, MA-SYS-002, MA-SYS-003, MA-SYS-005, MA-SYS-006, MA-SYS-007, MA-SYS-008, MA-SYS-020, MA-SYS-021, MA-SYS-022


### A.2 PARTIAL (25 rows)

| ID | Function | Agent status 2026-10-18 (shortened) |
|---|---|---|
| MF-007 | Rendered visual, responsive and accessibility parity of effyk… | partial - home page compared (desktop and mobile); other pages not co… |
| MF-054 | Zoho tax/GST mapping, invoice trigger and numbering, discount… | partial - Zoho owns GST/invoicing; verification only |
| MF-060 | Refund execution through the original payment mechanism | partial - refund amount computed and recorded; execution is manual by… |
| MF-065 | Per-order financial reconciliation view (customer paid, provi… | partial - order page groups Order, Zoho Payments, Zoho, Shiprocket |
| MF-079 | Transactional e-mail events N1..N11 (confirmation, shipping, … | in progress - SMTP configuration and check built; credentials and mes… |
| MF-086 | Blog index and posts (3 posts in media/blog_source); blog pos… | partial - 3 hidden DRAFT blog posts imported to the dev database 2026… |
| MA-ORD-020 | Filter by tags, channel, risk level, delivery method, return … | partial - named tests, bodies read 2026-10-18; tag, payment and shipm… |
| MA-ORD-084 | Mark delivered (record delivery) | partial - named tests, bodies read 2026-10-18; delivery can be record… |
| MA-ORD-104 | Bulk print packing slips / invoices | partial - named tests, bodies read 2026-10-18; packing slips tested; … |
| MA-ORD-137 | "Mark as delivered" on a single fulfilment | partial - named tests, bodies read 2026-10-18; labelled local simulat… |
| MA-ORD-142 | Order "More actions": Edit, Duplicate, Archive/Unarchive, Vie… | partial - Duplicate order not built (needs draft orders, DC-22) |
| MA-PRD-024 | Description (rich text) | partial - named tests, bodies read 2026-10-18; description is plain t… |
| MA-PRD-072 | Import products (CSV) | partial - named tests, bodies read 2026-10-18; the import is the cata… |
| MA-PRD-098 | Import products: CSV with downloadable sample, or "import fro… | partial - named tests, bodies read 2026-10-18; no CSV upload with a d… |
| MA-PRD-100 | Product list filters: vendor, tag, status, category, sales ch… | partial - named tests, bodies read 2026-10-18; category, tag, status,… |
| MA-CUS-006 | Customer addresses (multiple, default) | partial - one saved shipping address (identity.0005) |
| MA-CUS-012 | Marketing consent display (e-mail, SMS, WhatsApp) | partial - named tests, bodies read 2026-10-18; e-mail and WhatsApp co… |
| MA-DSC-007 | Applies to collections / categories | partial - coupons scope to products only (2026-10-19) |
| MA-DSC-014 | Edit / deactivate / delete a discount | partial - named tests, bodies read 2026-10-18; edit and switch off te… |
| MA-DSC-040 | Discount list filters (status active/scheduled/expired, type,… | partial - named tests, bodies read 2026-10-18; status, type and creat… |
| MA-ANA-018 | Report export and scheduling | partial - named tests, bodies read 2026-10-18; CSV export tested; sch… |
| MA-INT-006 | Shiprocket status | partial - named tests, bodies read 2026-10-18; the integrations page … |
| MA-USR-020 | Users: tabs Active, Pending, POS app-only, Requests; roles St… | partial - named tests, bodies read 2026-10-18; staff list with role a… |
| MA-USR-032 | Users: "Security" page (monitor user activity, collaborator r… | partial - named tests, bodies read 2026-10-18; own and per-staff sign… |
| MA-SYS-012 | Responsive accessible shell | partial - structural test plus real-browser overflow check (2026-10-1… |

### A.3 NOT DONE (3 rows)

| ID | Function | Agent status 2026-10-18 (shortened) |
|---|---|---|
| MA-PRD-066 | Bundles / combo packs as products | not built - fixed bundles (AC-21.3) |
| MA-PRD-102 | Rich-text description editor tools (headings, colour, alignme… | not built - plain-text content fields |
| MA-DSC-026 | Combo pack pricing (rule set) | not built - rule-based combo rule set (AC-21.2); per-SKU amount model… |

### A.4 DEFERRED (310 rows)

| ID | Function | Agent status 2026-10-18 (shortened) |
|---|---|---|
| MF-002 | Reviewed and committed baseline for the 28 uncommitted paths … | awaiting HU+DI decision |
| MF-005 | CI pipeline (`scripts/ci.sh` on every push) | awaiting HU+DI decision |
| MF-006 | Re-observation of the live Shopify Admin (statuses carried fr… | blocked - needs HU signed-in Shopify session |
| MF-008 | effyklean.com Distributor enquiry page: whether it is a form | observed - .com page has text only, the form is script-injected; Effy… |
| MF-009 | Competitor checkout and payment flows (effyklean.com, BRM) | evidence-only - competitor flow observation |
| MF-022 | Search type-ahead suggestions | authorized? NO - proposal only; pending HU+DI naming |
| MF-027 | Add-to-cart confirmation notice (BRM shows "Item added to you… | blocked - a notice needs a cookie or a changed redirect, both forbidd… |
| MF-029 | Home merchandising modules (best sellers, recent launches, cl… | authorized? NO - proposal only; pending HU+DI naming |
| MF-030 | Separate Household Combo or Bulk Combo collection page | deferred/excluded/not authorized |
| MF-032 | BRM raw-material taxonomy: 43 collections, 695 products, 12 b… | deferred/excluded/not authorized |
| MF-033 | Wishlist, save-for-later, recently viewed, reviews/ratings, r… | awaiting HU+DI decision |
| MF-034 | Technical documents (COA/SDS) download | not built - source disposition NO ACTION |
| MF-042 | No cash on delivery or partial payment on delivery | deferred/excluded/not authorized |
| MF-044 | No separate shipping charge | deferred/excluded/not authorized |
| MF-045 | "Free shipping" announcement bar | awaiting HU+DI decision |
| MF-050 | Cart persistence across devices for signed-in users | awaiting HU+DI decision |
| MF-055 | Customer mapping to Zoho contacts (shared contact vs approved… | awaiting HU+DI decision |
| MF-063 | Existing "Zoho Flow salesorder add" (Shopify to Zoho) must no… | awaiting HU+DI decision |
| MF-064 | Bank-transfer / UPI assisted payment verification and Zoho SO… | awaiting HU+DI decision |
| MF-070 | Shipment created only by Zoho -> Shiprocket (no second writer) | deferred - Zoho-managed Shiprocket, test later |
| MF-071 | Shipment status/tracking return path into orders | awaiting HU+DI decision |
| MF-074 | Weight/dimension source and location -> pickup mapping | direction recorded - Admin enters real values later; fields kept |
| MF-078 | GST amounts and invoice number/status visible in Admin; custo… | closed - Zoho-owned, not built |
| MF-083 | Distributor GST handling during Zoho outage | closed - Zoho-owned, not built |
| MF-084 | Own Privacy, Terms and Refund/Contact-information pages (foot… | awaiting HU+DI decision |
| MF-087 | Knowledge hub, formulation guides, ad landing pages | authorized? NO - proposal only; pending HU+DI naming |
| MF-088 | Videos page and media hosting (videos hot-link the old site) | awaiting HU+DI decision |
| MF-089 | Contact form (fail-closed until privacy wording and retention… | awaiting HU+DI decision |
| MF-090 | Newsletter subscription with mailbox verification and unsubsc… | awaiting HU+DI decision |
| MF-092 | Redirect and URL-parity plan from effyklean.com paths to effy… | separate transition phase - not part of this build |
| MF-093 | Analytics and marketing events with consent | awaiting HU+DI decision |
| MF-094 | Floating WhatsApp button (`.com` app) and language option (We… | observed - floating WhatsApp button exists on .com and not locally; s… |
| MF-101 | Inventory / low-stock view | closed - Zoho-owned, not built |
| MF-102 | Admin export of staff-visible data and orders (order export) | authorized? NO - proposal only; pending HU+DI naming |
| MF-105 | Customer sign-in help (password reset by staff) and customer … | awaiting HU+DI decision |
| MF-106 | Admin-assisted / manual / draft orders using the same commerc… | awaiting HU+DI decision |
| MF-107 | Hosting, HTTPS, domain, WSGI/ASGI server and deployment recip… | awaiting HU+DI decision |
| MF-109 | Process supervision for run_outbox, retry_integrations, recon… | authorized? NO - proposal only; pending HU+DI naming |
| MF-110 | Secrets management (DC-05); `.env` only locally | awaiting HU+DI decision |
| MF-114 | Performance and load baseline (page, checkout and Zoho latenc… | authorized? NO - proposal only; pending HU+DI naming |
| MF-115 | Release acceptance gate (exit gate rows 3, 5, 11 blocked) | awaiting HU+DI decision |
| MF-116 | Shopify Online Store themes, theme editor, Liquid templates, … | deferred/excluded/not authorized |
| MA-ORD-010 | Column: sales channel | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-011 | Column: delivery method | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-023 | Order count / stats strip (orders, items ordered, returns, fu… | closed by decision - ORD-131 'reliable metrics only' (2026-10-19) |
| MA-ORD-037 | Fraud / risk level display and analysis | awaiting HU+DI decision |
| MA-ORD-039 | Print invoice / GST tax invoice | closed - Zoho-owned, not built |
| MA-ORD-040 | Source / attribution (first session, referral) | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-062 | Cancel and restock inventory toggle | deferred/excluded/not authorized |
| MA-ORD-063 | Cancel and notify customer toggle | awaiting HU+DI decision |
| MA-ORD-067 | Edit line items (add, remove, change quantity) | deferred/excluded/not authorized |
| MA-ORD-068 | Edit prices or apply a discount to a placed order | deferred/excluded/not authorized |
| MA-ORD-069 | Refund (money back) | deferred/excluded/not authorized |
| MA-ORD-070 | Refund execution after an approved cancellation | awaiting HU+DI decision |
| MA-ORD-071 | Return items / create return | deferred/excluded/not authorized |
| MA-ORD-073 | Exchange | deferred/excluded/not authorized |
| MA-ORD-074 | Store credit issue | deferred/excluded/not authorized |
| MA-ORD-075 | Return label / return shipping | deferred/excluded/not authorized |
| MA-ORD-076 | Inspect returned package before restock | awaiting HU+DI decision |
| MA-ORD-077 | Mark as paid (manual payment) | awaiting HU+DI decision |
| MA-ORD-078 | Capture authorized payment | deferred/excluded/not authorized |
| MA-ORD-079 | Request payment / send payment link | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-080 | Fulfil items (create fulfilment) | deferred/excluded/not authorized |
| MA-ORD-081 | Add tracking number manually | deferred/excluded/not authorized |
| MA-ORD-086 | Move fulfilment to another location | awaiting HU+DI decision |
| MA-ORD-087 | Split fulfilment across locations | deferred/excluded/not authorized |
| MA-ORD-088 | Create shipping label | deferred/excluded/not authorized |
| MA-ORD-089 | Resend order confirmation / invoice / shipping e-mail | awaiting HU+DI decision |
| MA-ORD-090 | Send invoice to customer (draft order invoice) | closed - Zoho-owned, not built |
| MA-ORD-091 | Duplicate order | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-092 | Merge / split orders | deferred/excluded/not authorized |
| MA-ORD-095 | Cancel a Distributor/Bulk order as an Admin case | awaiting HU+DI decision |
| MA-ORD-103 | Bulk fulfil / create labels | deferred/excluded/not authorized |
| MA-ORD-105 | Bulk cancel | deferred/excluded/not authorized |
| MA-ORD-110 | Abandoned checkouts list | awaiting HU+DI decision |
| MA-ORD-111 | Abandoned checkout recovery e-mail | awaiting HU+DI decision |
| MA-ORD-112 | Payment reminder | awaiting HU+DI decision |
| MA-ORD-113 | Order-edit request from customer ("change request") | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-114 | Disputes / chargebacks | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-116 | Order routing rules to locations | deferred/excluded/not authorized |
| MA-ORD-121 | Order list column "Return status" | deferred/excluded/not authorized |
| MA-ORD-122 | Order list column "PO number" | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-123 | Order list column "Label status" | blocked - label status lives in Shiprocket (DC-18) |
| MA-ORD-124 | Order detail: "View map" of the delivery address | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-125 | Order detail: source session ("1st session from Google, 3 ses… | authorized? NO - proposal only; pending HU+DI naming |
| MA-ORD-130 | Order list "All locations" filter | deferred/excluded/not authorized |
| MA-ORD-136 | Bulk "Mark as": Unfulfilled, In progress, Fulfilled, On hold,… | deferred/excluded/not authorized |
| MA-ORD-138 | Bulk "Capture payments" | deferred/excluded/not authorized |
| MA-ORD-139 | Bulk "Request fulfillment" and "Cancel fulfillment requests" | deferred/excluded/not authorized |
| MA-ORD-140 | Bulk "Change fulfillment location" | deferred/excluded/not authorized |
| MA-ORD-141 | Bulk "Run Flow automation" on orders | deferred/excluded/not authorized |
| MA-ORD-144 | Order header "Refund" and "Return" buttons | deferred/excluded/not authorized |
| MA-ORD-145 | Fulfilment card "..." menu (not opened; contents unobserved) | evidence-only placeholder |
| MA-DRF-001 | Draft order list | awaiting HU+DI decision |
| MA-DRF-002 | Create draft order for a customer | awaiting HU+DI decision |
| MA-DRF-003 | Add products / custom items | awaiting HU+DI decision |
| MA-DRF-004 | Apply named order discount to a draft | deferred/excluded/not authorized |
| MA-DRF-005 | Tax-exempt flag on a draft | awaiting HU+DI decision |
| MA-DRF-006 | Draft shipping / delivery line | deferred/excluded/not authorized |
| MA-DRF-007 | Send draft invoice / payment link | awaiting HU+DI decision |
| MA-DRF-008 | Complete draft as paid / payment pending | awaiting HU+DI decision |
| MA-DRF-009 | PO number on a draft | awaiting HU+DI decision |
| MA-DRF-010 | Draft order timeline and notes | awaiting HU+DI decision |
| MA-DRF-011 | Delete / duplicate draft | awaiting HU+DI decision |
| MA-DRF-020 | Draft statuses: Open, Invoice sent, Completed, Submitted for … | awaiting HU+DI decision |
| MA-DRF-021 | Draft "Submitted for review" (approval step before an order) | awaiting HU+DI decision |
| MA-PRD-005 | Filter by vendor | deferred/excluded/not authorized |
| MA-PRD-007 | Filter by collection / sales channel | deferred/excluded/not authorized |
| MA-PRD-008 | Filter by stock level (low, out) | closed - Zoho-owned, not built |
| MA-PRD-010 | Column: inventory ("N in stock") | closed - Zoho-owned, not built |
| MA-PRD-012 | Column: channels | deferred/excluded/not authorized |
| MA-PRD-029 | Charge-tax flag | closed - Zoho-owned (GST/tax per Zoho; no charge-tax flag in EffyKlea… |
| MA-PRD-034 | Track quantity / sell when out of stock | deferred/excluded/not authorized |
| MA-PRD-035 | Quantity per location | closed - Zoho-owned, not built |
| MA-PRD-036 | Weight | direction recorded - Admin enters real values later; fields kept |
| MA-PRD-037 | Package / dimensions | direction recorded - Admin enters real values later; fields kept |
| MA-PRD-040 | Physical product / requires shipping | deferred/excluded/not authorized |
| MA-PRD-042 | Vendor | deferred/excluded/not authorized |
| MA-PRD-043 | Shopify taxonomy category | deferred/excluded/not authorized |
| MA-PRD-044 | Metafields (pinned custom data) | deferred/excluded/not authorized |
| MA-PRD-045 | Google-feed fields (age group, condition, gender, MPN) | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-046 | Theme template selector | deferred/excluded/not authorized |
| MA-PRD-047 | Verified commercial data marker (MRP, concentrate, Zoho) | awaiting HU+DI decision |
| MA-PRD-052 | Archive / unpublish a published product | awaiting HU+DI decision |
| MA-PRD-053 | "Unlisted" (reachable by link only) | deferred/excluded/not authorized |
| MA-PRD-054 | Delete product | deferred/excluded/not authorized |
| MA-PRD-057 | Schedule publish date | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-060 | Video and 3D media on a product | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-061 | Media from the Files library | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-063 | URL handle (slug) edit | parked - T38 (product ID is the fixed URL identity) |
| MA-PRD-064 | Variants and options (size, colour) | deferred/excluded/not authorized |
| MA-PRD-065 | Product family / pack-size grouping | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-067 | Related / complementary products | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-068 | Reviews and ratings | authorized? NO - proposal only; pending HU+DI naming |
| MA-PRD-069 | Product boosts / search ranking | deferred/excluded/not authorized |
| MA-PRD-070 | Selling plans / subscriptions | deferred/excluded/not authorized |
| MA-PRD-071 | Product quantity rules and price breaks | deferred/excluded/not authorized |
| MA-PRD-075 | Product translations | deferred/excluded/not authorized |
| MA-PRD-083 | Product/collection status "Suspended" (in addition to Active,… | deferred/excluded/not authorized |
| MA-PRD-084 | Product category determines tax rates (Shopify taxonomy) | deferred/excluded/not authorized |
| MA-PRD-091 | Bulk archive / unlist products | awaiting HU+DI decision |
| MA-PRD-092 | Bulk delete products | deferred/excluded/not authorized |
| MA-PRD-093 | Bulk include/exclude in sales channels and catalogs | deferred/excluded/not authorized |
| MA-PRD-096 | "Create email campaign" from selected products | deferred/excluded/not authorized |
| MA-PRD-104 | Inventory adjustment on the product page with a reason; unava… | deferred/excluded/not authorized |
| MA-PRD-105 | Package picker and "Manage packages" (sample box 22×13.7×4.2 … | deferred/excluded/not authorized |
| MA-COL-007 | Separate combo collections | deferred/excluded/not authorized |
| MA-COL-008 | Collection channel availability | deferred/excluded/not authorized |
| MA-INV-001 | Inventory page (per location counts) | closed - Zoho-owned, not built |
| MA-INV-002 | States: available, committed, unavailable, on hand, incoming | awaiting HU+DI decision |
| MA-INV-003 | Adjust quantity | deferred/excluded/not authorized |
| MA-INV-004 | Adjustment history | deferred/excluded/not authorized |
| MA-INV-005 | Reserve / commit stock | deferred/excluded/not authorized |
| MA-INV-006 | Low-stock alert | closed - Zoho-owned, not built |
| MA-INV-007 | Locations list | closed - Zoho-owned, not built |
| MA-INV-008 | Add / edit / deactivate location | deferred/excluded/not authorized |
| MA-INV-009 | Inventory-by-location report | closed - Zoho-owned, not built |
| MA-INV-010 | Purchase orders | deferred/excluded/not authorized |
| MA-INV-011 | Transfers between locations | deferred/excluded/not authorized |
| MA-INV-012 | Suppliers | deferred/excluded/not authorized |
| MA-INV-013 | Inventory CSV import / export | deferred/excluded/not authorized |
| MA-INV-020 | Inventory column "Bin name" | deferred/excluded/not authorized |
| MA-INV-021 | Inventory quick-transfer popover | deferred/excluded/not authorized |
| MA-INV-022 | Export inventory (from all locations) | deferred/excluded/not authorized |
| MA-INV-023 | Incoming popover with "Create transfer" | deferred/excluded/not authorized |
| MA-INV-024 | Purchase order list: statuses Draft, Ordered, Archived; suppl… | deferred/excluded/not authorized |
| MA-GFT-001 | Create / sell / redeem gift cards | deferred/excluded/not authorized |
| MA-GFT-002 | Gift card liability reporting | deferred/excluded/not authorized |
| MA-CUS-009 | Delete / anonymise customer | blocked - conflicts with frozen SPEC; HU+DI controlled change needed |
| MA-CUS-014 | Tax-exempt flag | deferred/excluded/not authorized |
| MA-CUS-015 | Customer metafields (budget, state, PIN from enquiry form) | deferred/excluded/not authorized |
| MA-CUS-017 | Send account invite | deferred/excluded/not authorized |
| MA-CUS-018 | Reset customer password / sign-in help | awaiting HU+DI decision |
| MA-CUS-020 | Merge customers | deferred/excluded/not authorized |
| MA-CUS-021 | Customer segments (list) | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-022 | Create segment by filter (ShopifyQL-like) | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-023 | Segment membership counts / use in marketing | deferred/excluded/not authorized |
| MA-CUS-024 | Companies (B2B) | deferred/excluded/not authorized |
| MA-CUS-025 | Company locations, contacts, payment terms | deferred/excluded/not authorized |
| MA-CUS-027 | Customer import | deferred/excluded/not authorized |
| MA-CUS-028 | Customer data request (export one customer) | awaiting HU+DI decision |
| MA-CUS-041 | Customer "deletable" flag (can this customer be deleted) | blocked - conflicts with frozen SPEC; HU+DI controlled change needed |
| MA-CUS-043 | Customer notification language ("Will receive notifications i… | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-044 | "Create order" from the customer page | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-045 | Customer "Collect tax" setting | deferred/excluded/not authorized |
| MA-CUS-050 | Bulk "Delete customer" | blocked - conflicts with frozen SPEC; HU+DI controlled change needed |
| MA-CUS-051 | Bulk "Add to company" | deferred/excluded/not authorized |
| MA-CUS-052 | Bulk "Remove tags" | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-053 | "Select all in this store" (selection beyond the page) | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-054 | Segment actions: use, duplicate, export, rename, delete | authorized? NO - proposal only; pending HU+DI naming |
| MA-CUS-055 | Describe-your-segment (natural-language segment builder) | deferred/excluded/not authorized |
| MA-CUS-056 | Import customers by CSV dialog | deferred/excluded/not authorized |
| MA-DSC-011 | One use per customer | awaiting HU+DI decision |
| MA-DSC-012 | Customer eligibility (all, segment, specific) | awaiting HU+DI decision |
| MA-DSC-020 | Automatic discount (no code) | authorized? NO - proposal only; pending HU+DI naming |
| MA-DSC-021 | Buy X get Y | authorized? NO - proposal only; pending HU+DI naming |
| MA-DSC-023 | Free shipping discount | deferred/excluded/not authorized |
| MA-DSC-024 | Sales-channel limitation of a discount | deferred/excluded/not authorized |
| MA-DSC-041 | Staff comments with @mention and links to records (orders, dr… | authorized? NO - proposal only; pending HU+DI naming |
| MA-CNT-004 | Page templates | deferred/excluded/not authorized |
| MA-CNT-008 | Blog comments moderation | deferred/excluded/not authorized |
| MA-CNT-011 | Metaobjects (definitions, entries) | deferred/excluded/not authorized |
| MA-CNT-014 | Themes: library, customise, edit code | deferred/excluded/not authorized |
| MA-CNT-015 | Online Store preferences (title, meta, social image, password… | authorized? NO - proposal only; pending HU+DI naming |
| MA-CNT-016 | Storefront search settings and filters (Search & Discovery) | deferred/excluded/not authorized |
| MA-CNT-019 | Forms (Shopify Forms) builder | deferred/excluded/not authorized |
| MA-CNT-020 | Customer-facing chat / chatbot (Tidio) | deferred/excluded/not authorized |
| MA-CNT-041 | Themes: published theme, draft themes, update, edit theme, im… | deferred/excluded/not authorized |
| MA-CNT-042 | Online Store home: 30-day sessions by device (mobile, desktop… | authorized? NO - proposal only; pending HU+DI naming |
| MA-MKT-001 | Marketing campaigns | deferred/excluded/not authorized |
| MA-MKT-002 | Attribution | deferred/excluded/not authorized |
| MA-MKT-003 | Automations / Autopilot | deferred/excluded/not authorized |
| MA-MKT-004 | Shopify Email / Messaging campaigns | deferred/excluded/not authorized |
| MA-MKT-006 | Abandoned cart automations | authorized? NO - proposal only; pending HU+DI naming |
| MA-MKT-007 | Social posting / audiences | deferred/excluded/not authorized |
| MA-MKT-011 | International markets, duties, local pricing | deferred/excluded/not authorized |
| MA-MKT-012 | Languages and translations | authorized? NO - proposal only; pending HU+DI naming |
| MA-MKT-013 | Market-specific domains / rollouts | deferred/excluded/not authorized |
| MA-CHN-002 | Point of Sale | deferred/excluded/not authorized |
| MA-CHN-003 | Facebook & Instagram channel | authorized? NO - proposal only; pending HU+DI naming |
| MA-CHN-004 | Google & YouTube channel / product feed | authorized? NO - proposal only; pending HU+DI naming |
| MA-CHN-005 | WhatsApp channel | authorized? NO - proposal only; pending HU+DI naming |
| MA-CHN-006 | Agentic / AI channel | deferred/excluded/not authorized |
| MA-CHN-007 | Marketplaces / Shop app | deferred/excluded/not authorized |
| MA-CHN-008 | Pixels and customer events (Meta, Google) | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-011 | Returning customer rate / cohorts | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-012 | Sessions, conversion rate, traffic sources | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-013 | Live view | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-014 | Product analysis: ABC, sell-through, days of inventory | closed - Zoho-owned, not built |
| MA-ANA-015 | Finance: payments, taxes, payouts | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-016 | Tax / GST summary report | closed - Zoho-owned, not built |
| MA-ANA-017 | Custom reports / saved reports | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-019 | Bulk-customer savings report | awaiting HU+DI decision |
| MA-ANA-020 | Search-terms report | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-021 | Behaviour reports: conversion, bounce, landing pages, device,… | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-022 | Customer reports: RFM analysis and list, predicted spend tier… | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-023 | Finance reports: finance summary, gross profit by order, cost… | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-024 | Acquisition reports: sessions by referrer/location, visitors | authorized? NO - proposal only; pending HU+DI naming |
| MA-ANA-025 | Inventory report: ABC product analysis | closed - Zoho-owned, not built |
| MA-ANA-026 | Storefront-agent (AI) session and conversation reports | deferred/excluded/not authorized |
| MA-ANA-027 | Pin a report; report library by category | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-001 | General: store name, contact e-mail and phone, address | awaiting HU+DI decision |
| MA-SET-002 | General: currency, time zone, units | deferred/excluded/not authorized |
| MA-SET-003 | Brand assets: logo, colours, slogan, social links | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-004 | Plan, billing, subscription | deferred/excluded/not authorized |
| MA-SET-005 | Payments: Razorpay settings | superseded - Razorpay replaced by Zoho Payments (CR-007) |
| MA-SET-006 | Payments: capture mode | closed - provider-side (Zoho Payments) |
| MA-SET-007 | Payments: manual payment methods | awaiting HU+DI decision |
| MA-SET-008 | Payments: COD | deferred/excluded/not authorized |
| MA-SET-009 | Payments: PayPal / alternative gateways | deferred/excluded/not authorized |
| MA-SET-010 | Payment customizations (hide / reorder methods) | deferred/excluded/not authorized |
| MA-SET-011 | Checkout settings: required fields, GST fields, order notes | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-012 | Checkout customisation | deferred/excluded/not authorized |
| MA-SET-013 | Customer accounts settings (sign-in type, self-serve returns,… | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-014 | Shipping profiles, zones, rates | deferred/excluded/not authorized |
| MA-SET-015 | Packages and packing slip template | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-016 | Local delivery and pickup | deferred/excluded/not authorized |
| MA-SET-017 | Carrier accounts / shipping labels | deferred/excluded/not authorized |
| MA-SET-018 | Taxes: GST rates and state overrides | deferred/excluded/not authorized |
| MA-SET-019 | Duties at checkout | deferred/excluded/not authorized |
| MA-SET-020 | Locations | deferred/excluded/not authorized |
| MA-SET-021 | Notifications: customer e-mail templates (confirmation, shipp… | awaiting HU+DI decision |
| MA-SET-022 | Notifications: staff e-mails (new order, store summary, dispu… | awaiting HU+DI decision |
| MA-SET-023 | Notifications: order-creation webhook | deferred/excluded/not authorized |
| MA-SET-024 | Notification SMS / WhatsApp templates | deferred/excluded/not authorized |
| MA-SET-025 | Apps and sales channels settings | deferred/excluded/not authorized |
| MA-SET-026 | Domains | deferred/excluded/not authorized |
| MA-SET-027 | Customer events (pixels) | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-028 | Metafields and metaobjects definitions | deferred/excluded/not authorized |
| MA-SET-029 | Languages | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-032 | Gift cards settings | deferred/excluded/not authorized |
| MA-SET-034 | Feature previews / labs | deferred/excluded/not authorized |
| MA-SET-050 | Transfer or move the store to an organization / external owner | deferred/excluded/not authorized |
| MA-SET-052 | Billing: list of bills (number, date, reason, total, status) | deferred/excluded/not authorized |
| MA-SET-055 | Taxes: "Global collected tax report" | awaiting HU+DI decision |
| MA-SET-056 | Taxes: country of origin and HS codes recorded on 0 of 66 var… | awaiting HU+DI decision |
| MA-SET-057 | Legal notice policy (not set) | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-058 | Privacy: "Shopify Network Intelligence" (enabled) | deferred/excluded/not authorized |
| MA-SET-059 | Privacy: double opt-in for marketing; e-mail and SMS marketin… | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-060 | Policies: "Default rules" for policy pages | deferred/excluded/not authorized |
| MA-SET-061 | Staff notification: "Fulfillment request notification" to a f… | deferred/excluded/not authorized |
| MA-SET-070 | Payment customization "Hides COD payment method for non-Magic… | deferred/excluded/not authorized |
| MA-SET-071 | Razorpay Magic Checkout (one-click checkout) | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-072 | Customer sign-in connections: Google, Facebook | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-073 | Packing slip template (editable HTML/Liquid; ship-to, PO numb… | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-074 | Metafield definitions in use: product boosts, related and com… | deferred/excluded/not authorized |
| MA-SET-075 | Languages: English published (4 domains); Hindi, Kannada, Mal… | authorized? NO - proposal only; pending HU+DI naming |
| MA-SET-076 | Payment capture method (label only; value not readable) | closed - provider-side (Zoho Payments) |
| MA-INT-007 | App store / marketplace | deferred/excluded/not authorized |
| MA-INT-008 | Custom/private apps and API tokens | deferred/excluded/not authorized |
| MA-INT-009 | Shopify Flow | deferred/excluded/not authorized |
| MA-INT-010 | Webhook subscriptions config | deferred/excluded/not authorized |
| MA-INT-011 | Zoho Flow workflows | deferred/excluded/not authorized |
| MA-INT-020 | Flow workflows: eight Shopify-template marketing workflows (w… | deferred/excluded/not authorized |
| MA-INT-021 | Flow: workflow tags, last run, version history | deferred/excluded/not authorized |
| MA-INT-022 | "EffyZohoFlow" custom app and "Zoho Inventory" app (names onl… | closed - names only |
| MA-INT-023 | App row menu: open, view details, get support, uninstall | deferred/excluded/not authorized |
| MA-USR-003 | Create staff / invite | awaiting HU+DI decision |
| MA-USR-004 | Reset staff MFA | awaiting HU+DI decision |
| MA-USR-006 | Granular per-area permissions | deferred/excluded/not authorized |
| MA-USR-012 | Collaborator accounts (agencies) | deferred/excluded/not authorized |
| MA-USR-022 | Permission "Requests" tab (staff asking for access) | deferred/excluded/not authorized |
| MA-USR-023 | POS app-only users | deferred/excluded/not authorized |
| MA-USR-030 | Roles page: 17 roles in three categories (store, organization… | deferred/excluded/not authorized |
| MA-USR-031 | Role permission catalogue (e.g. orders: edit, apply discounts… | deferred/excluded/not authorized |
| MA-SYS-004 | Command palette / keyboard shortcuts | authorized? NO - proposal only; pending HU+DI naming |
| MA-SYS-009 | Setup guide / promotions | deferred/excluded/not authorized |
| MA-SYS-010 | AI assistant (Sidekick) | deferred/excluded/not authorized |
| MA-SYS-011 | Help centre / support link | authorized? NO - proposal only; pending HU+DI naming |
| MA-SYS-013 | Multi-store switcher | deferred/excluded/not authorized |


## Revision 3 note
The detailed revision-3 reading ledger was folded into section 15. Gaps G-69 to G-76, minor findings m17 to m21 and decisions DEC-30 to DEC-32 were added in revision 3.
