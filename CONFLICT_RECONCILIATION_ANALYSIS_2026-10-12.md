# EffyKlean Admin Capability Reconciliation — Business Intent First

**Date:** 2026-10-12  
**Status:** HU+DI analysis record; assessment and reconciliation recommendations, not implementation authorisation.  
**Source comparison:** [COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md](COMPARISON_1_SHOPIFY_ADMIN_VS_DJANGO_ADMIN_2026-10-12.md)  
**Decision ledger:** [ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md](ADMIN_CAPABILITY_DECISION_LEDGER_2026-10-12.md)  
**Purpose:** Reassess the recorded Shopify-vs-Django differences using HU's governing test: **Is this a genuine conflict where two decisions cannot coexist?** If not, retain the desired capability and combine it with the existing business rules where useful.

## 1. Governing principle

The earlier conflict backlog over-classified differences as conflicts. HU clarified that the YES/NO capability review was intentionally conducted first so that EffyKlean's desired future Admin experience could be established before resolving genuine contradictions. A YES often means “this capability is desirable for a better customer/management experience, now or in the future,” not “replace our current business model” and not “implement immediately.”

Apply this sequence to every capability:

1. **Identify the business intent** behind the capability and preserve the original comparison ID(s).
2. **Check coexistence:** can the capability and the existing rule both be true?
3. If yes, **combine them** into a coherent feature; do not label a conflict.
4. If the capability is useful but not needed immediately, preserve it as a **future enhancement** rather than rejecting it.
5. If a literal Shopify implementation is unsuitable, adapt the underlying value to EffyKlean's business model rather than cloning Shopify's workflow.
6. Raise a decision to HU only if two explicit decisions cannot coexist and there is no reasonable adaptation that preserves the intent.
7. Keep implementation status, provider verification, priority and implementation authorisation separate from business intent.

Shopify's implementation is evidence that a capability exists in a real commerce platform and can be worth investigating. It is not, by itself, proof that the same workflow, permissions or provider setup is appropriate for EffyKlean.

## 2. Evidence and limitations

- The source comparison covers **494 capability rows** across 34 Shopify Admin areas and maps them to Django Admin.
- The comparison says Shopify observations were carried forward from read-only walks on 2026-10-05 and 2026-10-10, not re-observed on 2026-10-12. Some rows are DOC/UNK and are not verified for this store.
- The Django side in the source comparison was statically inspected; no fresh test/browser run or provider contact was performed for that comparison. Provider integrations are explicitly described as simulations/mocked HTTP rather than provider-proven.
- The decision ledger is a continuity aid recovered from prior discussion, and it contains known errors/ambiguities (including the malformed Orders range and some over-broad “conflict” labels). The row-level comparison is the capability catalogue; the ledger and conversation decisions supply business intent.
- This document reconciles the known groups and corrects the decision approach. It does **not** claim that all provider integrations or implementation behaviour have been verified, nor does it authorise code changes.

## 3. Existing business rules that remain in force

These rules are constraints to design around, not reasons to discard additional Admin capabilities:

