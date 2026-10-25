# Verification report — Last Mile Logistics 3PL demonstration

## Automated evidence

69 tests pass with Node's built-in test runner. Syntax checks pass for the workflow engine and interface module. Coverage includes ready balances; grouping and principal isolation rules; same-SKU multi-order grouping; physical stock caps; route-rate and missing-data checks; wrong/unknown/duplicate/excess product scans; carton aggregation; simulated role restrictions; retrievable evidence; current-version partial approval; manager rejection; independent scanner-failure reconciliation; dispatch retry/rollback behavior; POD/quantity gates; customer return caps; one-time usable-stock restoration; costs and final closure; immutable post-delivery evidence; and stock-movement lineage.

Tests exercise single-process pure commands on synthetic state. They do not establish secure authentication, multi-user database isolation, real-world scanning accuracy, legal document validity or operational acceptance.

## Browser evidence

- Local HTTP preview returned 200.
- Desktop overview visually inspected: sidebar, KPIs, pipeline, route display, attention items and shipment table.
- Warehouse transport details entered through the UI.
- Wrong-SKU product rejected visibly; ten sample LED unit identities verified.
- Carton linked to all ten products without quantity inflation.
- Synthetic invoice/e-way/LR content attached and verified using Accounts role.
- Dispatch enabled only after gates passed, then state advanced to in transit.
- POD attached/verified; delivery reconciled as 8 accepted and 2 returned.
- Linked return received/inspected as 1 usable and 1 damaged.
- Note reference and explanation reconciled through the UI.
- Costs entered as 4,500 freight + 300 unloading; interface showed 400 / 9.8% freight variance against 4,100, and a separate 4,800 all-in actual total.
- Manager closed the reconciled trip; closed controls became disabled.
- Two compatible same-SKU POs combined through the UI into a new 12-unit plan.
- Phone viewport 390 × 844 inspected; workspace selector reaches customer returns. Desktop viewport restored.
- Final overview screenshot saved as SIP_GREEN_PROJECT_PREVIEW.png in the parent outputs directory.

Browser QA was manual automation against synthetic data; no real carriers, principals, messages, scanners, accounting systems or IoT devices were used. Later identity-catalog, movement-ledger and manager-rejection refinements are covered by the final automated tests; the full browser journey was checked during implementation, not claimed as a separate automated end-to-end suite.

## Material limitations

- Browser-local persistence, limited shared quota, no server-side authentication or concurrent-user protection.
- Role selection demonstrates duties but grants no actual security isolation.
- One packaging aggregation level; mixed-SKU returns are deliberately blocked pending line-level delivery reconciliation.
- Returned-unit serialized identity lifecycle/repacking/re-dispatch requires further work; restored quantity alone does not reset a historical unique scan.
- Financial notes can be prepared, reviewed and downloaded as printable drafts, not legally issued instruments or accounting postings.
- Document gates check stored content and human review, not authenticity or statutory applicability.
- Optional LLM assistance is implemented, but successful live generation is blocked by API quota. OCR, live location, RFID/GPS and manufacturer identifier integrations are absent.
- Real route feasibility, customer slots, tax rules, contracts, liability and financial authority require owner validation.
- Synthetic historical shipment SG-1038 is a seeded in-transit scenario; it is not evidence of a prior real dispatch or a complete imported document history.
- Reset sample data if returning on a later day: old departure plans intentionally cannot dispatch in the past.

## Release status

Suitable for a clearly labeled interview demonstration and review of workflow decisions. Not approved for handling real warehouse stock or production data. GitHub publication and hosting were intentionally deferred by the owner. A private, unpublished Sites registration was created earlier; no project source was synchronized and no deployment was made.

Additional final browser check: manager rejected a five-of-six-unit partial request with a recorded hold reason; the interface showed Rejected / hold and retained the approval gates.

## Version 0.2 verification

40 automated tests now pass. Added tests cover weighted versus average variance, pending costs, zero baselines, principal/warehouse scope, dimension conversion, frozen estimates, affected-plan review, inactive trucks, draft arithmetic and rounding, internal note approval, edit invalidation, exact reconciliation, debit-note support, duplicate references, no-adjustment voiding and safe printable HTML escaping. Existing 24 workflow tests continue to pass after updating the note-closure scenario for mandatory preparation/review.

Browser checks: LED length changed 40→50 cm; the affected load required review. Entered costs for synthetic SG-1038 showed +12.2%, 5,100 all-in cost and 500 extra charges. Created a two-unit return, inspected usable/damaged quantities, prepared and internally approved a 3,600 credit-note draft, downloaded the printable HTML and reconciled the exact approved fields to close the return. The downloaded sample is provided separately for review. No actual financial note was issued.

Final guard verified: a no-adjustment reconciliation must carry zero amount. Total: 40 passing automated tests.


## Version 0.3 verification

56 tests pass: the previous 40 operational/master/note tests and 16 service-KPI tests. Added coverage: on-time complete versus late complete, split shipments counted once, a late remainder, short dispatch against original quantity, missing commitment versus ETA, missing actual dates and coverage, unassessed outcomes, confirmed discrepancies, overdue unfinished orders, future commitments, principal/warehouse filters, date validation, multi-order delivery allocation, locked commitments and audited manager correction.

Browser check: renamed interface and page title loaded, historical browser records/costs remained present, KPI definitions opened, a synthetic source-backed missing commitment was entered and historical delivery evidence was assessed. The sample 8-of-10 accepted receipt correctly produced 0/1 OTIF and 0/1 order accuracy with 100% coverage for that known example. These are synthetic demonstration results, not company performance.

## Version 0.4 AI verification — 26 October 2026

69 tests pass: 56 prior tests plus 13 AI/gateway tests. These exercise minimized context, deterministic arithmetic, strict structured requests, no tool access, rejected unsupported numbers/references/actions, review requirements, provider quota fallback, feature flags, usage caps, metadata-only logging, feedback linkage, origin/CSRF checks and private-file exclusion from HTTP. Provider success uses mocks; this is not a claim of live model quality.

A synthetic live smoke test returned HTTP 429, provider code insufficient_quota; the gateway returned a clearly labeled local-rules fallback. No successful live generation was observed. Browser checks verified the four-unit planning explanation, explicit local fallback and acceptance of a local review record. Prior browser records were retained.

Additional browser checks: transporter fallback included the selected shipment source details and editable review controls; document fallback listed missing invoice, e-way and LR files without bypassing dispatch gates.
