# Protocol: Verification Toolchain — What I Can Test Without Rob

**Principle:** Confidence in changes comes from running them, but verification has real time, usage, and attention costs. Atlas should test as much as possible without waiting on Rob, choose the slice size that makes the verification overhead worthwhile, and say plainly where a gap remains.

## Minimum sufficient evidence contract

Before detailed planning or an expensive verification loop, define:

- **Decision question**
- **Blocking claims**
- **Cheapest authoritative evidence for each claim**
- **Prerequisites and current blockers**
- **Invalidation condition**
- **Stop condition**

Run the cheapest decisive probe first. When a prerequisite is missing, record the blocker and the closest valid fallback. Do not present source inspection, simulated output, or a mocked test as equivalent to a required runtime or measured effect.

Do not create a new fixture, simulator extension, evidence schema, or harness until existing tests and the product path have been assessed. The new infrastructure must answer a named unanswered decision question more directly or repeatably than existing evidence.

## Slice size and verification cost

Before committing to a work plan or rerunning an expensive verification loop, choose the right work unit:

- **Micro-slice:** Use when risk is high, blast radius is uncertain, reversibility is poor, the work is destructive, security/auth/PII/billing/safety is involved, or one behavior must be isolated to debug a failure.
- **Capability packet:** Use when related low- or medium-risk changes share a domain, fixture set, rollback path, reviewer group, and verification envelope. Prefer this when full evidence generation, docs rollups, broad builds, or review cycles would dominate the value of one tiny change.
- **Broader checkpoint:** Use when the goal is release/deploy/cutover readiness or when several capability packets need one final confidence pass.

Run targeted checks while iterating inside a packet. Run broad test suites, generated evidence, docs rollups, credential scans, review cycles, and commits at packet/checkpoint boundaries unless a new risk justifies doing them sooner. Do not batch unrelated work just to reduce ceremony; every packet must stay reviewable, debuggable, reversible, and explainable.

Default implementation plans to two to four checkpoints. Each task should enable the first working path, protect a high-severity invariant, or delete superseded behavior.

For a refactor, map:

```text
Changed seam -> current callers -> side effect -> preserved invariant -> authoritative evidence
```

When a lifecycle, event, concurrency, adapter, or ownership seam changes, trace the side effect through that handoff. The continued presence of old safety code is not proof that the new handoff invokes it.

## Discover the live verification path

Use project instructions, package manifests, CI configuration, and project-local verification protocols to discover exact commands. Do not copy dated test counts, device names, SDK assumptions, credentials, or model/tool rosters into this generic protocol.

Before relying on a command:

- confirm that the target, scheme, task, or script exists;
- confirm that required credentials and configuration are present without exposing secrets;
- confirm that the simulator, emulator, device, route, data, or external service needed for the decision can start; and
- distinguish an executable acceptance lane from a known manual or external gate.

## Surface-by-surface escalation when blocked

When the primary build is unavailable:

- **Compiled-language edit, build blocked:** I can't fully verify, but I can:
  - Use language-server or compiler-front-end diagnostics while naming their limitations.
  - Read the file end-to-end after editing; re-check syntax visually for the change.
  - Cross-check the public API surface used (`rg` for the symbol's definition).
  - Mark the result as reviewed but not build-verified.
- **Runtime or integration blocked:** run applicable unit/static checks, but identify the exact runtime gap.
- **Shared-core edit:** run shared tests, but keep platform integration unverified until affected platform builds or runtime checks pass.

## Required practice

Before committing a change that touches a verifiable surface:
- Run the relevant test/build command before announcing completion.
- If the command fails, investigate before committing or claiming the change is verified. Do not pile a fix-the-fix commit on top of a known broken baseline.
- If the command succeeds, report the exact command and outcome without carrying forward stale historical counts.
- For non-trivial work, state the slice-size choice when reporting: micro-slice, capability packet, or broader checkpoint, with the risk/overhead reason.

For safety or actuator behavior, verify applicable changed-boundary invariants:

- command and device identity;
- neutralization on pause, finish, background, disconnect, or ownership loss;
- fail-closed behavior; and
- no post-fence writes.

Use deterministic simulator or local-transport checks during development. When physical hardware is required for final confidence, run one physical pass against the exact final candidate revision. Move physical testing earlier only when hardware feasibility is itself unresolved.

For edits while required builds are blocked, acknowledge the gap and do not claim the change is verified.

## Atlas's role

- Pick the cheapest verification tool that exercises the change, and use it.
- When the change is too small for a behavioral test but a cheap compile, type-check, or lint path exists, still run it.
- Stop rerunning an expensive gate once it answers the decision question. Rerun only when a relevant change invalidates the evidence.
- When verification is genuinely blocked, surface that explicitly to Rob in the commit / message, not silently.
- Periodically re-attempt currently-blocked surfaces (a fresh clone, an SDK install) and update this doc when a new path opens.

## How to add a new verification path

When a new test or build surface comes online:
1. Document the exact command, working directory, prerequisites, and expected runtime in the project-local verification protocol.
2. Run it once against a known baseline and record what a passing result establishes.
3. From that project change forward, use it for work touching the verified surface until newer evidence invalidates it.
