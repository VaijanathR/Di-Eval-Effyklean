# BUILD-245 decision reconciliation — HU+DI working result (2026-10-23)

**Purpose:** Reconcile `BUILD245_HUDI_DECISIONS_NEEDED_2026-10-22.md` against prior HU answers, the canonical 122-capability master, the 22-Oct disposition decision log, the updated 245-row BUILD ledger, and known frozen EffyKlean rules.

**Authority:** This is a reconciliation overlay, not new HU approval and not execution authorization. Preserve the original 430-line prompt report as historical evidence. Do not treat its 151 distinct IDs as 151 unanswered questions. Do not change implementation status merely because a disposition question is resolved.

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

## Genuine unresolved decisions/specification work to consolidate before asking Hu

These are candidate decision clusters, not 1:1 questions. Di must first reconcile the exact capability rows with the canonical master, frozen spec and later HU clarifications, then provide one recommended proposal per cluster. Do not ask the original prompts verbatim.

1. **Product lifecycle (DC-10):** MA-PRD-052/053/083/091. The original capability YES answers express desired scope, but the frozen spec deferred the exact archive/unpublish/unlisted/suspended state model. Propose the smallest safe lifecycle; retain history and prevent accidental removal of live products.
2. **Publication scheduling:** MA-PRD-057. Recommend keeping scheduled publication out unless a staff-authorisation and audit model is explicitly approved; it must not bypass verified-commercial-data and publication gates.
3. **Channel semantics — reconciled, no new HU decision:** MA-PRD-012/093, MA-COL-008, MA-PRD-100. Do not add a separate Staff-availability setting. Preserve the approved Draft / Active / Unlisted / Archived lifecycle and existing publication/catalogue/Zoho-mapping safeguards. Active does not mean hidden from the public website; Unlisted is the existing state for a product intentionally not publicly listed. Staff-entered orders follow the approved assisted-order workflow and verified-full-payment rule. Do not invent extra channel switches or POS-terminal behavior. Escalate only a concrete conflict with frozen requirements.
4. **Admin-editable store/settings surface:** MA-SET-001/003/013/020 and any safe remainder of MA-SET-011. Separate safe store contact/brand content from frozen checkout, returns/store-credit, location, tax and payment authorities. Recommend which fields are native settings versus controlled deployment/Zoho-owned data.
5. **Marketing, channels and providers:** MA-MKT-001/002/003/004/007/013; MA-CHN-002/003/005/006/007/008; MA-SET-072; MA-PRD-096. No provider/campaign/pixel/AI/marketplace/social-login action without purpose, data flow, consent, provider, wording and ownership defined. Existing WhatsApp notifications do not automatically approve WhatsApp commerce or marketing.
6. **Analytics/reporting:** MA-ANA-011/022/017/027/018/020 and MA-CNT-042; MA-ANA-012/013/021/024/026 remain gated by MF-093 where they require session/pixel tracking. Decide only report-library/custom-builder scope or customer-segment thresholds that are not already answered. Tracking-dependent features remain later until consent/privacy/retention is approved.
7. **Discount edge cases:** MA-DSC-011/012 and the unspecified edges of MA-DSC-026. Preserve the existing combo rule; propose customer eligibility/one-use identity and coupon precedence rules only where the canonical records truly leave them open.
8. **Gift cards:** MA-GFT-001/002 and MA-SET-032. Terms, redemption controls, expiry and liability/accounting need one consolidated proposal; do not implement before the rules are approved.
9. **Customer data:** MA-CUS-009/050/020. Customer/order-history deletion/anonymisation and merge behavior require retention/legal-hold safeguards and legal review. The contact-form MF-089 180-day rule is not automatically the customer/order-history rule.
10. **Tax exceptions:** MA-CUS-014/045. Obtain accountant-approved criteria; no ad hoc exemption/collect-tax toggles.
11. **Content/search/forms/chat:** MA-CNT-008/015/016/019/020 and MA-PRD-105. Distinguish a real EffyKlean use case from Shopify-specific builders/Tidio/theme mechanics. Existing contact form does not imply a general form-builder requirement; the sample package dimensions do not authorize a competing carrier workflow.
12. **Price breaks/subscriptions:** MA-PRD-071/070. Public quantity price breaks are separate from approved distributor slabs. Recurring charges require verified Zoho Payments capability and a separate policy; do not infer subscription support from a working sandbox.
13. **Draft orders:** MA-DRF-003/004/007 have recorded BUILD scope and must not be re-asked as yes/no. Remaining implementation details must preserve catalogue/Zoho mapping, full payment only, Zoho invoice/payment verification, and the approved manual-order workflow.
14. **Policy/notification details:** MA-SET-057/060, MA-SET-021/022/023/024, MA-ORD-063 and MF-079. Keep the already-selected channels; only ask for specific wording/provider/approval inputs that cannot be sourced from the existing record.

## Corrections required in the working records

- Mark the 22-Oct “decisions needed” document as superseded for question-generation purposes by this reconciliation overlay; preserve it unchanged as the historical generated list.
- **MA-ORD-103** and **MA-ORD-105** have now been corrected in `BUILD245_LEDGER_2026-10-22.csv` to current disposition `EXCLUDE` while retaining implementation status `DEFERRED` (not implemented). `CURRENT_597_DISPOSITION_CORRECTIONS_2026-10-23.csv` records the row-level current-scope correction. The 18-Oct 597-row snapshot independently shows both as EXC / REJECT-OOS. The 22-Oct working 597 CSV is zero-byte in GitHub, so this correction overlay plus updated current totals is the traceable current disposition record; the historical snapshot remains unchanged.
- Keep the original YES for product lifecycle capabilities in the canonical history while recording the later frozen-spec deferral as an unresolved refinement, not as a reversal of the original answer.
- Do not change any BUILD/Implemented status solely because a question was reconciled. Implementation, scope disposition, evidence, provider readiness, legal approval and production readiness remain separate fields.
- Do not ask a question for a capability already marked Implemented. For each remaining candidate, first verify its current 597-row disposition and any later project-history answer.

## Limits of this pass

This document reconciles established rules and known prior answers and consolidates the genuine decision clusters. The two known prior-NO disposition conflicts have been corrected in the 245-row ledger, and the current 597-item totals are updated; the full 22-Oct working 597 CSV is zero-byte, so the two-row current-disposition correction overlay is preserved separately while the 18-Oct full snapshot remains unchanged. This pass does not claim that the private/local app repository was available, that every technical dependency was freshly verified, or that any external provider action was performed. No coding agent was delegated; no production/provider writes or deployment were performed.

## Consolidated next-step decision queue

The concise, recommended HU+DI decision queue is now recorded in [HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md](./HU_DI_GENUINE_DECISIONS_SHORTLIST_2026-10-23.md). Use that shortlist instead of generating new questions from the historical 22-Oct prompt. It separates genuine policy decisions from technical/provider/legal follow-ups and explicitly preserves previously answered rules. The 22-Oct prompt remains historical evidence and is not a current question list.
