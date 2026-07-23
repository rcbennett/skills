# Protocol: Design First

**Principle:** Changes that reshape a complex system need an explicit architecture decision before implementation planning. Strengthen the whole system rather than making only the local edit convenient.

## Contents

- [Choose the design depth](#choose-the-design-depth)
- [Design the user experience when it changes](#design-the-user-experience-when-it-changes)
- [Architecture gate](#architecture-gate)
- [Start from the current architecture](#start-from-the-current-architecture)
- [Required design questions](#required-design-questions)
- [Compare real alternatives](#compare-real-alternatives)
- [Design artifact](#design-artifact)
- [Design review](#design-review)
- [Handoff to implementation planning](#handoff-to-implementation-planning)
- [Failure signals](#failure-signals)

## Choose the design depth

Use the smallest design artifact that resolves the architectural uncertainty:

- **Local design check:** For a narrow, reversible change that stays inside an established component and ownership boundary. Answer the boundary/invariant questions in working notes; no durable design document is required.
- **Architecture note:** For a meaningful refactor or extension of an existing pattern where the target shape is mostly established. Record the current boundary, proposed responsibility change, alternatives, migration, and consequences.
- **Full architecture design:** For a new subsystem or a material change to ownership, public interfaces, persistence, control/data flow, safety/security, platform sharing, scalability, or operational behavior.

Do not skip design because implementation seems urgent. Do not require a design document merely because several files change.

## Design the user experience when it changes

For a material user-facing flow or state-model change, define the intended outcome, primary flow, empty/loading/error/cancel/recovery states, accessibility contract, platform-native adaptation, and observable success before building views. This may be a short product/UX note or a section of the implementation plan; it does not by itself require a full architecture design.

When both the experience and system shape change, approve them together far enough to prove that the architecture supports the intended states and failure behavior. Do not use visual detail to hide unresolved behavior, and do not force identical controls across platforms when native adaptations preserve the same product intent.

## Architecture gate

Create and approve a durable design before implementation when work introduces or materially changes any of these:

- module, service, subsystem, collection, or external dependency;
- public API, persisted model, protocol, event contract, or shared schema;
- cross-platform/shared-core responsibility or platform-adapter boundary;
- lifecycle, concurrency, authority, ownership, caching, or synchronization model;
- safety, security, privacy, auth, billing, or destructive side-effect boundary;
- migration with dual-read, dual-write, compatibility, or rollback complexity;
- performance, availability, scale, or cost shape;
- system-wide pattern such as observability, error handling, configuration, or dependency injection; or
- a large refactor whose success depends on assigning responsibilities differently.

If the work stays inside an approved boundary and preserves its contracts, use the local design check and then choose direct implementation or durable planning under the planning gate.

## Start from the current architecture

Before proposing a target shape:

1. Read current architecture, requirements, decisions, and relevant incident evidence.
2. Identify the components and owners that currently perform the behavior.
3. Trace the important input-to-side-effect path, including lifecycle, concurrency, persistence, failure, and teardown.
4. Record the architectural constraint or failure that prevents the desired outcome.
5. Separate verified current behavior from assumptions.

Avoid architecture-by-analogy. A pattern used elsewhere is evidence only after its constraints are shown to match.

When a blocking architecture claim cannot be resolved through existing code, docs, traces, or a disposable test, allow a bounded non-production feasibility spike. Record its decision question, time/size limit, disposal or promotion rule, and result. A spike must not silently become the production architecture or bypass design approval.

## Required design questions

Answer the questions that materially apply:

1. **Problem and outcome:** What system capability or quality must improve?
2. **Scope and non-goals:** Which users, platforms, components, and behaviors are included or explicitly excluded?
3. **Responsibility and ownership:** Which component owns each decision, state, side effect, and lifecycle? At what scope—process, device, account, store, service, or system—is that authority unique, and how is it enforced or fenced? What must platform/UI/adapter layers not own?
4. **Boundaries and contracts:** Which public interfaces, data models, events, or protocols change?
5. **Invariants:** What must remain true across success, failure, retry, cancellation, replacement, and teardown?
6. **Data and control flow:** How does information and authority move through the system?
7. **Failure containment:** How does the design fail closed or degrade safely? How is partial failure recovered?
8. **Migration and compatibility:** How do current callers and mixed deployed versions move without parallel authorities or an indefinite compatibility layer? Distinguish code, data, and protocol rollback, and identify any forward-fix-only step.
9. **Observability:** What evidence proves the architecture is operating as designed?
10. **Evolution:** Which likely future changes are easy or hard after this decision?
11. **Performance, scale, and cost:** Which workload inputs drive behavior, what is the first credible cliff, and what measured threshold would trigger a redesign?
12. **Security, privacy, and safety:** Which trust or physical boundaries apply?
13. **Reversibility:** What can be rolled back, and what becomes expensive to change?

Do not invent scale numbers or future requirements. Name uncertainty and its revisit trigger.

When consolidating behavior from existing implementations, inventory their differences before choosing a canonical path. Classify each difference as intentional platform adaptation, product policy, defect, or unresolved; do not silently make the first implementation the specification.

## Compare real alternatives

Consider at least two credible shapes when the decision is material. Include the current/no-change path when it is genuinely viable.

For each option, state:

- responsibilities and interactions;
- benefits;
- complexity and operational cost;
- failure modes;
- migration/rollback cost;
- where it is the better choice; and
- evidence that would change the decision.

Do not create a weak alternative merely to justify the preferred design.

## Design artifact

Follow the repository's existing design convention. If none exists, use:

```text
docs/designs/<YYYY-MM-DD>-<short-slug>.md
```

Start from [../architecture-design-template.md](../architecture-design-template.md) when no project template exists, and remove irrelevant sections.

The approved artifact records:

- code and design baseline;
- scope and non-goals;
- decision question;
- evidence and current architecture;
- constraints and invariants;
- alternatives and tradeoffs;
- proposed responsibilities, interfaces, and flow;
- failure handling and observability;
- migration and rollback;
- accepted consequences; and
- revisit triggers.

Record the material decision in the repository's decision log or ADR location. The design is the canonical system-shape artifact; the decision record briefly preserves why it was chosen and links the design rather than duplicating it.

## Design review

Default to one independent architecture reviewer. Add one domain, safety, security, data, platform, or operations reviewer only when a distinct material risk needs specialist judgment.

Reviewers ask:

- Does the current-state model match the code and evidence?
- Does responsibility have one clear owner?
- Does the design solve the system problem rather than relocate it?
- Are boundaries cohesive and platform divergence intentional?
- Are failure, teardown, migration, rollback, and observability complete?
- Is the abstraction justified by current needs and credible evolution?
- Are performance, cost, security, privacy, and safety risks bounded?
- Is the design specific enough to guide a plan without prematurely specifying every class or method?

Outcome: **approve**, **approve with required changes**, or **reject with a stronger alternative**. Resolve blocking design findings before creating implementation tasks.

The named decision owner accepts the review outcome, resolves blockers, and changes the artifact status to approved. A reviewer advises and gates; they do not silently become the decision owner.

## Handoff to implementation planning

An approved design hands these items to `implementation-planning.md`:

- target responsibilities and ownership;
- changed boundaries and current callers;
- preserved invariants;
- migration order;
- compatibility and rollback constraints;
- authoritative acceptance evidence; and
- explicit non-goals.

The implementation plan may choose sequencing and local mechanics, but it must not quietly redesign these boundaries. A material design change returns to a design delta and decision update.

## Failure signals

- A plan or code change assigns responsibility before current ownership is traced.
- A new abstraction exists only to make tests or future possibilities easier.
- Multiple clients or services make the same policy decision independently.
- Migration creates two long-lived authorities.
- Failure, teardown, or rollback is deferred until implementation.
- The design optimizes one module while worsening the overall data/control flow.
- Review occurs after the architectural code is already written.
