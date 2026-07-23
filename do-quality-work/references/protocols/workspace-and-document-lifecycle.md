# Protocol: Workspace And Document Lifecycle

**Principle:** Clean as you go by giving every task-owned repository and document artifact an explicit disposition. Preserve work before cleanup; do not confuse an empty worktree with a safely completed task.

## Contents

- [When to use this protocol](#when-to-use-this-protocol)
- [Define clean proportionately](#define-clean-proportionately)
- [Establish ownership before cleanup](#establish-ownership-before-cleanup)
- [Manage source-control state](#manage-source-control-state)
- [Manage document roles](#manage-document-roles)
- [Reconcile at checkpoints and completion](#reconcile-at-checkpoints-and-completion)
- [Handle blocked work](#handle-blocked-work)
- [Guard destructive cleanup](#guard-destructive-cleanup)
- [Failure signals](#failure-signals)

## When to use this protocol

Read this protocol when the work creates or adopts a branch, worktree, stash, temporary directory, generated artifact, or multiple work documents, or when cleanup, archival, merge, rebase, release, migration, deletion, or handoff is in scope.

For a direct local change that creates none of those, a before/after worktree check is enough. Do not run a full repository inventory after every small edit.

## Define clean proportionately

Clean means:

- no unique task content is stranded only in an unnamed or unexplained local state;
- every task-created or task-adopted artifact is active for a stated reason, durably preserved, archived under the repository convention, or safely removed;
- durable project truth matches the implemented state;
- completed work artifacts no longer appear active; and
- pre-existing or unrelated user state remains untouched and is reported when it affects the handoff.

Clean does not require an empty global branch list, deletion of another task's state, merging beyond the user's request, or removal of evidence needed to resume blocked work.

## Establish ownership before cleanup

Before creating or adopting non-trivial workspace state, record enough baseline to distinguish:

- pre-existing or unrelated state;
- state created by this task; and
- existing state explicitly adopted into this task.

Track the task-owned delta, not an exhaustive ledger of every repository file. For merge, rebase, release, migration, branch cleanup, machine switch, or credible hidden-state risk, use the repository's cleanup playbook or inspect at least:

```text
git status --short --branch
git worktree list --porcelain
git branch -vv
git stash list --date=local
git clean -nd
```

Treat read-only inventory as evidence, not authorization to remove what it finds.

## Manage source-control state

- **Branches:** Give task-created branches a purpose and retirement condition. Before deletion, prove that their unique content is merged, published, intentionally abandoned with authorization, or preserved elsewhere. After a squash merge, compare tree or content equivalence; ancestry or a "merged" label alone is insufficient.
- **Worktrees:** Remove a task-created worktree only after its changes are clean or durably preserved and its branch still has an intentional home. Never remove a pre-existing worktree merely to make the list shorter.
- **Stashes:** Use a stash as a temporary bridge, not durable storage. Before completion, apply and finish it, convert its contents into a named branch/commit/follow-up, or retain it with an owner and exact recovery action. Never drop an unknown or pre-existing stash.
- **Untracked and ignored files:** Preview exact candidates and distinguish generated scratch from local configuration, credentials, fixtures, user data, and sole-copy evidence. Remove only task-created targets whose value or regenerability is proven.
- **Remote state:** Delete remote branches only when the user request or repository workflow authorizes it and preservation has been verified. Report intentionally retained unmerged or review-bound branches.

An active unmerged feature branch can be a clean handoff when it is committed or otherwise preserved, named, owned, and paired with the exact next action.

## Manage document roles

Classify documents by authority and lifecycle, not only by filename or directory:

| Role | During work | When its purpose ends |
|---|---|---|
| **Active control** — plan, migration checklist, rollout tracker | Keep status, owner, next action, and evidence current | Record the final receipt; mark `complete`, `superseded`, or `cancelled`; archive under the repository convention |
| **Durable source of truth** — overall design, README, requirements, current architecture, runbook, decision/state docs | Update in the same checkpoint that changes reality | Keep canonical; update in place or explicitly supersede with a current replacement |
| **Generated evidence/deliverable** — report, HTML, screenshot, trace, export | Record provenance, candidate revision, freshness, and consumer | Retain or archive when it is the deliverable or sole evidence; remove known-regenerable scratch copies |
| **Transient scratch** — disposable probe notes, temp exports, local diagnostics | Keep only while they answer an active question | Remove the exact task-created item after its result is captured |
| **Historical** — completed plan, superseded design, closed review | Keep out of active-work surfaces | Archive with final status, date, outcome, and canonical replacement when one exists |

Use these work-document statuses where the repository has no stronger convention:

- `planning`
- `active`
- `blocked`
- `complete`
- `superseded`
- `cancelled`

`planning`, `active`, and `blocked` still need attention. Do not mark a plan `complete` while required validation remains pending or failed. Archival is a location/disposition, not a substitute for status.

Before archiving or deleting a document:

1. Read it fully enough to classify its remaining authority.
2. Reconcile durable facts into the canonical documents.
3. Check and update inbound links, indexes, or references.
4. Reuse the repository's archive location. Do not invent competing archive trees.
5. Mark the outcome and replacement so archived material cannot be mistaken for current truth.

If no archive convention exists, do not invent one during a narrow task. Mark the artifact closed and establish one adjacent archive location only when completed artifacts are already obscuring active work or the user asks for repository-wide document cleanup.

Do not archive a README, current design, policy, runbook, requirement, or project-state document merely because it is old. Do not archive false guidance as legitimate history; correct canonical truth, then delete or clearly mark the false artifact according to repository policy.

## Reconcile at checkpoints and completion

At each material checkpoint:

- remove task-created scratch that no longer supports an open question;
- reconcile task-created branches, worktrees, stashes, and generated artifacts;
- update durable source-of-truth documents changed by the checkpoint;
- update the plan's status and next action; and
- record retained items that still have a purpose, owner, and retirement condition.

At final completion or handoff, produce a compact closeout receipt:

- baseline and final branch/revision;
- task-created state removed, archived, or retained;
- unique work and where it is durably preserved;
- durable documents updated;
- work documents closed, archived, or still active;
- generated evidence retained or removed and why; and
- remaining owner, blocker, and exact next action.

Do not delay all document reconciliation until the final sweep; that creates stale truth during implementation.

## Handle blocked work

Do not perform terminal cleanup merely because progress stopped. Preserve a blocked packet with:

- blocker and invalidated assumption;
- branch/ref and worktree path;
- dirty, untracked, or stash state;
- plan and evidence paths;
- owner; and
- exact resume or abandonment decision.

Archive only after the work is explicitly completed, superseded, cancelled, or abandoned with authority.

## Guard destructive cleanup

Before removing a branch, worktree, stash, file, directory, or document:

- resolve the exact target;
- prove content preservation, lack of unique value, or regenerability;
- confirm it is task-owned or explicitly in scope;
- use a dry-run or recoverable move when available;
- protect canonical, release, and user-state boundaries; and
- verify the result independently afterward.

When ownership or value is ambiguous, preserve and report the item rather than guessing.

## Failure signals

- A clean current worktree hides unique content in a branch, worktree, or stash.
- A task-created stash or temp directory survives without an owner or recovery action.
- Branch deletion relies only on ancestry or a merged label after a squash merge.
- Broad cleanup touches pre-existing, ignored, generated, or user data without classification.
- A completed plan or report remains in an active location with an active-looking status.
- A durable design, README, requirement, or runbook drifts behind the implementation.
- Several documents claim to be the current source of truth.
- A blocked task is archived or dismantled before its resume state is preserved.
