# Protocols

How the TerraFlo team actually works. Protocols are binding — Atlas enforces them. If a protocol is wrong, change the protocol; don't quietly ignore it.

| Protocol | Purpose |
|---|---|
| [learning.md](learning.md) | Every team member learns from what they do; findings are captured, not lost. |
| [code-review.md](code-review.md) | No change lands without a different viewpoint, from a different mind and usually a different model. |
| [plan-review.md](plan-review.md) | No non-trivial plan executes until it's been reviewed by a different persona on a different model — multiple personas when the plan spans concerns. |
| [design-first.md](design-first.md) | Every change considers system design; important changes earn a design review. Built for flexibility, maintainability, and bounded cost at scale. |
| [cross-platform-parity.md](cross-platform-parity.md) | Features land on all platforms that can carry them. Divergence is intentional, documented, and justified. |
| [model-selection.md](model-selection.md) | Pick the right model like you pick the right team member. The reviewer is always a different model than the author. |
| [verifying-claims.md](verifying-claims.md) | Subagent findings are claims, not facts. Triangulate "X is missing/broken" before propagating or acting. Lived experience trumps audit findings. |
| [verification-toolchain.md](verification-toolchain.md) | What I can test myself without Rob (CloudFunctions npm, web admin npm, SharedCore gradle). What I can't (Xcode builds, on-device behavior). |

## Meta-rules

- **One change, one protocol violation, one conversation.** If a protocol got skipped, Atlas surfaces it and we either fix the work or fix the protocol.
- **Protocols evolve through decisions.** Material changes to a protocol get a short entry in `decisions.md` with the reason.
- **Protocols are not ceremonies.** If a protocol isn't producing better outcomes, it's a bug. Flag it.
