# BUILD-245 decision reconciliation — HU+DI working result (2026-10-23)

**Purpose:** Reconcile `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md` against prior HU answers, the canonical 122-capability master, the 22-Oct disposition decision log, the updated 245-row BUILD ledger, and known frozen EffyKlean rules.

**Authority:** This is a reconciliation overlay, not new HU approval and not execution authorization.

**HU response evidence index:** See [HU response recovery register](./HU_RESPONSES_RECOVERED_REGISTER_2026-10-23.md), including the verbatim inventory of explicit HU messages from `HUDI Discussion/HuDI Conversation 17-part2.md` and their source line references. Treat exact quotations, normalized decisions, scope disposition and implementation evidence as separate things. Preserve the original 430-line prompt report as historical evidence. Do not treat its 151 distinct IDs as 151 unanswered questions. Do not change implementation status merely because a disposition question is resolved.

## Governing outcome

The old report combines five different things: (1) settled HU scope answers, (2) frozen business rules, (3) Zoho/Shiprocket ownership constraints, (4) technical/provider/legal validation actions, and (5) genuine unresolved design or business choices. Only category 5 can become a new HU+DI decision, and only after Di provides a concise recommendation and evidence. Categories 1–4 are not reasons to ask Hu to repeat an answer.

## Decisions/rules to carry forward without re-asking

### Inventory and fulfilment authority
- Keep inventory quantity adjustment/history, reservations, locations, purchase orders, transfers, suppliers, bins, incoming/transfer popovers and related stock operations in Zoho Inventory: **MA-INV-003/004/005/008/010/011/012/020/021/023/024**.
- **MA-INV-013**: inventory import authority stays in Zoho; do not introduce a competing local stock master.
- **MA-PRD-104**: any product-page adjustment must follow the approved Zoho-backed workflow and existing HU direction; it must not create a second inventory authority.
- Existing Zoho Inventory sandbox is working and was integrated with Shiprocket sandbox per Hu. Do not revive earlier “blocked” assumptions or repeat completed general sandbox setup checks. Narrow per-location stock reads/exports (**MA-INV-009/022**) remain specific validation tasks if not already evidenced.

### Payments and checkout
- Frozen rule: no COD, no partial payment, no Razorpay/alternative gateway fallback; no website-paid state without Zoho verification; **NO PAYMENT → NO DISPATCH**.
- **MA-SET-007/009/010/012** are not open choices to add manual/alternative gateways or payment/checkout customizations that violate the frozen rule.
- **MA-SET-011** must not become an Admin form that lets staff weaken frozen checkout/GST/payment requirements. Any safe editable fields must be derived from the frozen spec, not invented from the Shopify reference.
- Zoho Payments sandbox is working per Hu. This does not establish production readiness or authorise live writes.

### Zoho invoice, notification and shipping ownership
- Zoho owns invoicing and the existing Zoho-managed Shiprocket workflow remains intentional. Do not add a second invoice writer, notification engine, carrier-label writer or fulfilment/location master.
- **MA-ORD-039/090**: invoice generation/delivery follows Zoho ownership; Admin visibility may be built only within the recorded Zoho-compatible scope.
- **MA-ORD-080/084**: the recorded BUILD direction is status visibility/sync and constrained fallback for manually entered orders, not a parallel fulfilment system.
- **MA-ORD-088**, **MA-ORD-123**, **MA-INT-006**: preserve carrier/label/status ownership and source-of-truth constraints; technical status sync is an evidence/dependency task, not a fresh ownership question.
- **MA-ORD-111**: HU’s BUILD scope is abandoned-checkout recovery through a Zoho-managed notification approach, not a separate website email engine. Approved wording, consent, provider and credentials remain separate gates.
- **MA-ORD-103/105**: the canonical prior answer is NO for bulk fulfil/create-labels and bulk cancellation. Correct the stale ledger/register conflict; do not ask Hu to decide again.
- **MA-ORD-141**: BUILD was already explicitly recorded. Keep it scoped to the approved single action and existing Flow safeguards; this does not authorise unreviewed Zoho Flow writes.
- **MA-ORD-062/078**: remaining items are narrow read-only/capability checks (stock release on cancel; authorise-then-capture availability), not broad questions about payment or inventory ownership.