- Zoho remains the stock/inventory authority; storefront stock is a synchronised representation.
- HU's desired stock-sync model: sync Zoho items/products with the storefront on stock change, with hourly synchronisation/reconciliation as a fallback; support low-stock alerts in Zoho and on EffyKlean.in. Verify trigger support, retries, failure alerts and actual sync health before describing it as live.
- Product additions in Zoho or the storefront should include the required dimensions. Do not create duplicate Shiprocket dimension-management merely to repeat the same data; verify the data mapping at integration boundaries.
- HSN comes from the previously documented EffyKlean default and must be retrieved rather than guessed. HU's intended GST treatment: Karnataka intra-state supply uses 9% CGST + 9% SGST; other-state inter-state supply uses 18% IGST. Implement subject to correct place-of-supply and applicable product classification rules; the product category is not the tax engine.
- Product catalogue remains SKU-centric. A combo has no separate SKU; checkout computes combo pricing and the resulting Zoho order carries actual item SKUs, quantities, line prices and discounts.
- Combo pricing: first selected item receives no combo discount; subsequent selected items receive the configured amount-based discount; removing the first makes the next selected item first.
- One additional discount only, in line with the existing pricing rule. Distributor quantity slabs and negotiated Bulk pricing remain distinct from public promotions.
- No separate Household/Bulk combo collections. Distributor pricing uses quantity slabs; Bulk terms are negotiated using quantity, supply duration and payment factors.
- COD is excluded. **No refunds and no returns.** Replacements for damaged/incorrect goods remain a distinct existing process.
- **NO PAYMENT → NO DISPATCH.**
- No customer cancellation or editing after order placement. Admin may cancel an order based on the case.
- Admin may mark an order fulfilled and may add tracking or leave tracking blank (for example, a known customer collecting an online order from a location).
- Overrides require Director approval. Record the reason, actor and approver in the audit trail.
- Management may establish storefront/POS arrangements based on distributor discussions. A capability to support multiple sales contexts should not be dismissed merely because today's operation has one main web storefront.
- Zoho → Shiprocket remains the fulfilment/integration context. Existing Zoho Flow order-created workflow must be inspected and protected; do not replace or modify it without HU+DI review. Shiprocket WhatsApp notifications remain enabled.
- Email/WhatsApp are preferred; SMS is not the default channel. A non-default channel may be considered as a future configurable option where consent, compliance and business value are addressed.
- Existing role model includes ADMIN/DIRECTOR and MARKETING; ADMIN/DIRECTOR may manage marketing budgets. Director approval is required for overrides.
- Additional Admin powers are management capabilities used in the interest of the organisation. They are not automatically customer self-service features.

## 4. Outcome summary

**Assessment result:** the earlier backlog contains many apparent conflicts that are actually future capabilities, implementation differences, or opportunities to combine capability with a guardrail. After applying the coexistence test and the business rules above, **no additional HU decision is currently necessary merely to settle those false conflicts**.

Two areas need explicit implementation interpretation, but their business outcome is already clear:
- A self-service returns/refunds feature cannot be enabled because HU explicitly confirmed no refunds/returns. Admin order management can still be flexible.
- Shopify taxonomy-driven tax rates cannot be adopted literally because EffyKlean's GST rule and HSN handling are already defined. The useful product-tax/HSN data capability can still be supported without allowing a Shopify taxonomy to determine GST.

Other risks (provider proof, exact integration mechanics, data mapping, legal consent, security controls) are implementation/readiness checks—not reasons to ask HU to repeat business decisions.

## 5. Reconciliation by capability group

### 5.1 Orders and fulfilment — ORD-001..145

**Business intent:** a capable Admin order workspace with useful filtering, history, notes, exports, reconciliation, operational actions and management flexibility.

