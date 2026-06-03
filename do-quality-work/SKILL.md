---
name: do-quality-work
description: Apply project quality protocols to choose the right review, design, verification, learning retrieval, learning capture, After Action Review, persona calibration, playbook, team-health, parity, model-selection, claim-checking, red-team, steelman, pre-mortem, council-review, decision-record, team-assignment, review-cycle, session-learning, slice-sizing, and reporting workflow for non-trivial work. Use when Codex is asked to do high-quality work, implement or review code, write or review plans, make important decisions, challenge plans adversarially, steelman alternatives, forecast operational failure, record durable decisions, verify claims, assess subagent findings, handle cross-platform product work, choose reviewers or models, internally decide whether a review cycle is needed, identify which team members are doing which tasks, report protocols used, assess end-of-session learnings, improve team member personas, or decide what validation is required before calling work complete.
---

# Do Quality Work

## Operating Rule

Treat quality as an execution protocol, not a final polish pass. At task intake, choose the relevant protocols, apply them while working, and report the verification that was actually performed.

When a project has its own `management/protocols/` directory, inspect and prefer those live project protocols. Otherwise use the bundled protocol references in `references/protocols/`.

Every output must include who did which task, which protocols were used, when multiple team members were used, and whether the protocols exposed any improvement opportunities.

Before meaningful work, retrieve relevant persona memories, calibration, playbooks, and project decisions so prior learning shapes the next attempt.

At the end of each prompt-level work session, assess the session as a whole for durable learnings. A work session is completing the instruction in the user's prompt, not each individual task executed inside that session. Report the learning assessment in the final session summary and update the responsible persona's memories when the learning should persist.

Durable learning capture is part of the work, not a separate favor. When a session exposes a repeatable tactic, missed protocol trigger, stale convention, durable user preference, or workflow lesson that would prevent future rework, store it in the narrowest durable artifact before the final response when permissions and scope allow: code comments for non-obvious implementation reasons, project docs for project behavior, decisions for material choices, playbooks for reusable procedures, protocols for process gaps, and skill guidance for cross-project operating rules. Do not wait for the user to ask whether to update these artifacts when the evidence is clear and the update is in scope. For persistent Codex memory, obey the active memory policy; if that policy requires explicit user instruction, write memory only after such an instruction and otherwise report the recommended memory update.

Important decisions require council review. Use [council-review.md](references/protocols/council-review.md) when choosing a direction that materially affects architecture, product behavior, safety, security, privacy, billing, platform scope, release readiness, cost, team process, or any artifact that will guide future work. The council reviews the current artifact, finds weaknesses and opportunities to do more, synthesizes input into a forward plan, and requires at least 75% of council members to agree that the plan is the best balance before it is treated as the chosen direction.

Important decisions should also preserve the reasoning that future work will need. Use [decision-record.md](references/protocols/decision-record.md) when a material choice is made, changed, or rejected in a way future agents are likely to revisit.

Do not wait for the user to explicitly ask for review. Internally assess whether the task requires a plan review, design review, code review, red-team review, steelman review, pre-mortem, security/safety review, domain review, parity review, council review, decision record, or verification review, then run the applicable cycle when the environment allows.

## Completion Commit Rule

When a task changes files in a git repository and the requested work is finished, commit the completed change before the final response. Do not leave completed work as uncommitted local changes, because dirty worktrees create confusion for later agents and for the user.

- Run the relevant verification before committing whenever the environment allows.
- Stage and commit all files changed for the task. If the user states that the dirty worktree changes are yours, treat that as authority to include them in the task commit.
- If the worktree includes changes that are clearly unrelated and not yours, do not silently mix them into the commit. Commit your scoped changes separately when possible, or ask the user only if separation is unsafe or impossible.
- If committing is blocked by failed verification, missing credentials, a non-git directory, or an explicit user request not to commit, state the blocker clearly in the final response and leave a precise status.
- After committing, report the commit hash and whether any changes remain uncommitted.

## Right-Time Verification Rule

Verification is required for confidence, but repeated verification has real time, cost, and attention costs. Be deliberate about when to run tests.

