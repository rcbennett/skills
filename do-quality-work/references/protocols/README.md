# Protocols

How the TerraFlo team actually works. Protocols are binding — Atlas enforces them. If a protocol is wrong, change the protocol; don't quietly ignore it.

| Protocol | Purpose |
|---|---|
| [learning-retrieval.md](learning-retrieval.md) | Prior lessons shape the next attempt; retrieve relevant persona memories, calibration, playbooks, and decisions before work starts. |
| [learning.md](learning.md) | Every work session ends with a learning assessment; findings are captured in the right place, including persona memories. |
| [after-action-review.md](after-action-review.md) | Surprises, failures, milestones, and repeated rework become blameless expected-vs-actual reviews with concrete changes. |
| [persona-calibration.md](persona-calibration.md) | Persona judgment improves from evidence about useful signal, false positives, missed issues, and assignment fit. |
| [playbook-library.md](playbook-library.md) | Repeated successful tactics become reusable playbooks with applicability, verification, and failure modes. |
| [team-health.md](team-health.md) | Team conditions for learning are assessed: safety, dependability, clarity, meaning, impact, load, and learning culture. |
| [code-review.md](code-review.md) | No change lands without a different viewpoint, from a different mind and usually a different model. |
| [plan-review.md](plan-review.md) | No non-trivial plan executes until it's been reviewed by a different persona on a different model — multiple personas when the plan spans concerns. |
| [design-first.md](design-first.md) | Every change considers system design; important changes earn a design review. Built for flexibility, maintainability, and bounded cost at scale. |
| [cross-platform-parity.md](cross-platform-parity.md) | Features land on all platforms that can carry them. Divergence is intentional, documented, and justified. |
| [model-selection.md](model-selection.md) | Pick the right model like you pick the right team member. The reviewer is always a different model than the author. |
| [red-team.md](red-team.md) | High-risk work gets attacked for exploit paths, operational failures, hidden assumptions, missing rollback, weak observability, and abuse cases before it is trusted. |
| [steelman.md](steelman.md) | Serious alternatives are rejected only after their strongest coherent case, win conditions, and decision-changing evidence are understood. |
| [pre-mortem.md](pre-mortem.md) | Launches, deploys, migrations, and fragile changes assume future failure first, then define prevention, detection, rollback, and owners. |
| [council-review.md](council-review.md) | Important decisions get the whole active team reviewing the current artifact, synthesizing weaknesses and opportunities into a forward plan with at least 75% agreement. |
| [decision-record.md](decision-record.md) | Material choices leave a durable record of context, alternatives, rationale, consequences, evidence, and revisit triggers. |
| [verifying-claims.md](verifying-claims.md) | Subagent findings are claims, not facts. Triangulate "X is missing/broken" before propagating or acting. Lived experience trumps audit findings. |
| [verification-toolchain.md](verification-toolchain.md) | What I can test myself without Rob, when to run it, and how to balance verification overhead against progress by choosing micro-slices, capability packets, or broader checkpoints based on risk. |

## Meta-rules

- **One change, one protocol violation, one conversation.** If a protocol got skipped, Atlas surfaces it and we either fix the work or fix the protocol.
- **Protocols evolve through decisions.** Material changes to a protocol get a short entry in `decisions.md` with the reason.
- **Protocols are not ceremonies.** If a protocol isn't producing better outcomes, it's a bug. Flag it.
