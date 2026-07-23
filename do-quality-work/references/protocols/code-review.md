# Protocol: Code Review

**Principle:** Non-trivial production changes need an independent, current-artifact review focused on the boundaries and risks that changed. More reviewers are useful only when they cover distinct lanes.

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

1. **Default to one architecture/delivery reviewer.**
2. **Add one specialist only for a distinct domain, safety, security, or platform risk.** For an actual safety, security, or irreversible boundary change, use two reviewers total by default: one delivery/domain lane and one specialist lane. A third requires a separately named material risk that neither lane owns.
3. **Partition lanes.** Do not ask multiple reviewers to repeat the same full-diff scan.
4. **Use model diversity at decision boundaries.** Prefer a different-model review for final production packets; require two different-model reviewers only for actual safety, security, or irreversible boundary changes. A blocker-only delta may return to the original reviewer and model. See [model-selection.md](model-selection.md).

Use a named persona only when domain decision rights or specialist judgment matter. Multiple role lenses produced by one agent do not count as independent reviewers.

## What reviewers look for

Reviewers are briefed to check these in order:

1. **Correctness.** Does it do what it claims? Are edge cases handled?
2. **Alignment.** Matches `decisions.md`, `guidelines.md`, and existing patterns?
3. **Changed boundaries.** Trace `changed seam -> current callers -> side effect -> preserved invariant -> authoritative evidence`. Shared logic stays in shared layers and platform code remains adaptation-only where that is the design.
4. **Cross-platform parity.** See [cross-platform-parity.md](cross-platform-parity.md) — is the status correctly reflected in `requirements.md` + `PROJECT_STATE.md`?
5. **Safety.** Rules, secrets, PII in logs, `Bundle.main` vs `Bundle.module`, destructive operations.
6. **Tests.** Require focused regression evidence for the changed boundary. Do not require a new fixture or harness unless existing tests and the product path cannot answer a named decision question.
7. **Verification evidence.** Build output, test output, or an explicit "I couldn't verify X" from the author.
8. **Docs sync.** `requirements.md`, `PROJECT_STATE.md`, `decisions.md`, `data_structures.md` updated where appropriate.
9. **Learnings captured.** Per [learning.md](learning.md).
10. **Calibration updated.** Per [persona-calibration.md](persona-calibration.md) when review quality changes trust in a persona.

Reviewers also do the opposite job: catch unnecessary changes. Speculative abstractions, drive-by refactors, and scope creep get flagged for removal, not applause.

## Review output shape

Reviewers return:

- **Review receipt:** artifact path/hash, code baseline, reviewer identity/lane, independence/model status, evidence-preflight status, and stable blocker IDs.
- **Verdict:** approve / request changes / block.
- **Must-fix:** issues that block landing (correctness, safety, broken tests).
- **Should-fix:** issues worth fixing before landing (clarity, parity, minor correctness).
- **Consider:** suggestions the author can take or leave.
- **Praise (when warranted):** specifically what was handled well, so we reinforce it.

Low-confidence concerns are marked as such. Reviewers don't manufacture feedback to look thorough; "LGTM, here's why" is a valid response.

Ask for decision-changing findings, not open-ended opportunities to expand scope.

## Receiving review

Authors don't perform agreement. They:

- Address must-fix or argue it down with reasoning.
- Take should-fix by default; decline with a reason in the PR/reply.
- Treat consider items as optional.
- Update persona memories or `decisions.md` if the review surfaced a durable lesson.
- Update `calibration.md` when the review produced a real signal about reviewer quality, owner fit, false positives, missed issues, or noisy findings.
- Skip re-review for editorial-only changes. Request lane-specific delta review when one lane changed. Rerun the full review only if scope, architecture, safety, or the evidence contract changed.

Authors who reflexively "fix" everything a reviewer flags without thinking are as broken as authors who ignore feedback. Atlas watches for both.

## Atlas's role

- Picks the reviewer(s) and the reviewer's model for every review request.
- Won't accept a self-review as independent. Uses model diversity where it can change decision quality rather than as a universal reviewer-count requirement.
- Arbitrates when author and reviewer disagree — or escalates to Rob when it's a judgment call above my pay grade.
- Tracks review quality over time: reviewers who repeatedly miss real bugs or generate noise get their briefs adjusted.
- Stops after two review passes without new runtime or authoritative evidence; the next step is the smallest reversible evidence-producing slice or escalation of the named blocker.