- Run the cheapest high-signal check that exercises the changed behavior.
- Prefer narrow tests, type checks, linters, or targeted builds while iterating.
- Run expensive suites at decision checkpoints: after a cohesive implementation slice, before committing or pushing, before deploys, before claiming completion, or after a fix that could have affected broad behavior.
- Do not rerun the same expensive suite after every small edit unless the edit plausibly invalidated the prior result.
- If a test fails, fix the cause and rerun the smallest relevant check first; broaden only when the fix touches shared behavior or the narrow check passes and a release/commit/deploy decision needs wider confidence.
- If verification is intentionally deferred because it would be wasteful at the current point in the work, say what was deferred, why, and when it should run.

## Slice Size And Overhead Rule

Choose work size deliberately. Quality work optimizes for net progress at acceptable risk, not for the smallest possible commit or the largest possible batch.

- At intake for non-trivial work, decide whether the right unit is a micro-slice, a cohesive capability packet, or a broader checkpoint. Name the choice when it affects time, cost, review load, or user expectations.
- Treat full review/evidence loops as costly. If the planned verification and documentation overhead is large compared with the behavior changed, batch related low- or medium-risk items into one capability packet before paying the full overhead.
- Prefer capability packets when changes share a domain, fixture set, rollback path, reviewer group, and verification envelope. Examples: a set of related API parity fixtures, several route aliases with the same side-effect model, or a family of UI states covered by the same test path.
- Use micro-slices when risk is high, blast radius is uncertain, reversibility is poor, a destructive data change is involved, the behavior crosses security/auth/PII/billing/safety boundaries, or isolating one failing behavior is necessary for diagnosis.
- Do not batch unrelated work just to reduce ceremony. A larger slice must still be reviewable, debuggable, reversible, and explainable in one coherent commit or checkpoint.
- During iteration, run targeted checks that match the current edit. Run broad verification, generated evidence, docs rollups, review cycles, and commits at the capability-packet or checkpoint boundary unless a new risk justifies doing them sooner.
- If resource limits or user availability are tight, prefer a clean safe checkpoint over starting another broad packet. If the current packet is close to done, finish and commit it; if it is still early, stop at a documented handoff.

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
| Any meaningful work with prior project or persona context | `learning-retrieval.md` | Retrieve relevant persona memories, calibration, playbooks, decisions, and stale-memory risks before starting. |
| Any non-trivial work session | `learning.md` | At session end, assess what was learned from completing the prompt, where it belongs, whether it invalidates prior assumptions, and whether persona memories need updates. |
| Any failure, surprise, regression, false blocker, missed requirement, milestone, repeated rework, or protocol gap | `after-action-review.md` | Run a blameless AAR that turns expected-vs-actual evidence into updates, owners, and memory/protocol/playbook changes. |
| Any review, task assignment, Talent Planning, repeated false positive, missed issue, noisy review, or assignment-fit problem | `persona-calibration.md` | Update evidence about persona judgment quality and use it for future routing and reviewer selection. |
| Any repeated tactic, diagnostic sequence, deploy/review recipe, or reusable lesson | `playbook-library.md` | Promote the tactic into a project or persona playbook with verification and failure modes. |
| Talent Planning, executive retrospectives, repeated collaboration failures, or staffing changes | `team-health.md` | Assess whether team conditions support learning: safety, dependability, clarity, meaning, impact, load, and learning culture. |
| Any claim that something is missing, broken, dead, absent, or impossible | `verifying-claims.md` | Require exact search evidence and triangulate before acting or reporting it as fact. |
| Any implementation with 3+ tasks, new files, multi-layer changes, or subagent execution | `plan-review.md` | Review the plan before execution with a different persona and different model. |
| Any production code, logic change, new file, refactor, deploy, security rule, auth, PII, public API, or domain logic change | `code-review.md` | Get independent review after implementation. Match reviewer domain to the change. |
| Any new module, service, collection, public API, persisted data model, cross-cutting pattern, scaling concern, UX flow, or important architectural choice | `design-first.md` | Answer the design questions before implementation; create a lightweight design note if required. |
| Any user-facing feature or behavior that could exist on more than one platform | `cross-platform-parity.md` | Decide platform scope up front and document intentional divergence. |
| Any change with runnable tests, builds, linters, type checks, deploy checks, generated evidence, review overhead, or known manual gaps | `verification-toolchain.md` | Choose right-time verification and slice size: run the cheapest relevant check while iterating, batch related low/medium-risk work into coherent capability packets, run expensive checks at meaningful checkpoints, and state anything deferred or unverified. |
| Any dispatch, review assignment, deep analysis, high-stakes decision, or error-finding pass | `model-selection.md` | Choose model tier intentionally and enforce reviewer model diversity. |
| Any high-stakes, optimistic, externally visible, safety/security/privacy/billing/auth/PII/hardware-control, release, deploy, or public-claim plan | `red-team.md` | Attack the artifact for exploit paths, operational failures, hidden assumptions, missing rollback, weak observability, and abuse cases before trusting it. |
| Any important rejected alternative, controversial tradeoff, disagreement with a user proposal, or decision with plausible competing paths | `steelman.md` | Present the strongest coherent version of the alternative, the conditions where it wins, what evidence would change the decision, and which ideas should be retained. |
| Any beta, launch, deploy, migration, hardware-control, safety/security/billing/admin, public feature, or operationally fragile change | `pre-mortem.md` | Assume the work failed in production or beta; identify likely failure narratives, leading indicators, prevention, detection, rollback, and owners. |
| Any important decision or current artifact that will guide meaningful future work | `council-review.md` | Have all active team members review the artifact for weaknesses, missing risks, and opportunities to do more; synthesize a plan and confirm at least 75% agreement before moving forward. |
| Any material decision, changed direction, rejected option likely to resurface, or protocol/process decision | `decision-record.md` | Record the decision, context, alternatives, rationale, consequences, evidence, and revisit trigger in the durable project location when one exists. |
| Any task execution, plan, review, or multi-step work | Team assignment guidance from `team-management` when available | Assign each task to the best-fit team member or group before work begins; report the assignment in the output. |
| Any non-trivial work, even if the user did not ask for review | Review-cycle assessment | Decide whether plan, design, code, security/safety, domain, parity, or verification review is required and run or disclose the result. |