### Existing product, customer and commercial rules
- Products are physical shipped products: **MA-PRD-040** does not justify adding non-shipping products without a real use case.
- **MA-PRD-063 — HU approval (23-Oct-2026):** keep product IDs as the fixed URL identity (`/products/<id>/`). Editable slugs, slug-editing UI, and slug-change redirect behaviour are out of scope; preserve the existing product-ID URL pattern.
- No bulk product deletion; archive/unpublish is safer (**MA-PRD-092**). This does not by itself settle the exact product lifecycle state model.
- Platform-to-platform imports stay out; do not silently expand the existing CSV import (**MA-PRD-098**).
- Preserve the approved combo rule: first qualifying item has no discount; subsequent qualifying items are discounted; if the first item is removed, the next becomes first. **MA-DSC-026** is not a reason to ask Hu to restate that rule; only genuinely unspecified precedence/edge cases may need a recommendation.
- Customer address decision already recorded: one saved address, three-month retention and active-order protection. Multiple saved addresses are parked (**MA-CUS-006**); do not re-open it as a generic yes/no question.
- GST is inclusive; GST Number + Name produces a Zoho GST invoice only when the pair is valid, otherwise consumer treatment. Do not invent tax exemptions. **MA-CUS-014/045** need accountant-approved tax rules before any exception is implemented.
- **MA-PRD-047**: publication must be blocked until commercial data is verified. This is a gate, not permission to publish provisional MRP/concentrate/Zoho data.
- **MA-PRD-057 — HU clarification (23-Oct-2026):** A scheduled publication time does not publish the product automatically. Publication occurs only after the required approval is complete and an authorised Admin or Director manually publishes it. If they forget or approval remains incomplete, the product stays unpublished, even after the scheduled time. Do not implement automatic publication or any schedule-based bypass of approval, authorisation, or verified-commercial-data gates.

### Shopify-only mechanics and consent/language constraints
- Shopify plan/billing, packing-slip Liquid/package mechanics, app settings and feature previews have no direct EffyKlean equivalent as-is: **MA-SET-004/015/017/025/034**. Reuse the underlying business need only if the frozen spec or a prior HU decision requires a Django-native equivalent.
- Shopify theme-editor/theme-library/code-editor mechanics are not themselves an EffyKlean requirement (**MA-PRD-046, MA-CNT-014, MA-CNT-041**). Page/template/structured-content items (**MA-CNT-004/011**) must be mapped to native Django capabilities only where an approved need exists; do not copy Shopify's implementation model.
- DNS/domain changes (**MA-SET-026**) are restricted hosting/security actions, not ordinary Admin-editable settings.
- English is the approved language until verified translations are supplied. Do not ask about language again: **MA-SET-029/075, MA-MKT-012, MA-PRD-075, MA-CUS-043, MF-094** remain English-first; translations/rollout are deferred pending verified text.
- SMS is excluded; email/WhatsApp are preferred. This answers channel preference only; it does not approve marketing campaigns, providers, wording or credentials. Marketing consent must be explicit. Optional analytics/marketing tracking remains **LATER** under MF-093 and must not be enabled without an approved consent state (**MA-SET-027** and tracking-dependent analytics items).

## Technical, operational, legal and provider actions — not fresh HU questions

