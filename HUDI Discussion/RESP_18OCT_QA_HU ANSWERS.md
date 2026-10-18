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


## Batch 2 — Items 11–20

### 11. Backup and recovery retention
**HU selection:** Yes — defer exact retention periods; keep backup capability.
**Direction:** Keep backup/restore capability and the existing recovery-drill evidence. Do not block implementation on an arbitrary retention number. Propose practical retention periods later with recovery objectives and cost implications. **Status:** Direction recorded; exact periods deferred.

### 12. Frozen acceptance criteria and the 590+ task inventory
**HU selection:** Need more information.
**HU note:** “I need more information on this. what is 139 AC frozen baseline? i want all the 590+ tasks mapped and implemented. provide more information and ask this question again with proper data for me to take a call”
**Direction:** Do not treat this as an accepted reduction in scope, and do not treat a passing test suite as proof that all 590+ tasks are mapped or implemented. HU wants the full 590+ task inventory mapped and implemented, and needs a data-backed explanation before deciding the acceptance-criteria approach. The “139 AC frozen baseline” means the count of acceptance criteria in frozen SPEC v0.8 (commit `8601602`); it is not the total task count. The latest agent report separately says 100 criteria remain untagged, down from 122. These are different measures: acceptance criteria are testable requirements; implementation tasks are work items, and they need an explicit traceability mapping rather than being assumed equivalent. **Required follow-up:** Re-present this question only after assembling the actual inventory: source and count of all 590+ tasks; unique task IDs and status; mapping to the 139 frozen ACs, specification sections, architecture/ADRs, implementation commits and tests/evidence; tasks with no AC mapping and ACs with no task/evidence; duplicates, superseded tasks and genuine conflicts; what “implemented” means and what remains. Show counts and examples, not just a headline, then ask HU to decide the treatment of unmapped tasks. **Status:** Pending data-backed explanation and re-ask; no scope reduction approved.

### 13. Zoho OAuth scopes and credential rotation
**HU selection:** No — authorize all scopes listed in the report.
**HU note:** “DI dont be so conservative and suspicious as if the agent is trying to steal money. this sandbox environment. give the permissions to implement the tasks i want to be implemented.”
**Direction:** HU authorizes the listed Zoho scopes for the sandbox implementation/testing environment so the agent can implement the intended tasks. The listed scopes are: Zoho Inventory `items.UPDATE`, `contacts.UPDATE`, `invoices.READ`, `customerpayments.READ`, `inventoryadjustments.CREATE`, `packages.READ`, `shipmentorders.READ`; and Zoho Payments settings create/read/update scopes as specified in the agent report. Apply this authorization to sandbox credentials and sandbox organization only; this is not authorization to change production credentials, perform production writes, or expose secrets. Credential rotation should be coordinated to avoid unnecessarily breaking the working sandbox. **Status:** Sandbox scope authorization recorded; agent must use the exact scope strings supported by the Zoho app/API.

### 14. Temporary webhook URL and scheduler
**HU selection:** No selection submitted; interim direction supplied in HU note.
**HU note:** “i have already told the agent that i will keep update the webhook if required till we come to a concrete plan on endpoint. use the current temporary setup till we complete testing and development.”
**Direction:** Continue using the current temporary webhook/tunnel arrangement for development and sandbox testing. HU will update the webhook URL as needed while the team works toward a concrete endpoint plan. Keep temporary URL/tunnel secrets out of committed configuration. This does not approve production deployment or make the temporary URL the permanent go-live endpoint. Scheduler/production hosting decision remains open until the concrete plan is ready. **Status:** Interim testing direction recorded; long-term endpoint/hosting/scheduler plan pending.

### 15. Shopify / effyklean.com data preservation and eventual redirect
**HU selection:** No selection submitted; substantive direction supplied in HU note.
**HU note:** “collect all the details you want from shopify and effyklean.com and save it to our effyklean project. for all the redirect or integrations not the functionality and setup and keep it. I can keep the shopify account active as long as i want. and once the effyklean.in the current project is live i will redirect effyklean.com to effyklean.in. is my answer clear? you dont have to close shopiffy, you just take all those data content and links and integrations and save to our project.”
**Direction:** Do not close or deactivate Shopify. Collect and preserve the relevant Shopify and effyklean.com content, product/catalogue data, URL/link inventory, redirect information, integration details and configuration/operating notes in the EffyKlean project so that needed content and integrations can be retained or deliberately recreated. Preserve the current functionality/setup; do not assume that the new site should discard an integration just because it is Shopify-related. When effyklean.in is live, HU intends to redirect effyklean.com to effyklean.in. Gather/export evidence first; do not change domain/DNS, close the store, or alter live integrations as part of this collection task. **Status:** Direction recorded; data collection and preservation required; eventual redirect is a future HU-directed action.