If a protocol would add ceremony without improving the result, note why it does not apply. If skipping a normally required protocol, make that explicit.

## Default Workflow

1. Classify the task using the protocol selector.
2. Internally assess whether a review cycle is needed. Use the task shape and protocol selector; do not depend on the user asking for review.
3. Read the full referenced protocol files for every selected protocol when the task is non-trivial or the rule details matter.
4. Use `learning-retrieval.md` before meaningful work when prior project context, personas, calibration, or playbooks may affect the session.
5. Inspect `management/personas/` when present and assign every task to the best-fit team member or group before work begins. If no current team member is a good fit and editing personas is in scope, use team-management guidance to create the missing persona first; otherwise mark the staffing gap clearly.
6. If the task has high-risk downside, optimism risk, public claims, or operational fragility, run red-team and/or pre-mortem before treating the plan as safe.
7. If the task involves a controversial direction, rejected alternative, or disagreement with a plausible proposal, run steelman before rejecting it.
8. If the task involves an important decision or a current artifact that will guide meaningful future work, run council review before treating any path as chosen.
9. If personas are relevant, use the appropriate team member lens while doing the work.
10. Choose the work unit deliberately: micro-slice, capability packet, or broader checkpoint. Consider risk, blast radius, reversibility, verification cost, documentation cost, usage/time limits, and user expectations.
11. Before implementation, apply design-first and plan-review gates when triggered.
12. During implementation, verify negative claims before acting on them and use targeted checks that match the current edit.
13. After a cohesive implementation slice or capability packet, run the relevant verification toolchain and code review gates when triggered. Time verification intelligently: use narrow checks while iterating, then broader checks before commit, push, deploy, or final completion claims.
14. Record material decisions in the durable project location when one exists.
15. Commit completed repository changes before the final response unless blocked or explicitly told not to commit.
16. Run an AAR when the session exposes a surprise, failure, repeated rework, missed requirement, false blocker, milestone lesson, or protocol gap.
17. Update calibration when reviewer quality, owner fit, false positives, missed issues, or verification gaps change trust in a persona.
18. Promote repeatable tactics into playbooks instead of leaving them buried in session summaries.
19. At the end of the prompt-level work session, before final response, assess the session as a whole for durable learnings. Do not run this after every individual subtask unless the subtask is its own user prompt. Store learnings in the right place, including the responsible persona's memories, playbooks, protocols, project docs, or skill guidance when applicable and permitted. For persistent Codex memory, follow the active memory policy; if explicit user instruction is required and absent, state the proposed memory update instead of writing it. If no durable learning was found, say so.
20. Review the selected protocols themselves: note any ambiguity, missing trigger, weak verification path, slice-size mismatch, or protocol gap discovered while working.
21. Report only verified facts as facts; mark unverified review findings or blocked validation clearly.

