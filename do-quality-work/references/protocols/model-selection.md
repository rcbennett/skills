# Protocol: Model Selection

**Principle:** Picking the right model is almost as important as picking the right team member. Different models have different strengths, different blind spots, and different costs. Atlas chooses deliberately — and a reviewer always runs on a different model than the author.

## The roster

We route work across the current Codex / GPT-5 family exposed by the harness. Treat the live tool roster as source of truth; this document describes **selection tiers**, not permanently blessed SKUs.

| Tier | Typical examples in this harness | Strengths | Good for |
|---|---|---|---|
| **Flagship reasoning** | `gpt-5.4`, `gpt-5.2` | Deep reasoning, long-context synthesis, judgment | Architecture, ambiguous specs, security review, high-stakes decisions |
| **Implementation-focused Codex** | `gpt-5.2-codex`, `gpt-5.3-codex`, `gpt-5.1-codex-max` | Strong code editing and repo execution | Routine implementation, most code review, multi-file changes |
| **Fast scout / mini** | `gpt-5.4-mini`, `gpt-5.1-codex-mini`, `gpt-5.3-codex-spark` | Speed, low cost, broad parallel scouting | First-pass triage, bounded transforms, repo search tasks |

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

## Reviewer ≠ Author (the model diversity rule)

Per [code-review.md](code-review.md), the reviewer's model must differ from the author's. Blind spots correlate within a model family, so a reviewer from a different tier or model often catches what the author normalized away.

Pairings, by default:

- Flagship author → **implementation-focused reviewer** (sometimes fast-scout first for a quick sanity pass, then implementation-focused for depth).
- Implementation-focused author → **flagship reviewer** for high-stakes work; **fast-scout reviewer** for low-risk mechanical work.
- Fast-scout author → **implementation-focused reviewer**.
- Anyone → **flagship reviewer** for any security, auth, or rule change.

For critical changes, Atlas runs **two reviewers on different models** and reconciles findings.

## Dispatching with model overrides

When dispatching a subagent via the `Agent` tool, set `model` explicitly for any non-default choice. Examples:

- Research sweep across many files → multiple fast-scout / mini subagents in parallel.
- Architecture proposal → flagship reasoning subagent adopting the relevant persona (Morgan, usually).
- Routine Swift view implementation → implementation-focused Codex subagent adopting Ishaan.
- Review of the above → a different flagship or implementation-focused model adopting a different persona.

The persona and the model are independent choices. Ishaan on a mini scout and Ishaan on a flagship reasoner are different instruments; pick by the task, not the title.

## Cost & cache hygiene

- Keep conversations with Atlas warm: avoid gratuitous 5-minute+ idle gaps that invalidate the prompt cache (see ScheduleWakeup guidance when using `/loop`).
- Parallelize independent subagent calls in one dispatch block — one round-trip, multiple results.
- Don't use flagship reasoning for work an implementation-focused model will nail; don't use mini scouts for work that needs judgment.
- If a fast-scout result looks confidently wrong, that's a signal to re-dispatch to an implementation-focused or flagship model, not to argue with the scout.

## When to revisit this protocol

- The harness roster changes materially. Update the example table and the defaults; record the change in `decisions.md`.
- We notice a systematic blind spot in a pairing. Rotate the defaults.
- Persona calibration shows a reviewer or owner has changed strengths, blind spots, false-positive rate, or assignment fit.
- Cost becomes a real constraint. Tighten the "default cheaper, escalate on stall" rule.

## Atlas's role

- Picks model and persona for every dispatch. Both decisions are logged implicitly by the dispatch itself.
- Enforces the reviewer ≠ author model rule without exception on non-trivial changes.
- Tracks which pairings produce real bugs caught vs. noise, and adjusts defaults over time.
- Uses `management/personas/<member-slug>/calibration.md` when available before choosing reviewers for high-impact work.
- Teaches, doesn't gatekeep: when a choice surprises Rob, I explain why I picked it.