**Reconciliation:**
- Keep order list/detail, status/payment/fulfilment filters, customer and line-item detail, payment/provider references, EKI/Zoho/Shiprocket references, audit/timeline, customer history, attention flags, order exports, print/export options, destination/PO details, tracking links and other useful operational views as capability candidates. Missing in Django means an enhancement, not a conflict.
- Admin cancellation (ORD-060/061) coexists with the rule that customers cannot cancel after placement (ORD-064 is not to be exposed as customer self-service). Cancellation does not itself authorise an inventory adjustment; Zoho remains stock authority.
- Delivery contact/address corrections before handover can coexist with prohibiting post-order line-item, quantity, price or discount edits. Customer change requests can be handled by Customer Care/management without providing a self-service edit control.
- No refunds, returns, exchanges, store credit or return labels in the baseline (ORD-069..075, ORD-144 and related settings). Replacement for damaged/incorrect items remains separate (ORD-072).
- Admin fulfilment and tracking (ORD-080/081) are desired operational powers in HU's clarified model. Admin may mark fulfilled, add tracking, or leave it blank for local pickup. Keep this action auditable and ensure it cannot bypass payment verification. A manual delivery/fulfilment entry is an Admin record, not a claim that carrier data was received.
- Director approval is required for overrides; record approver/reason. The UI should make the distinction between ordinary Admin action and override explicit.
- Hold/release, exception resolution, retries, bulk selection/export, bulk status conveniences, order notes/comments, archive, duplication and related utilities should be evaluated as useful Admin capabilities with guardrails. Do not automatically reject bulk features merely because a previous recommendation called them unsafe. For destructive/high-impact bulk actions, use confirmation, preview, permission checks and audit; Director approval where the action is an override.
- Do not automatically reassign/split fulfilment locations or change routing in a way that contradicts the agreed operations model. The capability may be designed for future authorised management/distributor/POS needs; do not build an independent inventory or carrier system.
- Customer-facing tracking (ORD-109/143) can coexist with Admin fulfilment operations. The actual status source should be clear: provider/carrier status where verified, otherwise an explicitly recorded Admin update.
- ORD-141 “Run Flow automation” can be interpreted as a future Admin automation capability, not an instruction to implement Shopify Flow. It must coexist with and not silently replace the existing Zoho Flow. Define allowed triggers/actions, permissions and audit before implementation.
- ORD-145 remains unknown in the source comparison because the menu was not observed; this is a read-only evidence gap, not a business conflict. Inspect it only if it adds a unique capability not already represented.

**Disposition:** mostly desired capability/enhancement; no new business question. Preserve no refunds/returns, customer self-service restrictions, Zoho stock authority, payment gate and Director override approval.

### 5.2 Draft orders, distributor and Bulk workflow — DRF-001..021; CUS-029..033; relevant ORD rows

**Business intent:** help management serve distributors and Bulk customers with enquiries, quotations, negotiated pricing, approvals and convenient order creation.

**Reconciliation:**
- Shopify-style Draft Orders, custom line items, PO numbers, notes/timelines, review statuses and payment links are potential tools, not a requirement to copy Shopify wholesale.
- Build around EffyKlean's distributor application, distributor pricing, Bulk enquiry and Bulk quote/business-account model.
- Default to catalogue SKUs. Non-catalogue custom lines can be an explicitly controlled future capability if the business needs them; they must not bypass product/tax rules or create ambiguous Zoho order lines.
- Draft shipping lines are not required by default under the current shipping rule. This does not block draft/quotation workflows.
- Tax-exempt controls must not override the established GST/place-of-supply and HSN logic without a valid tax basis.
- Draft statuses, “submitted for review,” approval and payment links can improve the management workflow. Creating/sending a payment link is not payment confirmation. Do not dispatch until payment is verified unless HU+DI later approves a documented alternative.
- A quotation may be converted to a proper order with agreed SKU lines, quantities, prices and discounts; Zoho does not need a combo SKU.

**Disposition:** opportunity/addendum, not a conflict. Exact workflow is a future design/implementation detail; no repeat question needed.

### 5.3 Products, catalogue, collections and inventory — PRD-001..105; COL-001..010; INV-001..024

**Business intent:** richer product administration, efficient catalogue maintenance, better customer discovery, accurate logistics data and stock visibility without creating a second inventory system.

**Reconciliation:**
- Preserve product create/edit/revision/approval/publish, product history, preview, SEO, media, image alt text, tags, sorting/filtering, product export, safe bulk edits, and other catalogue conveniences as desired capabilities.
- Product import, bulk edits and archive operations can coexist with SKU-centric controls when designed with validation, preview, duplicate detection, approval, audit and rollback. Do not confuse “CSV import capability desired” with permission for unvalidated imports or platform-to-platform migration. No bulk product deletion; archive/unpublish is safer.
- Inventory adjustment, inventory import/export, purchase orders, supplier management, stock reservations and transfers remain outside EffyKlean Admin's independent authority. This does not exclude read-only Zoho-sourced stock, inventory indicators, low-stock filters/alerts or reports after integration is verified.
- Product weight/dimensions belong in the product-creation workflow as HU described. Ensure the same canonical values map to Zoho/Shiprocket as required; do not create a separate duplicate package database without need.
- HSN should use the previously documented default and the established GST logic. Shopify taxonomy must not determine GST (PRD-084); a useful tax/HSN data field or classification view may still exist independently of Shopify taxonomy.
- Product status, category, tags, bulk edits, collections and product filters are business tools. Do not introduce separate Household/Bulk combo collections. A future collection/catalog capability may support discovery, campaigns or distributor-specific storefronts if it does not violate that explicit exclusion.
- Combo products/bundles should not be implemented as separate SKU inventory when HU's combo model is a storefront calculation. Keep line-item details in the resulting order.
- Video/3D media, product translations, metafields, channel-specific product settings and other catalogue extras should be treated as future opportunities or lower-priority enhancements where useful; not automatically “conflicts.” Raw theme/code editing is different from safe content/layout controls and should be scoped with security/release controls.