- **MA-INV-001/002/007**: targeted sandbox/read validation for inventory page, stock-state fields and locations, only where not already evidenced. Do not repeat completed OAuth/scope/general-read setup.
- **MA-INV-009/022; MA-ANA-014/025**: targeted per-location stock and Zoho purchase/received-quantity read checks. Preserve Zoho as authority; no stock writes.
- **MF-020**: re-check the development DB catalogue at the planned checkpoint; not a business decision.
- **MF-054**: inspect evidence for Zoho GST/invoice trigger/numbering/arithmetic/HSN/place-of-supply automation. Zoho invoicing ownership is already decided.
- **MF-055**: retrieve and apply the exact recorded S-5 customer-to-Zoho-contact mapping rule; do not invent a mapping policy or ask a broad repeat question.
- **MF-063; MA-INT-011/022**: read-only inspection of existing Zoho Flow/custom-app configuration by Hu. No Flow rewrite or external write is authorised.
- **MF-079; MA-SET-021/022/023/024; MA-ORD-063; MA-CUS-043; MA-MKT-006**: consolidate the notification matrix and ownership. Channel preference is already known; still-needed wording/provider/credential/consent approvals are specific dependencies. Do not enable SMS or build a second notification engine.
- **MF-084; MA-SET-057/060**: legal/policy wording requires Hu/legal review; do not fabricate legal text or label it compliant.
- **MF-086**: Director review of blog posts.
- **MF-088**: media hosting/Spaces belongs to the later hosting sequence; do not jump the agreed order.
- **MF-094**: do not reinstate Weglot or untranslated language choices; English-first rule stands.
- **MF-105**: BUILD was already approved. Preserve its split scope and security constraints: verified, time-limited single-use reset links; staff never view/set passwords; identity-verified customer-only export with secrets/other-customer data excluded, audit and legal-hold handling. This is not a fresh disposition question.
- **MF-110**: secrets-manager selection belongs to the security/hosting gate.
- **MF-115**: release acceptance follows its documented dependencies; it is not an independent scope question.
- **MA-CHN-004**: Merchant Center feed registration/validation is an external operational task.
- **MA-ANA-015/023**: settlement API/cost-basis/COGS reporting needs source and accounting evidence; do not invent settlement values or a cost authority.
- **MA-SYS-012**: responsive/accessibility browser re-check is validation, not a new feature question.

## Status of the former decision queue after Hu's 23-Oct answers

The historical 22-Oct prompts must not be used as an active questionnaire. The following decisions were resolved in the later conversation and are recorded in `HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md`:

1. **Product lifecycle — resolved:** Draft, Active, Unlisted (direct-link only), Archived. No Suspended state absent a concrete evidenced need. Preserve history and authorised actions.
2. **Publication scheduling — resolved:** MA-PRD-057 is manual-only after required approval by an authorised Admin/Director. Scheduled time alone never publishes; forgetting to publish leaves the product unpublished.
3. **Channel semantics — resolved without a new switch:** no separate Staff-availability setting; no invented channel switches or POS-terminal behaviour. Preserve the approved lifecycle, catalogue/Zoho-mapping and assisted-order safeguards.
4. **Admin-editable settings — baseline approved:** audited safe contact/brand content only; frozen checkout/payment/GST/tax, shipping authority, Zoho-owned data and domains/DNS remain restricted. Extra fields require HU+DI approval.
5. **Marketing/channels — scope approved:** implement approved marketing/channel capabilities as features, not future-only items. WhatsApp marketing is managed through Meta. Provider-specific configuration, live credentials, campaigns, sends and privacy-sensitive tracking remain separately gated.
6. **Analytics/segmentation — prior scope answers stand:** essential operational reporting and previously approved customer segmentation are not new questions. MF-093 tracking-dependent analytics remains LATER pending privacy/consent/retention controls.
7. **Discount controls — resolved:** optional one-use-per-customer and optional eligibility restrictions are in scope; existing combo, no-stacking, sale-price and distributor rules remain unchanged.
8. **Gift cards — resolved:** excluded/deferred unless HU+DI reopens the decision and accountant-approved terms are available.
9. **Customer records — resolved as scoped:** deletion YES for authenticated Admin/Director with safeguards; anonymisation NO; customer-record merging unapproved. Do not infer bulk deletion approval from the general deletion answer.
10. **Tax-exemption controls — scope approved:** authenticated Admin/Director only with change audit and supporting reason/evidence where applicable.
11. **Content/forms/search/chat/package — prior YES answers stand:** do not ask again; preserve privacy, moderation, provider and Zoho/Shiprocket boundaries.
12. **Quantity price breaks and updates subscription — resolved:** public quantity price breaks are in scope and set a tier selling price rather than stacking a discount. “Subscribe” is for EffyKlean updates, not recurring product orders/payments.
13. **Product URL identity — resolved:** fixed `/products/<id>/`; no editable slugs or slug-change redirects.

### Remaining work is not a fresh HU decision

