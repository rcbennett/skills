# Protocols

Protocol references for proportionate, evidence-led work. Project-local protocols take precedence when present.

| Protocol | Purpose |
|---|---|
| [learning-retrieval.md](learning-retrieval.md) | Prior lessons shape the next attempt; retrieve relevant persona memories, calibration, playbooks, and decisions before work starts. |
| [learning.md](learning.md) | One root session assessment captures only surprising, durable findings that are in scope to preserve. |
| [after-action-review.md](after-action-review.md) | Surprises, failures, milestones, and repeated rework become blameless expected-vs-actual reviews with concrete changes. |
| [persona-calibration.md](persona-calibration.md) | Persona judgment changes only from meaningful catches, misses, false positives, noisy reviews, or assignment-fit evidence. |
| [playbook-library.md](playbook-library.md) | Repeated successful tactics become reusable playbooks with applicability, verification, and failure modes. |
| [team-health.md](team-health.md) | Team conditions for learning are assessed: safety, dependability, clarity, meaning, impact, load, and learning culture. |
| [code-review.md](code-review.md) | Review current production changes with bounded, risk-partitioned lanes and artifact receipts. |
| [plan-review.md](plan-review.md) | Review only deeply enough to make the first safe working slice executable and evidence-producing. |
| [design-first.md](design-first.md) | Every change considers system design; important changes earn a design review. Built for flexibility, maintainability, and bounded cost at scale. |
| [cross-platform-parity.md](cross-platform-parity.md) | Features land on all platforms that can carry them. Divergence is intentional, documented, and justified. |
| [model-selection.md](model-selection.md) | Match models to work and use model diversity at important decision boundaries without adding ceremony. |
| [red-team.md](red-team.md) | High-risk work gets attacked for exploit paths, operational failures, hidden assumptions, missing rollback, weak observability, and abuse cases before it is trusted. |
| [steelman.md](steelman.md) | Serious alternatives are rejected only after their strongest coherent case, win conditions, and decision-changing evidence are understood. |
| [pre-mortem.md](pre-mortem.md) | Launches, deploys, migrations, and fragile changes assume future failure first, then define prevention, detection, rollback, and owners. |
| [council-review.md](council-review.md) | Escalate irreversible, disputed, genuinely cross-domain, or explicitly requested decisions to a small relevant council. |
| [decision-record.md](decision-record.md) | Material choices leave a durable record of context, alternatives, rationale, consequences, evidence, and revisit triggers. |
| [verifying-claims.md](verifying-claims.md) | Subagent findings are claims, not facts. Triangulate "X is missing/broken" before propagating or acting. Lived experience trumps audit findings. |
| [verification-toolchain.md](verification-toolchain.md) | Establish the minimum evidence contract, admit fixtures deliberately, and verify changed boundaries at the right time. |

## Meta-rules

- **One primary protocol plus at most one risk overlay.** Additional overlays need distinct named risks and decision questions.
- **Evidence before ceremony.** Run the cheapest authoritative probe before detailed plans, fixtures, or broad review.
- **Protocols evolve through decisions.** Material changes to a protocol get a short entry in `decisions.md` with the reason.
- **Protocols are not ceremonies.** If a protocol isn't producing better outcomes, it's a bug. Flag it.
