# Acceptance-criteria evidence pass (2026-10-18)

Scope: the 147 criteria of SPEC section 33 (the 139 frozen criteria plus later amendments). Regenerated index: `docs/foundation/AC_TEST_INDEX.md` (`python scripts/ac_index.py --check`).

**Result:** criteria with no test naming them fell from **100 to 21**; criteria named by a test function rose from 24 to **126**; criteria named only by a file header or comment fell from 23 to **0**. A criterion is tagged (`# Covers AC-x.y`) only where the test asserts what the criterion states. A tag records traceability; it is not formal acceptance of the criterion, and an area test is never taken as acceptance of every related requirement. Where a criterion has two halves and only one is tested, the tag was left off (AC-27.2, AC-20.1, AC-9.8, AC-10.8) or the gap is stated below.

## Work done
* **Tagged on existing tests** (no behaviour change): most of the 99 newly named criteria, including AC-1.2, 6.1 to 6.10 (6.7 new test), 7.1, 8.1, 8.3, 9.1 to 9.5, 10.1, 10.2, 10.5, 11.1, 11.4 to 11.6, 12.1 to 12.4, 12.10 to 12.15, 14.1, 14.2, 14.6, 14.7, 15.3, 16.1 to 16.9, 17.1 to 17.6, 18.4, 18.5, 18.6, 18.8, 19.1, 19.2, 20.3, 20.4, 21.4, 21.5, 22.2, 23.2, 23.3, 24.1, 28.1, 29.1.
* **New behaviour tests written:** AC-9.7 (replaced-rule link), 10.4, 10.6, 10.7, 10.9, 10.11, 10.12, 12.9, 13.3, 15.2, 18.7, 19.3, 20.2, 20.5, 22.1, 25.5; the Director deletion path (AC-9.6: a suspended role is removed first, then the record can be deleted).
* **New structural tests** (`tests/test_ac_structural_evidence.py`): AC-2.1, 5.1, 5.2, 7.3, 10.3, 13.5, 14.5, 21.6, 26.1 (secrets not tracked), 29.2, 29.3.
* **Two defects found and fixed while writing tests (both implemented, tested, local):**
  1. **AC-9.7**: a pricing rule did not record which rule it replaced. `DistributorDiscountRule.replaced_rule` added (migration `orders.0027`, **not applied** to `effyklean`).
  2. **AC-10.7**: the Bulk customer was never shown cumulative savings. Orders now record the MRP per line in the payment snapshot; the account page shows "Your savings so far: X against the Sale Price and Y against the MRP". Orders placed before this change have no MRP in their snapshot, so the MRP figure is withheld for an account that has such an order rather than guessed from today's MRP.

## The 21 criteria still without a naming test, each with its reason (all parked, none skipped for effort)
| Criteria | Why | Needed |
|---|---|---|
| 7.4, 9.8, 10.8 | Spec asks for GST-exclusive business prices and GST kept on the undiscounted price (₹100 + ₹18, discount ₹10, pay ₹108, GST ₹18). The settled rule (`modules/orders/tax.py`) extracts GST from the amount paid, and prices are tax-inclusive. A genuine spec-versus-decision conflict; also blocks Plan row D-06. | HU+DI: which rule governs; then amend one of them |
| 12.5, 12.6, 27.1, 27.2 (override half) | Bank-transfer/UPI verification and Admin-assisted orders are not built (DC-22, rows MF-064, MF-106) | HU+DI decision, then build |
| 12.7, 12.8, 15.1 | Worded for Razorpay settlement and charges; the provider is Zoho Payments (CR-007) and settlement data is not held | HU+DI restatement |
| 18.1 | Shipments are created and tracked by Shiprocket through Zoho (HU: complete); EffyKlean's own shipment path is a stub and it has no inbound delivery-status feed (register C-01, C-02). The Admin delivery column is tested, but the criterion is about Shiprocket itself | Shiprocket sandbox access / HU |
| 16.5 | The criterion asks for the refund through the original payment mechanism; HU decided no refund execution. EffyKlean records the refund, staff execute it in the provider dashboard | HU+DI: restate the criterion |
| 13.6, 13.7 | No local tax master and no guessing when Zoho tax data is unavailable: needs the GST decision above and a Zoho outage rule for business orders | HU+DI |
| 13.8 | The Admin order page does not show the Zoho GST invoice number or status: needs the `invoices.READ` scope on the Zoho token and working invoice automation in the sandbox org | HU (scope, Zoho Flow) |
| 20.1 | Mandatory email and phone at checkout is tested; "email is sent for transactional communication" is not built: no mail credentials | HU (credentials, wording) |
| 21.2, 21.3 | Rule-based combos (quantity rules) and fixed bundles are not built; the per-SKU amount model (SPEC 21.2A) is (DC-33) | HU+DI |
| 23.1 | "Not copied blindly" conflicts with HU's 2026-10-17 approval to copy effyklean.com content as is; needs a spec amendment | HU+DI |
| 26.2 | Checked: the events that exist are recorded. "Integration failures after retries" and "order exception/reconciliation states" are written to the integration log (exhausted outbox task, `ZOHO_SYNC_FAILED`, an open action-required item) and shown on the order timeline and reconciliation queue (`tests/test_outbox.py::test_transient_failure_retries_then_exhausts_after_three_total_attempts`), not in the Admin audit table. Bank-transfer/UPI verification and assisted-order events do not exist | with DC-22 |
| 26.3 | Privacy policy, terms and cookie consent stay unpublished until HU supplies approved legal text | HU |