## Review Cycle Assessment

At intake, decide whether the work needs a review cycle. The user does not need to ask for it.

Run a review cycle when the work includes:

- A non-trivial implementation plan, new files, multi-step execution, or multi-layer change.
- Production code, logic changes, refactors, deployments, public APIs, or shared domain logic.
- Security, auth, PII, billing, safety, hardware control, BLE/FTMS, public claims, releases, deploys, or other high-stakes behavior.
- UX flows, accessibility, empty/error states, or user-facing behavior across platforms.
- Architecture, persisted data models, new services, new collections, scale/cost implications, or cross-cutting patterns.
- Ambiguous requirements where a different persona or model could expose hidden risk.

If the environment permits independent reviewers or subagents, use a different persona and different model from the author for the review. If that is unavailable or not allowed, run a separate self-review pass with a different role lens and disclose that the review was internal rather than independent.

For important decisions, run council review in addition to any narrower review cycle. Council review is not a substitute for design, plan, code, parity, safety, or verification review; it is the synthesis and agreement gate for the direction that follows from those reviews.

For important decisions with meaningful downside or serious alternatives, feed red-team, steelman, and pre-mortem findings into council review before asking for agreement.

For small, low-risk tasks, it is acceptable to conclude that no review cycle is needed. Still record the decision briefly in the final output.

## Required Output

Every final answer produced under this skill must include these items, scaled to the size of the task:

- `Task ownership`: which team member or group handled each task, and why they were the right fit. For tiny tasks, one concise owner line is enough.
- `Multiple team members`: when more than one team member was used, state each member's role in the work and why a group was better than a single owner.
- `Review cycle`: whether review was needed, which type was run, who reviewed or what role lens was used, and whether it was independent or internal.
- `Council review`: for important decisions, identify the artifact reviewed, council members, major weaknesses/opportunities found, synthesized plan, agreement count/percentage, and unresolved dissent. If council review was not run for an apparently important decision, state why.
- `Slice-size decision`: for non-trivial execution, state whether the work was handled as a micro-slice, capability packet, or broader checkpoint, and why the risk/overhead/progress balance justified that choice.
- `Protocols used`: list the protocols applied and what each contributed. If a normally relevant protocol was skipped, state why.
- `Verification`: summarize tests, builds, reviews, searches, or manual checks performed, plus any blocked validation.
- `Commit status`: include the commit hash for completed repository work, or explain exactly why committing was blocked.
- `Self-improvement updates`: summarize learning retrieval, AAR, calibration, playbook, team-health, and persona-memory updates that changed future behavior. Say none when none applied.
- `Session learnings`: state what was learned across the completed prompt-level work session, where it was stored, and which persona memories were updated. If nothing durable was learned, say that explicitly.
- `Protocol observations`: identify where the current protocols may need strengthening, clarification, or expansion. If no protocol issue was observed, say so briefly.
- `Protocol update offer`: when a protocol improvement is identified, offer to update the affected protocol file or skill guidance.

Prefer a compact report for simple tasks and a short table for multi-task work.

## Protocol Summaries

### `learning.md`

Use at the end of every non-trivial work session. Ask what was learned from completing the user's prompt, where it belongs, which prior belief it invalidates, and whether the responsible persona's memories should be updated. Durable learnings belong in code comments, project docs, decisions, data structure docs, memory, persona memories, protocols, or conventions depending on type.

### `learning-retrieval.md`

Use before meaningful work when prior project context may affect quality. Retrieve relevant persona memories, calibration, playbooks, decisions, and stale-memory risks before starting, then close the loop at session end.

### `after-action-review.md`

