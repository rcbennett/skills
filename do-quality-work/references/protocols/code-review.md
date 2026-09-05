# Protocol: Code Review

The [main skill](../../SKILL.md) governs review triggers, reviewer count, mechanical exceptions, and blocker handling. This protocol describes the selected review; it does not grant additional exceptions based on file count, passing tests, or file type.

## Review the actual change

Use one capable independent reviewer for a coherent ordinary change, with specialist coverage under the main policy. A fresh execution must inspect the current artifact and relevant context; merely asking the author to adopt another persona is self-review. An authorized external reviewer is also valid. If required independence is unavailable, preserve a review-pending handoff.

The owner supplies the baseline and final diff/artifact, requested behavior, affected callers and boundaries, design/plan when applicable, executed evidence, and remaining gaps. Reviewers inspect these in order:

1. **Correctness and ownership:** trace input through state transitions and side effects, including relevant failure, cancellation, and teardown. Is each policy decision owned once?
2. **Design fit:** does the change solve the requested problem within agreed scope and approved boundaries? Are dependencies and responsibilities understandable? Flag speculative abstractions and unnecessary alternate paths with evidence.
3. **Replacement and retirement:** have consumers moved and superseded code, registrations, flags, config, fixtures, dependencies, and implementation-specific tests been reconciled? Retention requires the verified compatibility contract described in the main skill. No unused wrapper or dormant implementation survives merely because it is documented.
4. **Changed boundaries:** trace `boundary -> callers -> side effect -> invariant -> evidence`. For cross-platform changes, check intentional adaptation and affected runtime integration under [cross-platform-parity.md](cross-platform-parity.md).
5. **Consequential risks:** security/privacy, persistence, concurrency, external contracts, device safety, and irreversible behavior when affected. CI or dependency edits receive review according to their effects, not their filename.
6. **Verification:** do tests protect observable behavior or invariants without mocking away the change? Do results support the actual claim? Is required evidence current? Do not request new harnesses or broad tests without a named unanswered risk.
7. **Current project truth:** update only the canonical requirements, architecture, API, operational, or state docs affected by the result. Learning/calibration is conditional, not a completion ritual.

## Findings and receipt

Return **approve**, **request changes**, or **block**. Each material finding identifies source location, concrete failure/maintenance consequence, evidence, and smallest correction. Separate blockers from optional suggestions; mark uncertainty. A review with no findings is valid.

Use a compact receipt with reviewed artifact/revision, reviewer/lane, independence/model status, verdict, evidence and gaps. Add hashes and stable finding IDs when follow-up needs exact identity. Do not duplicate the full author's evidence log.

## Resolve and finish

The owner verifies factual claims under [verifying-claims.md](verifying-claims.md). Fix demonstrated blockers or reject them with evidence. Do not reflexively accept findings or expand scope for optional cleanup. Return material ownership, contract, authority, or finish-line changes to design acceptance.

Use lane-specific delta review for behavior-changing fixes. Mechanical/editorial follow-ups need an owner check; full review repeats only for a material change to scope, architecture, risk, or evidence contract.

After two passes without new decisive evidence, stop repeating the review. An unresolved blocker permits only a bounded non-production probe outside the blocked boundary under [design-first.md](design-first.md), or escalation. It never permits production implementation or acceptance merely because the proposed slice is reversible.
