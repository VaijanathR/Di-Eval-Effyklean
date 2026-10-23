# HU+DI genuine decision shortlist — 23 October 2026

Purpose: replace repeated questions from the generated 22-Oct prompt with a small, evidence-led decision queue. This is a recommendation list, not authority to implement deferred work. Prior YES/NO answers remain binding; implementation status and current scope disposition are separate.

## Decision queue

1. **Product lifecycle — MA-PRD-052/053/083/091 (DC-10).**
   - Existing answer: original YES scope answers stand; exact lifecycle model was deferred by the frozen spec.
   - Di recommendation: use the smallest safe model: Draft, Active, Unlisted (direct-link only), Archived; do not add a separate Suspended state unless a specific operational need is evidenced. Archive/unlist must preserve order/history, block new sales as defined, and require authorised staff action. Bulk archive/unlist only after individual lifecycle behavior is verified.
   - **HU approval (23-Oct-2026): APPROVED.** Adopt the four-state model: Draft, Active, Unlisted (direct-link only), Archived. No Suspended state unless a concrete operational need is evidenced. Authorised staff action required; preserve order/history; scheduled publication must not bypass authorisation. This records the policy decision only; it does not authorise implementation.

2. **Gift cards — MA-GFT-001/002, MA-SET-032.**
   - Di recommendation: keep excluded/deferred until a written policy covers issuance, redemption, expiry, partial redemption, refunds, fraud controls and liability/accounting. No implementation before policy approval.
   - **HU decision (23-Oct-2026): AGREED with Di.** Exclude gift cards from current scope and leave them deferred for possible future reconsideration. No implementation unless HU+DI reopens the decision and accountant-approved terms are available.

3. **Customer/order-history deletion, anonymisation and merging — MA-CUS-009/020/050.**
   - **HU decision (23-Oct-2026): DELETION = YES for implementation; ANONYMISATION = NO for implementation.** Deletion is a GO for authenticated users with the Admin or Director role only. Customers and other staff must not have this capability.
   - **Customer-record merging remains unapproved/out of scope** unless Hu explicitly approves it separately.
   - Implementation guardrails for deletion: define exactly which customer/order data is deleted; preserve required tax/accounting records, active-order integrity and audit evidence; log privileged actions. Where a record cannot safely or lawfully be erased, specify the permitted outcome rather than silently deleting linked records. Treat contact-form MF-089's 180-day retention separately.
   - This is scope approval only; it does not authorise coding-agent delegation, implementation, or live deletion without the applicable explicit authorisation.

4. **Tax-exemption controls — MA-CUS-014/045.**
   - **HU decision (23-Oct-2026): APPROVED for implementation.** Only authenticated Admin or Director users may manage tax-exemption controls; the business rule is that these roles are responsible for applying the applicable tax rules.
   - Implementation must still enforce role-based access, record who changed exemption status and when, and retain the evidence/reason captured for the decision where applicable. This approval does not authorise non-compliant exemptions or remove applicable legal/tax obligations.

5. **Marketing, channels, pixels and social/AI commerce — MA-MKT-001/002/003/004/007/013; MA-CHN-002/003/005/006/007/008; MA-SET-072; MA-PRD-096.**
   - **HU decision (23-Oct-2026): KEEP THESE AS FEATURES.** Marketing/channel capabilities remain features in the product scope/roadmap, not blanket exclusions. WhatsApp marketing is handled through Meta; it is not to be operated directly from EffyKlean's Admin page. EffyKlean may provide integration configuration and API-key/credential settings for supported integrations.
   - Integration settings must be access-controlled and secrets must not be exposed in the Admin UI, logs or ordinary responses. A configured integration does not itself authorise campaigns, tracking pixels, social login, marketplaces, AI-commerce, customer-data sharing or consent changes; review the specific provider/use case, data flow, consent, wording, ownership and ongoing cost before enabling it.
   - This records scope direction only; it does not authorise implementation, new provider connections, live credentials, campaigns or tracking. Existing transactional WhatsApp notifications remain distinct from marketing.

