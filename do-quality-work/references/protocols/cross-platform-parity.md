# Protocol: Cross-Platform Parity & Inclusion

**Principle:** TerraFlo is one product across many clients. If a feature makes sense everywhere, it ships everywhere. Divergence is allowed when platforms *genuinely* differ, and it is always a conscious, documented choice — never an accident of who happened to build it first.

## Platforms we care about

- **macOS** — primary focus today
- **iOS** — actively shipping
- **Android** — launch-critical for public launch, but not yet launch-ready
- **Web admin** — different audience (admins, not athletes); parity rules below apply only where scope overlaps
- **Future platforms** (e.g. tvOS, watchOS) — slot in under the same rules when added

## The parity rule

For every user-facing feature or behavior change:

1. **Decide the intended platform scope up front**, not after the code is written.
   - Options: *All athlete clients* / *macOS + iOS only* / *Single-platform by design* / *Admin-only*.
   - Default scope is **all athlete clients** unless there's a reason otherwise.
2. **Record the scope in `requirements.md`** with per-platform status, and keep it current in `PROJECT_STATE.md`.
3. **If the feature lands on one platform first**, the others are tracked as open items owned by their respective personas (Ishaan / Aarav). They don't quietly fall off the list.
4. **If a feature is single-platform by design**, write one sentence of justification in `requirements.md` or `decisions.md`. "The tvOS client doesn't have BLE pairing because tvOS doesn't expose Core Bluetooth peripheral APIs" is a good justification. "Only built it for macOS because that's what I was working on" is not.

## Legitimate reasons to diverge

- **Platform capability differs** (BLE APIs, filesystem access, background execution, input model).
- **Platform idioms differ** (macOS menu bar vs iOS sheet vs web toolbar — same outcome, different affordance).
- **Audience differs** (admin tooling vs athlete tooling).
- **Hardware differs** (watch screen size, tv input model).

## Not legitimate reasons

- "I only had time for one platform." → Track the others as open work.
- "The other platform engineer didn't ask for it." → Inclusion is the default; they shouldn't have to ask.
- "It's easier in Swift." → Move the logic into `SharedCore` so Kotlin gets it for free.

## Shared logic goes in the shared core

If a feature has business logic that could apply to more than one platform, it belongs in `SharedCore` (KMP) or `VideoGPSCore` (Swift-only when it's genuinely Swift-only). Reimplementing the same rule in Swift and Kotlin is a parity bug waiting to happen — Linnea is the default owner of shared logic, and she catches drift between platforms.

## Atlas's role

- **At task intake:** asks "what's the platform scope?" before dispatching. Updates `requirements.md` with the answer.
- **At review time:** confirms per-platform status is recorded honestly, even if only one platform is landing first.
- **At release time:** no release notes claim a feature is available on a platform where it isn't — and the docs reflect divergence, not wishful thinking.
- **Launch-critical gaps stay visible:** Harper keeps Android parity and launch-gap work visible until the public-launch bar is honestly met.

## Signal that this is failing

- A feature appears on macOS, ships, and six months later iOS users notice it's missing.
- `requirements.md` claims parity that the code doesn't have.
- The same logic exists in two platform view layers and drifts.
- A cross-platform bug is fixed on one platform only.

Any of these is Atlas's problem to surface and fix.
