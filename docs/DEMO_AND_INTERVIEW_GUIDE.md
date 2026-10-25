# Demonstration and MBA interview guide

## A 60-second introduction

I focused on one logistics execution vertical rather than attempting an entire ERP. The principal owns goods and contracts a 3PL to manage bulk deliveries. The problem is fragmented planning and weak handoff evidence: an approved order, a printed label or a planned departure alone does not prove the right product reached the right destination.

The prototype connects ready POs, compatible grouping, explainable truck selection, departure planning, product verification, principal-backed exception approval, documents, dispatch, delivery and customer returns. Its value proposition is fewer uncontrolled handoffs and clearer accountability. I would validate that value using measured operating data, not claim invented savings.

## Preparation

Run node server.mjs and open the local address. Begin with Project guide → Reset demo data if you want fresh sample records. Role selection simulates responsibilities. Never use actual company documents in this browser-local demo.

## Five-minute happy path

1. Overview: explain principal ownership, 3PL custody, warehouse scope and sample pipeline.
2. Shipment planning: select PO-AMZ-2402 and PO-AMZ-2403. Show compatibility, truck capacity, rate, low-utilization warning and departure date. Explain why ETA is separate. Confirm as Planner.
3. Warehouse & scans: select SG-1041 for the shorter 10-unit scenario. Switch to Warehouse. Enter sample transporter, vehicle and driver.
4. Attempt FAN-U-0001: wrong SKU is rejected. Verify LED-U-0001 through LED-U-0010. The insert-sample button fills the next code; Verify product records it. Try a duplicate to show protection.
5. Seal carton CTN-SG-1041-01. Show that ten product scans plus one carton still represent ten goods, not eleven.
6. Documents: attach explicitly synthetic invoice, e-way and LR samples. Switch to Accounts and verify each. Samples are not actual legal evidence.
7. Warehouse: readiness clears. Confirm dispatch. Stock issue, reservation release and actual departure are recorded once.
8. Trip costs: attach POD, verify it as Accounts in Documents, then record delivery as Warehouse. For an uncomplicated path use 10 accepted, 0 returned.
9. Accounts: declare freight/holding/unloading/extras. Manager: close reconciled trip. Show the audit trail and comparable freight variance.

## Exception path: partial shipment

Use SG-1042 before scanning. Warehouse adjusts packed quantity from 6 to 5 and requests partial dispatch with urgency, shortage and cost explanation. Attach a labeled sample principal-permission email in Approvals. Manager records the decision. Show that approval is bound to the current manifest; change the quantity again to invalidate it. No automatic commercial decision is made by AI.

## Exception path: failed scanner

Warehouse records failure and reconciliation evidence reference. Switch to Checker for independent count/identity verification, then Manager for approval. Seal a manually reconciled carton. Verified manual units stay distinguished from actual scans. Explain that a real device failure and a whole-system/network outage are different; emergency offline dispatch is not implemented.

## Customer return path

For a dispatched shipment with POD, record 8 accepted / 2 returned. Open one linked return for 2 units. Checker receives/inspects 1 usable and 1 damaged; only 1 restores available stock. Accounts prepares a credit/debit-note draft with issuer, recipient, invoice source, quantity, rate and manually supplied tax. Manager approves the draft, Accounts reconciles the exact approved reference/amount, and the printable draft can be downloaded. Manager closes the trip after the linked return is reconciled. Vendor return belongs to procure-to-pay and is excluded.

## Likely interview questions

**Why this process?** It has measurable operational risk, cross-functional handoffs and clear physical/financial evidence boundaries. A bounded vertical can be demonstrated and tested credibly.

**Who owns inventory and loss risk?** The principal owns inventory, the 3PL manages custody. Liability depends on contract, evidence and circumstances; software should record the investigation and agreement, not automatically assign every loss.

**Why manager approval for partial dispatch?** Extra transport, service obligations and principal consent have commercial implications. Preserve the principal email and manager rationale before executing a changed manifest.

