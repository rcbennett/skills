# Protocol: Implementation Planning

**Principle:** A durable implementation plan is the control surface for complex work. It translates an approved direction into sequenced, observable, reversible checkpoints and stays current as agents hand work off.

## Contents

- [Choose the right planning depth](#choose-the-right-planning-depth)
- [Plan location and identity](#plan-location-and-identity)
- [Required plan structure](#required-plan-structure)
- [Checkpoint quality](#checkpoint-quality)
- [Plan lifecycle](#plan-lifecycle)
- [Workspace and document lifecycle](#workspace-and-document-lifecycle)
- [Status model](#status-model)
- [Review and execution handoff](#review-and-execution-handoff)
- [Failure signals](#failure-signals)

## Choose the right planning depth

Use the lightest artifact that can safely coordinate the work:

- **No durable plan:** Use for a narrow, local, reversible change with one obvious owner and acceptance path.
- **Implementation plan:** Use when material work spans modules or platforms, needs multiple checkpoints, production implementers, or planned handoffs, changes an ownership boundary, requires coordinated migration/deletion, carries a material validation gate, or is expected to continue across sessions. Read-only subagents or reviewers do not by themselves trigger a durable plan.
- **Architecture design plus implementation plan:** Use when `design-first.md` triggers. Approve the target architecture before turning it into implementation tasks.

Do not use a long checklist to compensate for an unresolved design decision or unavailable acceptance environment.

## Plan location and identity

Follow the repository's existing plan convention. If none exists, use:

```text
docs/plans/<YYYY-MM-DD>-<short-slug>.md
```

Record:

- status;
- accountable owner;
- code baseline;
- current reviewed plan revision or content hash;
- scope and explicit exclusions;
- finish line; and
- linked design or decision record when architecture review was required.

Create the plan before production implementation begins. A plan written retrospectively is a receipt, not evidence of advance control.

Link canonical design, decision, requirements, and evidence artifacts instead of restating them. The plan owns execution status and checkpoint history; it is not another architecture specification.

## Required plan structure

Use the project template when one exists. Otherwise start from [../implementation-plan-template.md](../implementation-plan-template.md) and delete irrelevant sections.

Keep these elements:

1. **Decision and evidence contract**
   - decision question;
   - blocking claims;
   - cheapest authoritative probes and results;
   - prerequisites and blockers;
   - invalidation condition;
   - stop condition.
2. **Architecture contract**
   - current state and ownership;
   - approved target shape or linked design;
   - changed-boundary map;
   - preserved invariants;
   - non-goals and deferred work.
3. **Execution contract**
   - two to four implementation checkpoints by default;
   - one active checkpoint at a time;
   - discrete task IDs;
   - allowed or expected touch points;
   - checkpoint acceptance, rollback, and exit gate.
4. **Progress control**
   - compact progress summary;
   - separate implementation and validation status;
   - base/final revisions;
   - evidence paths and blockers;
   - next action.
5. **Completion contract**
   - final authoritative validation;
   - deletion/static ownership audit where applicable;
   - documentation/decision reconciliation;
   - scoped source-control and temporary-artifact reconciliation;
   - active, durable, generated, and historical document disposition; and
   - clean handoff and rollback state.

## Checkpoint quality

Default to two to four checkpoints after any planning/setup checkpoint. Each checkpoint should produce one coherent result that can be reviewed and reverted.

Every task must do at least one of these:

- enable the first or next working end-to-end path;
- protect a high-severity invariant;
- produce authoritative evidence for a blocking claim; or
- delete superseded behavior.

Use the fewest meaningful tasks that make the checkpoint executable. Treat twelve tasks as a soft maximum; split or simplify a checkpoint that needs more. Put command details and acceptance observations under the task they verify rather than expanding them into unrelated process checklists.

The first implementation checkpoint should prove a walking skeleton through the changed architecture. Do not make its only result interfaces, fixtures, or scaffolding.

When materially different platform constraints can alter the shared architecture, probe the most constrained platform during design and exercise a representative adapter from each platform family in the first or earliest viable working slice.

## Plan lifecycle

- Keep one accountable plan owner.
- Multiple implementers may work within the one active checkpoint when their task boundaries and integration owner are explicit; do not activate several checkpoints in parallel.
- Update the progress summary and active checkpoint at checkpoint boundaries, not after every small edit.
- Close a checkpoint with a compact receipt: objective, changed files, acceptance commands/results, runtime or physical evidence, workspace/document disposition, remaining gap, and next action.
- Collapse completed detail to receipts when the plan becomes difficult to scan. The plan is not a transcript or evidence dump.
- Preserve stable task and blocker IDs so later agents can perform narrow handoffs and delta reviews.
- Treat editorial changes and receipt updates as non-design changes.
- Re-review only the affected lane when a task, acceptance command, or local checkpoint detail changes.
- Return to architecture design when ownership, public interfaces, data flow, persistence, safety/security boundaries, or the finish line changes materially.
- Start a linked corrective plan when newly discovered work establishes a different finish line or architecture boundary. Do not indefinitely append new projects to a completed plan.

## Workspace and document lifecycle

Read [workspace-and-document-lifecycle.md](workspace-and-document-lifecycle.md) when the plan creates or adopts source-control state, temporary/generated artifacts, or multiple work documents.

Record only the task-owned or task-adopted delta:

- baseline branch/revision and relevant pre-existing state that must be protected;
- task-created branches, worktrees, stashes, untracked/temp artifacts, and their retirement conditions;
- active control documents and their status/next action;
- durable source-of-truth documents the checkpoint must maintain;
- generated evidence or deliverables and their provenance/retention; and
- completed or superseded work artifacts to close and archive under the repository convention.

Reconcile this delta at checkpoint boundaries. A retained item must have a continuing purpose, owner, and exact next action. Do not require a globally empty repository or move unrelated state into the plan.

When a plan completes, record its final receipt and transition it from active control to a completed historical artifact. Archive it only after durable facts, decisions, and links are reconciled. A blocked plan stays active with a preservation packet; it is not terminally cleaned or archived.

## Status model

Track implementation and validation independently.

Implementation status:

- `pending`
- `in progress`
- `software complete`
- `blocked`
- `complete`

Validation status:

- `not started`
- `partial`
- `awaiting runtime validation`
- `awaiting physical validation`
- `failed`
- `blocked`
- `complete`

Do not call the overall plan complete until its required validation state is complete. Do not leave software-complete work ambiguously marked `in progress`.

## Review and execution handoff

If architecture design was required:

1. Approve the design under `design-first.md`.
2. Record the material decision.
3. Create the implementation plan from the approved boundaries.
4. Review the plan under `plan-review.md`.
5. Begin the first working checkpoint only after blocking plan findings are resolved.

If architecture design was not required, create and review the implementation plan directly when the durable-plan trigger applies.

Reviewers verify that the plan implements the approved architecture rather than quietly redesigning it. Implementers stop and return a design delta when reality invalidates a material assumption.

## Failure signals

- Production code starts before a required plan exists.
- A plan lists classes and APIs but cannot explain the current architecture or preserved invariants.
- Several agents edit different checkpoints simultaneously.
- The first checkpoint produces only scaffolding.
- Checkboxes close without executed acceptance evidence.
- A plan grows through repeated incident addenda after its original finish line is complete.
- The summary, checkpoint status, branch, or reviewed plan revision disagrees with the current artifact.
- Unique task work remains only in an unexplained local branch, worktree, stash, or untracked file.
- Cleanup removes or rewrites pre-existing state that the task did not own.
- A completed plan remains active-looking, or generated evidence competes with canonical project truth.
- Durable designs, READMEs, requirements, runbooks, decisions, or project-state documents drift behind the implemented result.