### 16. Shiprocket and Zoho dispatch workflow
**HU selection:** No selection submitted; explicit deferral supplied in HU note.
**HU note:** “WHY? why do you want to check what zoho does with shiprocket? i told you so many times that its zoho functionality. leave it for later time for testing.”
**Direction:** Leave the current Zoho-managed Shiprocket behavior alone for now. Defer Shiprocket sandbox testing and any trigger/workflow investigation to a later testing phase. Do not redesign or duplicate Zoho dispatch functionality. HU has already stated second-day dispatch and customer delay notifications are managed through Zoho. **Status:** Deferred; not a current decision blocker.

### 17. Outbox tasks marked done for stub orders
**HU selection:** Need more information.
**HU note:** “what is this - we are replacing stubs with sandbox links. if sandbox link is there then disable stubs if not keep them. why is this a rocket science question?”
**Direction:** HU's intended replacement rule is: where a working sandbox integration/link is available, disable the corresponding stub; where it is not available, retain the stub. Do not interpret a stub task marked “done” as proof of a real sandbox sync. Before asking again, provide a short evidence-based list of the five affected outbox tasks: test order/correlation marker, task type, what “done” currently means in code/data, whether a real sandbox call occurred, whether a working sandbox path exists, and the proposed action (disable stub or retain). Keep the check narrow. **Status:** General direction recorded; specific five-task interpretation awaits concrete evidence, then re-ask only if a real choice remains.

### 18. Distributor and Bulk customer functionality
**HU selection:** No selection submitted; HU note supplied.
**HU note:** “why is this a question? I WILL DELETE A DISTRIBUTOR OR A BULK CUSTOMER. I WANT THAT FUNCTIONALITY NO QUESTIONS ASKED”
**Direction:** Record HU's requirement that authorized Admin functionality must allow deletion of a Distributor or Bulk customer record without unnecessary business-decision escalation. Do not silently equate customer-record deletion with whether a Distributor/Bulk customer may cancel an order: those are different operations. Preserve the explicit deletion requirement; before implementation, check the frozen spec and data-integrity protections so deletion does not cascade into orders, payments or audit records contrary to existing safeguards. If a separate order-cancellation behavior genuinely remains ambiguous, bring concrete current-vs-spec evidence rather than repeating the prior broad question. **Status:** Customer deletion requirement recorded; implementation details must preserve related business records and frozen safeguards.

### 19. Director/Admin and Marketing role
**HU selection:** No selection submitted; substantive direction supplied in HU note.
**HU note:** “what is this? what role removal? the director and admin will have marketing function. dont need a new marketing role if it has to be developed”
**Direction:** Director and Admin should have the Marketing function; do not create a separate Marketing role merely to provide that function. The earlier question conflated this with a separate role-removal/permission conflict. Before raising it again, identify the exact existing role-removal operation, frozen-spec clause and later rule that supposedly conflict. Do not change permissions or role-removal behavior based on an unexplained abstract conflict. **Status:** Marketing access direction recorded; any distinct role-removal issue requires precise evidence before escalation.

### 20. Admin low-stock view and invoice details
**HU selection:** No selection submitted; HU note supplied.
**HU note:** “why are you guys so much into other peoples business that is zoho functionality let zoho take care of it. what is inthe storefront that is troubling you?”
**Direction:** Low-stock management and invoice status/details belong to Zoho's operational functionality. Do not add a parallel storefront/Admin implementation merely because Zoho exposes those functions. Only consider a storefront feature if a frozen acceptance criterion explicitly requires it or evidence shows it is necessary for the website's own safe order flow; if so, present the exact criterion and affected screen before asking HU. **Status:** Defer; no additional storefront feature authorized.

## Batch 2 summary
- Directions recorded: 11, 13, 14 (interim testing setup), 15 (Shopify data preservation and future redirect), 16 (defer Shiprocket testing), 17 (stub replacement rule), 18 (Distributor/Bulk customer deletion requirement), 19 (Director/Admin Marketing function), 20 (Zoho owns low-stock/invoice operations).
- Needs a data-backed explanation and a new decision question: 12, including full mapping of the 590+ task inventory.
- Needs a narrow evidence package before any re-ask: 17 (five outbox tasks) and any distinct role-removal conflict in 19.
- No agent instructions issued. This document remains a decision register, not an execution prompt.


## HU clarification update — Batch 2 corrections (approved by HU)

HU approved the following corrected wording on 2026-10-18. These corrections supersede any inconsistent summary language in Batch 2 items 12, 15, and 20 above. Preserve the earlier entries as history; apply the following as the current direction.

### 12. Implementation plan, 597 activities, and clarification audit — corrected

