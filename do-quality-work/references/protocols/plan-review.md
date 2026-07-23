# Protocol: Plan Review

**Principle:** Review the current durable plan only deeply enough to make the first safe working slice executable while preserving the approved architecture. Evidence, implementation, and deletion of obsolete paths matter more than speculative completeness.

## Contents

- [When review is required](#when-review-is-required)
- [Reviewer selection rules](#reviewer-selection-rules)
- [What plan reviewers look for](#what-plan-reviewers-look-for-in-order)
- [Review output shape](#review-output-shape)
- [Receiving review](#receiving-review)
- [Integration with other protocols](#integration-with-other-protocols)
- [Minimum executable shape](#minimum-executable-shape)

## When review is required

| Plan type | Review required? | Personas |
|---|---|---|
| Multi-module implementation or refactor plan | Yes | One architecture/delivery reviewer |
| Motion-capable equipment, BLE/FTMS control, auth, security, PII, billing, or destructive behavior | Yes | Architecture/delivery reviewer + one safety/security specialist |
| Grade pipeline, derived metrics, or specialized domain math | Yes | One domain reviewer; add architecture only if boundaries change |
| Cross-platform or shared/platform-boundary plan | Yes | One architecture/parity reviewer; add one affected-platform specialist only for a distinct platform risk |
| Narrow reversible implementation with an obvious path | Lightweight owner review | Add an independent reviewer only if a material risk is present |
| Back-of-the-envelope plans or single-file doc edits | No | — |

"Non-trivial" means the plan changes production behavior across modules or layers, changes a durable boundary, or protects a high-severity invariant. The number of bullets, existence of a new file, or use of subagents does not by itself make a plan high risk.

Before review, complete the decisive-evidence preflight:

- decision question;
- blocking claims;
- cheapest authoritative probe and result;
- prerequisites and blockers;
- invalidation condition; and
- stop condition.

Do not compensate for a blocked authoritative probe with a larger speculative plan.

When `implementation-planning.md` requires a durable plan, review that repository artifact rather than a chat-only summary. Confirm that it records the code baseline, reviewed plan revision, finish line, current checkpoint, implementation/validation status, and linked approved design when `design-first.md` triggered.

## Reviewer selection rules

1. **Default to one architecture/delivery reviewer.**
2. **Add one specialist only for a distinct domain, safety, security, or platform risk.** For an actual safety, security, or irreversible boundary change, use two reviewers total by default. A third requires a separately named material risk that neither lane owns.
3. **Partition lanes.** Do not ask multiple reviewers to repeat the same full-plan scan.
4. **Use model diversity deliberately.** Prefer a different-model review for initial architecture decisions; require a second different-model reviewer only for actual safety, security, or irreversible boundary changes. See [model-selection.md](model-selection.md).
5. **Use personas only when decision rights or specialist judgment matter.** A named role is not a substitute for independent execution.

## What plan reviewers look for (in order)

Plan reviewers are briefed to check these — not code quality (nothing is written yet), but **plan quality**:

1. **Evidence sufficiency.** Did the preflight answer the blocking claims with the cheapest authoritative probes?
2. **Architecture readiness.** Was design performed when triggered, and does the plan preserve the approved responsibilities, contracts, invariants, migration, and non-goals?
3. **Plan control integrity.** Is the artifact current, does it have one active checkpoint, and are implementation and validation status distinct?
4. **Workspace and document lifecycle.** Does the plan distinguish task-owned from pre-existing state, keep durable truth current, and give branches, worktrees, stashes, temporary/generated artifacts, and completed work documents safe dispositions?
5. **First working path.** Can the first checkpoint produce an end-to-end result instead of infrastructure without behavior?
6. **Changed-boundary map.** For refactors, does the plan show `changed seam -> current callers -> side effect -> preserved invariant -> authoritative evidence`?
7. **Dependency ordering.** Does each checkpoint enable the next, and can obsolete paths be removed promptly?
8. **Scope / YAGNI.** Are abstractions, fixtures, schemas, and harness changes admitted by a named unanswered decision question?
9. **Missing pieces.** Cancellation, teardown, error paths, ownership transfer, observability, rollback, and deletion of replaced code.
10. **Safety.** Does the plan verify the side effect across every changed lifecycle, event, concurrency, or adapter handoff?
11. **Testability.** Do checks exercise behavior at the changed boundary instead of mocking around it?
12. **Alignment.** Does the plan match current decisions and explicit user constraints?

Plan reviewers explicitly look for **gold-plating** — complexity the plan adds beyond MVP intent — and call it out.

## Review output shape

Plan reviewers return:

- **Review receipt:** plan path/hash, code baseline, linked design revision when applicable, reviewer lane, independence/model status, preflight status, and stable blocker IDs.
- **Verdict:** SHIP / SHIP WITH FIXES / REWRITE.
- **Blockers:** issues that make the plan incorrect, unsafe, non-executable, architecturally inconsistent, or unable to reach its finish line. Must fix before execution begins.
- **Concerns:** issues worth fixing before execution but not strictly blocking (logging, teardown, error surfacing).
- **Red flag hunt (scope discipline):** anything the reviewer thinks is gold-plating or premature abstraction.
- **Praise (when warranted):** what the plan gets right.

Low-confidence concerns are marked as such. "This looks correct, LGTM" is a valid response for simple plans — reviewers don't manufacture findings.

## Receiving review

Plan author:

- **Blockers must be fixed before any implementer subagent is dispatched.** No exceptions.
- **Concerns are fixed by default.** Decline only with a reason recorded in the plan.
- **Scope/red-flag items** get resolved by removing complexity, not by arguing it's justified.
- **Editorial changes need no re-review.** Lane-specific changes need only a delta review from that lane. Full re-review is required only when scope, architecture, safety, or the evidence contract changes.
- **Material architecture changes return to design review.** Do not resolve them by adding implementation tasks to the plan.
- If the plan needs a REWRITE verdict, discard and start over — do not patch an incoherent plan.

Authors who reflexively "fix" every flag without thinking are as broken as authors who dispatch despite blockers. Atlas watches for both.

After two review passes without new runtime or authoritative evidence, stop reviewing. Implement the smallest reversible slice that can produce the missing evidence, or escalate the specific unresolved decision.

## Atlas's role

- Runs the decisive-evidence preflight before detailed review.
- Dispatches only the reviewer lanes that can change the decision.
- Picks personas and models per the matrix above without manufacturing extra votes from role lenses.
- Summarizes review findings honestly to Rob — does not paper over concerns.
- Blocks execution if any blocker is unfixed, even under time pressure.
- If multiple reviewers disagree, arbitrates or escalates to Rob.
- Tracks plan-review quality: a reviewer who green-lights a plan that then produces visible bugs gets their brief tightened.

## Integration with other protocols

- **[code-review.md](code-review.md)** reviews code after it's written. This protocol reviews the plan before. Both happen.
- **[implementation-planning.md](implementation-planning.md)** defines when the durable plan is required and how it is maintained.
- **[workspace-and-document-lifecycle.md](workspace-and-document-lifecycle.md)** governs task-owned repository state, document authority, archival, and safe closeout.
- **[design-first.md](design-first.md)** approves the architecture above the plan. A plan that disagrees with its design needs a design delta or rewrite, not a quiet fix.
- **[verifying-claims.md](verifying-claims.md)** applies inside review: a reviewer who asserts "this won't compile" should cite the line. A reviewer who says "there's a Sendable issue" should name the type.

## Minimum executable shape

- Default to two to four checkpoints.
- Require each task to enable the first working path, protect a high-severity invariant, or delete superseded behavior.
- Use stable task IDs and separate implementation from validation status.
- Require a scoped closeout that preserves unique work, reconciles durable truth, and retires completed task artifacts.
- Prefer focused checks during implementation and one broader verification pass at the packet boundary.
- For hardware-dependent behavior, use deterministic simulator or local-transport checks during development and one physical pass against the exact final candidate revision unless physical feasibility is the unresolved question.
