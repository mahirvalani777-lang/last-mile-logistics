# Requirements and decisions — version 1.5

This is the current delivery-only demonstration baseline. It supersedes earlier broad-ERP plans and older interpretations of appointment dates or vendor returns.

## Confirmed by the owner

| ID | Decision | Implementation evidence |
|---|---|---|
| BR-01 | A 3PL can serve multiple principals; each principal owns its goods | Principal and warehouse references on stock, orders, shipments and returns |
| BR-02 | 3PL manages custody; loss liability depends on the contract | No automatic liability posting; contract references displayed |
| BR-03 | Bulk deliveries on specified routes/destinations | PO grouping and principal/route sample rate lookup |
| BR-04 | Begin with approved POs and available stock; exclude procure-to-pay | Seeded approved order snapshots and ready quantities; no sourcing module |
| BR-05 | Appointment means warehouse departure | Departure label separate from route-estimated arrival and actual event |
| BR-06 | Partial dispatch needs principal email permission and manager rationale | Evidence attachment, request, current-version approval and revised document gates |
| BR-07 | Scan every product and carton/pallet | Serialized product register and packaging aggregation; scanner text input |
| BR-08 | Failure requires independent reconciliation and manager exception | Warehouse incident → Checker → Manager; manual quantity stays manual |
| BR-09 | 3PL issues/prepares invoice/credit/debit documentation | 3PL preparation role and explicit legal-issuer field; draft preparation, internal approval and printable document; no statutory issuance |
| BR-10 | Customer returns, notes, reconciliation and closure included | Linked case, quantity cap, inspection, stock movement, note reference and closure |
| BR-11 | Vendor returns outside this logistics vertical | No vendor-return screen |
| BR-12 | Focus on project first; defer GitHub/hosting | Local project, tests and documentation; no publication/deployment |

Principal means the contracting stock-owning business. Customer means its buyer/recipient. The 3PL is the warehouse/logistics operator; a transporter supplies carriage. Principal is a contractual role, not an assertion of corporate parent/subsidiary ownership.

## Implemented demonstration rules

- Ready = max(0, min(approved minus dispatched, allocated-undispatched) minus active planned commitments). Physical stock also caps aggregate new plans.
- Compatibility requires identical principal, warehouse, destination, platform and category. No cross-principal co-loading.
- Truck recommendation checks weight and volume using explicit sample SKU dimensions and principal/route rates. Missing route or dimensions cannot become a fabricated quote.
- Individual unit identity must exist in the sample catalog for that principal/warehouse. A carton links its contents without incrementing verified units.
- A packed-quantity change invalidates partial/manual approvals. Documents must record the current packed quantity.
- Manager partial-dispatch approval requires attached principal permission evidence; an urgent relationship does not replace permission.
- A scanner exception needs independent Checker verification. New scans invalidate a prior independent incident count. Manager approval authorizes remaining manual units only.
- Dispatch checks physical confirmation, packaging link, current approvals, vehicle/driver/transporter, departure date and invoice/e-way/LR sample evidence. Then issues stock once and releases the matching order allocation.
- Delivery requires verified POD and accepted + returned = dispatched. Duplicate delivery is refused.
- Return quantity is limited to declared returned shipment units. Usable + damaged + missing = expected; only usable received stock is restored, once.
- Credit/debit records retain issuer, preparation role, reference, amount and explanation. No official note or external accounting posting is created.
- Costs have explicit freight/holding/unloading/extras. Variance compares freight with frozen freight estimate, not total actual cost with freight-only estimate.

## Proposed demonstration policies, not owner-confirmed company policy

1. Require invoice, e-way evidence and LR on all sample journeys. Real applicability is contract/document-policy work.
2. Require linked returns and note reconciliation to close before trip closure. The business may instead allow a closed journey with an open settlement; this needs a separate decision.
3. Checker inspection constitutes authorization to restore usable goods in the demo. Real QC/disposition authority needs confirmation.
4. Use serialized per-product IDs and one packaging level. Real QR contents, serial allocation, rework, repacking and nested pallets need device/master-data validation.
5. Use calendar-day route estimates and INR, without statutory tax calculation or live traffic.
6. Low utilization warns when both weight/volume utilization are under 20%. This is a labeled example heuristic, not a contractual threshold or optimization claim.

## Remaining production decisions

Legal issuer and principal authorization; official document layouts and applicability; customer/warehouse scopes and named approvers; return condition/disposition policy; note perspective and settlement confirmation evidence; receiving-slot rules; route calendars and SLA/penalty formulas; loss investigation and liability allocation; physical scanning devices and QR mappings; attachment retention; backup/recovery objectives; outage dispatch authorization; and whether trip closure may precede settlement.

Do not turn the demo's simulated permission email into an assertion of real principal consent. Do not present sample records as operational data or as proof of business savings.

## Version 0.2 enhancements — confirmed requested additions

The owner requested note preparation, truck/material masters and a director overview of cost variance. These features extend the existing demonstration; they do not change its browser-local security/storage boundary.

- Accounts/Manager prepares a credit or debit draft for an inspected customer return. It records issuer, recipient, invoice reference, SKU/quantity, rate, manually supplied tax and reason. Manager review is mandatory before financial-note reconciliation. Editing resets review; duplicates per issuer are rejected. Closed historical reconciliation records remain intact.
- Downloaded HTML is printable using browser Print / Save as PDF and prominently labeled DRAFT / DEMONSTRATION. It is not a statutory note, automatic tax assessment, financial posting or message send.
- A no-adjustment closure needs an explanation and voids an unused draft rather than leaving it apparently active.
- Manager edits truck types (payload kg, usable m³, base rate and availability) and packed material dimensions (cm), gross unit weight and goods value. Volume derives from dimensions. Changes flag affected preparing shipments; Planner/Manager must review them before dispatch. Existing freight estimates remain frozen.
- Overloaded/inactive-truck review is blocked. Reassignment/cancellation/replanning of already committed loads remains a next-stage feature; restore correct master data or leave the affected shipment on hold in this demonstration.
- Director metrics use only dispatched trips and explicitly report missing cost declarations. Weighted variance is computed on positive, known freight estimates with matching declared actual freight, not averaged per-trip percentages. Zero/missing baselines are disclosed as excluded. Extra charges and all-in actual total remain separate from freight variance. Principal and warehouse filters apply to the whole panel and drilldown.

## Version 0.3 — Last Mile Logistics and service KPIs

Brand renamed to Last Mile Logistics; historical source IDs remain stable. Dashboard adds original-order OTIF and order accuracy, cutoff date, evidence coverage and a definitions/order drilldown. Approved-order customer commitment and actual delivery/accuracy evidence are captured separately from departure/ETA. Missing evidence does not silently pass. See LOGISTICS_KPIS.md for formulas, reporting cohort and limitations.

Agreed commitments cannot be moved after dispatch. Delivery assessment/date corrections are audited and preserve prior evidence; only a Manager can correct an existing actual receipt date. Order-level split quantities are explicitly reconciled. This expands logistics execution reporting without introducing procurement, vendor returns or autonomous financial actions.
