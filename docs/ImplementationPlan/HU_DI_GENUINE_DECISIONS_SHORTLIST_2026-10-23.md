# HU+DI genuine decision shortlist — 23 October 2026

Purpose: replace repeated questions from the generated 22-Oct prompt with a small, evidence-led decision queue. This is a recommendation list, not authority to implement deferred work. Prior YES/NO answers remain binding; implementation status and current scope disposition are separate.

## Decision queue

1. **Product lifecycle — MA-PRD-052/053/083/091 (DC-10).**
   - Existing answer: original YES scope answers stand; exact lifecycle model was deferred by the frozen spec.
   - Di recommendation: use the smallest safe model: Draft, Active, Unlisted (direct-link only), Archived; do not add a separate Suspended state unless a specific operational need is evidenced. Archive/unlist must preserve order/history, block new sales as defined, and require authorised staff action. Bulk archive/unlist only after individual lifecycle behavior is verified.
   - **HU approval (23-Oct-2026): APPROVED.** Adopt the four-state model: Draft, Active, Unlisted (direct-link only), Archived. No Suspended state unless a concrete operational need is evidenced. Authorised staff action required; preserve order/history; scheduled time never publishes automatically; publication occurs only after required approval is complete and an authorised Admin or Director manually publishes. If approval is incomplete or they forget, the product remains unpublished. This records the policy decision only; it does not authorise implementation.

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
   - **HU correction (23-Oct-2026): IMPLEMENT THESE AS IN-SCOPE FEATURES, NOT FUTURE FEATURES.** Marketing and channel capabilities are intended to be implemented as part of the product scope. WhatsApp marketing is handled through Meta, not directly through EffyKlean's Admin page. EffyKlean should provide integration configuration and API-key/credential settings for supported integrations.
   - Integration settings must be access-controlled and secrets must not be exposed in the Admin UI, logs or ordinary responses. Implement the required supported integration capabilities while respecting each provider's data flow, consent requirements, customer-data sharing limits, wording, ownership and ongoing cost. Do not assume every possible provider, pixel, social login, marketplace or AI-commerce integration is included without mapping it to the approved implementation requirements.
   - This corrects the roadmap disposition: these are implementation-scope features, not merely future possibilities. It does not by itself authorise a live provider connection, live credentials, campaign launch or tracking that requires separate operational/privacy approval. Existing transactional WhatsApp notifications remain distinct from WhatsApp marketing.

6. **Analytics and customer segmentation — MA-ANA-011/022/017/027/018/020; MA-ANA-012/013/021/024/026; MA-CNT-042; MF-093.**
   - **Resolved from prior HU decisions and frozen requirements; no new HU question.** AD-15 reporting/analytics is approved with the condition that operational reports use authoritative PostgreSQL/application data. The customer/segment/B2B capabilities in the previously approved CUS groups (CUS-001–033, 040–045, 050–056) remain YES scope decisions; segmentation includes filter-based selection, counts, marketing use, a natural-language builder, actions and CSV import. Do not ask HU to approve these again.
   - Implement the essential operational reports from authoritative data, including orders, sales, payments, fulfilment, inventory exceptions, distributor/bulk activity, replacements and integration failures. Honour SPEC-required reporting, including bulk-customer cumulative savings. Do not make Zoho-owned inventory/shipping data locally authoritative.
   - **MF-093 remains LATER:** optional session/visitor/conversion/behaviour analytics and tracking-dependent marketing events stay disabled until the applicable consent, privacy notice, retention and access controls are approved and implemented. No pixels or behavioural tracking merely to reproduce Shopify dashboards. This is a dependency/evidence gate, not a new scope question.
   - Report export/custom report builder details should follow the approved capability requirements and be verified against the canonical records; do not invent extra scheduling, report-library or segment-threshold behaviour where it is not specified.

7. **Discount edge cases — MA-DSC-011/012/026.**
   - Existing combo rules remain unchanged: the first qualifying combo item receives no combo discount; later qualifying items receive it; if the first item is removed, the next becomes first. Combo rules are evaluated oldest-created first, and qualifying quantities cannot be reused.
   - **HU decision (23-Oct-2026): APPROVED for implementation scope.** Coupon/promotion capability must support an optional one-use-per-customer limit and optional eligibility restrictions, including all customers, new customers, or specific customers/approved segments, so campaigns such as a generic festive coupon can control repeated redemption and audience eligibility.
   - These controls are configurable per promotion/coupon, not mandatory for every offer. Preserve the existing discount precedence: B2C may use a combo discount OR a valid company promotion/coupon, not both; only one additional discount may apply to a sale price. Distributor pricing remains product-specific with optional quantity discounts and no combo offers.
   - This records scope/business rules only; it does not by itself authorise coding-agent delegation, implementation, live campaign launch or marketing sends. Apply the applicable consent and campaign-approval requirements.

