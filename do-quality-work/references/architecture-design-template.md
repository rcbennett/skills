# <Architecture Design Title>

> Use only when the architecture gate triggers. Prefer precise boundaries and tradeoffs over speculative implementation detail.

**Status:** draft
**Owner:**
**Decision owner/approver:**
**Code baseline:**
**Reviewed design revision:**
**Decision record:**
**Decision question:**

## Problem And Desired Outcome

Describe the user/product problem, why the current architecture is insufficient, and the observable outcome the design must enable.

## Scope And Non-Goals

Name the users, platforms, components, and behaviors covered. List explicit non-goals so the design does not become a general cleanup project.

## Evidence And Current Architecture

Document the source evidence and current responsibilities, ownership, data/control flow, lifecycle, persistence, and failure behavior.

## Constraints And Invariants

- INV-1:

Include compatibility, safety, security/privacy, performance, cost, platform, migration, and operational constraints that materially apply.

## Open Questions And Decision-Changing Probes

| Question or assumption | Cheapest authoritative probe | Result/blocker | Decision impact |
|---|---|---|---|
| | | | |

## Options Considered

### Option A — <name>

**Shape:**
**Benefits:**
**Costs/risks:**
**When it wins:**

### Option B — <name>

**Shape:**
**Benefits:**
**Costs/risks:**
**When it wins:**

## Proposed Architecture

### Responsibilities and ownership

| Component/boundary | Owns | Authority scope and enforcement | Must not own | Inputs/outputs |
|---|---|---|---|---|
| | | | | |

### Control and data flow

Describe the important path from input to side effect, including lifecycle, concurrency, error, and teardown behavior.

### Failure handling and observability

Describe failure containment, retry/fallback, rollback, diagnostics, and how operators or developers know the system is healthy.

### Evolution, scale, and cost

Identify the workload inputs, likely next changes, design seams that support them, the first scaling/cost cliff, and the measured threshold that would justify a later redesign.

## Migration And Compatibility

Describe how existing consumers and mixed deployed versions move without dual authority. Separate code, data, and protocol rollback; identify any forward-fix-only step and how interrupted or repeated migration is handled.

For consolidation work, add a divergence table that classifies each current behavior as intentional adaptation, product policy, defect, or unresolved before choosing the canonical behavior.

## Decision And Consequences

**Chosen option:**
**Why:**
**Tradeoffs accepted:**
**Rejected options:**
**Revisit trigger:**

## Design Review Receipt

**Reviewed design revision:**
**Reviewer and lane:**
**Independence/model status:**
**Verdict:**
**Blocking finding IDs:** none

## Implementation-Plan Handoff

List the boundaries, invariants, migration order, and acceptance evidence the implementation plan must preserve.