**Disposition:** most rows are enhancements. The two explicit limits are no independent stock authority and no Shopify-taxonomy-driven GST. Neither requires rejecting useful adjacent capabilities.

### 5.4 Customers, distributor accounts, segments, data import/merge — CUS-001..056

**Business intent:** stronger customer history, follow-up, segmentation, account management and growth/retention tools.

**Reconciliation:**
- Customer list/search/details/order history/notes/tags/export, filters, segments, customer timelines and safe account-management tools can coexist with EffyKlean's customer and business-account model.
- Shopify “Companies” is a data model, not the only way to support B2B. EffyKlean can continue using distributor applications, business accounts, Bulk enquiries/quotes and distributor pricing, while adding useful account/contacts/locations/terms capability if business needs justify it.
- Customer import/merge is not inherently a business contradiction; it is a data-quality/privacy risk. If retained as future capability, require duplicate detection, mapping preview, validation, audit, backup/rollback and controlled permissions. Do not perform an unreviewed bulk import or merge. Customer deletion/anonymisation and data-request handling need legal/privacy rules and audit.
- Customer segments and filtered lists can support marketing and follow-up. They do not require copying ShopifyQL or Shopify's exact UI.
- Consent display can coexist with future consent updates and marketing tools; honour actual consent and channel-specific requirements. SMS is not the default and must not be sent without appropriate consent.
- Customer account invitations/sign-in assistance can be considered if customer accounts become part of the approved storefront experience; do not confuse Admin staff MFA reset with customer account recovery.

**Disposition:** enhancement opportunities with data/privacy controls; no need to reopen YES answers.

### 5.5 Discounts, promotions, combos and commercial pricing — DSC-001..041

**Business intent:** flexible commercial campaigns while preserving clear and predictable pricing.

**Reconciliation:**
- Discount lists, fixed/percentage discounts, eligibility, minimums, usage limits, date ranges, duplicate/code generation, reports and management comments can coexist with the existing pricing model.
- DSC-018 “combinations with other discounts” should be implemented as a configurable capability whose valid configuration is constrained by the existing “one additional discount only” rule. It must not silently permit unlimited stacking. If a requested future promotion would exceed the rule, treat it as a deliberate business-rule revision, not a hidden side effect.
- DSC-023 free-shipping discount is not needed in the current baseline. That does not block other discount types or a future shipping-promotion decision if the shipping model changes.
- DSC-026 combo pricing must implement the existing per-item selection rule. Do not create a combo SKU or a separate combo inventory ledger.
- Distributor quantity slabs and negotiated Bulk pricing remain separate from public promotional discounts; distributor/Bulk exclusion from public promotions is retained.
- Admin powers may include creating, scheduling, deactivating, duplicating and analysing discounts, subject to permissions and audit.

**Disposition:** combine the discount-combination UI with the one-extra-discount guardrail; preserve the established combo calculation. No new question needed.

### 5.6 Gift cards — GFT-001..002; SET-032

**Business intent:** possible future customer acquisition, gifting, retention and liability reporting.