6. **Analytics and customer segmentation — MA-ANA-011/022/017/027/018/020; MA-ANA-012/013/021/024/026; MA-CNT-042.**
   - Di recommendation: keep tracking-dependent analytics gated by MF-093 privacy/consent/retention approval. Prefer essential operational reports first; do not add pixels or behavioural tracking to reproduce Shopify dashboards.
   - HU+DI decision needed only for a named report/custom-builder or segment-threshold that is not already answered.

7. **Discount edge cases — MA-DSC-011/012/026.**
   - Existing rule: first qualifying combo item receives no discount; later qualifying items receive the discount; if the first item is removed, the next becomes first.
   - Di recommendation: preserve this rule; do not introduce customer-specific one-use limits or segment eligibility without a concrete need. Resolve coupon precedence only if coupon support is actually in scope.
   - HU+DI decision needed only if a concrete campaign requires these extra rules.

8. **Public quantity price breaks / subscriptions — MA-PRD-071/070.**
   - Di recommendation: keep public price breaks out until separately approved; distributor slabs are not public price breaks. Keep subscriptions out until Zoho Payments recurring-charge capability is verified and separate charging/cancellation policy is approved.
   - Next action: capability verification and commercial proposal; no implementation from sandbox success alone.

9. **EffyKlean-specific content/forms/search/chat/package features — MA-CNT-008/015/016/019/020; MA-PRD-105.**
   - Di recommendation: do not reproduce Shopify theme builders, generic form builders or Tidio by default. Retain the existing contact form and current storefront search unless a concrete unmet user journey is documented. Keep package/shipping ownership with the approved Zoho/Shiprocket flow.
   - HU+DI decision needed only against a specific documented use case.

10. **Safe Admin-editable settings — MA-SET-001/003/011/013 and related settings rows.**
    - Di recommendation: allow only clearly safe business content (e.g. contact details and brand assets) through audited Admin controls. Keep payment, checkout/GST rules, taxes, locations, shipping authority, domains/DNS and Zoho-owned data outside ordinary editable settings; domains/DNS are restricted operations.
    - HU+DI decision needed only for the precise field list after the safe/frozen/externally-owned split is prepared.

## Not HU decision questions

These are execution or evidence gates, not new business decisions: targeted read-only Zoho Flow/app inspection; inventory-by-location and purchase/received-quantity reads; Zoho invoice automation/contact mapping verification; dev-catalogue recheck; SMTP/provider setup and notification wording; Merchant Center feed validation; Spaces provisioning; secrets-manager choice at the hosting/security gate; responsive/accessibility browser recheck; and release acceptance after dependencies. Perform them only at their recorded gate and with the existing authorisation limits.

## Explicitly not reopened

- MA-ORD-103 and MA-ORD-105: prior NO; current disposition corrected to EXCLUDE, implementation status remains DEFERRED.
- MA-INV-003/004/005 and MA-PRD-104: prior scope/Zoho ownership answer; do not ask again or create a competing local inventory authority.
- Zoho Payments sandbox and Zoho Inventory/Shiprocket sandbox integration: treat as working per Hu's recorded update; do not revive stale blocked assumptions.
- Frozen rules remain: no COD, no partial payment, no alternate payment gateway fallback, no dispatch before full verified payment; Zoho owns invoicing and the existing Zoho-managed Shiprocket workflow remains intentional.
- One saved address, three-month retention and active-order protection remain the recorded customer-address scope; multiple addresses stay parked.
- English-only until verified translations are supplied; no SMS; email/WhatsApp preference does not authorise marketing campaigns.
- GST-inclusive pricing; GST invoice only when both GST Number and Name validate; otherwise consumer invoice. No returns/refunds baseline. Combo pricing rule above remains unchanged.

## Source / limits

Reconciled against the 151-item decision/action report, the 245-row BUILD ledger, the 23-Oct reconciliation overlay, the canonical 122-capability decision master and the 18-Oct 597-row snapshot. The 22-Oct working 597 CSV is zero-byte in GitHub, so current corrections are recorded in a separate overlay; the historical snapshot is unchanged. The private/local application repository was not available for fresh source-code verification in this pass. No production/provider writes, deployment or coding-agent delegation occurred.