- **MA-PRD-047:** technical/specification follow-up to identify the verified source field for concentrate data. The existing fail-closed rule is settled: unverified/provisional commercial data cannot be published or used to display savings.
- Other provider, privacy, hosting, catalogue, Zoho/Flow, email, Merchant Center, Spaces, accessibility and release-acceptance items remain execution/evidence gates at their proper stages. They must not be presented as unanswered business decisions unless the specific evidence reveals a genuine unresolved choice.
- Scope approval is not implementation evidence or permission for coding-agent delegation, production writes, live provider changes or deployment.

## Corrections required in the working records

- Mark the 22-Oct “decisions needed” document as superseded for question-generation purposes by this reconciliation overlay; preserve it unchanged as the historical generated list.
- **MA-ORD-103** and **MA-ORD-105** have now been corrected in `BUILD245_LEDGER_2026-10-22.csv` to current disposition `EXCLUDE` while retaining implementation status `DEFERRED` (not implemented). `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv` records the row-level current-scope correction. The 18-Oct 597-row snapshot independently shows both as EXC / REJECT-OOS. The 22-Oct working 597 CSV is zero-byte in GitHub, so this correction overlay plus updated current totals is the traceable current disposition record; the historical snapshot remains unchanged.
- Keep the original YES for product lifecycle capabilities in the canonical history while recording the later approved four-state model as the resolved refinement, not as a reversal of the original answer.
- Do not change any BUILD/Implemented status solely because a question was reconciled. Implementation, scope disposition, evidence, provider readiness, legal approval and production readiness remain separate fields.
- Do not ask a question for a capability already marked Implemented. For each remaining candidate, first verify its current 597-row disposition and any later project-history answer.

## Limits of this pass

This document now incorporates the end-to-end reconciliation of `HUDI Discussion/HuDI Conversation 17-part2.md`; the answered decisions listed above are not open questions. The two known prior-NO disposition conflicts remain corrected in the 245-row ledger, and the current 597-item totals are recorded in the existing correction overlay because the full 22-Oct working 597 CSV is zero-byte; the 18-Oct full snapshot remains historical. This pass does not claim that the private/local app repository was available, that every technical dependency was freshly verified, or that any external provider action was performed. No coding agent was delegated; no production/provider writes or deployment were performed.

## Consolidated next-step decision queue

The concise, recommended HU+DI decision queue is now recorded in [HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md](./HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md). Use that shortlist instead of generating new questions from the historical 22-Oct prompt. It separates genuine policy decisions from technical/provider/legal follow-ups and explicitly preserves previously answered rules. The 22-Oct prompt remains historical evidence and is not a current question list.


## 597-ID HU response reconciliation — 23 October 2026

The row-level response index is [HU_RESPONSE_RECONCILIATION_597_2026-10-23.csv](./HU_RESPONSE_RECONCILIATION_597_2026-10-23.csv). It covers all 597 IDs from the immutable 18-Oct source snapshot and distinguishes (1) recorded HU decisions/responses, (2) ledger-only reconciliation that is not a new HU response, and (3) no decision found in sources checked (not proof no answer exists). Verified counts: 215 rows with existing HU decision/response evidence, 144 reconciled from existing ledgers without inventing a new response, and 238 requiring historical-source review before any question could be considered. This is an evidence index, not a fresh approval or execution authorization.

**Known data defect:** RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv currently returns zero bytes from GitHub. The immutable 18-Oct snapshot remains intact; the new response crosswalk does not fabricate current dispositions for the 352 rows lacking row-level current-disposition evidence in the 245-row ledger/crosswalk. Reconstruct that disposition view separately from source evidence before claiming the 597-row current disposition register is fully repaired.


## Superseding update — 23 October 2026, earlier HU answers incorporated

After the initial crosswalk pass, I also reconciled the 18-Oct persistent HU answers file [RESP_18OCT_QA_HU ANSWERS.md](../../HUDI%20Discussion/RESP_18OCT_QA_HU%20ANSWERS.md) against the 597 IDs and attached the applicable directions to 56 distinct rows. This preserves earlier instructions while leaving later, more-specific decisions authoritative. The row-level crosswalk has been re-fetched and now contains **597 unique IDs** with these current counts:
- **252** rows with an existing HU decision/response source recorded;
- **127** rows reconciled from existing ledgers without treating that reconciliation as a new HU response;
- **218** rows where no HU decision was found in the sources checked so far. This is not proof that Hu never answered and does not mean all 218 require a question.