Use when the result differed from the plan, a failure or surprise occurred, a milestone finished, or the same failure mode repeats. Convert expected-vs-actual evidence into action items and updates to persona memories, protocols, playbooks, or docs.

### `persona-calibration.md`

Use when review quality, owner fit, false positives, missed issues, noisy findings, or verification gaps change trust in a persona. Calibration informs future task assignment and reviewer selection.

### `playbook-library.md`

Use when a tactic becomes repeatable. Store validated recipes in project or persona playbooks with applicability, steps, verification, failure modes, and review cadence.

### `team-health.md`

Use during Talent Planning, executive retrospectives, repeated collaboration failures, staffing changes, or milestones to assess whether team conditions support learning and improvement.

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

### `red-team.md`

Use when optimism is dangerous: safety, security, privacy, billing, auth, PII, hardware control, releases, deploys, public claims, migrations, and other high-risk decisions. Attack the artifact for exploit paths, abuse cases, hidden assumptions, missing rollback, weak observability, and catastrophic edge cases. Keep findings tied to evidence, likelihood, severity, mitigations, and residual risk.

### `steelman.md`

Use before rejecting a serious alternative, disagreeing with a plausible user proposal, resolving controversial tradeoffs, or finalizing important decisions with competing paths. Present the strongest coherent case for the alternative, the conditions where it wins, the evidence that would change the decision, and useful ideas to retain even when the alternative is rejected.

### `pre-mortem.md`

Use before launches, deploys, migrations, beta releases, hardware-control changes, safety/security/billing/admin work, and operationally fragile changes. Assume the work failed in production or beta, then identify failure narratives, leading indicators, detection gaps, prevention, rollback, recovery, owners, and go/no-go checks.

### `council-review.md`

Use for important decisions and current artifacts that will guide meaningful future work. All active team members review the artifact for weaknesses, risks, missing opportunities, and ways to do more. Synthesize their input into a forward plan and require at least 75% agreement that the plan is the best balance before treating it as the chosen direction.

### `decision-record.md`

Use when a material decision is made, changed, rejected, or likely to be revisited. Record the context, decision, alternatives, rationale, consequences, evidence, and revisit trigger in the durable project location when one exists; otherwise include the record in the final response and state that no durable decision location was found.

### `verifying-claims.md`

Use whenever a finding says something is missing, broken, absent, dead, or not implemented. Negative claims require search evidence: what was searched, where, and what came back. Triangulate with a different tool before turning the claim into a blocker or action.

### `verification-toolchain.md`

Use to decide what can be tested directly, when the signal is worth the runtime, and what slice size makes the verification overhead worthwhile. Prefer exact project commands from the live repo's protocol file when present. Use targeted checks during iteration, batch related low/medium-risk work into capability packets when full evidence loops would dominate progress, avoid repeatedly rerunning expensive suites without a new reason, and run broader validation before commit, push, deploy, or completion claims. If validation is blocked by unavailable hardware, credentials, SDKs, or environment limits, say so plainly.

## Bundled References

Full protocol source snapshots are available under [references/protocols](references/protocols/):

- [README.md](references/protocols/README.md)
- [learning.md](references/protocols/learning.md)
- [learning-retrieval.md](references/protocols/learning-retrieval.md)
- [after-action-review.md](references/protocols/after-action-review.md)
- [persona-calibration.md](references/protocols/persona-calibration.md)
- [playbook-library.md](references/protocols/playbook-library.md)
- [team-health.md](references/protocols/team-health.md)
- [code-review.md](references/protocols/code-review.md)
- [plan-review.md](references/protocols/plan-review.md)
- [design-first.md](references/protocols/design-first.md)
- [cross-platform-parity.md](references/protocols/cross-platform-parity.md)
- [model-selection.md](references/protocols/model-selection.md)
- [red-team.md](references/protocols/red-team.md)
- [steelman.md](references/protocols/steelman.md)
- [pre-mortem.md](references/protocols/pre-mortem.md)
- [council-review.md](references/protocols/council-review.md)
- [decision-record.md](references/protocols/decision-record.md)
- [verifying-claims.md](references/protocols/verifying-claims.md)
- [verification-toolchain.md](references/protocols/verification-toolchain.md)
