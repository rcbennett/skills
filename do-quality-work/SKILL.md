---
name: do-quality-work
description: Design, implement, review, and verify maintainable changes with clear ownership, complete retirement of replaced code, proportionate testing, independent review, and scoped cleanup. Use for substantive engineering work, architecture or implementation plans, and clean repository handoffs.
---

# Do Quality Work

## Authority and outcome

Prioritize architecture and long-term maintainability. Do the smallest coherent amount of work that fully solves the requested problem; this need not be the smallest diff. Fully refactor the affected component when necessary, including retirement of replaced paths. Defer unrelated areas. If a coherent solution requires scope expansion, identify the concrete dependency and ask before expanding.

Current user instructions and higher-priority instructions govern scope and authorization. This entrypoint owns lead/worker execution, workflow selection, design/plan depth, review policy, and completion. The linked model-selection protocol owns model, effort, and runtime dispatch mechanics. Project protocols supply domain invariants, exact commands, acceptance criteria, and explicit project gates. Preserve materially stricter project gates; reconcile contradictory generic ceremony with the user's scope rather than stacking it. Bundled references describe how to perform selected work; they do not independently activate extra workflows. Use the relevant project procedure when available, otherwise the linked reference. When reviewing this skill, inspect its bundled references too.

Proceed autonomously with authorized in-scope decisions after proportionate review. Design approval means acceptance by the authorized decision owner, not an automatic request for user confirmation. Ask about material product tradeoffs, scope expansion, or irreversible consequences not already authorized. Before an approval request, prepare the concrete reviewable work that is already authorized. A request to assess or review does not itself authorize edits.

## Lead and worker execution

The top-level lead orchestrates task-specific work. Assign every bounded work packet that produces implementation, diagnosis, research, review, or an authored artifact to a suitably instructed worker when the active runtime permits that delegation. Small size, close integration, or dispatch cost alone does not transfer execution to the lead. Use a coherent packet rather than a new agent for each tool call.

The lead owns intent, scope, acceptance criteria, task decomposition, role and model selection, sequencing, coordination, inspection of returned evidence, integration decisions, and the final user response. Workers own their assigned execution and artifact changes, including corrective changes requested after review. The lead may inspect source and results to make those decisions; do not duplicate the worker's investigation or silently take over its implementation.

Before dispatch, give the worker the outcome, owned files or responsibility, relevant live evidence and instructions, constraints, decision rights, acceptance and verification requirements, expected deliverable, and escalation condition. Tell it that other agents may share the workspace and it must preserve their edits. Select model and supported effort under [model-selection.md](references/protocols/model-selection.md). A persona name supplies a lens; it is not an execution or a substitute for a sufficient brief.

This dispatch obligation applies to the top-level lead. Workers execute their assigned packets themselves and return evidence; they do not recursively apply the lead's dispatch obligation. A worker requests decomposition from the lead when a packet needs additional ownership. The lead may explicitly authorize a named nested assignment when it satisfies the same runtime constraints and has distinct useful work.

Only these direct-execution exceptions apply:

