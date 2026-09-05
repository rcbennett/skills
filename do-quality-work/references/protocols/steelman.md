# Protocol: Steelman Review

**Principle:** Reject the strongest version of an alternative, not the easiest version to dismiss. A steelman review protects decisions from premature convergence and uncharitable reasoning.

## When to use this lens

Use when selected by the main skill for a serious disputed alternative whose strongest case could change a consequential decision, or when requested. It can be a paragraph in an existing design review. Do not keep evidence-ruled-out options alive or require a separate workflow for routine disagreement.

## Inputs

Capture:

- Preferred path and why it currently looks best.
- Alternative path being steelmanned.
- Constraints: time, budget, risk, platform support, compatibility, user value, safety, verification limits, and reversibility.
- Evidence already gathered and evidence still missing.

## Procedure

1. **State the alternative cleanly.** Describe the strongest coherent version of the path, not a caricature.
2. **Name the win condition.** Explain the situation where this alternative is better than the preferred path.
3. **List its real advantages.** Include simplicity, speed, user value, operational safety, compatibility, cost, reversibility, learning value, or risk reduction.
4. **Name its strongest objections to the preferred path.** Be concrete about what the preferred path may be underestimating.
5. **Identify decision-changing evidence.** Say what search result, test, user constraint, benchmark, device behavior, cost number, or production fact would make the alternative win.
6. **Compare honestly.** Explain why the final recommendation still chooses the preferred path, chooses the alternative, or changes to a hybrid.
7. **Retain useful ideas.** Preserve the parts of the alternative that should influence the chosen path even if the alternative loses.

## Guardrails

- Steelman is not faux neutrality. A strong final recommendation is allowed.
- Do not invent facts to make the alternative stronger. Mark unknowns as unknown.
- Do not let the review sprawl into every imaginable option. Steelman the serious competing path or paths.
- If the steelman reveals that the preferred path depends on an unverified negative claim, apply [verifying-claims.md](verifying-claims.md).

## Required output

Report:

- **Alternative steelmanned:** the path reviewed.
- **Strongest case:** why a reasonable expert would choose it.
- **Where it wins:** conditions or constraints that favor it.
- **Decision-changing evidence:** what would flip the recommendation.
- **Final judgment:** chosen path and why.
- **Ideas retained:** useful pieces carried into the chosen path.

For small decisions, this can be a compact paragraph. For architecture, safety, billing, or release decisions, preserve enough detail for future agents to understand why the alternative lost.

## Integration with other protocols

- [council-review.md](council-review.md) can consume these findings only after its escalation trigger is met.
- [red-team.md](red-team.md) may provide the strongest objection to the preferred path.
- [decision-record.md](decision-record.md) records alternatives considered and why the chosen path won.
- [design-first.md](design-first.md) uses steelman findings to avoid locking in a brittle system shape.