## Defects found in the evidence, not fixed (parked above)
AC-7.4/9.8/10.8 (GST display) and AC-13.4 (consumer fallback) are the two places where the frozen acceptance criteria and the built behaviour disagree.

## Change to a customer-facing page made for AC-18.7 and AC-20.5
The Shipping and delivery page now says the delivery partner sends the delivery messages and makes the call before each attempt, and that anything needing EffyKlean's help goes to Customer Care (phone and e-mail from the canonical details). Wording follows SPEC 23.5 (no courier terms); test in `tests/test_storefront_policies.py`. HU may wish to review the sentence.

## Row-by-row review of the 228 "implemented" rows (final pass)
Every mapped test was opened and read against its row. Outcomes (details in `RECONCILED_597_STATUS_2026-10-18.csv`, column `basis_2026_10_18`):
* **Re-mapped** where the first match was wrong or loose: MF-058, MF-061, MF-111, MA-ORD-031, MA-ORD-042, MA-ORD-043, MA-CUS-032, MA-CHN-001 and others.
* **Defects and gaps found and fixed:** the Admin order page still said settlement data is "not fetched from Razorpay" (now Zoho Payments, tested); MA-PRD-015 had no product count summary (built and tested; one extra query, the list's query budget is now 28); reports "Orders by status" and "Payment attempts" had no test (added); the Admin payment reference had no test (added).
* **Reclassified:** MA-PRD-029 (charge-tax flag) is Zoho-owned, not built.
* **Marked partial with the exact missing part** (status text starts "partial - named tests"): MA-ORD-014, 020, 023, 084, 104, 107, 131, 132, 137, 142; MA-PRD-024, 072, 098, 100; MA-CUS-012; MA-DSC-014, 040; MA-CNT-040; MA-ANA-018; MA-INT-006; MA-USR-020, 032; MA-SYS-012.

## Update 2026-10-19 (after the completion audit)
* **AC-13.4 built and tested** (mock transport): when Zoho rejects a Sales Order carrying GST details, the adapter retries once as a consumer order, the order logs "Zoho did not accept the GST details…", and any rejection without GST details or a second rejection still fails. The real Zoho rejection response has never been observed; the fallback treats any non-auth, non-rate-limit 4xx as a rejection and a retry that also fails is a real failure.
* **AC-9.2, 10.11, 10.12:** weak tags replaced by purpose-written tests (rejected, information-requested and new applicants get no business account or price; a normal Bulk order needs no approval and a Director rejection is audited with a reason; a replacement quote prices nothing until approved and accepted).
* **AC-16.5 untagged:** the criterion asks for the refund through the original payment mechanism; HU's decision is no refund execution (ORD-074/075/076/144, SET-013 excluded; `tests/test_refund_guard.py`). EffyKlean computes and records the refund; staff execute it in the provider dashboard. Parked as a spec-versus-decision conflict.
* **Left as they are, with the limit stated:** AC-12.9 (a design property: one writer; no real feed), AC-6.1/6.2/14.1 (structural), AC-18.5 (the tracking page, not a notification).
* **PIN table:** sampled against India Post's public data (95 PINs, read-only): two real gaps found and fixed (Yanam 533464, Diu 362520), the rest matched (three name-spelling differences only). Not an exhaustive check; the city is still not verified.

## Audit follow-up pass (2026-10-19 05:18 IST): results item by item
| Item | Result |
|---|---|
| A1 ORD-131 stats strip | Already built (orders, items, payable value, fulfilled, delivered); the earlier "partial" was a test gap. Test added. Reversals are omitted by decision; order-to-fulfilment time is blocked on real Shiprocket data (DC-18). |
| A2 ORD-132 export scopes | Already supported (page, all, search, selected, by date). Test added. |
| A3 ORD-142 Duplicate order | **Not built, blocked:** it is the draft-orders feature (decision list ORD-091 "DEFER: with drafts"; DC-22). |
| A4 ORD-014 flags | Already built for every flag the data supports (needs attention, cancellation open, details corrected, replacement, held); no risk score by decision (ORD-037). Test added. |
| A5 ORD-107 order-ID prefix | **No change:** the EKI format is the approved fixed format; an editable prefix is not authorised. Reclassified from partial to "fixed by decision". |
| A6 AC-13.4 | Built (see above), mock evidence only. |
| B8 PIN table | Sampled against India Post public data; two gaps fixed. |
| B9 stale comments | Fixed (four in `tests/test_f05_boundaries.py`). |
| B10 122 map | Reconciled with the 597 file: 13 rows named, 33 with a stated reason. |
| B11 weak tags | 9.2, 10.11, 10.12 replaced by real tests; 16.5 untagged (conflicts with a decision). |
| B12 dev DB after 0027 | Read-only queries on every new column ran; the dev DB has no pricing rules or business accounts to exercise further. |
| B13/B14 renders and browser submissions | Done in headless Chromium (list in the log). |