**Reconciliation:**
- The ledger records GFT-001/002 as later YES answers while the comparison's older recommendation says REJECT. Under HU's stated method, a later YES is evidence of desired future capability, not a contradiction to be discarded.
- Gift cards are not the same as refunds, returns or store credit. They can be evaluated as a separate future commercial instrument with expiry/terms, liability accounting, fraud prevention, redemption controls and Zoho/accounting mapping.
- Do not conflate a gift card with issuing store credit on cancellation or refund; the latter remains excluded.

**Disposition:** future business enhancement; prior recommendation to reject is superseded as a recommendation by the later YES intent. Not implementation-authorised.

### 5.7 Content, Files, navigation, themes, forms, chat and structured content — CNT-001..042; related PRD/SET rows

**Business intent:** management should be able to improve storefront content, customer education, navigation, lead capture and engagement without depending on a developer for every routine update.

**Reconciliation:**
- Page creation/edit/publish, SEO, navigation, blog content, FAQ, redirect management, Files/media library, how-to content, forms and chat can be evaluated as capabilities supporting customer engagement and conversion.
- A previous “no theme editor/code” recommendation does not imply “no storefront customisation.” Prefer safe, versioned settings/layout controls and controlled publish/preview. Arbitrary raw theme-code editing should not be exposed casually; if ever required, it belongs in a separately controlled developer/release workflow.
- Forms and chat can coexist with existing distributor enquiry/Bulk intake and customer-care channels; integrate rather than duplicate data capture.
- Metaobjects/structured content can be represented by approved domain models where needed; copying Shopify's object model is unnecessary.
- Files library and media references can improve content management; enforce size/type, alt text, reference checks and safe deletion.
- Video/translation/localisation features are future enhancements, not conflicts. Implement only when content and support operations are ready.

**Disposition:** treat as growth/customer-experience opportunities; adapt the implementation to Django architecture and safe publishing rather than cloning Shopify internals.

### 5.8 Marketing, channels, messaging, POS and distributor storefronts — MKT-001..013; CHN-001..008; SET-024/059; relevant SET rows

**Business intent:** reach customers through useful channels, support distributor/POS operations and expand the business over time.

**Reconciliation:**
- Marketing campaigns, attribution, email, audience tools, social posting, Meta/Google/YouTube, WhatsApp and marketplace connections can be future capabilities where business value and provider setup support them. Earlier recommendations to reject these as “not in scope” should not override later YES intent by themselves.
- Keep the MARKETING role and ADMIN/DIRECTOR budget authority. Provide permissions, budget limits, approval and audit where needed.
- Existing email/WhatsApp preference and Shiprocket WhatsApp notifications remain. SMS is not the default; channel capability is not permission to send messages without valid consent or required compliance.
- POS and distributor storefronts are opportunities. HU confirmed management may create storefront/POS arrangements based on distributor discussions. The previous “single channel” rationale is not a permanent business prohibition.
- Multi-store or multi-channel architecture should be designed deliberately; do not add a Shopify-specific store switcher unless it maps to an actual EffyKlean operating model.
- International markets, languages, duties and local pricing can remain future capabilities; current India/INR operation is not a contradiction to future expansion.

**Disposition:** future growth capabilities; retain explicit NOs only where HU clearly said NO (e.g., COD, Razorpay Magic Checkout, or a specific unwanted Shopify-only mechanism).

### 5.9 Analytics and reports — ANA-001..027; SYS-008/022; CNT-042

**Business intent:** improve operational decisions, conversion, customer retention, financial control and growth planning.

**Reconciliation:**
- Sales/order/payment/discount/state reports, GST summaries, customer cohorts, average order value, inventory visibility, exports, scheduled reports, traffic/conversion and acquisition metrics can coexist with the business model when their data sources are available and trustworthy.
- Reports that depend on cost, payout, stock, traffic or carrier data must identify data source, freshness and coverage; do not manufacture unavailable metrics.
- ANA-026 AI-agent sessions/conversations was marked REJECT in the comparison while the ledger records a later YES for ANA-001..027. Treat the later YES as desired future scope to assess, not as a requirement to build a specific AI agent. It is only useful if EffyKlean actually deploys such a customer-facing agent and has appropriate privacy/retention controls.
- Home alerts/notifications and traffic/conversion cards can be added as management convenience when underlying data exists.

