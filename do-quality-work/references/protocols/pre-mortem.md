# Protocol: Pre-Mortem

**Principle:** Before high-impact work ships, assume it failed and explain why. A pre-mortem turns plausible future failure into prevention, detection, and recovery work now.

## When to use this lens

Use when selected by the main skill for a fragile operational cutover or consequential recovery uncertainty, or when the user requests it. A routine public feature or deploy alone does not create another ceremony. Integrate failure narratives into existing rollout/review work when sufficient.

## Inputs

Start with:

- Planned change and rollout path.
- Users, devices, data, systems, and operators affected.
- Verification already done and known manual gaps.
- Monitoring, logging, support, rollback, and recovery options.
- Constraints: time, credentials, hardware access, platform limitations, and production access.

## Failure narratives

Write the most plausible failure stories as if the work has already failed:

- **Trigger:** what caused the failure.
- **Symptom:** what users, operators, logs, devices, or metrics showed.
- **Impact:** who was affected and how badly.
- **Missed signal:** what warning sign was ignored or unavailable.
- **Prevention:** what can be changed before release to reduce likelihood.
- **Detection:** how the team will know the failure is happening.
- **Recovery:** rollback, mitigation, support response, data repair, device stop path, or feature disable.
- **Owner:** who owns the prevention or response step.

Prefer three to seven high-signal narratives over a long generic checklist.

## Go/no-go synthesis

After narratives are written:

1. Identify blockers that must be fixed before release or execution.
2. Identify watch items that can ship with explicit monitoring and rollback.
3. Confirm rollback or recovery for each high-severity narrative.
4. Decide whether any manual checklist, runbook, smoke test, alert, or support note is needed.
5. Escalate to council only when an unresolved tradeoff meets the main skill's trigger; importance alone is insufficient.

## Required output

Report:

- **Scope:** change or release being pre-mortemed.
- **Top failure narratives:** concise table or bullets.
- **Blockers:** issues that must be fixed before proceeding.
- **Watch items:** accepted risks and how they will be detected.
- **Rollback/recovery:** concrete path for high-severity failures.
- **Owners and timing:** who acts before release and who watches after release.

If rollback, monitoring, hardware access, credentials, or production access cannot be verified, say so plainly.

## Integration with other protocols

- [red-team.md](red-team.md) finds adversarial and edge-case risks that may become pre-mortem narratives.
- [verification-toolchain.md](verification-toolchain.md) decides which prevention and detection checks can run now.
- [council-review.md](council-review.md) uses pre-mortem results for important release or architecture decisions.
- [decision-record.md](decision-record.md) records accepted operational risk and revisit triggers.
