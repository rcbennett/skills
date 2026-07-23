---
name: do-quality-work
description: Apply an evidence-first quality workflow for non-trivial implementation, review, planning, decisions, cross-platform work, and validation. Use when Codex must choose proportionate protocols and reviewers, verify claims, protect safety or platform boundaries, size an executable slice, assess a plan or code change, record a material decision, or capture a durable learning without letting process overhead replace progress.
---

# Do Quality Work

## Core Rule

Resolve the decision's main uncertainty with authoritative evidence, then do the smallest coherent amount of work that safely answers it.

When a project has live protocols, use them for domain invariants, exact commands, and local acceptance criteria. This skill still governs protocol dominance, review budget, evidence freshness, and reporting unless a project protocol explicitly documents a higher-severity exception. Use the bundled files under `references/protocols/` only when the project has no applicable protocol or when this skill itself is under review.

Retrieve relevant project decisions, playbooks, persona learnings, and calibration before meaningful work when prior context can change the approach. Do not reload the same material repeatedly during one artifact cycle.

## 1. Establish the Evidence Contract

Before detailed planning, fixture creation, or broad review, write down:

- **Decision question:** What must this work establish or change?
- **Blocking claims:** Which claims could change the decision or make the work unsafe?
- **Cheapest authoritative probe:** What direct observation, test, trace, build, report, or source inspection can resolve each blocking claim?
- **Prerequisites:** What credentials, data, environment, hardware, or artifact freshness does the probe require?
- **Invalidation condition:** What later change would make the evidence stale?
- **Stop condition:** What result is sufficient to decide, implement, or hand off?

Run the cheapest decisive probe early. If it is blocked, record the blocker and use the closest valid fallback without presenting fallback evidence as equivalent.

Do not add a fixture, simulator extension, evidence schema, or test harness until existing tests and the real product path have been assessed. New infrastructure must answer a named decision question that cannot be answered more cheaply.

For a simple read-only answer or lightweight spot-check, use only the decision question, current artifact, cheapest probe, and stop condition. Do not manufacture blockers, prerequisites, or evidence fields that add no information.

## 2. Choose the Work Unit

Default an implementation plan to two to four checkpoints. Each discrete task must do at least one of these:

- enable the first working end-to-end path;
- protect a high-severity invariant; or
- delete or simplify superseded behavior.

Choose one work unit:

- **Micro-slice:** Use for high risk, uncertain blast radius, poor reversibility, destructive work, or isolated diagnosis.
- **Capability packet:** Use for related low- or medium-risk changes with one rollback path and verification envelope. This is the normal default.
- **Broader checkpoint:** Use for release, deploy, migration, or final integration readiness.

Do not batch unrelated work to reduce ceremony. Do not fragment one behavior into checkpoints whose review and evidence cost exceeds their value.

For a refactor, include this changed-boundary map before implementation:

```text
Changed seam -> current callers -> side effect -> preserved invariant -> authoritative evidence
```

Treat preservation of safety code as insufficient when the event, lifecycle, concurrency, adapter, or ownership seam changes. Trace the side effect across the changed handoff and add focused regression evidence for any uncovered boundary.

## 3. Select Protocols Without Stacking Ceremony

Choose one **primary protocol** for the current decision or phase and, when a distinct material risk exists, at most one **risk overlay**. More overlays require separate named risks and separate decision questions. A task may move through different primary protocols over time; do not run all applicable protocols simultaneously.

| Current task or phase | Primary protocol | Typical risk overlay |
| --- | --- | --- |
| Plan that will direct implementation | `plan-review.md` | safety/domain/parity reviewer |
| Production implementation or refactor | `code-review.md` | safety/security/domain review |
| System shape or durable interface decision | `design-first.md` | `steelman.md` or `red-team.md` |
| Cross-platform behavior or shared/platform boundary | `cross-platform-parity.md` | domain or safety review |
| Negative claim such as missing, broken, or impossible | `verifying-claims.md` | none |
| Test, build, runtime, release, or hardware confidence | `verification-toolchain.md` | `pre-mortem.md` for fragile cutovers |
| Material disputed or hard-to-reverse decision | `council-review.md` | only the specialist evidence needed |
| Durable choice likely to be revisited | `decision-record.md` | none |
| Surprise, regression, or repeated rework | `after-action-review.md` | none |

Use `learning-retrieval.md`, `learning.md`, `persona-calibration.md`, `playbook-library.md`, `team-health.md`, and `model-selection.md` only when their specific triggers are present. They are support protocols, not mandatory parallel workstreams.

Read the primary protocol and risk overlay once per artifact cycle. Reread only when the protocol, scope, risk, or artifact class changes.

## 4. Budget Review and Escalation

Use the fewest independent reviewers that cover the material risks:

- Default to one architecture/delivery reviewer for a non-trivial plan or implementation.
- Add one domain or safety reviewer only when specialist judgment can change the result.
- Partition reviewer lanes. Do not ask several reviewers to perform the same full scan.
- After two review passes without new runtime or authoritative evidence, implement the smallest reversible slice or escalate the specific unresolved decision.

