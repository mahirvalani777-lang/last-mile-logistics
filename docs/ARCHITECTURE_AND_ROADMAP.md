# Architecture, controls and next delivery stages

## Current implementation

Browser UI → pure workflow commands → cloned state → one localStorage save on success. Failed engine commands leave input unchanged. This provides deterministic single-browser demonstration behavior, not database transactions across concurrent users.

The engine keeps principal/warehouse stock keys, approved orders, active plan commitments, registered product units, shipment scans/cartons, evidence files, versioned approvals, delivery outcomes, costs, returns, movement records and audit events. Every mutation goes through a command with allowed simulated roles. Browser role selection and local validation are explicitly not a security boundary.

Static assets have no required package installation. The local HTTP server binds loopback and serves only dist/. Optional Google Fonts affect typography only; system fonts are available if offline. User-entered content is escaped before HTML rendering. No secrets, real contacts, API calls, external sends or financial postings are needed.

## Production target

1. Authenticate named users and authorize role, principal and warehouse access on every server operation and file request.
2. Move commands to a server application with a relational database, foreign keys, version checks, transactional stock/reservation updates and idempotency keys.
3. Move files to private object storage with content checks, size limits, malware handling, authorized retrieval and retention. Separate upload success, file verification, legal validity and business approval.
4. Make audit/movement records durable and access-controlled. Record prior/current versions and rejected operations appropriately; do not log secrets or unnecessary personal details.
5. Integrate actual product/pack identifiers, scanners and label generation. Validate units versus cartons and nested aggregation without double counting.
6. Implement damaged/quarantine/disputed stock ledgers, line-level delivery/returns, cost lineage and controlled corrections/reversals.
7. Confirm issuer authority and accounting interfaces; add retries/reconciliation without duplicate financial postings.
8. Test concurrency, failure recovery, backups/restores, data migration and real operator acceptance before live stock.

## Assistance versus AI

Implemented: compatible-group checks, missing-data rejection, weight/volume calculations, low-utilization warning, editable transporter template, evidence checklist and comparable cost variance.

Implemented in version 0.4: optional server-side LLM drafting/explanations with operator review and local fallback. Live availability is currently blocked by API quota. Not implemented: OCR, statistical anomaly scoring, trained cost/delay models, contextual bandits, full reinforcement learning or IoT tracking.

Implemented optional LLM gateway: server-only credentials, minimum authorized context, structured responses, prompt-injection resistance for untrusted documents, factual checks, timeouts/usage caps, per-feature flags, operator review and manual fallback. It must have no independent dispatch, stock, finance or send authority.

Later predictive models: collect historical planned-versus-actual data, known-at-planning-time features and stable labels; compare to route-rate/rule baselines with held-out evaluation. Report uncertainty and data limitations. Do not use future outcomes in training features.

Later bandits: log eligible actions and action probabilities, define a reward that does not encourage unsafe shortcuts, evaluate offline and get explicit authorization for a constrained experiment. Operator edits alone are not reinforcement learning.

## Phases after the first demonstration

A. Review demonstration with the owner, confirm open company policies, improve real data samples and complete line-level edge cases.
B. Implement authenticated server/database version, durable attachments and exact custody/stock/return semantics.
C. Validate devices, document layouts and controlled accounting interfaces on isolated data.
D. Introduce evaluated optional LLM assistance; predictions only when sufficient outcome data exists.
E. Run a small supervised operational pilot with reconciliation, restore rehearsal and a rollback plan. Obtain explicit go-live authorization.

No fixed production completion estimate is asserted from the interview demo. Estimate each phase after policy/data/integration review.

## Version 0.2 module additions

The pure enhancements.mjs module handles master-data edits, compatibility-preserving browser-state migration, draft-note preparation/approval, printable draft HTML and director cost calculations. enhancement-ui.mjs provides the master screens, director summary and note workbench. Existing records and estimates are preserved; no schema reset is required.

Master edits are audited and flag affected preparing loads. Existing estimates are not repriced automatically. The director percentage uses matched freight-only components and reports pending declarations and excluded zero/missing baselines. Draft note amounts use integer currency subunits and retain approved revision linkage. These controls remain demonstration rules, not server security or legal validation.

## Version 0.3 service reporting

logistics-kpis.mjs provides date validation, order-level aggregation, per-order delivery outcomes, commitment locks and audited receipt/accuracy evidence corrections. kpi-ui.mjs renders the service dashboard and evidence forms. Browser-state migration retains the earlier storage record and stable shipment IDs while using the Last Mile Logistics brand/storage namespace for new changes. See LOGISTICS_KPIS.md for cohorts and exclusions.

## Version 0.4 assistant

See AI_COPILOT.md for request boundaries, feature flags, evaluations and quota status. Browser → loopback gateway → minimized facts + structured Responses request → validation → operator review. No tools or operational mutations are exposed to the model. Browser-supplied facts are untrusted; this gateway is not a production authorization boundary.
