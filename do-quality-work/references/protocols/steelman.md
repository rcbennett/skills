# Protocol: Steelman Review

**Principle:** Reject the strongest version of an alternative, not the easiest version to dismiss. A steelman review protects decisions from premature convergence and uncharitable reasoning.

## When steelman review is required

Run steelman review when:

- Rejecting a serious alternative design, implementation path, product behavior, vendor, process, or protocol change.
- Disagreeing with a plausible user proposal or replacing it with a different recommendation.
- Choosing between options where cost, risk, schedule, user value, or reversibility point in different directions.
- A council review has dissent or a viable minority path.
- Red-team or pre-mortem findings make the preferred path look weaker than expected.
- Rob asks for a steelman, strongest argument, charitable case, or counterargument.

Do not use steelman review to keep impossible options alive. If hard evidence rules out an option, cite the evidence and move on.

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

- [council-review.md](council-review.md) should consume steelman findings before agreement on important decisions.
- [red-team.md](red-team.md) may provide the strongest objection to the preferred path.
- [decision-record.md](decision-record.md) records alternatives considered and why the chosen path won.
- [design-first.md](design-first.md) uses steelman findings to avoid locking in a brittle system shape.
