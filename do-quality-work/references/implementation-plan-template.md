# <Implementation Plan Title>

> Delete sections that do not apply. Keep this document as an execution control surface, not a transcript.

## Contents

- [Plan Review Receipt](#plan-review-receipt)
- [Evidence Preflight](#evidence-preflight)
- [Architecture Contract](#architecture-contract)
- [Progress Rules](#progress-rules)
- [Progress Summary](#progress-summary)
- [Implementation Checkpoints](#implementation-checkpoints)
- [Deferred Work](#deferred-work)
- [Definition Of Done](#definition-of-done)

**Status:** planning
**Owner:**
**Code baseline:**
**Reviewed plan revision:**
**Scope:**
**Finish line:**
**Design/decision:** link or `not required`

## Plan Review Receipt

**Reviewed plan revision:**
**Linked design revision:**
**Reviewer and lane:**
**Independence/model status:**
**Verdict:**
**Blocking finding IDs:** none

## Evidence Preflight

**Decision question:**

| Blocking claim | Cheapest authoritative probe | Result | Prerequisite/blocker | Invalidated by |
|---|---|---|---|---|
| | | | | |

**Stop condition:**

## Architecture Contract

### Current state

Link the canonical design/current-system evidence and summarize only the execution-critical facts needed to sequence this plan.

### Target state

Link the approved design revision and list only the boundaries and invariants this plan must operationalize; do not restate the architecture.

### Changed-boundary map

| Changed seam | Current callers | Side effect | Preserved invariant | Authoritative evidence |
|---|---|---|---|---|
| | | | | |

### Invariants

- INV-1:

### Non-goals and deferred work

- _None._

## Progress Rules

- Keep one checkpoint active at a time.
- Parallel tasks inside that checkpoint require explicit non-overlapping boundaries and one integration owner.
- Update this document at checkpoint boundaries.
- Record implementation and validation status separately.
- Stop and return a design delta when a material architecture assumption changes.
- Admit new work only when it blocks the active checkpoint or final acceptance.

## Progress Summary

| Checkpoint | Implementation | Validation | Base/final revision | Result, blocker, or next action |
|---|---|---|---|---|
| 0. Plan and scope lock | complete | complete | | |
| 1. First working slice | pending | not started | | |
| 2. <Second working slice or remaining migration> | pending | not started | | |
| 3. <Convergence, deletion, or final validation> | pending | not started | | |

## Implementation Checkpoints

## Checkpoint 0 — Plan And Scope Lock

**Objective:** establish evidence, architecture, scope, and an executable plan before production edits.

- [ ] C0.1 Record the code baseline and confirm unrelated work is excluded.
- [ ] C0.2 Complete the evidence preflight.
- [ ] C0.3 Approve or link the architecture design when required.
- [ ] C0.4 Inventory the changed seams and current callers.
- [ ] C0.5 Review the plan and resolve blocking findings.

**Exit gate:** the first implementation checkpoint is runnable and no required design or plan blocker remains.

## Checkpoint 1 — First Working Slice

**Objective:** prove the target architecture through one end-to-end path.

### Implementation

- [ ] C1.1

### Acceptance

- [ ] C1.A1

**Rollback:**

**Exit gate:**

**Receipt:** base/final revision, changed files, commands/results, runtime evidence, remaining gap, next action.

## Checkpoint 2 — <Second Working Slice Or Remaining Migration>

**Objective:** state the next coherent behavior, migration, or convergence result.

### Implementation

- [ ] C2.1

### Acceptance

- [ ] C2.A1

**Rollback:**

**Exit gate:**

**Receipt:** base/final revision, changed files, commands/results, runtime evidence, remaining gap, next action.

## Checkpoint 3 — <Convergence, Deletion, Or Final Validation>

**Objective:** state the final convergence, deletion, and validation result that applies to this work.

### Deletion and static audit

- [ ] C3.1

### Final acceptance

- [ ] C3.A1

**Rollback:**

**Candidate gate:**

**Physical/manual gate:** `not required`, `awaiting validation`, or exact candidate procedure.

**Receipt:** final revision, changed files, commands/results, runtime/physical evidence, remaining gap, next action.

## Deferred Work

- _None._

## Definition Of Done

- [ ] The approved architecture and ownership boundaries are present.
- [ ] Superseded paths are deleted or intentionally documented.
- [ ] Required automated, runtime, and physical evidence is current for the final candidate.
- [ ] Decisions and project truth documents are reconciled.
- [ ] Checkpoint changes are reviewable/revertible and repository state is reconciled for handoff.