These counts supersede the earlier initial-pass counts recorded above. The 18-Oct source was not a verbatim transcript of every earlier conversation; this is still not an exhaustive audit of every historical chat. The zero-byte 597-row disposition working CSV remains a separate unresolved record-reconstruction defect.


## Final response-triage update — 23 October 2026 (supersedes earlier counts)

The 597-row crosswalk now incorporates the grouped original HU decisions from the canonical 12-Oct master and the applicable 18-Oct QA answer record, in addition to the 22-Oct decision log and 23-Oct refinements. The CSV was re-fetched and checked: **597 rows, 597 unique IDs**.

Current row-level classification:
- **530 rows** have a recorded HU decision/response source linked to the requirement ID. Original grouped YES/NO decisions are preserved as historical decisions; later specific refinements remain controlling. Decision-log summaries are not mislabeled as verbatim quotations.
- **11 rows** are reconciled from existing ledgers without treating that reconciliation as a new HU response.
- **44 rows** have an implemented/closed/no-action source status and need no HU question now; revisit only if concrete evidence reveals a material gap.
- **12 rows** were individually triaged as existing scope boundaries, frozen-spec/technical gates, or unapproved proposals. No broad HU question is warranted now; verify reference-site/SPEC evidence first, and STOP → REPORT → HU+DI DECIDE only if a real conflict remains.

The prior 18-Oct/12-Oct cross-source pass has reduced the set with no recorded answer source to zero *untriaged* questions in this pass. This does **not** prove that every historical chat has been audited, nor that the remaining items are all implemented. The 597-row primary-disposition CSV is still zero bytes on GitHub, and only 245 rows currently have row-level disposition evidence in the active BUILD ledger/crosswalk. Do not claim that the complete 597 primary-disposition register is repaired; that separate reconstruction remains outstanding and must use source evidence rather than guessed classifications.


## Correction — working disposition CSV restored, but not fully reconciled (23 October 2026)

Correction to the earlier note that the working disposition CSV was zero bytes: it has now been populated and re-fetched. [RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv](./RECONCILED_597_DISPOSITION_WORKING_2026-10-22.csv) contains **597 rows and 597 unique IDs**. It keeps the immutable 18-Oct source fields, carries the prior HU response evidence, and separates the decision/scope answer from the current primary disposition.

Row-level primary-disposition evidence now verifies **255 rows**: 84 Implemented, 160 BUILD, 2 EXCLUDE, and 9 INVESTIGATE. The other **342 rows are explicitly marked UNRECONCILED — DO NOT GUESS** because the existing sources checked so far do not support a reliable row-level current disposition for them. The previously reported aggregate 597 totals (340 Implemented, 160 BUILD, 10 LATER, 9 INVESTIGATE, 78 EXCLUDE) are retained as historical reported totals but are **not yet independently verified against all 597 row-level entries**. Reconstruct the 342 rows from source evidence before calling the disposition register complete or using aggregate totals as row-level proof.


## Latest disposition-register update — 23 October 2026 (supersedes prior row counts)

The working CSV now uses the historical status field to recover the **256 remaining rows explicitly marked implemented** in the 18-Oct snapshot. Re-fetch verification confirms 597 unique IDs. Row-level primary-disposition classifications now stand at **511 verified rows**: 340 Implemented, 160 BUILD, 2 EXCLUDE, and 9 INVESTIGATE. **86 rows remain UNRECONCILED — DO NOT GUESS.** The historical aggregate implies those 86 consist of 10 LATER and 76 EXCLUDE, but that split is not yet mapped to individual IDs from authoritative row-level evidence. Do not apply those aggregate numbers to specific rows by assumption. This supersedes the earlier statement that 255 dispositions were verified and the other 342 were unreconciled.

## Superseding update — BUILD-245 prior-input reconciliation and stale-question cleanup (23-Oct-2026)

This update supersedes earlier current-disposition counts in this document where they conflict with the corrected row-level records.

