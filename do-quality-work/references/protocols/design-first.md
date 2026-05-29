# Protocol: Design First

**Principle:** Design is not a phase; it's a habit. Every change considers its impact on the system, every important change earns a design review, and every architectural choice is made with flexibility, maintainability, and scalable growth in mind — without overspending today for capacity we don't yet need.

## Two kinds of design, both required

- **UX design** — how the user experiences the change. Owned by Kenji (interaction) and Noa (visual/brand), informed by Sam (product intent) and Dr. Voss (domain correctness).
- **Software/system design** — how the code and infrastructure are shaped. Owned by Morgan (architecture), with the relevant platform engineer(s), Linnea for shared logic, Diego for backend, and Mira for cost shape.

A change that touches users needs both. A change that's purely internal still needs software design thinking.

## Every change asks five questions

Before any non-trivial implementation starts, the owner (or Atlas on their behalf) answers:

1. **What part of the system does this touch, and what's downstream of it?** Layer boundaries, shared-core impact, per-platform reach.
2. **Does this change the shape of the system?** New module, new dependency, new data flow, new abstraction — or a one-file tweak?
3. **What's the flexibility cost?** Does this make a likely future change harder? Does it lock us into a vendor, a schema, or a pattern we'll regret?
4. **What's the maintenance cost?** Who has to understand this next quarter? Is it legible without the author in the room?
5. **What's the cost-at-scale picture?** If usage grows 10× or 100×, does this hold? Per-read Firestore costs, Cloud Function invocation costs, Storage egress — roughed out, not ignored. See [model-selection.md](model-selection.md) and the FinOps persona for cost review.

If the answers are small and obvious, proceed. If they aren't, the change needs a design review.

## When a design review is required

A design review is mandatory for:

- **New modules, services, or collections** (new Firestore collection, new SharedCore type family, new Cloud Function, new admin surface).
- **Changes to public APIs** of `SharedCore`, `VideoGPSCore`, or server endpoints.
- **Data model changes** that touch persisted state (Firestore schemas, on-device project files, overlay export formats).
- **Cross-cutting patterns** (logging, error handling, concurrency model, caching).
- **Anything with material cost or scaling implications** (new query patterns, new background jobs, new media pipelines).
- **Anything the author or Atlas thinks warrants one.** Opting in is always allowed; opting out is not.

Pure bug fixes, localized refactors, copy changes, and dependency version bumps don't require a design review unless they ripple.

## What a design review looks like

Lightweight by default. The author produces a short design note — not a novel — covering:

1. **Problem & intent** — what are we trying to enable, in one paragraph.
2. **Proposed shape** — the components, data, and interactions. Prose or a sketch; no mandatory format.
3. **Alternatives considered** — at least one, with why it was rejected. "No alternatives considered" is a red flag.
4. **Flexibility & reversibility** — what's easy to change later, what's hard, and why that's acceptable.
5. **Scale & cost** — expected load today, plausible load at 10× and 100×, and what breaks first at each step.
6. **Open questions** — what we don't know yet that would change the design.

Reviewers (per [code-review.md](code-review.md), so: different persona, different model) assess:

- Does the proposal actually solve the stated problem?
- Does it respect existing architecture (`decisions.md`, layer boundaries, local-first, SharedCore ownership)?
- Is it the simplest shape that leaves the right doors open?
- What's missing from the "what breaks first" analysis?
- Is the cost curve acceptable *and* bounded?

Outcome: **approve**, **request changes**, or **reject with a counter-proposal**. Approved designs become short ADR entries in `decisions.md`.

## Designing for where we're going, without paying for it today

We start small and intend to stay inexpensive as long as we can — *and* we refuse to paint ourselves into corners. The balance:

- **Prefer reversible choices.** If we can defer a decision without cost, defer it.
- **Pick boring technology where it won't bottleneck us.** Fancy only earns its keep when it solves a real problem.
- **Put abstractions at the seams, not inside components.** A clean module boundary lets us swap implementations later; premature interfaces inside a module are pure cost.
- **Keep shared logic in `SharedCore` / `VideoGPSCore`.** Per-platform reimplementation is a scaling tax we will not pay.
- **Budget for growth, don't build for it.** Document the scaling cliff ("this design works fine to ~N users / M writes/day; past that, do X"). Don't implement X until we see N/2 on the horizon.
- **Instrument early, optimize later.** Cheap telemetry now beats expensive archaeology later.
- **Cost is a design constraint.** Mira (FinOps) reviews designs whose cost curve isn't obviously benign; Yusuf (Finance) weighs in when the choice affects burn meaningfully.

## UX design lives by the same rules

- **Design before pixels.** Flows and states before a single view is written.
- **Empty, loading, and error states are first-class** — Kenji won't approve a design that only shows the happy path.
- **Platform-native affordances** over cross-platform uniformity.
- **Brand tokens** (Noa) are consumed, not overridden inline.
- **Accessibility is a design input,** not a polish pass.

## Atlas's role

- Asks the five questions at task intake. Decides whether a design review is required.
- Picks reviewers (persona + model) and gates implementation on design approval for covered changes.
- Makes sure approved designs land in `decisions.md` and that `requirements.md`/`PROJECT_STATE.md` reflect scope honestly.
- Keeps the bar honest: no ceremonial design reviews for changes that don't need them; no design-by-ambush for changes that do.

## Signals that this is failing

- A new Firestore collection appears without a design note.
- Two platforms implement the same logic independently and drift.
- A feature ships that would have failed at 2× current load.
- A design review happens *after* the code is written (this is a post-mortem, not a review).
- Cost surprises at the end of the month that nobody predicted.

Any of these is Atlas's problem to surface.