**HU clarification:** The 590+ activities were already part of the implementation plan. The earlier assessment identified 597 activities (103 cross-cutting/platform and 494 Shopify Admin), 71 locally actionable tasks, and a proposed first batch of 55. A separate audit identified 122 rows requiring classification or clarification. HU wants the planned activities accounted for and implemented—not a new scope exercise that treats the 139 frozen acceptance criteria as the entire task inventory.

**Direction:** Continue from the existing implementation plan and preserve its task IDs, grouping, dependencies, priorities, and evidence. Do not rerun the assessment or recreate the inventory unnecessarily.

Reconcile the existing records and report:
- The status of all 597 planned activities, with original IDs preserved.
- Which are implemented, partially implemented, not started, blocked, superseded, duplicated, or awaiting a specific decision, with evidence where available.
- The disposition of each of the 122 audit rows: already answered by HU, resolvable from an established rule or existing evidence, or genuinely missing a decision.
- Which activities map to the 139 frozen acceptance criteria, and which are platform, operational, integration, or other tasks that require separate traceability.
- The exact remaining work and genuine blockers, without presenting already-settled questions as unresolved.

Ask HU only about decisions that remain genuinely unresolved after this reconciliation, with the relevant evidence and specific choices. Do not infer that all 122 rows require HU input, and do not reduce the planned implementation scope to the acceptance-criteria count.

**Status:** Existing plan is the baseline. Reconciliation against current implementation evidence is required; no scope reduction is approved.

### 15. Shopify and effyklean.com project knowledge and functionality — corrected

**HU clarification:** The requirement is that everything relevant from Shopify and effyklean.com be available within the EffyKlean project for use. The concern is not whether HU keeps or closes a Shopify account.

**Direction:** Collect and preserve the relevant existing site content, catalogue/product information, page and URL inventory, configuration, integrations, workflows, and other implementation-relevant details from Shopify and effyklean.com in the EffyKlean project. Keep the source information and evidence organized so it can be used to build, validate, and operate the new project. Do not assume an existing integration or configuration should be discarded merely because the new storefront is being built independently.

The intended future state is for effyklean.in to provide the storefront functionality represented by Shopify and effyklean.com, with the required existing integrations connected to EffyKlean Admin and effyklean.in as they previously operated with Shopify Admin/settings and effyklean.com. Any eventual domain redirection is a separate transition activity.

**Status:** Project knowledge and functionality preservation are required. Collect and document the source details; do not make live domain, account, or integration changes as part of the collection work.

### 20. Storefront scope versus Zoho and other integrations — corrected

**HU clarification:** Do not build Zoho functionality into the storefront. The storefront should implement the functionality that exists on Shopify and effyklean.com—no additional Zoho operational features or parallel implementations.

**Direction:** Treat Shopify and effyklean.com as the functional reference for the storefront scope. Reproduce the relevant existing customer-facing and site functionality in effyklean.in. Keep integrations working with EffyKlean Admin and effyklean.in in the corresponding way they previously worked with Shopify Admin/settings and effyklean.com.

Zoho remains responsible for its own operational functionality, including stock/inventory operations, invoicing, GST handling, and its existing connected workflows. Do not add parallel storefront/Admin features for those functions merely because Zoho provides them. Implement only the integration interfaces and website behavior needed to preserve the intended end-to-end operation.

**Status:** Scope boundary recorded. Any proposed feature outside the existing Shopify/effyklean.com storefront functionality must be supported by a specific frozen requirement and reviewed before inclusion.

## Current HU decision status after approved corrections

- Items 1–11: directions/answers recorded as described in Batch 1 and Batch 2.
- Item 12: the plan is not awaiting a broad HU scope decision. Reconcile the 597-task plan and the 122-row clarification audit against actual evidence, then ask only genuinely unresolved questions.
- Item 13: listed Zoho scopes authorized for sandbox implementation/testing only; no production authorization.
- Item 14: current temporary webhook/tunnel may be used for development/testing; permanent endpoint/hosting plan remains pending.
- Item 15: collect and preserve Shopify and effyklean.com project knowledge; no account-closure decision is requested.
- Item 16: Shiprocket sandbox/trigger testing deferred to a later testing phase.
- Item 17: use a working sandbox integration where available; otherwise retain the stub. Present evidence for the five outbox tasks before asking any remaining narrow question.
- Item 18: authorized Admin customer-record deletion for Distributor/Bulk customers is a requirement; preserve related orders/payments/audit records and distinguish customer deletion from order cancellation.
- Item 19: Director and Admin have the Marketing function; do not create a separate Marketing role. Any distinct role-removal conflict must be supported by exact spec and implementation evidence before escalation.
- Item 20: storefront scope is the functionality represented by Shopify and effyklean.com. Do not implement parallel Zoho operational functionality.
- No coding-agent execution prompt has been issued. This register remains separate from any future implementation prompt.
