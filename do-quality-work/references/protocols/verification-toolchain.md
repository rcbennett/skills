# Protocol: Verification Toolchain

The [main skill](../../SKILL.md) owns verification depth, work sizing, and review gates. This protocol helps choose authoritative checks for the affected path. Passing tests and independent review answer different questions; neither substitutes for the other.

## Choose sufficient evidence

Identify the requested result, changed boundary, decisive observation, and stop condition. Add prerequisites, blocking claims, and invalidation conditions when uncertainty makes them useful. Use focused behavior tests and affected builds by default; broaden integration, failure, and recovery checks for named risks or repository gates.

Tests should protect a meaningful behavior/invariant and detect the defect in question. Avoid reproducing implementation details or mocking around the changed boundary. Update or remove obsolete implementation-specific tests while preserving valid behavior coverage. Assess existing tests and the real product path before adding fixtures, simulators, schemas, or a harness.

For refactors, trace `boundary -> callers -> side effect -> invariant -> evidence`. The continued presence of safety logic does not establish that a new lifecycle, concurrency, event, or ownership handoff still invokes it. Verify consumer migration and retirement alongside behavior preservation.

## Discover executable checks

Use live project instructions, manifests, CI configuration, and local protocols for exact commands. Confirm the target/script exists, prerequisites are present without exposing secrets, and the required runtime/environment can start. Do not hard-code old SDKs, device names, historical test counts, or credentials into generic guidance.

Run narrow checks while iterating. At a coherent candidate/checkpoint, run required broader checks once. Repeat only for relevant changes, failures, or unresolved risks that invalidate confidence. Do not expand testing merely because time remains or because a file changed.

## Build and process monitoring

Use direct process/completion tools under [model-selection.md](model-selection.md), with bounded waits and backoff consistent with responsiveness. Retain command, directory, candidate, process ID, log location, and exit result. Avoid repeated model turns over unchanged logs. Unexpected output or failure calls for diagnosis with appropriate capability, not repeated automatic restarts.

## Handle failures and blocked surfaces

Investigate enough to separate a patch failure from a pre-existing baseline issue. Fix relevant failures within scope; do not silently take ownership of unrelated repairs. State precisely what remains unverified.

- Build blocked: use applicable compiler-front-end/static diagnostics and source/API checks, marking the result as not build-verified.
- Runtime/integration blocked: run valid local/unit checks, retaining the exact runtime gap.
- Shared-core changed: shared checks do not prove every affected platform adapter integrates correctly.

Do not claim final validation or completion when a required gate is pending or failed. Preserve a resumable handoff. Do not rerun an unavailable expensive gate without a changed prerequisite or a reason it may now succeed.

## Safety and hardware

For affected actuator/safety boundaries, verify command/device identity, neutralization on pause/finish/background/disconnect/ownership loss, fail-closed behavior, and no writes after the terminal fence. Distinguish requested, locally accepted/rejected, written, acknowledged, and measured effects.

Use deterministic local/simulator evidence during development. Validate physical behavior against the exact final candidate when required; test hardware early when feasibility is unknown. A source/static pass or simulated output does not establish a measured physical effect.

## Record reusable verification paths

Document a new repeatable check in the project's existing verification location with command, directory, prerequisites, expected duration, and what a pass proves. Run it against an appropriate baseline. Keep the final response to meaningful results and gaps; exact command receipts can live in the plan or evidence artifact.
