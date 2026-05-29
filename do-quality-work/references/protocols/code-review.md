# Protocol: Code Review

**Principle:** No non-trivial change lands without at least one independent viewpoint. The reviewer is a different persona *and* a different model than the author. Different minds see different bugs.

## When review is required

| Change type | Review required? |
|---|---|
| Production code in any client, SharedCore, or Cloud Functions | Yes |
| Security rules, auth config, or anything touching PII | Yes — Riley is always a reviewer |
| Public API surface of `SharedCore` or `VideoGPSCore` | Yes — Morgan is always a reviewer |
| Grade pipeline or derived-metric changes | Yes — Dr. Voss is always a reviewer |
| Docs-only edits, typo fixes, CI-only tweaks, dependency lock refreshes | No (Atlas spot-checks) |

"Non-trivial" means: any logic change, any new file, any refactor, any deploy. When in doubt, review.

## Reviewer selection rules

1. **Different persona from the author.** Ishaan doesn't rubber-stamp Ishaan.
2. **Different model from the author.** If the author used a flagship reasoning model, the reviewer should use a different model, usually from a different tier (implementation-focused or fast-scout) when appropriate. See [model-selection.md](model-selection.md).
3. **Domain-appropriate.** Pick a reviewer whose "Owns" or "Consult when" intersects the change.
4. **Add a second reviewer when the blast radius warrants it.** Security + domain expert. Tech lead + platform engineer. Atlas decides.

The reviewer is not a single lens — Atlas frames it as "review this as Riley would" (or whichever persona), so the subagent adopts that point of view.

## What reviewers look for

Reviewers are briefed to check these in order:

1. **Correctness.** Does it do what it claims? Are edge cases handled?
2. **Alignment.** Matches `decisions.md`, `guidelines.md`, and existing patterns?
3. **Boundaries.** Shared logic in `VideoGPSCore`/`SharedCore`, not leaking into views. Platform-specific code stays in its platform.
4. **Cross-platform parity.** See [cross-platform-parity.md](cross-platform-parity.md) — is the status correctly reflected in `requirements.md` + `PROJECT_STATE.md`?
5. **Safety.** Rules, secrets, PII in logs, `Bundle.main` vs `Bundle.module`, destructive operations.
6. **Tests.** Regression test for every bug fix. Unit tests for new logic. Integration tests for UI/hardware flows when feasible.
7. **Verification evidence.** Build output, test output, or an explicit "I couldn't verify X" from the author.
8. **Docs sync.** `requirements.md`, `PROJECT_STATE.md`, `decisions.md`, `data_structures.md` updated where appropriate.
9. **Learnings captured.** Per [learning.md](learning.md).

Reviewers also do the opposite job: catch unnecessary changes. Speculative abstractions, drive-by refactors, and scope creep get flagged for removal, not applause.

## Review output shape

Reviewers return:

- **Verdict:** approve / request changes / block.
- **Must-fix:** issues that block landing (correctness, safety, broken tests).
- **Should-fix:** issues worth fixing before landing (clarity, parity, minor correctness).
- **Consider:** suggestions the author can take or leave.
- **Praise (when warranted):** specifically what was handled well, so we reinforce it.

Low-confidence concerns are marked as such. Reviewers don't manufacture feedback to look thorough; "LGTM, here's why" is a valid response.

## Receiving review

Authors don't perform agreement. They:

- Address must-fix or argue it down with reasoning.
- Take should-fix by default; decline with a reason in the PR/reply.
- Treat consider items as optional.
- Update persona files or `decisions.md` if the review surfaced a durable lesson.

Authors who reflexively "fix" everything a reviewer flags without thinking are as broken as authors who ignore feedback. Atlas watches for both.

## Atlas's role

- Picks the reviewer(s) and the reviewer's model for every review request.
- Won't accept a self-review. Won't accept a review by the same model that authored, except in emergencies (which get logged in `decisions.md`).
- Arbitrates when author and reviewer disagree — or escalates to Rob when it's a judgment call above my pay grade.
- Tracks review quality over time: reviewers who repeatedly miss real bugs or generate noise get their briefs adjusted.
