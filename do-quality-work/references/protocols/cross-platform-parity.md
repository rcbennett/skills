# Protocol: Cross-Platform Parity And Inclusion

**Principle:** One product can use platform-native adapters without duplicating product policy. Platform scope and intentional divergence are design decisions, not implementation accidents.

## Establish the actual platform set

Read the project's current requirements, source targets, release state, and platform decisions. Do not rely on a hard-coded or remembered client list.

For every affected behavior, record:

- the intended product outcome;
- each in-scope client or platform family;
- current and target status;
- shared policy owner;
- platform-owned adaptation;
- authoritative acceptance evidence; and
- any intentional exclusion with rationale and owner.

Default to all clients that can support the product outcome. An incremental rollout is a sequence, not permission to lose the remaining platforms.

## Sequence architecture and parity work

When work changes shared/platform responsibility, public contracts, lifecycle authority, or system shape, use `design-first.md` as the primary architecture phase and treat parity as a design constraint. After the architecture is approved, use this protocol as the primary migration and parity-assessment phase.

During design, probe the most constrained materially different platform early. During implementation, exercise representative adapters from each platform family soon enough that their lifecycle, storage, input, or media constraints can still change the architecture.

## Adjudicate existing divergence before consolidation

Before moving duplicated behavior into a shared owner, inventory the current implementations:

| Platform/client | Current behavior and owner | Intended classification | Target owner/adaptation | Evidence or decision needed |
|---|---|---|---|---|
| | | intentional adaptation / product policy / defect / unresolved | | |

Do not declare one existing client canonical by default. Resolve product-policy and unresolved differences explicitly. Preserve platform adaptations only when they support the same product intent or a documented platform-specific requirement.

Create shared semantic or conformance examples for the decided behavior before deleting divergent owners. Runtime evidence must still cover representative real adapters; shared tests alone do not prove platform integration.

## Keep policy shared and adaptation local

Put portable product rules, state transitions, calculations, ordering, and policy decisions in the project's shared domain layer when one exists. Platform clients should normally own only:

- native API and event translation;
- UI/input presentation;
- lifecycle hooks;
- platform storage or media primitives behind approved contracts; and
- native side effects that cannot live in the shared layer.

Do not force technology sharing where the runtimes cannot share code. In that case, define one semantic contract and conformance evidence so separate adapters do not become separate policy authorities.

## Legitimate reasons to diverge

- Platform capability or operating-system policy differs.
- Native interaction or accessibility idioms differ while preserving the same outcome.
- Audience, hardware, screen, or input model materially differs.
- A staged rollout is explicit, owned, time-bounded, and visible in project truth.

Schedule, convenience, language preference, or “the other client did not ask” are not architectural reasons to diverge.

## Keep status honest

Use the repository's requirements, project-state, release, or plan documents to record current per-platform status. Do not claim parity from a shared build alone, and do not claim a feature on a platform whose runtime path was not validated.

Final parity evidence should include:

- shared semantic or contract checks;
- focused runtime evidence for every in-scope materially different adapter;
- lifecycle, failure, and teardown behavior where relevant;
- a static ownership/deletion audit after convergence; and
- documented intentional divergence and remaining rollout work.

## Failure signals

- One platform implementation becomes the specification without adjudication.
- The same policy decision remains in multiple client layers.
- A platform adapter reacquires shared policy during migration.
- A feature is reported as cross-platform from shared tests only.
- Project status omits an unimplemented client or an intentional exclusion.
- A cross-platform defect is fixed on only one client without a scoped decision.
