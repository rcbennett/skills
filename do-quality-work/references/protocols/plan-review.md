# Protocol: Plan Review

**Principle:** A bad plan produces bad code cheaply *and* bad code expensively. Plans get reviewed *before* execution, not after. The reviewer is a different persona *and* a different model than the plan author. For plans that span concerns (architecture + safety + UX), review in parallel with multiple personas.

## When review is required

| Plan type | Review required? | Personas |
|---|---|---|
| Implementation plan with 3+ tasks or any new file | Yes | Morgan (architecture) + domain-appropriate personas |
| Any plan that drives motion-capable equipment, writes BLE control points, or touches FTMS | Yes | Morgan + **Riley** (safety) mandatory |
| Any plan that changes user-facing flows, empty/error states, or accessibility | Yes | Morgan + **Kenji** (UX) mandatory |
| Any plan that changes Firestore rules, auth, or PII handling | Yes | **Riley** mandatory, Diego recommended |
| Plans modifying the grade pipeline or derived metrics | Yes | **Dr. Voss** mandatory, Linnea recommended |
| Cross-platform plans (iOS + macOS + Android + tvOS) | Yes | Morgan + **all affected platform engineers** |
| Back-of-the-envelope plans or single-file doc edits | No (Atlas spot-checks) | — |

"Non-trivial" means: any plan with a file structure diagram, any plan that spawns subagent execution, any plan that touches more than one layer (shared + platform, or client + backend). When in doubt, review.

## Reviewer selection rules

1. **Different persona from the plan author.** Atlas doesn't rubber-stamp Atlas.
2. **Different model from the plan author.** If Atlas wrote the plan on a flagship reasoning model, at least one reviewer should come from a different model, usually from a different tier. See [model-selection.md](model-selection.md).
3. **Domain-appropriate.** At least one reviewer's "Owns" or "Consult when" must intersect the plan's scope.
4. **Parallel when possible.** If the plan spans concerns, dispatch all needed personas simultaneously — don't serialize reviews unless later reviewers depend on earlier findings.
5. **Add a safety reviewer when motion or PII is involved.** Non-negotiable.

## What plan reviewers look for (in order)

Plan reviewers are briefed to check these — not code quality (nothing is written yet), but **plan quality**:

1. **Correctness of specified code.** Do types, method signatures, and property names agree across tasks? Does the code in each snippet actually compile as written?
2. **Dependency ordering.** Are tasks in the right order? Does Task N depend on something Task N+2 defines?
3. **Scope / YAGNI.** Is the plan building more than needed? Premature abstractions? Speculative flexibility? Test seams that leak into production?
4. **Missing pieces.** Cancellation plumbing, resource teardown, error paths, logging, deletion of replaced code.
5. **Assumptions vs. reality.** Does the plan assume APIs or singletons that don't exist? Is any "existing type" actually present?
6. **Safety.** If the plan drives hardware, can it safely halt? If it touches auth/PII, does it respect rules?
7. **Testability.** Are the tests written in the plan actually verifying behavior, or just mocking their way to green?
8. **Alignment.** Matches `decisions.md`, existing design notes, and `guidelines.md`?

Plan reviewers explicitly look for **gold-plating** — complexity the plan adds beyond MVP intent — and call it out.

## Review output shape

Plan reviewers return:

- **Verdict:** SHIP / SHIP WITH FIXES / REWRITE.
- **Blockers:** issues that will produce wrong or non-compiling code. Must fix before execution begins.
- **Concerns:** issues worth fixing before execution but not strictly blocking (logging, teardown, error surfacing).
- **Red flag hunt (scope discipline):** anything the reviewer thinks is gold-plating or premature abstraction.
- **Praise (when warranted):** what the plan gets right.

Low-confidence concerns are marked as such. "This looks correct, LGTM" is a valid response for simple plans — reviewers don't manufacture findings.

## Receiving review

Plan author:

- **Blockers must be fixed before any implementer subagent is dispatched.** No exceptions.
- **Concerns are fixed by default.** Decline only with a reason recorded in the plan.
- **Scope/red-flag items** get resolved by removing complexity, not by arguing it's justified.
- **Re-review is required** if blockers were non-trivial fixes. Light concerns don't require re-review.
- If the plan needs a REWRITE verdict, discard and start over — do not patch an incoherent plan.

Authors who reflexively "fix" every flag without thinking are as broken as authors who dispatch despite blockers. Atlas watches for both.

## Atlas's role

- Dispatches reviewer(s) **before** the first implementer subagent, not alongside.
- Picks personas and models per the matrix above.
- Summarizes review findings honestly to Rob — does not paper over concerns.
- Blocks execution if any blocker is unfixed, even under time pressure.
- If multiple reviewers disagree, arbitrates or escalates to Rob.
- Tracks plan-review quality: a reviewer who green-lights a plan that then produces visible bugs gets their brief tightened.

## Integration with other protocols

- **[code-review.md](code-review.md)** reviews code after it's written. This protocol reviews the plan before. Both happen.
- **[design-first.md](design-first.md)** reviews designs, which are the layer above plans. A plan that disagrees with its own design is a rewrite, not a fix.
- **[verifying-claims.md](verifying-claims.md)** applies inside review: a reviewer who asserts "this won't compile" should cite the line. A reviewer who says "there's a Sendable issue" should name the type.

## Minimum cadence

- **Always** for plans matching the matrix above.
- **Never skip** because "the plan is simple" or "we're in a hurry." If the plan is simple, the review is also simple and cheap.
- **Never bypass** by executing "just the first task" before review lands. Plans are reviewed as wholes; partial execution violates the protocol.