Treat model diversity as a property of the review, not as an extra reviewer role. Use a different-model review for an initial architecture decision or a final production packet when available. For an actual safety, security, or irreversible boundary change, use two independent reviewers total by default: one architecture/delivery or domain lane and one safety/security lane, on different models when available. Add a third reviewer only for a separately named material risk that neither lane owns. Evidence administration or generic QA does not by itself justify another reviewer. A blocker-only delta may return to the original reviewer and model.

Use explicit personas only when work has multiple owners, domain decision rights, or specialist risk. Do not create assignment theater for a single-owner task.

Run council review only when:

- the decision is irreversible or costly to reverse;
- independent reviewers remain in substantive disagreement;
- a genuine cross-domain tradeoff cannot be resolved by evidence; or
- the user explicitly requests a team, council, consensus, or vote.

Use two to five relevant council members, not every active persona. One independently executed reviewer gets one vote. Multiple role lenses produced by one agent remain one vote. Verified unresolved blockers override consensus.

## 5. Keep Reviews Fresh and Actionable

Every formal review must identify:

- artifact path or identifier and content hash when available;
- code or decision baseline;
- reviewer identity and lane;
- independence and model-diversity status;
- evidence-preflight status;
- verdict and stable blocker IDs.

Review the current artifact, not a remembered draft. Editorial changes need no re-review. A change confined to one reviewer lane needs only delta review for that lane. Rerun the full review only when scope, architecture, safety, or the evidence contract changes.

Ask reviewers for decision-changing findings. Do not ask for open-ended "opportunities to do more." Verify factual and negative claims before promoting them to blockers.

A lightweight owner spot-check is not a formal review. It needs only the artifact, decision question, evidence inspected, and verdict; add a receipt or blocker IDs only when another agent must act on them.

## 6. Execute and Verify

Run narrow high-signal checks while iterating. Run broader suites at a cohesive packet or checkpoint boundary, before commit/push/deploy, and before claiming completion when the later action depends on them. Do not rerun an expensive gate unless a relevant change invalidated its result.

For safety or actuator paths, verify the applicable invariants at the changed boundary, including:

- command and device identity;
- neutralization on pause, finish, background, disconnect, or ownership loss;
- fail-closed behavior; and
- no writes after the terminal fence.

Use deterministic simulator or local-transport checks during development. When physical hardware is required for final confidence, run one physical pass against the exact final candidate revision. Move hardware testing earlier only when feasibility itself is unresolved.

Report only what the evidence establishes. Keep source values, commands, simulated state, requested output, and measured/applied effects distinct.

## 7. Learn Proportionately

For a non-trivial session, run one session-level learning assessment at the root:

1. What was surprising and not obvious from current code or docs?
2. Where is the narrowest durable home?
3. Which prior belief, if any, did it invalidate?

Ask a subagent for a learning note only when its work exposed a surprising, reusable fact. Update persona calibration only for a useful catch, material miss, false positive, noisy review, or meaningful assignment-fit signal.

Write durable learning only when it is within the user's scope and the active memory policy allows it. Otherwise propose the exact update without making it.

## 8. Complete and Report

Follow the user's instruction and the repository's established workflow for commits. Implementation work should be committed when requested or when the repository workflow requires a completed-task commit. Read-only reviews and plans do not need commit narration. Never mix unrelated user changes into a task commit.

Default the final response to four items:

- **Outcome**
- **Verification and gaps**
- **Required next action**
- **Change/commit status**

Add ownership, council results, protocol details, or learning/calibration notes only when they materially affected the outcome or the user requested them.

For a read-only answer with no requested or performed write, omit change/commit status unless it clarifies a likely ambiguity.

Do not claim completion while a required blocker remains unresolved. Do not let consensus, passing unit tests, or preserved code substitute for missing authoritative runtime evidence.

## Bundled References

Use only the files selected by the workflow:

- [README.md](references/protocols/README.md)
- [learning-retrieval.md](references/protocols/learning-retrieval.md)
- [learning.md](references/protocols/learning.md)
- [after-action-review.md](references/protocols/after-action-review.md)
- [persona-calibration.md](references/protocols/persona-calibration.md)
- [playbook-library.md](references/protocols/playbook-library.md)
- [team-health.md](references/protocols/team-health.md)
- [code-review.md](references/protocols/code-review.md)
- [plan-review.md](references/protocols/plan-review.md)
- [design-first.md](references/protocols/design-first.md)
- [cross-platform-parity.md](references/protocols/cross-platform-parity.md)
- [model-selection.md](references/protocols/model-selection.md)
- [red-team.md](references/protocols/red-team.md)
- [steelman.md](references/protocols/steelman.md)
- [pre-mortem.md](references/protocols/pre-mortem.md)
- [council-review.md](references/protocols/council-review.md)
- [decision-record.md](references/protocols/decision-record.md)
- [verifying-claims.md](references/protocols/verifying-claims.md)
- [verification-toolchain.md](references/protocols/verification-toolchain.md)
