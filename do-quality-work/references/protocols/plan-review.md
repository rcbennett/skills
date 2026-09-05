# Protocol: Plan Review

Review the current plan enough to make a coherent implementation executable while preserving the accepted architecture. The [main skill](../../SKILL.md) owns planning/review triggers, reviewer count, autonomy, and blocker policy. Independent code review is separate from planning depth: a small logic fix may need no plan document but still needs code review.

## Inputs

Inspect the canonical plan (or combined design/execution note), current code baseline, requested scope, architectural decision where applicable, decisive evidence, and blockers. Do not require another chat summary of the same artifact. Use the smallest evidence contract that answers the decision; do not turn unavailable evidence into a larger speculative checklist.

## Review questions

- Does current ownership and behavior match the evidence? Does the target have clear responsibilities and one policy authority?
- Is the architecture accepted by the authorized owner, with consequential tradeoffs resolved? Are the first working path and affected consumers clear?
- Do tasks form coherent checkpoints rather than infrastructure-only work? Are implementation and validation status distinct?
- Are lifecycle, failure, teardown, migration, and rollback handled at changed boundaries?
- Does replacement include consumer migration and retirement of superseded code, wiring, flags, fixtures, config, and tests? Does temporary compatibility have a verified need and removal condition, and does a permanent adapter have a verified supported contract, maintenance owner, and one canonical policy authority?
- Are real behavior differences adjudicated before consolidation? Are platform exclusions explicit and within user scope?
- Are abstractions and test infrastructure justified by current needs rather than hypothetical reuse? Does verification exercise the changed boundary?
- Does workspace cleanup protect pre-existing state and preserve unique work? Are affected canonical docs current?

## Findings and acceptance

Return **approve**, **request changes**, or **block**, with the artifact/revision, reviewer/lane, independence, evidence, and concrete findings. Use stable IDs when findings require follow-up. Separate blockers from optional refinements; a no-findings verdict is valid.

The owner verifies findings, makes supported corrections, and rejects incorrect objections with evidence. A scope or complexity objection is not automatically right; retain justified design boundaries and do not expand into optional work. Resolve required blockers before production implementation. A reviewer advises and gates but does not silently acquire the user's product decision rights.

Mechanical/editorial edits need no re-review; affected behavior or sequencing changes receive lane-specific delta review. Material ownership, interface, authority, or finish-line changes return to design acceptance. Do not restart a coherent plan solely because a reviewer suggests a different structure.

After two passes without new decisive evidence, stop repetitive review. Only a bounded non-production feasibility probe outside the blocked boundary under [design-first.md](design-first.md), or escalation, is allowed while blockers remain. Reversibility and review time spent do not waive blockers.

## Execution handoff

Link [implementation-planning.md](implementation-planning.md) for plan maintenance, [code-review.md](code-review.md) for implementation review, and [workspace-and-document-lifecycle.md](workspace-and-document-lifecycle.md) for cleanup. Reuse their procedures only when the phase requires them. The first checkpoint should produce useful behavior and evidence, not another review artifact.
