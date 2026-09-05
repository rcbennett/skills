# Protocol: Verifying Claims Before Acting

Treat reports of missing, broken, impossible, or dead behavior as claims until the evidence supports them. The [main skill](../../SKILL.md) governs workflow and scope; this protocol supplies claim verification when needed.

## Establish exactly what is claimed

Identify the artifact/revision, environment, expected behavior, and observation needed. A negative search finding must state the pattern, search boundary, and result. A scoped search supports a scoped conclusion, not a repository-wide absence claim.

Use a decisive independent observation before a consequential claim becomes a blocker or drives deletion:

- A Git index entry establishes tracking, not working-tree existence or commit membership. Check the filesystem for existence and the relevant commit/tree for committed content when those are the claims.
- Search plausible symbol names, paths, generated sources, and entry points. For behavior, follow the actual implementation and execute the relevant acceptance path when possible.
- For an allegedly broken build or runtime, compare current revision/configuration and run the appropriate command when available. Historical tags or remembered paths are not generic prerequisites.
- Before deleting code, inspect applicable callers, dynamic registration/reflection, serialized names, platform UI/configuration, plugins, generated bindings, external consumers, and published contracts. No textual references is insufficient when dispatch is indirect.

A second tool repeating the same limited search is not necessarily independent evidence. Choose the observation that can disprove the claim. Avoid mandatory multi-tool rituals when one authoritative check resolves it.

## Reconcile conflicting observations

User experience is strong counterevidence to an audit. Acknowledge it and reconcile revision, environment, configuration, timing, and reproduction. Neither the user's recollection nor an agent's confident summary automatically overrides current evidence. State uncertainty if both observations remain valid under different conditions.

Verify factual findings before fixing them. Reject unsupported blockers with the evidence, and correct earlier false claims where they affected the task. Do not build a missing feature or replace allegedly dead code before understanding its current owner and path.

## Handoff

For decision-changing findings, retain the claim, inspected artifact/boundary, decisive evidence, and conclusion. Use the project's existing inventory when helpful; do not create a new inventory system for a small review. Report gaps honestly and keep any learning update within scope and active memory policy.