**Disposition:** reporting enhancements; no conflict merely because Django lacks the report today.

### 5.10 Settings, payment providers, tax, shipping, privacy and domains — SET-001..076

**Business intent:** management needs enough configuration visibility and control to run the business and expand capabilities without bypassing approved rules.

**Reconciliation:**
- Read-only settings/health views, store profile, brand assets, domains, languages, policies, customer privacy, notifications, payment capture configuration and provider readiness can improve operations.
- A YES for alternative gateways/settings means the capability may be desired in future; it does not mean a new gateway is already approved/configured or should be activated without testing. Razorpay remains the approved gateway in the current baseline; verify the current domain/account and capture mode before live use.
- COD remains an explicit NO and must not become available merely because a payment-settings screen exists.
- Self-service returns/store credit must not be enabled because HU explicitly confirmed no refunds and no returns. This is a feature-level constraint, not a reason to remove the rest of the customer-account/settings capability.
- Shipping profiles, local delivery/pickup and packing-slip templates may support future operations; Admin fulfilment without tracking is already accepted. Do not add an independent carrier or inventory authority.
- Tax settings must preserve the intended GST/place-of-supply logic and HSN mapping. Do not make Shopify taxonomy or an arbitrary Admin override the tax engine.
- Billing/plan screens specific to Shopify are not applicable to a self-hosted Django app. That is a platform-specific non-equivalence, not a business conflict; implement useful cost/usage/operational reporting only if there is a real requirement.
- Domains and sales-channel settings can support future storefront/POS expansion but do not prove DNS, Razorpay domain approval or provider configuration is complete.
- SMS and social sign-in may be future optional capabilities; consent, security and explicit channel choice remain required.
- Editable packing-slip templates can be useful, but the fulfilment source and actual output must be defined.
- Privacy/policy controls need HU-approved legal text and appropriate review; a capability does not authorise inventing legal policy.

**Disposition:** capability/configuration opportunities, with explicit exclusions and provider verification retained.

### 5.11 Integrations, automation and Zoho Flow — INT-001..023; ORD-141; SET-023

**Business intent:** transparent integration health, recovery, automation and fewer manual operations.

**Reconciliation:**
- Integration readiness, webhook logs, reconciliation queues, outbox/worker views, Zoho mapping/sync health, Shiprocket status, webhook subscription configuration and read-only workflow visibility are useful Admin capabilities.
- INT-009 “Shopify Flow” and INT-020/021 Shopify Flow-specific builder/history are platform-specific. Their prior rejection does not rule out EffyKlean-owned automation capabilities or Admin actions that run approved workflows.
- ORD-141 “Run Flow automation” can coexist with protecting Zoho Flow if interpreted as a future controlled automation action, not as permission to replace the existing Zoho order-created workflow or install Shopify Flow.
- HU's stock-sync intent is change-triggered Zoho-to-storefront sync plus hourly reconciliation/fallback, with low-stock alerts in both systems. Implementation must verify Zoho capabilities, event delivery, retries, idempotency, monitoring and recovery. Do not claim this is live until provider-proven.
- The existing Zoho order-created workflow that updates Zoho order details must be inspected read-only before any changes. Keep Shiprocket WhatsApp notifications enabled.
- Provider integrations currently shown as simulations/mocked HTTP in the comparison are not proof of live connectivity. Provider verification is a release/readiness task, not a business conflict.

**Disposition:** build toward reliable, observable integration operations while protecting existing workflows; no repeated business question.

### 5.12 Staff, roles, security, system shell and admin experience — USR-001..032; SYS-001..022

**Business intent:** empower management and staff while ensuring sensitive actions and information are controlled.