1. Direct conversation, clarification, status reporting, task coordination, and simple self-contained factual replies that require no substantive investigation or authored deliverable.
2. Deterministic read-only retrieval, inspection needed for orchestration or acceptance, and process launch, completion, or waiting for an already selected verification command. Use tools rather than a monitoring agent. This exception does not authorize authoring a patch, repair, configuration, script, or deliverable in the lead.
3. A higher-priority instruction or actual runtime constraint prevents the bounded assignment: for example no callable worker facility, a prohibited spawn, or no useful independent lead work where the runtime requires it. Do not manufacture busywork, spawn a placeholder, or create a separate user-visible task to bypass the constraint. Reuse or sequence an existing eligible worker before treating a temporary capacity limit as a blocker. If permitted direct execution is necessary to continue the authorized task, state the concrete limitation and the narrow work taken over. Preserve any unavailable required independent-review gate.
4. The lead may make a clearly mechanical local edit under [the mechanical-edit criteria](#5-review-without-diluting-judgment), with an owner check of the final diff and relevant automated checks. Stricter project gates still apply. If inspection or checks leave behavior or interface preservation uncertain, route the work through the normal worker and independent-review path before proceeding.
5. The user explicitly requests direct execution for the particular packet.

Apply the rest of this skill only where the task needs its engineering workflow. Routine delegation does not require a durable persona, plan, assignment ledger, or extra approval. Mandatory independent reviews and project evidence gates remain separate from implementation ownership.

## 1. Establish the evidence and finish line

Inspect the current artifact and retrieve only prior context that can change the approach. Identify the requested outcome, affected boundary, cheapest authoritative probe, and sufficient finish line. For consequential uncertainty, also name blocking claims, prerequisites, what invalidates evidence, and the stop condition. Keep this in working notes unless coordination requires a durable artifact.

Run the decisive probe early. If blocked, distinguish valid fallback evidence from the unavailable proof. Do not create fixtures, simulators, schemas, or harnesses before checking existing tests and the real product path; new infrastructure must answer a named question more usefully than existing evidence.

When a new user message steers ongoing work, preserve the original objective, incorporate the correction, and invalidate dependent actions or evidence as needed. Continue independent authorized work while an optional answer is pending. Ask questions one at a time with A/B/C choices when choices are useful; do not let optional questions block progress.

## 2. Choose design and planning depth

- **Bounded implementation:** reversible work inside established responsibilities with clear acceptance. Apply the lead/worker policy to choose the implementer. No durable design or plan is needed. Logic changes still require independent code review.
- **Durable plan:** material multi-module or cross-platform work, coordinated migration/deletion affecting consumers or rollback, multiple checkpoints/implementers, handoffs, or work spanning sessions. Read [implementation-planning.md](references/protocols/implementation-planning.md).
- **Architecture decision and execution plan:** material changes to ownership, public contracts, persistence, lifecycle/concurrency, shared/platform responsibility, safety/security/privacy, migration strategy, or credible scale/cost behavior. Read [design-first.md](references/protocols/design-first.md). Resolve architecture before detailed implementation tasks. A medium change may use one canonical document with design and execution sections; use separate artifacts when depth or handoffs justify them.

Use existing repository locations and templates. Otherwise use `docs/plans/` and `docs/designs/` with [implementation-plan-template.md](references/implementation-plan-template.md) and [architecture-design-template.md](references/architecture-design-template.md), deleting irrelevant sections. Simple private dead-code removal does not alone trigger a durable plan.

Keep one accountable owner and one active checkpoint, with distinct implementation and validation status. Default to two to four coherent checkpoints for coordinated work. Update at checkpoint boundaries, preserve compact receipts, and revisit design when responsibilities, contracts, authority, or the finish line materially change. Do not implement across unresolved required design or plan blockers.

## 3. Design for clear ownership and complete replacement

Trace the affected path before changing it:

```text
Changed boundary -> current callers -> state/side effect -> preserved invariant -> authoritative evidence
```

Give each policy decision, state transition, and side effect one authoritative owner. Extend the established path before adding another. Justify abstractions through current duplication, a real boundary, or a cohesive domain concept. Prefer clear names, explicit dependencies, and locally understandable control flow. Avoid forwarding-only layers, speculative frameworks, and mode switches that conceal competing responsibilities.

Consolidate duplicated knowledge when semantics and reasons to change are shared. Similar-looking code with different responsibilities can remain separate. Inventory behavior differences before choosing a canonical implementation; classify intentional adaptation, product policy, defects, and unresolved differences. Shared policy and native adaptation remain distinct; see [cross-platform-parity.md](references/protocols/cross-platform-parity.md) when relevant.

**Replacement is not complete until retirement is complete:** migrate in-scope consumers and remove the superseded implementation in the same coherent change when compatibility permits. Inspect affected registrations, flags, config, dependencies, fixtures, docs, and tests. Remove unused wrappers and commented-out code; do not retain another implementation “just in case.” Preserve valid behavior coverage while deleting implementation-specific tests that no longer apply.

Retain temporary compatibility only for a verified consumer or deployment constraint. Name the canonical policy owner, removal owner, observable removal condition, and bounded follow-up in the existing plan or issue. Documentation alone does not justify retention. A verified permanent external contract may justify an adapter with a maintenance owner and one canonical policy authority, without an invented retirement commitment.

Verify retirement through applicable callers, dynamic registration/reflection, serialized identifiers, external consumers, generated bindings, and platform configuration. No text matches alone does not prove code dead. Build or exercise the changed path after removal. Protect user data and unrelated state; code retirement is not permission for broad deletion.

## 4. Select protocols and execution resources

Select one primary protocol for the phase and at most one overlay for a distinct material risk. Additional overlays require separate decision questions. A risk lens can be included in an existing review without another agent, artifact, or vote.

| Phase or decision | Reference |
|---|---|
| Architecture or durable planning | `design-first.md`, then `implementation-planning.md` as needed |
| Plan acceptance | [plan-review.md](references/protocols/plan-review.md) |
| Code or behavior-changing configuration review | [code-review.md](references/protocols/code-review.md) |
| Runtime, build, test, release, or hardware confidence | [verification-toolchain.md](references/protocols/verification-toolchain.md) |
| Unverified missing/broken/dead claim | [verifying-claims.md](references/protocols/verifying-claims.md) |
| Task-owned workspace/document cleanup | [workspace-and-document-lifecycle.md](references/protocols/workspace-and-document-lifecycle.md) |
| Unresolved consequential tradeoff | [council-review.md](references/protocols/council-review.md) |
| Material durable choice | [decision-record.md](references/protocols/decision-record.md) |

Use [red-team.md](references/protocols/red-team.md) for a concrete adversarial risk, [pre-mortem.md](references/protocols/pre-mortem.md) for a fragile operational cutover, and [steelman.md](references/protocols/steelman.md) for a serious disputed alternative when their judgment can change the decision or the user requests them. They do not activate automatically from a public feature, API, deploy, or the word “important.”

Read [model-selection.md](references/protocols/model-selection.md) at meaningful dispatch or model-choice boundaries. It owns capability, effort, cost, context, and supported runtime selection. Apply the lead/worker policy above to execution ownership and its narrow exceptions; do not substitute a coordination-cost preference for that policy.

Explicit personas are useful for specialist judgment or multiple decision owners, not a prerequisite for routine work. Team-management owns conditional role administration. Read each selected reference once per artifact cycle and only reread for a material change.

## 5. Review without diluting judgment

**Every code change requires independent review except clearly mechanical edits.** A clearly mechanical edit is local and demonstrably preserves both behavior and interfaces with no material risk, such as fixing a typo in a non-normative comment or renaming a private local variable with verified references. Small tested logic changes are not exempt. Dependencies, CI permissions, public interfaces, persistence, concurrency, security, and device control require independent review even for one line. Behavior-changing instruction/configuration changes receive independent review too; ordinary prose edits need an owner check unless consequential policy or factual risk warrants more.

An **owner check** is the implementing agent's final-diff inspection of scope, references, intended result, unintended behavior, and obsolete remnants, plus relevant automated checks. It is not independent review. If mechanical status is uncertain, request independent review.

Default to one capable independent reviewer for a coherent change or architecture/plan decision. Add a specialist only for a distinct material risk. For actual safety, security, or irreversible boundary changes, use two independent lanes by default; a third needs a separately named uncovered risk. Competence comes before model diversity. Prefer another model when available and suitable, but do not downgrade judgment merely to obtain a different model name.

Give the reviewer the current artifact, baseline, affected boundaries, acceptance evidence, and constraints. Require evidence-backed decision-changing findings and permit a no-findings verdict. Use a compact receipt: reviewed artifact/revision, reviewer/lane, independence, verdict, evidence and gaps; add hashes or stable blocker IDs when exact handoff/follow-up requires them. Never count multiple personas in one execution as independent reviews.

Verify findings before fixing them. Resolve blockers or reject them with evidence; optional suggestions do not expand scope by default. Clearly mechanical follow-ups receive an owner check. Behavior changes get lane-specific delta review. Repeat a full review only after material scope, architecture, risk, or evidence-contract change.

After two passes with no new decisive evidence, stop repetitive review. With unresolved blockers, perform only a bounded **non-production** evidence probe outside the blocked boundary under the feasibility-spike rule in design-first, or escalate the specific decision. Review time spent and reversibility never waive blockers. If independent review is unavailable, preserve a review-pending handoff; do not present self-review as independence or silently claim completion.

## 6. Verify proportionately

Use focused behavior checks and affected builds while iterating. Tests should detect a meaningful defect or protect a changed invariant; avoid mirroring implementation or mocking away the affected boundary. Do not add tests for reversible low-impact edits without a useful behavioral question.

Before adding an expensive test or review pass, identify the decision its result could change or the acceptance claim a required gate must establish. Reuse evidence that still supports the claim for the affected path, candidate, and conditions. Repeat only checks or review lanes affected by a relevant change or failure, needed to resolve a named risk, or required for the candidate. Share this reasoning in existing working notes when useful. Separate patch failures from pre-existing failures and keep unrelated repairs outside the task.

For changed lifecycle, event, concurrency, or ownership handoffs, trace whether the side effect actually crosses the new boundary. For actuator/safety work, verify applicable device/command identity, neutralization on pause/finish/background/disconnect/ownership loss, fail-closed behavior, and no writes after the terminal fence. Preserved safety code does not prove it is still invoked.

Use deterministic local or simulator checks during development. When final confidence requires physical hardware, validate the exact final candidate; probe hardware early if feasibility is uncertain. Distinguish source inspection, simulated state, requested commands, accepted/written/acknowledged output, and measured effects. Report unavailable required runtime/physical evidence as a gap.

## 7. Reconcile and complete

Track the task-created/adopted delta, not the whole repository. At checkpoints, remove obsolete task scratch, reconcile task branches/worktrees/stashes and generated artifacts, update changed canonical docs, and close completed plans. Read workspace-and-document-lifecycle when these artifacts are involved. Before removal, verify exact targets, scope, unique-content preservation or regenerability, references, and recovery. Keep blocked work resumable and protect pre-existing user state.

For repository implementation work, completion includes integration and cleanup. Once a coherent body of work passes its required reviews and checks, commit the scoped changes, merge into the intended integration branch using repository policy, verify the merge on the remote, delete the task's feature branches locally and remotely, remove its linked worktrees, and prune stale tracking refs. The user's standing preference authorizes this ordinary task closeout without another permission request; later narrower instructions and actual repository gates still govern. A draft/open PR or finished implementation alone is not completion. Protect `main`, `release/*`, unrelated or in-progress work, and worktrees still used by another agent. This does not independently authorize a release or deployment. Follow [workspace-and-document-lifecycle.md](references/protocols/workspace-and-document-lifecycle.md) for preservation and final-state verification.

Use [learning-retrieval.md](references/protocols/learning-retrieval.md) only when prior lessons affect the work. Make one session-level learning assessment for non-trivial work under [learning.md](references/protocols/learning.md); write only surprising reusable findings within scope and active memory policy. No finding means no learning artifact. Use [after-action-review.md](references/protocols/after-action-review.md), [persona-calibration.md](references/protocols/persona-calibration.md), [playbook-library.md](references/protocols/playbook-library.md), and [team-health.md](references/protocols/team-health.md) only for their concrete triggers. Keep one canonical home and link rather than duplicating records.

Report the outcome with concise remote integration and branch/worktree cleanup evidence. If a real gate or preservation blocker prevents closeout, keep the work resumable and name the specific blocker, retained artifact, and exact next action; do not invent an approval requirement or call the task complete. Required reviews, code retirement, integration, cleanup, evidence, and current project truth determine completion; passing unit tests or a clean worktree alone do not.
