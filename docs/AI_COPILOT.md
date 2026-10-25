# AI copilot — operator and interview guide

Version 0.4, 26 October 2026. Three optional assistants are implemented: explain a selected shipment plan, draft a transporter message, and summarize document gaps. The API key is saved only in the owner's ignored local environment file. **The live smoke test returned insufficient_quota. No successful live model output has been verified.** The local rules/template fallback remains usable.

## Demonstrate it

Run `node server.mjs`, open http://127.0.0.1:4173 and select a ready PO in Shipment planning. Choose **AI explain this plan**, inspect Source facts, then **Use local rules / template**. Review/edit the result and accept or reject it. Shipment detail offers the transporter assistant; Documents offers the document-gap assistant. Acceptance records a review; it does not book, send, dispatch, change stock or approve finance.

For four LED units at ₹1,800 each, value is ₹7,200. A ₹4,100 freight quote is 56.9% of goods value. Weight is 4.8 kg; volume follows the current material master. These are distinct from truck utilization. Compatible consolidation is a suggestion subject to stock, customer deadlines and manager review. Historic shipment explanations use current material dimensions and are not measured loading evidence.

Document assistance receives checklist metadata and optionally pasted text (8,000-character cap), not uploaded file bytes. It performs no automatic OCR, authenticity verification or statutory validation. Missing references remain missing; operators verify the source evidence.

## Setup and quota

The shared ZIP contains `.env.example`, not credentials. For a separate local installation, copy its settings to `.env.local`, provision your own key securely and enable AI. Never put a key in dist/, browser code, GitHub or a screenshot. Restart the server after changing configuration. The owner's existing `.env.local` is already configured; do not overwrite it.

The account owner must review [API billing](https://platform.openai.com/settings/organization/billing) and [usage limits](https://platform.openai.com/settings/organization/limits) to resolve insufficient_quota. The application cannot resolve account funding. A previous unused Codex key from the failed secure handoff remains in Platform and should be revoked there. No additional key creation is needed for this installation.

Flags: AI_ENABLED is the global switch; AI_EXPLAIN_ENABLED, AI_TRANSPORTER_ENABLED and AI_DOCUMENTS_ENABLED control individual assistants. AI_MAX_CALLS_PER_RUN defaults to 30; AI_TIMEOUT_MS defaults to 25,000. The gateway permits one live request at a time and six per minute per running process. These demonstration caps do not replace provider billing limits. Static GitHub Pages alone cannot run this server-side gateway; hosting remains a separate decision.

## Architecture and controls

Browser selection → minimized snapshot → loopback gateway → deterministic facts → optional OpenAI response → output validation → editable operator review → feedback record. The configured model is changeable using OPENAI_MODEL. Integration uses [Responses structured outputs](https://developers.openai.com/api/docs/guides/structured-outputs?api-mode=responses) and the [documented model capabilities](https://developers.openai.com/api/docs/models/gpt-5.6-terra).

Credentials remain server-side. Requests use store:false, a strict schema and no tools. Only selected order/SKU quantities, route, principal, departure, configured truck/material facts and document checklist data are included; driver/contact details and file bytes are excluded. Optional pasted text goes to OpenAI only when live generation is requested. Treat it as untrusted and use synthetic data in this demo. store:false is not a promise of zero provider retention.

The gateway checks loopback Host, same-origin requests, a session cookie, CSRF token, request size and schema. Arithmetic is computed in code. Response validation checks shape, fact references, unsupported numeric literals, explicit unauthorized-action claims and the review-required flag. These checks cannot guarantee semantic correctness or eliminate prompt injection. Operator review remains mandatory.

Local metadata logs in `.local/ai-audit.jsonl` record request ID, feature, source fingerprint, provider/fallback reason, model/prompt version, latency, usage and review outcome. They exclude prompts, raw documents, generated text and secrets. Accepted/edited drafts are kept in the current browser's last 25 suggestion records. Rejected content is not retained there. Neither store is tamper-proof; protect/delete local demonstration records according to your needs. No automatic model training occurs.

Browser data and role selection are editable by the browser owner. This is a single-device demo, not authenticated multi-user ERP authorization. Production needs server-owned records, principal/warehouse access checks, named reviewers, durable private evidence, retention rules, usage ownership and operational approval controls.

## What qualifies as AI

LLM copilot: language explanations, drafts and document-text suggestions. Rule engine: compatible grouping, capacity, scan/document gates and freight variance arithmetic. Predictive model: future freight/delay estimation trained on sufficient historic outcomes, with time-based validation and baseline comparison; not implemented. Contextual bandit/RL: learning a constrained decision policy from logged actions, probabilities and outcomes; not implemented. Operator feedback is evaluation data, not reinforcement learning.

## Evaluation and next phases

1. Current: deterministic facts, three assistants, reviewed output, explicit fallback, flags and metadata logging. Automated suite: 69 passing tests, including 13 AI/gateway cases with mocked provider responses. Real-provider smoke: blocked by quota.
2. After quota resolution: one synthetic smoke test, then a curated evaluation set covering ordinary plans, missing documents, contradictory extracts, injection attempts and high freight. Record correctness, unsupported claims, omissions, edit rate, latency, token cost and fallback rate. Require zero unauthorized actions and correct source arithmetic; agree acceptance targets before pilot. Mock tests alone do not establish model quality.
3. Production pilot: authenticated server and database, governed access, approved provider/data terms, budget limits, named operator review and rollback. Disable AI to fall back without interrupting workflow gates.
4. Predictions later: collect planned and actual costs, route/truck/load attributes known at planning time, delay outcomes and coverage. Compare held-out results with existing rate/rule baselines. Preserve estimate version and separate freight from extras.
5. Bandits/RL only after a stable baseline and adequate data: define eligible actions and safe reward, log selection probabilities, evaluate offline, authorize a constrained supervised experiment. Never optimize away document, scan or approval gates.

For an interview: “The ERP owns calculations and controls. The LLM explains and drafts, with a human decision. We have implemented the integration and tested failure handling; live model evaluation is pending account quota.”
