# Protocol: Model Selection

**Principle:** Pick models deliberately for the work and the risk. Model diversity is a property of an important review boundary, not a reason to add reviewers or rerun bounded work.

## Selection tiers

Treat the live harness roster as the only source of truth. Do not preserve model names in this protocol; they drift faster than the selection principles.

| Tier | Strengths | Good for |
|---|---|---|
| **Flagship reasoning** | Deep reasoning, long-context synthesis, judgment | Architecture, ambiguous specs, security review, high-stakes decisions |
| **Implementation-focused** | Strong code editing and repository execution | Routine implementation, most code review, multi-file changes |
| **Fast scout** | Speed, low cost, broad parallel scouting | First-pass triage, bounded transforms, repository search |

Atlas typically operates on the current default frontier coding model, then reaches for implementation-focused or mini subagents to parallelize and get independent viewpoints.

## How to pick

Match model to task:

| Task shape | Default model |
|---|---|
| Design, architecture, ADR-worthy decisions | Flagship reasoning |
| Security rules, auth, anything adversarial | Flagship reasoning |
| Domain-heavy work (grade pipeline, metric correctness) | Flagship reasoning |
| Multi-file refactor or cross-module change | Flagship reasoning or implementation-focused Codex |
| Single-file, well-scoped implementation | Implementation-focused Codex |
| Most code reviews | Implementation-focused Codex |
| Targeted "find X in the repo" searches | Fast scout / mini |
| Parallel scouting / "which of these files mention Y" | Fast scout / mini (many in parallel) |
| Docs edits, mechanical renames | Fast scout / mini |

When uncertain, start cheaper. Escalate to a larger model when the smaller one stalls, hedges, or returns generic work. Do not escalate just because a first pass had flaws — fix the brief first.

## Model diversity at decision boundaries

Blind spots can correlate within a model family, so a different model is valuable when review judgment can change an architecture choice or a final production decision.

Use these defaults:

- Initial architecture or durable-boundary decision → prefer one reviewer on a different model or tier from the author.
- Final production packet → prefer one different-model reviewer when the change is non-trivial.
- Actual safety, security, or irreversible boundary change → use two independently executed reviewers on different models or tiers when available, with partitioned lanes.
- Blocker-only delta → the original reviewer and model may verify the narrow fix.
- Low-risk mechanical or editorial work → model diversity is optional.

Do not count model diversity as an additional reviewer. One agent applying several personas or role lenses remains one independently executed review and, in a council, one vote.

## Dispatching with model overrides

When dispatching a subagent, set `model` explicitly for any non-default choice. Examples:

- Research sweep across many files → multiple fast-scout / mini subagents in parallel.
- Architecture proposal → flagship reasoning subagent adopting the relevant architecture or domain owner.
- Routine single-platform view implementation → implementation-focused subagent.
- Review of the above → a different flagship or implementation-focused model when the review sits at an architecture or final-production boundary.

The persona and the model are independent choices. The same domain persona on a fast scout and on a flagship reasoner are different instruments; pick by the task, not the title.

## Cost & cache hygiene

- Keep conversations with Atlas warm: avoid gratuitous 5-minute+ idle gaps that invalidate the prompt cache (see ScheduleWakeup guidance when using `/loop`).
- Parallelize independent subagent calls in one dispatch block — one round-trip, multiple results.
- Don't use flagship reasoning for work an implementation-focused model will nail; don't use mini scouts for work that needs judgment.
- If a fast-scout result looks confidently wrong, that's a signal to re-dispatch to an implementation-focused or flagship model, not to argue with the scout.

## When to revisit this protocol

- The harness capabilities change materially. Update the tier guidance only when selection behavior should change; do not add a drifting SKU list.
- We notice a systematic blind spot in a pairing. Rotate the defaults.
- Persona calibration shows a reviewer or owner has changed strengths, blind spots, false-positive rate, or assignment fit.
- Cost becomes a real constraint. Tighten the "default cheaper, escalate on stall" rule.

## Atlas's role

- Picks model and persona for every dispatch. Both decisions are logged implicitly by the dispatch itself.
- Applies model diversity at architecture, final-production, safety, security, and irreversible decision boundaries.
- Does not add reviewers merely to satisfy model variety; every reviewer has a distinct lane and decision question.
- Tracks which pairings produce real bugs caught vs. noise, and adjusts defaults over time.
- Uses `management/personas/<member-slug>/calibration.md` when available before choosing reviewers for high-impact work.
- Teaches, doesn't gatekeep: when a choice surprises Rob, I explain why I picked it.
