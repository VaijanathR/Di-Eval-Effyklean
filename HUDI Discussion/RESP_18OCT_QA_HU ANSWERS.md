# EffyKlean — HU Answers to QA / Decision Questions

Persistent register of HU's answers to Di's batched questions. Update this same file after every batch submission. This is a decision record, not an agent execution prompt. No deployment, publication, push, paid provisioning, production changes, or destructive actions are authorized unless explicitly stated.

## Batch 1 — Items 1–10

### 1. Dispatch timing and Zoho / Shiprocket
**HU:** “Second day dispatch is a NORM. This is always taken care in zoho - you dont have to enforce anything. sometimes if the dispatch gets delayed for whats so ever reason the customer is notified from zoho. ( zoho has integrations with whatsapp and email which takes care of this)” 

**Direction:** Treat second-day dispatch as the normal operating rule managed by the existing Zoho workflow, including customer notifications through Zoho WhatsApp/email. Do not duplicate dispatch enforcement without a demonstrated need. A possible same-day Shiprocket trigger is only a narrow factual question about whether Zoho behaves as HU describes, not approval to redesign the workflow. **Status:** Direction recorded; limited verification may remain.

### 2. Product dilution instructions
**HU:** “any product that says makes 1 liter, needs dilution with apprximatley 1 liter of dimeneralized water, any product that says makes 5 liter, needs dilution with approximately 5 liter of dimineralized water. why is there a confusion about this? for example if a cocentrate is 30 ml it will may make 1 liter and the same product with 100 ml may make 5 liter.”

**Direction:** A product labelled as making approximately 1 litre is diluted with approximately 1 litre of demineralized water; a product labelled as making approximately 5 litres is diluted with approximately 5 litres. Concentrate quantity varies by product/pack size (e.g. 30 ml versus 100 ml). Reconcile contradictory fields on specific SKUs; do not ask HU to restate this general rule or invent SKU-specific directions. **Status:** General rule recorded; SKU conflicts require reconciliation.

### 3. Fifteen SEO drafts
**HU selection:** Yes — retain drafts for review.
**Direction:** Keep all 15 SEO revisions unpublished. No publication authorized. **Status:** Recorded.

### 4. Tools Required tables
**HU selection:** Yes — verify before updating.
**HU note:** “I need to see this visually where is this?”
**Direction:** Show visual evidence of where the Tools Required section appears on the two floor-cleaner product pages and/or Admin screens, identifying the section. Do not ask HU to approve unseen content or invent tool requirements. **Status:** Awaiting visual evidence.

### 5. Weights, dimensions, barcodes and prices
**HU selection:** No — I will provide confirmed values.
**HU note:** “Dont worry about this. these will be set by the admin for all the product in the real world. currently stop bothering about this. just keep the functionality as observed in Shopify, we will take care of adding the wt and dimensions manually for each product later”
**Direction:** Preserve functionality as observed in Shopify. Admin will enter real-world values later. Do not repeatedly raise missing values as current implementation blockers and do not invent values. **Status:** Direction recorded; later Admin data-entry task.

### 6. HSN and new SKU fields
**HU selection:** No — I have approved values or a change request.
**HU note:** “I have said this so many times. THE HSN FOR EFFYKLEAN PRODUCTS IF FIXED. DONT WORRY ABOUT IT/ KEEP THE FIELDS and admin will add them. and make sure they the storefront and zoho has the same HSN mapping”
**Direction:** Keep HSN fields available for Admin entry and ensure storefront and Zoho use consistent HSN mapping. Do not reopen whether fields should exist. Do not guess or silently hard-code values. **Status:** Direction recorded; mapping consistency must be preserved.

### 7. GST and invoicing
**HU:** “why is this is problem? this is functionality in ZOHO. and wil be taken care of in zoho.”
**Direction:** Zoho owns GST and invoicing. Do not propose a separate EffyKlean invoicing engine. Sandbox evidence that some confirmed sales orders appeared unpaid/uninvoiced should be reconciled with the existing Zoho configuration; this is verification, not a request to redesign the process. **Status:** Operating model recorded; limited verification may remain.

### 8. Push three local commits
**HU selection:** Yes — inspect before pushing.
**Commits:** `02aeb80`, `7a13cf8`, `625e210`.
**Direction:** Inspect exact diffs and relevant validation before deciding whether to push. No immediate push authorized. **Status:** Awaiting evidence.

### 9. Spaces and media cleanup
**HU selection:** Yes — verify real migration before deletion.
**HU note:** “I told the agent that we will keep the folder as of now and once we have spaces we will upload the media there and later we will cleanup before going live”
**Direction:** Retain current media folders. After Spaces is available, upload and verify copies; clean up later before go-live only after references and copies are verified. No deletion authorized; this answer alone does not authorize paid provisioning. **Status:** Direction recorded.

### 10. Transactional email
**HU:** “i told the agent that zoho has its own email and whatsapp setup. i have the support@effyklean.com setup from go daddy. what else do you need, why cant the current email setup provided by godaddy can be used here? is this so difficult to understand?”
**Direction:** Start with existing GoDaddy `Support@EffyKlean.com` and Zoho email/WhatsApp setup. Do not assume a new provider is required or purchase/open another paid service without explicit approval. Only establish which system sends each type of website/transactional message and verify sending/authentication/delivery configuration. **Status:** Existing setup is the starting point; no new provider approved.

## Batch 1 summary
- Directions recorded: 3, 5, 6, 8, 9, 10.
- Operating model recorded; limited factual verification may remain: 1 and 7.
- General rule recorded; SKU-specific conflicts need reconciliation: 2.
- Visual evidence requested: 4.
- No agent instructions issued; HU requested decisions be discussed and recorded first.

## Update protocol
After every later HU batch submission, append the submitted answers, notes, clarifications, status changes, and pending evidence to this same document. Preserve history; do not silently overwrite earlier answers. Keep this register separate from any eventual coding-agent execution prompt.
