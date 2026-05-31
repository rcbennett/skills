# Protocol: Decision Record

**Principle:** Important decisions should leave a trail that future agents can trust. A decision record captures the context, alternatives, rationale, consequences, and revisit trigger before the reasoning is lost.

## When a decision record is required

Create or update a decision record when:

- A material architecture, product behavior, platform-scope, data-model, API, security, privacy, billing, release, deploy, vendor, or process decision is made.
- A previous material decision is changed, narrowed, reversed, or found stale.
- A serious alternative is rejected and future agents are likely to revisit it.
- Council review reaches agreement on a path forward.
- Red-team, steelman, or pre-mortem review leads to accepted risk or a meaningful tradeoff.
- A protocol or skill operating rule changes.
- Rob asks for a decision record, ADR, durable decision, or rationale.

Mechanical edits, tiny copy changes, and fully reversible local fixes do not need a decision record unless they alter a durable rule.

## Where to record it

Prefer the project's durable decision location:

- `decisions.md`
- `management/decisions/`
- `docs/decisions/`
- Architecture Decision Records, design notes, runbooks, or protocol-specific decision logs

If a project has an established format, use it. If no durable location exists and creating one is outside scope, include the record in the final response and state that no durable decision location was found.

Do not hide durable decisions only in chat when the repository or skill has an obvious decision log.

## Decision record shape

Use the smallest durable shape that preserves the reasoning:

- **Date:** exact date.
- **Decision:** the chosen direction.
- **Status:** proposed, accepted, superseded, or rejected.
- **Context:** problem, constraints, and why a decision was needed.
- **Options considered:** serious alternatives, including steelmanned alternatives when applicable.
- **Rationale:** why this option won, including evidence and review findings.
- **Consequences:** benefits, costs, risks, migrations, docs, tests, support, or future maintenance burden.
- **Verification:** tests, searches, docs, manual checks, or blocked validation.
- **Revisit trigger:** condition that should reopen the decision.

For protocol decisions, include the protocol files changed and the behavior the change is meant to improve.

## Guardrails

- Record decisions, not transcripts. Preserve the reasoning, not every discussion turn.
- Separate evidence from judgment. If evidence is incomplete, say so.
- Do not create large ADR machinery for a small project unless the existing style supports it.
- If a decision is temporary, say what will retire it.
- If a decision supersedes another, link or name the older decision.

## Required output

Report:

- **Decision recorded:** summary and status.
- **Location:** file path or final-response-only if no durable location exists.
- **Alternatives:** options captured or reason none were material.
- **Revisit trigger:** when future agents should reconsider.
- **Gaps:** missing evidence, blocked verification, or missing durable decision location.

## Integration with other protocols

- [council-review.md](council-review.md) produces decisions that should usually be recorded.
- [steelman.md](steelman.md) supplies the alternatives and decision-changing evidence.
- [red-team.md](red-team.md) and [pre-mortem.md](pre-mortem.md) supply accepted risk and operational consequences.
- [learning.md](learning.md) decides whether the decision also belongs in memory, docs, personas, or conventions.