**Reconciliation:**
- Staff invite/create, deactivate/reactivate, MFA reset, sign-in history, audit export, permission visibility, cost/report/export access restrictions, global search, recent items, notification centre, home metrics and help/support links can improve the Admin experience.
- A prior rejection of a custom granular role builder does not contradict the need to control access. Implement the approved role model (including ADMIN/DIRECTOR/MARKETING) and clear capability permissions; do not assume a full Shopify-style role editor is required.
- MFA reset and account recovery should be restricted, audited and use appropriate re-verification. Staff invite/create needs secure activation and MFA onboarding.
- Cost, sensitive reports and exports should be limited to authorised roles. Director approval for overrides must be enforceable and auditable.
- Customer notification centre and staff operational alerts can coexist; do not send messages to customers without consent and configured providers.
- Home analytics should only show metrics backed by available, reliable data. A multi-store switcher is unnecessary until EffyKlean has a genuine multi-store operating model, but management's future distributor storefront/POS intent should inform the architecture.

**Disposition:** desired management flexibility with least privilege, audit and explicit Director override controls.

## 6. Explicit decisions versus future implementation details

Do not ask HU again about these unless new evidence demonstrates a real contradiction:

- Admin-only order cancellation; no customer cancellation/editing after placement.
- No refunds or returns; replacements remain separate.
- Admin can fulfil an order with or without tracking, including local pickup.
- Director approval for overrides.
- Distributor-driven storefront/POS arrangements are possible.
- Zoho stock authority and desired stock sync on change plus hourly reconciliation/fallback; low-stock alerts in Zoho and storefront after verification.
- Product dimensions are entered during product creation; map them consistently to relevant systems.
- GST logic and default HSN follow the previously documented rule; retrieve the HSN from source rather than invent it.
- Combo pricing is calculated on the storefront; Zoho receives individual SKU lines, not a combo SKU.
- Additional Admin capabilities are opportunities for business growth, not conflicts merely because they are absent from the current Django implementation.

## 7. Remaining items that are not business conflicts

These items require evidence or implementation planning, not another business-intent questionnaire:

1. Verify Zoho change-triggered sync, hourly reconciliation, retry/idempotency, stale-data visibility and alert thresholds.
2. Retrieve the previously documented HSN code and confirm the source of product GST classification.
3. Inspect existing Zoho/Shiprocket mapping and dimension fields; avoid duplicate data ownership.
4. Verify Razorpay domain/account approval and capture configuration before live use.
5. Verify actual Zoho/Shiprocket/provider connectivity; comparison currently records simulated/mocked outcomes.
6. Confirm the precise Director-approval mechanism and audit schema during implementation design.
7. Inspect ORD-145's menu read-only if its contents could add a unique capability.
8. Prioritise and sequence accepted capabilities into controlled implementation phases; the YES answers do not imply all features should be built at once.

## 8. Decision on whether any genuine conflicts remain

Using HU's test—**“Can these decisions coexist?”**—the current evidence does not identify a remaining business contradiction that requires HU to choose between two otherwise desired capabilities.

Where an exact Shopify feature would violate an explicit EffyKlean rule, preserve the rule and adapt or exclude only the incompatible behaviour:
- Do not enable customer self-service returns/refunds.
- Do not let Shopify taxonomy determine GST.
- Do not enable COD.
- Do not let storefront Admin independently change Zoho stock.
- Do not replace the existing Zoho Flow without inspection and HU+DI review.
- Do not dispatch without verified payment under the current rule.

These are design boundaries, not reasons to discard adjacent Admin capabilities. If later evidence exposes a truly irreconcilable pair of explicit decisions, record the exact source IDs, the two statements, why they cannot coexist, and the smallest decision needed from HU. Do not manufacture a conflict to keep a review checklist populated.

## 9. Recommended next step

Use this reconciliation record to update the decision ledger, correcting the false-conflict backlog and preserving the original YES/NO intent. Then produce an implementation-planning view with:
- capability/source IDs;
- business purpose;
- current implementation status;
- dependencies/provider evidence;
- security/audit guardrails;
- priority/phase;
- explicit implementation authorisation state.

This analysis is not implementation authorisation. It is the reconciled statement of desired business capability and the rules those capabilities must respect.
