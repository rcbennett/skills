# Protocol: Council Review

**Principle:** Council review is an escalation mechanism for decisions that focused evidence and targeted review cannot resolve. It synthesizes independent judgments without turning every important task into an all-team ceremony.

## When council review is warranted

Run council review when at least one of these applies:

- The choice is irreversible or expensive to reverse.
- Independent reviewers remain in substantive disagreement after evidence is gathered.
- A genuine cross-domain tradeoff cannot be resolved by an accountable owner or an authoritative probe.
- Rob asks for a council, team, focus group, consensus, or vote.

Do not use council review merely because a plan is non-trivial, cross-platform, user-facing, or safety-adjacent. Those conditions may require focused plan, domain, safety, parity, or code review; council is needed only when the resulting decision still meets an escalation trigger.

## Council membership

Use two to five members whose decision rights or expertise cover the unresolved tradeoff:

- Include the accountable owner and only the domain, safety, product, or operations members whose judgments can change the decision.
- State missing coverage rather than padding the council with unrelated personas.
- Partition review lanes so members do not repeat the same full scan.

One independently executed reviewer receives one vote. Multiple role lenses produced by one agent remain one vote. When independent agents are unavailable, disclose that the result is an internal synthesis and do not present role-lens counts as independent votes.

## Inputs

Start from the current artifact, not an idealized version of it:

- Artifact under review: design, implementation plan, code, report, requirements, protocol, product decision, or other working artifact.
- Artifact path or identifier and content hash when available.
- Code or decision baseline.
- Decision to be made and constraints: time, cost, risk, platform scope, product goals, compatibility, and verification limits.
- Evidence-preflight result: authoritative probes run, prerequisites, blockers, fallbacks, and stop condition.
- Prior focused reviews and stable blocker IDs.

## Member review brief

Each council member reviews the artifact and returns:

- **Weaknesses:** defects, missing constraints, hidden risks, wrong assumptions, brittle dependencies, incomplete states, or places the artifact will mislead future work.
- **Adversarial risks:** exploit paths, operational failures, abuse cases, missing rollback, weak observability, and unsafe edge cases that need red-team treatment.
- **Strongest alternative:** the serious competing path or dissenting view they would steelman before rejecting it.
- **Decision-changing improvements:** the smallest changes that would alter the recommendation, remove a blocker, or materially reduce risk.
- **Tradeoff judgment:** what to keep small, what is worth expanding, and what should be deferred.
- **Verification and documentation needs:** evidence, tests, manual checks, decisions, requirements, or runbooks needed before the plan is trusted.
- **Recommended path:** the path they support and the path they reject.
- **Vote:** whether they agree that the synthesized forward plan is the best balance once it is proposed.

Council members should be concrete. A useful concern names the artifact section, code path, plan step, assumption, or missing evidence it depends on.

## Synthesis

The council lead synthesizes, not averages:

1. Cluster findings by theme: blockers, important concerns, decision-changing improvements, deferred ideas, and invalid or unverified claims.
2. Verify factual and negative claims before treating them as blockers. Use `verifying-claims.md` when a member says something is missing, broken, absent, impossible, or dead.
3. Use red-team, steelman, or pre-mortem input only when it answers a distinct unresolved risk; do not stack them automatically.
4. Separate must-fix issues from optional refinement. Reject open-ended scope expansion.
5. Produce a forward plan that balances correctness, product value, risk, cost, schedule, platform scope, and reversibility.
6. Explain which council suggestions were accepted, which were deferred, and why.
7. Record material accepted decisions with `decision-record.md` when a durable location exists.

The output is a plan the team would execute, not a transcript.

## Agreement rule

The plan needs at least 75% council agreement before it is treated as the chosen direction.

- Denominator: independently executed members who reviewed the exact artifact.
- Threshold: round up `0.75 * member_count`.
- Agreement means the member believes the synthesized plan is the best balance to move forward, even if it is not their personal ideal.
- Dissent is allowed, but unresolved dissent must be visible.
- Consensus never overrides a verified unresolved blocker or missing required evidence.

If agreement is below 75%, revise the plan around the strongest objections and run another vote. If a second pass still fails, do not claim consensus. Present the unresolved options, dissenting reasons, and the safest reversible next step, then escalate to Rob for the decision.

## Required output

For every council review, report:

- **Artifact reviewed:** what was reviewed and what decision it informs.
- **Review receipt:** artifact identifier/hash, baseline, evidence-preflight status, reviewer lanes, independence/model status, and blocker IDs.
- **Council members:** who participated, vote eligibility, whether review was independent or internal, and any missing coverage.
- **Weaknesses and decision-changing improvements:** the major findings, grouped by theme.
- **Synthesized plan:** the proposed forward plan.
- **Agreement:** vote count, percentage, threshold, and dissent.
- **Follow-up requirements:** verification, docs, protocol updates, or decisions needed before execution or release.

Keep the report proportional. For a small decision, a compact table is enough. For a major architecture or release decision, preserve enough detail that a future agent can understand why the plan won.

## Integration with other protocols

- Council review consumes focused design, plan, code, safety, parity, or verification findings only after an escalation trigger is met.
- `plan-review.md` can be one input, but most important plans should be resolved by their accountable owner and focused reviewers without a council.
- `red-team.md`, `steelman.md`, and `pre-mortem.md` are optional risk inputs, not automatic prerequisites.
- `model-selection.md` applies when assigning independent council reviewers.
- `decision-record.md` applies after council agreement when the decision should guide future work.
- `learning.md` applies after the council: durable conclusions belong in the appropriate docs, decisions, protocols, or memory.
