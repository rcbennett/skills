# Protocol: Red Team Review

**Principle:** Optimism is useful for building, but dangerous for trusting. A red-team review tries to break the artifact before users, attackers, devices, deploy systems, or production data do.

## When red-team review is required

Run red-team review for:

- Security, auth, privacy, PII, billing, admin, secret-handling, or public API changes.
- Safety-sensitive behavior, hardware control, BLE/FTMS, motion-capable equipment, or device-command paths.
- Launches, beta releases, deploys, migrations, public claims, and externally visible promises.
- Architecture, vendor, data-model, process, or release decisions with high cost of being wrong.
- Plans that depend on optimistic assumptions, incomplete evidence, model-generated analysis, or "this probably works" reasoning.
- Any task where Rob asks for adversarial review, red team, abuse-case review, or failure hunting.

Small reversible edits do not need red-team review unless they affect a high-risk surface.

## Inputs

Start with the artifact as it exists:

- Artifact under review: plan, code, design, release checklist, public claim, policy, protocol, or decision.
- Assets and invariants to protect: users, safety, data, money, trust, uptime, credentials, device state, reputation, and future maintainability.
- Boundaries and assumptions: auth state, network, devices, platform APIs, deploy targets, data migrations, permissions, rate limits, and manual operations.
- Existing evidence: tests, logs, docs, source searches, manual checks, user reports, and known gaps.

## Review brief

The red team looks for concrete ways the artifact can fail or be abused:

- **Abuse paths:** malicious user, confused user, compromised admin, bad input, stale client, replay, spoofing, escalation, data leak, or policy bypass.
- **Operational failures:** dependency outage, race, queue back-pressure, partial deploy, migration failure, rollback failure, stale config, clock skew, platform mismatch, or rate limits.
- **Safety failures:** uncontrolled motion, stale commands, missing stop path, incorrect units, ignored device capability, bad default, or unsafe retry.
- **Evidence gaps:** claims with no search evidence, tests that mock away the risk, manual-only assumptions, unverified platform behavior, or missing logs.
- **Blast radius:** who is affected, how quickly, how visibly, and whether the failure can spread across users, data, devices, or releases.

Useful findings are specific. They name the artifact section, code path, plan step, assumption, test gap, or operational step that creates the risk.

## Finding shape

Each finding should include:

- **Scenario:** the exploit or failure path in concrete steps.
- **Impact:** what breaks, who is affected, and why it matters.
- **Likelihood:** high, medium, low, or unknown with a reason.
- **Severity:** blocker, high, medium, low, or informational.
- **Evidence:** source search, test output, docs, logs, or note that it is a hypothesis.
- **Mitigation:** the smallest practical change that reduces the risk.
- **Residual risk:** what remains after mitigation and how it will be watched.

Do not inflate hypothetical concerns into facts. If a finding says something is missing, broken, absent, impossible, or dead, apply [verifying-claims.md](verifying-claims.md) before treating it as a blocker.

## Synthesis

The review lead converts findings into action:

1. Separate blockers from risks that can be mitigated later.
2. Prefer mitigations that reduce blast radius, add observability, preserve rollback, or make unsafe states impossible.
3. Do not let red-team review become solution design by fear. A risk can be accepted when severity, likelihood, mitigation cost, and reversibility justify it.
4. Feed material findings into council review when the reviewed artifact guides an important decision.

## Required output

Report:

- **Artifact reviewed:** what was attacked and why red-team review applied.
- **Top risks:** findings grouped by severity.
- **Mitigations:** accepted changes, deferred changes, and accepted residual risk.
- **Evidence:** searches, tests, docs, logs, or manual checks used.
- **Escalations:** items requiring Rob, live device access, credentials, production access, legal/security review, or follow-up protocol work.

Keep the output proportional. A small release checklist may need three bullets; a safety, auth, or billing decision may need a full risk table.

## Integration with other protocols

- [steelman.md](steelman.md) protects against rejecting alternatives too quickly after adversarial findings.
- [pre-mortem.md](pre-mortem.md) turns red-team risks into operational failure narratives and rollback needs.
- [council-review.md](council-review.md) consumes red-team findings for important decisions and consensus.
- [decision-record.md](decision-record.md) records accepted high-risk tradeoffs and revisit triggers.
- [verification-toolchain.md](verification-toolchain.md) decides which mitigations can be tested now and which require manual or production validation.
