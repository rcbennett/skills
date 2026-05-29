---
name: do-quality-work
description: Apply project quality protocols to choose the right review, design, verification, learning, parity, model-selection, claim-checking, team-assignment, review-cycle, and reporting workflow for non-trivial work. Use when Codex is asked to do high-quality work, implement or review code, write or review plans, make design decisions, verify claims, assess subagent findings, handle cross-platform product work, choose reviewers or models, internally decide whether a review cycle is needed, identify which team members are doing which tasks, report protocols used, or decide what validation is required before calling work complete.
---

# Do Quality Work

## Operating Rule

Treat quality as an execution protocol, not a final polish pass. At task intake, choose the relevant protocols, apply them while working, and report the verification that was actually performed.

When a project has its own `management/protocols/` directory, inspect and prefer those live project protocols. Otherwise use the bundled protocol references in `references/protocols/`.

Every output must include who did which task, which protocols were used, when multiple team members were used, and whether the protocols exposed any improvement opportunities.

Do not wait for the user to explicitly ask for review. Internally assess whether the task requires a plan review, design review, code review, security/safety review, domain review, parity review, or verification review, then run the applicable cycle when the environment allows.

## Right-Time Verification Rule

Verification is required for confidence, but repeated verification has real time, cost, and attention costs. Be deliberate about when to run tests.

- Run the cheapest high-signal check that exercises the changed behavior.
- Prefer narrow tests, type checks, linters, or targeted builds while iterating.
- Run expensive suites at decision checkpoints: after a cohesive implementation slice, before committing or pushing, before deploys, before claiming completion, or after a fix that could have affected broad behavior.
- Do not rerun the same expensive suite after every small edit unless the edit plausibly invalidated the prior result.
- If a test fails, fix the cause and rerun the smallest relevant check first; broaden only when the fix touches shared behavior or the narrow check passes and a release/commit/deploy decision needs wider confidence.
- If verification is intentionally deferred because it would be wasteful at the current point in the work, say what was deferred, why, and when it should run.

## Global Model Diversity Rule

Use a variety of models, reasoning strengths, and reviewer perspectives whenever the environment and task permissions allow. Different models catch different mistakes.

- For non-trivial plans, use a reviewer on a different model from the plan author.
- For non-trivial code or production changes, use at least one reviewer on a different model from the author.
- For high-stakes work such as safety, auth, PII, data model changes, cross-platform architecture, billing, or hardware control, use two independent reviewers on different models or model tiers when available.
- Pair model diversity with persona diversity. A different model using the same narrow perspective is not enough for broad risk discovery.
- Treat subagent or reviewer findings as claims until independently verified.
- If multiple models or subagents are unavailable or disallowed by the current environment, run a distinct second-pass review with a different role lens and disclose that true multi-model review was not performed.

Do not name fixed model SKUs as permanent requirements. Treat the live model roster exposed by the harness as the source of truth.

## Protocol Selector

Apply these protocols based on task shape. More than one may apply.

| Task condition | Apply | What to do |
| --- | --- | --- |
| Any non-trivial task | `learning.md` | Capture what was learned, where it belongs, and whether it invalidates prior assumptions. |
| Any claim that something is missing, broken, dead, absent, or impossible | `verifying-claims.md` | Require exact search evidence and triangulate before acting or reporting it as fact. |
| Any implementation with 3+ tasks, new files, multi-layer changes, or subagent execution | `plan-review.md` | Review the plan before execution with a different persona and different model. |
| Any production code, logic change, new file, refactor, deploy, security rule, auth, PII, public API, or domain logic change | `code-review.md` | Get independent review after implementation. Match reviewer domain to the change. |
| Any new module, service, collection, public API, persisted data model, cross-cutting pattern, scaling concern, UX flow, or important architectural choice | `design-first.md` | Answer the design questions before implementation; create a lightweight design note if required. |
| Any user-facing feature or behavior that could exist on more than one platform | `cross-platform-parity.md` | Decide platform scope up front and document intentional divergence. |
| Any change with runnable tests, builds, linters, type checks, deploy checks, or known manual gaps | `verification-toolchain.md` | Choose right-time verification: run the cheapest relevant check at meaningful checkpoints, avoid needless repeated expensive runs, and state anything that was deferred or could not be verified. |
| Any dispatch, review assignment, deep analysis, high-stakes decision, or error-finding pass | `model-selection.md` | Choose model tier intentionally and enforce reviewer model diversity. |
| Any task execution, plan, review, or multi-step work | Team assignment guidance from `team-management` when available | Assign each task to the best-fit team member or group before work begins; report the assignment in the output. |
| Any non-trivial work, even if the user did not ask for review | Review-cycle assessment | Decide whether plan, design, code, security/safety, domain, parity, or verification review is required and run or disclose the result. |

If a protocol would add ceremony without improving the result, note why it does not apply. If skipping a normally required protocol, make that explicit.

## Default Workflow

