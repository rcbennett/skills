# Protocol: Council Review

**Principle:** Important decisions need the whole team in the room. A council review turns individual critique into a balanced forward plan that the team can actually stand behind.

## When council review is required

Run council review for any important decision, including:

- Architecture, design, implementation plans, or code paths that will guide meaningful future work.
- Safety, security, privacy, auth, billing, hardware control, BLE/FTMS, public API, release-readiness, or deploy decisions.
- Product behavior, UX flows, accessibility, platform-scope, or cross-platform parity choices.
- Persisted data models, new services, new collections, scaling/cost tradeoffs, or irreversible vendor/process choices.
- Strategy, staffing, protocol, or team-process changes.
- Any task where Rob asks for a council, team, focus group, consensus, or "best balance" decision.

Small reversible edits, narrow copy tweaks, and mechanical fixes do not need council review unless they are being used to choose a larger direction.

## Council membership

Use all active team members from the applicable roster:

- If the project has `management/personas/`, include every active persona in that roster.
- If the `team-management` skill has a current roster, use it as the source of truth.
- If no roster exists, include every assigned task owner plus every domain persona needed to cover the decision. State that this is a provisional council.
- Do not omit dissenting or inconvenient roles for speed. The point is to expose weak assumptions.

When the environment permits independent agents or multiple models, use them for meaningful independence. When it does not, run separate role-lens passes yourself and disclose that the council was internal rather than independently staffed.

## Inputs

Start from the current artifact, not an idealized version of it:

- Artifact under review: design, implementation plan, code, report, requirements, protocol, product decision, or other working artifact.
- Decision to be made and constraints: time, cost, risk, platform scope, product goals, compatibility, and verification limits.
- Evidence already gathered: docs, repo searches, tests, reviewer findings, user constraints, and known open questions.
- Applicable protocols: design-first, plan-review, code-review, red-team, steelman, pre-mortem, cross-platform parity, verification, claim-checking, model-selection, decision-record, and learning as triggered.

## Member review brief

Each council member reviews the artifact and returns:

- **Weaknesses:** defects, missing constraints, hidden risks, wrong assumptions, brittle dependencies, incomplete states, or places the artifact will mislead future work.
- **Adversarial risks:** exploit paths, operational failures, abuse cases, missing rollback, weak observability, and unsafe edge cases that need red-team treatment.
- **Strongest alternative:** the serious competing path or dissenting view they would steelman before rejecting it.
- **Opportunities to do more:** practical improvements that raise product quality, reliability, safety, clarity, leverage, maintainability, user value, or verification confidence.
- **Tradeoff judgment:** what to keep small, what is worth expanding, and what should be deferred.
- **Verification and documentation needs:** evidence, tests, manual checks, decisions, requirements, or runbooks needed before the plan is trusted.
- **Recommended path:** the path they support and the path they reject.
- **Vote:** whether they agree that the synthesized forward plan is the best balance once it is proposed.

Council members should be concrete. A useful concern names the artifact section, code path, plan step, assumption, or missing evidence it depends on.

## Synthesis

The council lead synthesizes, not averages:

1. Cluster findings by theme: blockers, important concerns, opportunities, deferred ideas, and invalid or unverified claims.
2. Verify factual and negative claims before treating them as blockers. Use `verifying-claims.md` when a member says something is missing, broken, absent, impossible, or dead.
3. Run or summarize red-team, steelman, and pre-mortem findings when the decision has meaningful downside, serious alternatives, or operational fragility.
4. Separate must-fix issues from "do more" opportunities. Favor improvements that materially change outcome quality without bloating scope.
5. Produce a forward plan that balances correctness, product value, risk, cost, schedule, platform scope, and reversibility.
6. Explain which council suggestions were accepted, which were deferred, and why.
7. Record material accepted decisions with `decision-record.md` when a durable location exists.

The output is a plan the team would execute, not a transcript.

## Agreement rule

The plan needs at least 75% council agreement before it is treated as the chosen direction.

- Denominator: all council members who were required to review the artifact.
- Threshold: round up `0.75 * member_count`.
- Agreement means the member believes the synthesized plan is the best balance to move forward, even if it is not their personal ideal.
- Dissent is allowed, but unresolved dissent must be visible.

If agreement is below 75%, revise the plan around the strongest objections and run another vote. If a second pass still fails, do not claim consensus. Present the unresolved options, dissenting reasons, and the safest reversible next step, then escalate to Rob for the decision.

## Required output

For every council review, report:

- **Artifact reviewed:** what was reviewed and what decision it informs.
- **Council members:** who participated, whether review was independent or internal, and any missing roster coverage.
- **Weaknesses and opportunities:** the major findings, grouped by theme.
- **Synthesized plan:** the proposed forward plan.
- **Agreement:** vote count, percentage, threshold, and dissent.
- **Follow-up requirements:** verification, docs, protocol updates, or decisions needed before execution or release.

Keep the report proportional. For a small decision, a compact table is enough. For a major architecture or release decision, preserve enough detail that a future agent can understand why the plan won.

## Integration with other protocols

- Council review sits above narrower reviews. It can consume design, plan, code, security, safety, parity, and verification findings, then decide the balanced path forward.
- `plan-review.md` can be one input to council review, but it does not replace the council when the decision is important.
- `red-team.md`, `steelman.md`, and `pre-mortem.md` provide structured inputs before council agreement when downside risk, serious alternatives, or operational failure modes matter.
- `model-selection.md` applies when assigning independent council reviewers.
- `decision-record.md` applies after council agreement when the decision should guide future work.
- `learning.md` applies after the council: durable conclusions belong in the appropriate docs, decisions, protocols, or memory.