- The 245-row ledger and 597-ID response crosswalk were joined by exact activity ID. Before correction, the 245-row ledger showed 160 BUILD dispositions, 83 Implemented and 2 EXCLUDE. Of those 160 BUILD rows, 156 had an identified prior response/decision source (16 existing 18-Oct answer sources, 69 existing decision/response sources, 69 canonical original HU decisions, and 2 original YES decisions later refined to exclude/defer). Four rows — MF-055, MF-084, MF-094 and MF-115 — were ledger-only reconciliations, not explicit HU responses.
- The row-level check found that MA-GFT-001, MA-GFT-002 and MA-SET-032 still showed BUILD despite the later HU decision excluding gift cards from current scope and leaving them deferred for possible future reconsideration. All three are now EXCLUDE in both the 245-row ledger and the 597-ID response crosswalk; implementation status remains DEFERRED. Reopen only through a later explicit HU+DI decision and accountant-approved terms. Original YES decisions remain preserved as history.
- `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv` now contains five row-specific corrections: MA-ORD-103/105 and MA-GFT-001/002 plus MA-SET-032.
- The corrected 245-row current-disposition totals are **83 Implemented, 157 BUILD and 5 EXCLUDE**. The 245-row implementation statuses remain **83 DONE (verified), 62 PARTIAL and 100 DEFERRED**. These are separate dimensions.
- Forty-six stale next-action/reason-category entries were corrected in the 245-row ledger. The changes remove repeated broad questions where prior HU input already resolves them, while preserving specific legal/accounting, provider, validation, evidence and detailed-specification dependencies. No implementation, deployment, or live provider action is authorized by this reconciliation.
- The full 597-row current-disposition register is still not repaired: its working CSV fetches as zero bytes. The row-level evidence now verifies 511 IDs (340 Implemented, 157 BUILD, 5 EXCLUDE and 9 INVESTIGATE); **86 IDs remain UNRECONCILED — DO NOT GUESS**. Aggregate arithmetic implies 10 LATER and 76 EXCLUDE among those 86, but those IDs are not yet assigned from authoritative row-level evidence. Continue source-by-source reconciliation before asking any remaining genuine HU+DI decision. No coding agent was delegated.

## Latest superseding update — 160-row prior-input reconciliation (23-Oct-2026)

This supersedes the preceding disposition counts where they conflict with the corrected row-level files.

- Current 245-row dispositions: **83 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE**. Implementation status remains **83 DONE (verified), 62 PARTIAL, 100 DEFERRED**.
- Ninety-five unique rows in `BUILD245_LEDGER_2026-10-22.csv` have at least one corrected disposition, reason category or next action compared with the pre-reconciliation version. Stale broad questions were replaced by the recorded HU direction plus the specific remaining technical, provider, legal, consent, evidence or detailed-specification gate.
- Current-scope refinements now applied in both the 245-row ledger and 597-ID crosswalk:
  - LATER: MA-CUS-006 (multiple saved addresses), MA-PRD-075, MA-SET-029, MA-SET-075, MA-MKT-012 (translations pending verified text), MA-ANA-012/013/021/024/026, MA-SET-027, MA-CNT-042 and MA-MKT-002 (optional tracking/attribution pending the MF-093 consent/privacy/retention/access gate).
  - EXCLUDE: MA-CUS-020 (customer merging unapproved) and the earlier MA-GFT-001/002/MA-SET-032 gift-card exclusions. MA-ORD-103/105 remain excluded.
- `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv` now contains **19 row-specific corrections**. Implementation statuses remain separate from scope dispositions; no completed implementation is inferred from a disposition change.
- The complete 597-row current-disposition register is still not reconstructed because its working CSV fetches as zero bytes. Row-level classifications verify 511 IDs: 340 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE and 9 INVESTIGATE. **86 IDs remain UNRECONCILED — DO NOT GUESS**; aggregate arithmetic implies 10 additional LATER and 76 additional EXCLUDE, but the IDs are not yet mapped from authoritative evidence. No coding agent, implementation, deployment or live provider action was authorized by this reconciliation.

## Latest correction — 23-Oct-2026: 597-row working register re-fetched and synchronized

This update supersedes earlier statements in this document that the 597-row working-disposition CSV was zero-byte. The current GitHub fetch returns **597 rows and 597 unique IDs**. In this pass, all 245 IDs in the current BUILD ledger were synchronized to the corrected 245-row ledger and response crosswalk; a direct ID join found **zero disposition mismatches** between those three records. The 597-row working register now reflects the corrected dispositions and later HU refinements.

