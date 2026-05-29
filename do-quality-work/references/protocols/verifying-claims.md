# Protocol: Verifying Claims Before Acting

**Principle:** Subagent findings — especially "X is missing/broken" — are *claims*, not facts. They are produced by narrow file reads, glob patterns, and partial views of the project. They are frequently wrong about absence. Verify before propagating, before acting, and before letting them shape Rob's priorities.

## Why this exists

Two real false positives in the first three days of this engagement:

1. **xcframework "missing"** — Morgan's architecture audit confidently claimed `SharedCore.xcframework` was absent, gating all builds. Reality: committed at `PlatformClients/apple/SharedCore.xcframework/`. The audit globbed the wrong path.
2. **App icons "needed wiring"** — Ishaan's audit listed wiring app icons into `Assets.xcassets` as an open task. Reality: iOS, macOS, watchOS, and tvOS all have populated `AppIcon.appiconset/` directories with rendered PNGs, all sharing the same brand-asset MD5.

Both were errors of *negative claim* — saying something is absent when it isn't. They cost time, polluted the blockers list, and risked driving wasted refactoring work. They also eroded trust in the team's findings overall, which is the more expensive cost.

## The rule

**Three things, in order, before a "missing/broken" finding becomes a blocker, an action, or anything Rob hears about:**

### 1. Negative claims demand evidence of search

A finding that says "X is missing" / "Y is absent" / "Z is not implemented" must include:

- **What was searched for** — exact pattern, path, or query.
- **Where it was searched** — directories, files, globs.
- **What the search returned** — quoted, not paraphrased.

Findings without this are inadmissible. Rewrite the brief or re-dispatch the agent.

### 2. Triangulate before propagating

Before forwarding a "blocker" or "critical" finding to Rob, or before acting on it as one, run an independent check with a different tool:

- **Files allegedly absent:** `git ls-files <path>`, `find . -name "<name>"`, plain `ls`. If `git ls-files` returns the path, the file is committed and present. End of investigation.
- **Symbols allegedly absent:** `grep -rn "<symbol>" <path>` across plausible locations.
- **Targets / build artifacts allegedly broken:** try the actual build command if available (see [verification-toolchain.md](verification-toolchain.md)).
- **Behaviors allegedly wrong:** read the actual implementation. Don't trust the agent's summary of how a function behaves; read the function.
- **For all "X is broken" claims: cross-check `git log --oneline pre-atlas-autonomous-2026-04-14..HEAD -- <path>` to see whether a commit since the rollback tag has already addressed it.** A claim from a stale audit becomes a false positive the moment a fix lands; the inventory pass on 2026-04-15 hit this three times for fixes that landed in commit `008d08d`.

### 3. Lived experience trumps audit findings

When a finding conflicts with Rob's stated experience ("the app builds fine"), **Rob is the source of truth.** The audit is the suspect. Investigate why the audit got it wrong — the answer often sharpens a different, real finding nearby.

Examples:
- "Build is broken because xcframework missing" + Rob: "build is fine" → audit globbed wrong path; the real finding was about something else entirely.
- "Feature is missing on platform X" + Rob: "I just used it yesterday" → audit looked at the wrong file or didn't follow a `NavigationLink`.

## How this changes briefs to subagents

When dispatching audit / review / explorer agents:

- Frame asks as **"what exists, where, in what state"** instead of **"what is missing."** Inventory > absence detection.
- For any negative claim the agent makes, the brief must require **the search performed and the result quoted.** Vague "X is missing" findings fail this requirement and must be re-issued.
- Provide the agent with **canonical project locations** (build artifact paths, asset paths, target memberships) so it doesn't have to guess.
- For anything safety-critical or build-critical, **request triangulation in the same pass** — "verify with `find` AND `git ls-files`."

## How this changes Atlas's behavior in messages to Rob

- Findings I have not personally verified must be marked as such ("the scout report claims X" instead of "X is broken").
- Lived contradictions get acknowledged immediately and tracked back to root cause, not waved off.
- Blockers list doesn't get a "BLOCKER" label until the claim is verified by Atlas (or by a confirmation pass).
- When a claim turns out wrong, retract publicly in the same channel where it was raised (commit message, blockers.md, message to Rob).

## How this changes implementation work

- Before refactoring "missing" code into existence, run `git ls-files` and `find` for the alleged-missing file. If it exists, the work is different (probably a wiring or rename issue, not new construction).
- Before deleting "dead" code, grep for callers and storyboard / xib references in addition to source.
- Before adding a "missing" UI element, check the full hierarchy — including conditional branches not visible in the immediate file.
- For decisions that contradict the code (e.g., decision says X is removed but the code has X), don't trust either; verify which is current and update the other.

## Inventory companion

To make verification cheap, this protocol pairs with an explicit inventory of known-good locations: build artifacts, asset directories, configuration files, decision records. Inventory lives at `management/inventory.md` and is refreshed when major refactors land.

When in doubt about whether something exists, **the inventory is the first place to look** — before dispatching another scout.

## Atlas's role

- Enforce all three steps before any blocker reaches Rob's view.
- Run the inventory refresh after significant moves (a new module, a deleted target, a renamed directory).
- When subagent quality drops (false-positive rate climbs), tighten brief templates rather than tolerate the noise.
- When verification finds an audit was wrong, write up *why the audit went wrong* — the meta-failure is more valuable than the specific retraction.
