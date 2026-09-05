# Protocol: Model Selection

## Decision rule

Optimize total cost to reach a correct, maintainable accepted result, including context transfer, inference, coordination, retries, and review. Choose the least costly path confidently capable of meeting the task's quality and risk requirements. **When suitability is uncertain, favor a more capable model.** Do not require a cheap failed attempt before using appropriate capability.

The [main skill](../../SKILL.md) owns workflow and review gates. Select the route at meaningful task/phase boundaries, not every tool call. Model capability, reasoning effort, reviewer independence, and number of agents are separate choices.

## Routing

| Work | Default route | Escalate when |
|---|---|---|
| Process/build waiting or deterministic status retrieval | Direct tool and bounded completion wait; no monitor agent | Failure, credible stall, or unexpected state needs judgment |
| Clear extraction, structured summary, mechanical transformation | Lightweight model with low supported reasoning if tools alone are insufficient | Ambiguity, conflicting evidence, unreliable output |
| Established-pattern implementation with clear acceptance | Balanced coding model, usually medium reasoning | Hidden coupling, changed ownership/contracts, uncertain failure handling |
| Ordinary independent code review | Fresh capable coding reviewer with enough effort to trace the behavior | Architecture or specialist risk needs greater capability |
| Architecture, substantial refactor, uncertain diagnosis | More capable model with high reasoning | Especially demanding unresolved reasoning justifies greater effort |
| Safety, security, irreversible migration, complex authority | More capable owner and competent independent specialist lanes | Preserve required evidence and expertise regardless of cost |

Do not classify by file count: a one-line concurrency fix can demand more judgment than a large mechanical edit. Keep the capable parent default unless the user asks to change it. Higher capability does not always require maximum effort.

## Runtime selection and dispatch

Use the live runtime roster and supported effort combinations. Do not preserve a drifting model-name table in personas or this protocol. If the roster does not establish a choice, use current official guidance and observed task outcomes. Do not infer subscription dollar cost from API token prices.

For each non-default dispatch, explicitly select model and a supported reasoning effort when the tool permits it. Provide the objective, relevant files/evidence, boundary, acceptance, escalation condition, and necessary context. Prefer a bounded or empty history fork when it supplies sufficient context and enables the override; do not discard context needed for correctness merely to reduce tokens.

Do not assume named profile selection, a model change for the running parent, or an API-only parameter is available. Check the current tool contract. A saved file or a model's self-description does not prove which configuration ran. Verify runtime selection through execution metadata when available, and distinguish requested from confirmed-effective settings. If an override is unavailable, use the current capable runtime and disclose the limitation when it matters. Do not create separate user-visible tasks solely to simulate switching.

Create persistent worker profiles only when requested or justified by recurring work and effective selection can be tested. Preserve existing account/provider settings. Do not weaken permissions, restore credentials, or add a paid service merely to make routing work.

## Delegate only when it helps

Use independent execution for required reviews and bounded parallel tasks whose expected benefit exceeds dispatch and integration cost. Avoid several scouts repeating a search that one tool call answers. Keep one integration owner, distinct lanes, and concise evidence-backed results. Do not make the parent redo each worker's entire investigation; inspect the evidence needed for integration and consequential claims.

Reviewer competence comes before model diversity. Prefer a different capable model when available, but never downgrade a reviewer merely to get another model name. Distinct personas within one execution are not independent reviews. An unavailable alternate vendor is not by itself a reason to stop if a suitable independent execution is available.

## Monitoring and escalation

Launch the authorized build/process once. Retain command, directory, candidate identity, process ID, log location, and required completion criteria. Use native completion events or bounded waits with backoff consistent with responsiveness. Avoid repeated model turns over unchanged logs, copying whole logs, or speculative commentary.

On completion, inspect the exit status and concise relevant result. Successful compilation proves only what was compiled. On failure or unexpected state, collect enough error context and route diagnosis to appropriate capability. A cheap monitor does not invent repairs or restart processes repeatedly. Do not claim all waiting is free; the goal is to avoid unnecessary inference and context ingestion.

Escalate promptly on a material missed requirement, uncertain architecture, conflicting evidence, or unreliable results. One focused brief correction can help a clearly underspecified task; do not repeat cheap attempts through a capability mismatch. Preserve useful evidence during escalation.

## Evaluate value

Use existing dispatch/receipts for selected model, effort, and any material routing rationale or escalation. Do not create a routing ledger per small task. Compare accepted-result quality, elapsed delivery time, rework, review signal, and available usage on comparable tasks. Promote the more capable route when cheaper attempts increase total work or weaken maintainability. Do not report estimated savings as measured billing.

There is no cache-keepalive timer or polling quota in this policy. Discover actual environment behavior when relevant; never manufacture turns just to keep a cache warm.