1. Classify the task using the protocol selector.
2. Internally assess whether a review cycle is needed. Use the task shape and protocol selector; do not depend on the user asking for review.
3. Read the full referenced protocol files for every selected protocol when the task is non-trivial or the rule details matter.
4. Inspect `management/personas/` when present and assign every task to the best-fit team member or group before work begins. If no current team member is a good fit and editing personas is in scope, use team-management guidance to create the missing persona first; otherwise mark the staffing gap clearly.
5. If personas are relevant, use the appropriate team member lens while doing the work.
6. Before implementation, apply design-first and plan-review gates when triggered.
7. During implementation, verify negative claims before acting on them.
8. After a cohesive implementation slice, run the relevant verification toolchain and code review gates when triggered. Time verification intelligently: use narrow checks while iterating, then broader checks before commit, push, deploy, or final completion claims.
9. Before final response, capture durable learnings in the right place or state that no durable learning was found.
10. Review the selected protocols themselves: note any ambiguity, missing trigger, weak verification path, or protocol gap discovered while working.
11. Report only verified facts as facts; mark unverified review findings or blocked validation clearly.

## Review Cycle Assessment

At intake, decide whether the work needs a review cycle. The user does not need to ask for it.

Run a review cycle when the work includes:

- A non-trivial implementation plan, new files, multi-step execution, or multi-layer change.
- Production code, logic changes, refactors, deployments, public APIs, or shared domain logic.
- Security, auth, PII, billing, safety, hardware control, BLE/FTMS, or other high-stakes behavior.
- UX flows, accessibility, empty/error states, or user-facing behavior across platforms.
- Architecture, persisted data models, new services, new collections, scale/cost implications, or cross-cutting patterns.
- Ambiguous requirements where a different persona or model could expose hidden risk.

If the environment permits independent reviewers or subagents, use a different persona and different model from the author for the review. If that is unavailable or not allowed, run a separate self-review pass with a different role lens and disclose that the review was internal rather than independent.

For small, low-risk tasks, it is acceptable to conclude that no review cycle is needed. Still record the decision briefly in the final output.

## Required Output

Every final answer produced under this skill must include these items, scaled to the size of the task:

- `Task ownership`: which team member or group handled each task, and why they were the right fit. For tiny tasks, one concise owner line is enough.
- `Multiple team members`: when more than one team member was used, state each member's role in the work and why a group was better than a single owner.
- `Review cycle`: whether review was needed, which type was run, who reviewed or what role lens was used, and whether it was independent or internal.
- `Protocols used`: list the protocols applied and what each contributed. If a normally relevant protocol was skipped, state why.
- `Verification`: summarize tests, builds, reviews, searches, or manual checks performed, plus any blocked validation.
- `Protocol observations`: identify where the current protocols may need strengthening, clarification, or expansion. If no protocol issue was observed, say so briefly.
- `Protocol update offer`: when a protocol improvement is identified, offer to update the affected protocol file or skill guidance.

Prefer a compact report for simple tasks and a short table for multi-task work.

## Protocol Summaries

### `learning.md`

Use on every non-trivial task. Ask what was learned, where it belongs, and what prior belief it invalidates. Durable learnings belong in code comments, project docs, decisions, data structure docs, memory, personas, protocols, or conventions depending on type.

### `code-review.md`

Use after non-trivial production changes. Reviewer must be a different persona and different model from the author when available. Review correctness, alignment, boundaries, parity, safety, tests, verification evidence, docs sync, and learnings.

### `plan-review.md`

Use before executing non-trivial plans. Mandatory for plans with 3+ tasks, new files, motion-capable equipment, BLE/FTMS, UX flow changes, Firestore/auth/PII, grade or derived-metric changes, and cross-platform work. Review plan correctness, dependency order, scope discipline, missing pieces, assumptions, safety, testability, and alignment.

### `design-first.md`

Use before important changes and any change that reshapes the system. Ask what the change touches, whether it changes system shape, flexibility cost, maintenance cost, and cost-at-scale. Require design review for new modules, services, collections, public APIs, persisted data models, cross-cutting patterns, and material scale or cost implications.

### `cross-platform-parity.md`

Use for user-facing behavior across clients. Decide platform scope before coding, default to all applicable clients, and document divergence when platform capability, idiom, audience, or hardware differs. Shared business logic belongs in shared core layers where available.

### `model-selection.md`

Use whenever assigning agents, reviewers, or deep analysis work. Match model strength to task risk and complexity. Use cheaper scouts for bounded search, implementation-focused models for code execution and review, and flagship reasoning for architecture, security, domain-heavy, or ambiguous decisions. Always prefer reviewer model diversity for non-trivial work.

### `verifying-claims.md`

Use whenever a finding says something is missing, broken, absent, dead, or not implemented. Negative claims require search evidence: what was searched, where, and what came back. Triangulate with a different tool before turning the claim into a blocker or action.

### `verification-toolchain.md`

Use to decide what can be tested directly and when the signal is worth the runtime. Prefer exact project commands from the live repo's protocol file when present. Use targeted checks during iteration, avoid repeatedly rerunning expensive suites without a new reason, and run broader validation before commit, push, deploy, or completion claims. If validation is blocked by unavailable hardware, credentials, SDKs, or environment limits, say so plainly.

## Bundled References

Full protocol source snapshots are available under [references/protocols](references/protocols/):

- [README.md](references/protocols/README.md)
- [learning.md](references/protocols/learning.md)
- [code-review.md](references/protocols/code-review.md)
- [plan-review.md](references/protocols/plan-review.md)
- [design-first.md](references/protocols/design-first.md)
- [cross-platform-parity.md](references/protocols/cross-platform-parity.md)
- [model-selection.md](references/protocols/model-selection.md)
- [verifying-claims.md](references/protocols/verifying-claims.md)
- [verification-toolchain.md](references/protocols/verification-toolchain.md)
