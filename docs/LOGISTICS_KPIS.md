# Last Mile Logistics — service KPI definitions

Version 0.3 | 26 October 2026

## Naming and compatibility

The application is now Last Mile Logistics. Branding is updated in the interface, page title, export names, printed draft notes, launcher and project documentation. Historical shipment identifiers such as SG-1038 remain unchanged to preserve relationships. Existing browser records from the previous storage key are migrated without erasing shipments, files, approvals or costs. The project folder is now last-mile-logistics.

## Reporting scope

The service panel reports at original approved customer-order level, not per truck. Principal/warehouse filters in Director's view also scope service KPIs. Reporting defaults to the previous completed local calendar day in Asia/Kolkata. A selected current-day report is explicitly provisional. This version reports cumulative history through the selected date; it is not a rolling-month or date-range report.

## OTIF: on-time delivery in full

OTIF = orders confirmed accepted in full on/before their agreed customer delivery date / evaluable due orders × 100.

- Due orders have an agreed customer delivery date on/before the report cutoff.
- Accepted quantities from split shipments are combined by original order. The complete approved order quantity is the target; a manager-approved short dispatch does not reduce that target.
- An order whose recorded accepted quantity is incomplete by its deadline is a miss, including overdue orders with no recorded completion.
- A known full receipt after the deadline is a miss even if products and paperwork were accurate.
- Historical delivery records with unknown actual dates or ambiguous allocation across orders are disclosed as evidence missing and excluded from the evaluable denominator. The panel shows due count, evaluated count, misses and evidence coverage alongside the percentage.
- If every due order lacks usable evidence, OTIF is unavailable, not 100% or an assumed zero.
- Route ETA, planned departure and POD upload time are not substitutes for an agreed delivery commitment or actual receipt date.

Example: an order for 10 has 5 accepted by the deadline and 5 the following day. OTIF fails for one original order, not a 50% trip success calculation. If all 10 arrive by the deadline across two trips, it passes once.

## Order accuracy rate

Order accuracy = accurate orders / assessed completed orders × 100.

A completed order has at least its full approved quantity shipped and all linked delivery outcomes recorded by the report cutoff. Accuracy checks product identity, accepted quantity and document correctness. Confirmed accepted quantity below the approved quantity is a known discrepancy. Otherwise, each order-line delivery requires an explicit accurate/error assessment and evidence reference. Successful warehouse scans alone do not prove delivery accuracy.

Unassessed completed orders are excluded from the rate and disclosed in coverage. Historical records without actual dates/line allocations remain unknown, not automatically accurate. Explicit inaccurate assessments make an order inaccurate even if it arrived on time.

This is the project's transparent working definition. It is not a claim that every 3PL contract uses this exact denominator. Agree contractual reporting and exclusions before production use.

## Data entry and safeguards

- Overview → Definitions & order breakdown → Commitment: Planner/Manager records the agreed date and source reference.
- Existing commitments cannot be moved after dispatch. A missing original historical commitment can be entered once against an explicit source, with audit evidence; it is not inferred from ETA.
- Delivery entry now records actual receipt date and accuracy assessment. Multi-order shipments record accepted/returned outcomes separately for each order line, reconciling to shipment totals.
- Existing deliveries: Definitions & order breakdown → shipment evidence. Checker/Manager can add assessments; only Manager may change an already recorded actual date, retaining previous evidence in history.
- Dates must be valid and not in the future. Where actual departure is known, delivery cannot precede it.
- Correcting evidence does not issue stock, change delivered totals, or create financial postings.

## Demonstration and evidence boundary

A fresh synthetic dataset has explicitly labeled sample commitments, not historical company targets. It starts with no completed measured performance, so KPI values can be unavailable. Older browser records retain unknown commitments/dates rather than receiving fabricated defaults. Use the source/evidence forms to demonstrate measured outcomes.

The existing synthetic receipt of 8 accepted and 2 returned against 10 ordered correctly fails OTIF and order accuracy once its actual date/commitment is supplied. Settlement/return closure cannot turn it into a successful delivery.

Browser-local storage and simulated roles remain the same demonstration limitation. No production authorization, live tracking, contract compliance or business improvement is established by these percentages.