8. **Public quantity price breaks / updates subscription — MA-PRD-071/070.**
   - **HU decision (23-Oct-2026): APPROVED.** Public product quantity price breaks are in scope (consistent with the prior YES recorded for MA-PRD-071). A quantity-based selling-price tier is a defined price for the qualifying quantity, not an extra discount stacked on top of a combo offer, coupon/promotion or another discount. Preserve the approved discount precedence and no-stacking rules. Distributor quantity slabs remain separate from public price breaks.
   - **HU clarification (23-Oct-2026): “Subscribe” means subscribing to EffyKlean updates/communications, not a recurring product order or recurring payment.** Do not gate the updates-subscription feature on Zoho Payments recurring-charge capability or product-subscription charging/cancellation policies.
   - Implement the updates-subscription capability according to the approved requirements, including applicable consent, communication preferences and unsubscribe handling. A subscription to updates does not by itself grant consent to every marketing channel or campaign.
   - MA-PRD-070 product selling plans/recurring product subscriptions remain separate from updates subscriptions; do not infer approval for recurring product orders or charges.

9. **EffyKlean-specific content/forms/search/chat/package features — MA-CNT-008/015/016/019/020; MA-PRD-105.**
   - **Prior scope answers must stand:** the 23-Oct reconciled decision ledger records YES for MA-CNT-008, MA-CNT-015, MA-CNT-016, MA-CNT-019, MA-CNT-020 and MA-PRD-105. Hu explicitly answered YES for site preferences, storefront search settings/filters, forms builder and customer-facing chat/chatbot on 12-Oct. Do not ask those scope questions again or silently turn them into EXCLUDE. Note: the older canonical master labels some of these Shopify comparison entries EXC/MISS, so the newer HU decision ledger is the scope-decision evidence; it does not supply all detailed acceptance criteria.
   - Scope does **not** mean cloning Shopify theme-builder mechanics or selecting Tidio automatically. Keep the existing contact, distributor and bulk enquiry flows intact; any general forms-builder work must preserve the contact form's MF-089 fail-closed/privacy requirements. For search, implement only grounded EffyKlean catalogue filters/settings; do not invent search-ranking behavior. Site-level title/meta/social-image preferences need a defined field model. Customer chat provider, escalation, hours, consent, data handling and any promises need explicit provider/use-case detail before connection or launch. Blog-comments scope needs moderation/privacy requirements before public comments are enabled.
   - **Package/shipping boundary:** although MA-PRD-105 is marked YES in the newer ledger, it does not override the earlier LATER decision for package weights/dimensions (MA-PRD-036/037, DC-19) or authorise a competing carrier/shipping workflow. Zoho/Shiprocket remains the approved shipping flow. Resolve any package-data UI only within that boundary and do not create local shipping authority.
   - This section records scope and remaining specification gates only; it does not authorise implementation, live third-party connections, provider credentials or launch.

10. **Safe Admin-editable settings — MA-SET-001/003/011/013 and related settings rows.**
    - **HU approval (23-Oct-2026): APPROVED as the baseline split.** Allow safe business content such as store contact details and brand assets through audited Admin controls, while protecting canonical business identity and support details from unauthorised changes.
    - Keep payment, checkout/GST and tax rules, checkout requirements, shipping rates/authority, Zoho-owned locations/data and domains/DNS out of ordinary editable settings. Domains/DNS remain restricted operations. Do not create a competing local authority for Zoho-owned data.
    - Customer-account settings must preserve approved account/access rules. Do not enable self-service returns or store credit under this approval; those conflict with the existing business decisions. Any additional editable field must be proposed individually for HU+DI approval before implementation.
    - This is a scope/ownership decision only; it does not authorise coding-agent delegation, implementation, deployment or live changes.


11. **Product/collection channel semantics — MA-PRD-012/093, MA-COL-008, MA-PRD-100.**
    - Reconciled without a new HU decision: do not introduce a separate Staff-availability setting. Preserve the approved Draft / Active / Unlisted / Archived lifecycle and existing publication, catalogue and Zoho-mapping safeguards. Active does not mean a product must be hidden from the public website; Unlisted is the existing state for a product intentionally not publicly listed.
    - Staff-entered orders continue to use the approved assisted-order workflow, including catalogue/pricing safeguards and verified full payment before order creation/dispatch. Do not invent additional channel switches or POS-terminal behaviour. Any concrete conflict with frozen requirements must be reported for HU+DI decision rather than solved by adding functionality.

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