Current 597-row register counts: **340 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE, 9 INVESTIGATE and 86 UNRECONCILED — DO NOT GUESS** (597 total). Thus 511 rows have a row-level classification; the 86 unreconciled rows remain unassigned. Aggregate arithmetic implies 10 further LATER and 76 further EXCLUDE among those 86, but those individual IDs are not mapped to authoritative evidence. Do not assign them from the aggregate.

Current 245-row ledger dispositions: **83 Implemented, 143 BUILD, 13 LATER and 6 EXCLUDE**. Its implementation-status counts remain 83 DONE (verified), 62 PARTIAL and 100 DEFERRED. The 597-ID response crosswalk has 597 unique IDs; the decision overlay has 151 rows; the correction overlay has 19 unique row-specific corrections. Original HU answers remain historical evidence, and later specific refinements control current disposition. No coding agent was delegated and no implementation/deployment/provider action was performed by this reconciliation.

## Latest audit correction — 23-Oct-2026

The earlier count of 95 changed rows was an interim checkpoint. After the final pass replacing stale repeated questions with specific evidence/provider/legal/implementation actions, comparison with the pre-reconciliation 245-row ledger now confirms **114 unique rows** have at least one corrected disposition, reason category or next action. This does not mean those 114 capabilities are implemented.

The current 597-row working register is populated (597 rows / 597 unique IDs) and has been synchronized with the corrected 245-row ledger and HU-response crosswalk. Re-fetch verification confirms zero disposition mismatches across the 245 exact-ID join. Current overall counts remain 340 Implemented, 143 BUILD, 13 LATER, 6 EXCLUDE, 9 INVESTIGATE and 86 UNRECONCILED — DO NOT GUESS. The 86 unresolved IDs still need authoritative source-by-source reconciliation; do not assign them from aggregate arithmetic.


## Superseding response-reconciliation update — 23 October 2026 (Hu's instruction)

This pass reconciled the 245 unique implementation-ledger IDs against the 597-ID response crosswalk and the 151-row BUILD-245 decision/action overlay by exact ID. Of the 245 rows, **234 have an identified prior HU decision/response source** and **11 are ledger-only reconciliations, not explicit HU answers**. Do not present the latter as words Hu said. The crosswalk still covers 597 unique IDs; the remaining historical-source coverage boundary is recorded above and is not proof that no other answer exists.

- **35 row-specific next-action entries** were corrected in both the 245-row implementation ledger and the decision/action overlay. The corrections remove repeated broad scope/provider questions where prior HU input already settles scope, preserve genuine unresolved choices, and state the actual technical, evidence, provider, consent or legal follow-up. These are record corrections, not new HU approvals.
- Two stale current dispositions were corrected from BUILD to **EXCLUDE**: **MA-PRD-083** (Suspended-only state; Hu approved Draft/Active/Unlisted/Archived and no Suspended absent evidenced need) and **MA-PRD-092** (bulk product deletion; archive/unpublish is the approved safer alternative). Both remain **DEFERRED** as implementation status. Their original historical decisions are retained.
- The correction overlay now contains **21 row-specific corrections**. Current dispositions in the 245-row ledger now count **141 BUILD, 83 Implemented, 8 EXCLUDE and 13 LATER** (245 total). Implementation status is a separate dimension and is unchanged by these scope corrections.
- Do not treat the reported aggregate 597-item disposition totals as fully row-verified: the known unreconciled portion remains governed by the explicit coverage warning above. No deployment, live provider writes or coding-agent delegation was authorised by this pass.

- Three additional implementation-ledger follow-up descriptions were clarified from prior Hu direction: **MF-063** (Zoho Flow/Shiprocket inspection parked for later testing), **MF-079** (existing GoDaddy/Zoho messaging direction retained; exact drafts, credentials and delivery evidence remain), and **MF-088** (Spaces is the approved storage direction, but provisioning remains a separate HU-authorised action). These are operational follow-ups, not new scope questions.

- Two additional repeat questions were removed: **MA-PRD-067** is already DONE (verified) under the recorded YES (G-23 no longer asks whether related links are wanted), and **MA-DSC-020** is already DONE (verified) under the frozen no-stacking/discount-precedence rules. Neither is a new HU decision.