**How do you prevent double planning?** Subtract dispatched and active committed quantities correctly, validate aggregate physical stock and recheck before confirmation. The local prototype demonstrates sequential checks; concurrent production use needs server/database transactions.

**Why scan carton and product?** Product identity confirms contents; carton/pallet identity confirms the logistics unit containing them. Parent-child aggregation preserves traceability without counting the same goods twice.

**Is a scan proof of correct packing?** It is evidence, not complete physical assurance. Identifier master quality, actual packaging, unit conversions, process discipline, exception controls and inspection still matter.

**Where is AI?** Current assistance is templates, rules and arithmetic. A live LLM could draft/condense verified information after evaluation. Forecasting needs historical outcomes. Feedback logging is not reinforcement learning.

**Why not start with RL?** No validated reward/data baseline exists. A bad reward could encourage unsafe cheap departures or skipped verification. Establish rules and outcome logging first, then evaluate constrained alternatives offline.

**What would you measure?** Wrong-SKU attempts, scan exception rate, document completeness, planning time, approval turnaround, on-time departure, accepted/returned quantity, return-cycle time and like-for-like freight variance. Separate operational improvement from causation and seasonality.

**How do you calculate ROI?** Compare measured labor/error/exception costs before and after, subtract development, hosting, support, equipment and model usage. Do not treat principal merchandise value as 3PL revenue. Use contract revenue and actual variable costs for contribution analysis.

**What if a truck suggestion is wrong?** Show missing-data warnings and calculation assumptions; keep human review. Weight/volume fit is not a guaranteed physical load arrangement or live route feasibility.

**How does it scale to hundreds of orders?** Production needs indexed queries, pagination, client/warehouse isolation, transactional allocation, safe background processing and monitoring. The small browser-local dataset demonstrates logic, not scale evidence.

**How do you protect data?** This version uses synthetic data only. Production needs named-user authentication, server RBAC, private attachments, retention, secure secrets, audit protection, backup and restore tests.

**Who built it, and what did you contribute?** Be accurate: explain your business problem framing, workflow decisions, requirements, prioritization and testing involvement. Disclose AI-assisted implementation. Do not claim unverified deployment results or sole authorship of generated code.

## Strong closing statement

The project demonstrates how to translate a 3PL operating problem into explicit responsibilities, controlled state transitions and testable evidence. The next investment would be real data validation and a secure server-backed pilot, not unsupported claims of AI autonomy.

## Enhancement walkthrough

1. Fleet & materials → Manager role → edit LED packed length from 40 to 50 cm. Volume changes from 0.008 to 0.010 m³. Open SG-1041: the master-review hold appears. Planner/Manager can review it if the chosen truck still fits. No historical freight estimate is overwritten.
2. Trip costs → SG-1038 → Accounts/Manager → declare freight 4,600, holding 200, unloading 300, extras 0. Overview now shows +12.2% weighted freight variance, 5,100 total actual cost, 500 additional charges and 100% cost-declaration coverage in this one-trip scope. This is entered sample data, not company performance.
3. Customer returns → inspect a return → use Credit / debit note preparation. Accounts saves the draft, Manager approves it, and View / download produces printable HTML. Accounts reconciles the approved amount/reference before return closure. Editing a draft resets internal approval.
4. In a fresh workspace no actual costs are entered. The director percentage therefore shows unavailable rather than a fabricated improvement. No adjustment closure remains available with a recorded explanation.

## Version 0.3 KPI interview points

Open Overview → Logistics service KPIs. Explain that OTIF measures the full original order against the customer-agreed delivery deadline, while order accuracy measures correct delivered products, quantity and paperwork. A late correct shipment can pass accuracy but fail OTIF. A small approved partial dispatch does not redefine the original order as delivered in full.

Use Definitions & order breakdown to show agreed commitments, misses, missing evidence and assessments. The report defaults through yesterday; current-day results are provisional. Do not claim unavailable evidence as 100% performance. Review LOGISTICS_KPIS.md before describing the denominator or making a company performance claim.
