# Protocol: Learning Retrieval Before Work

**Principle:** A team member only improves if prior lessons shape the next attempt. Capture after work, retrieve before work.

## When to use this

Use this before meaningful execution, review, task assignment, Talent Planning, an After Action Review, or any task in an area where the team has prior persona memories, playbooks, decisions, or known failure modes.

Skip only when the work is tiny, no project context exists, or retrieval would add ceremony without changing decisions.

## Retrieval sources

Check the smallest relevant set of sources, in this order:

1. Current user prompt, explicit constraints, and newest instructions.
2. `management/personas/executive/persona.md` and `management/personas/executive/learnings.md` when assignment, management, or prioritization is involved.
3. Assigned members' `persona.md`, `learnings.md`, and `calibration.md`.
4. Relevant `management/playbooks/` entries.
5. Project truth sources such as `decisions.md`, `requirements.md`, `PROJECT_STATE.md`, `data_structures.md`, and `management/inventory.md`.
6. Active memory system entries when the learning is user preference, validated recurring judgment, or cross-session workflow context.

Do not bulk-load everything. Retrieve only what plausibly affects this session's decisions, risks, verification, or communication.

## Required output before work

Before starting substantial work, keep a compact internal retrieval note:

- `Relevant lessons`: prior lessons that affect this session.
- `Known failure modes`: mistakes this member or reviewer must avoid.
- `Applicable playbooks`: reusable tactics to follow.
- `Calibration signals`: reviewer or owner strengths, weak spots, false-positive patterns, or confidence limits.
- `Stale or conflicting memory`: anything that needs verification before use.

Surface this to the user only when it changes the plan, the assignment, the risk, or the final summary.

## Rules

- Treat retrieved memories as evidence, not authority. Current code, current docs, and current user instructions beat stale memory.
- If a retrieved memory is wrong or stale, update or supersede it during the session instead of silently ignoring it.
- If retrieval prevents a mistake, record that in the session learning summary.
- If retrieval finds nothing useful, say so only when the final output requires a learning or protocol report.

## Closing the loop

At session end, note whether retrieved lessons helped, misled, or were missing. Use that result to update:

- The responsible member's `learnings.md`.
- The member's `persona.md` if behavior should change.
- `calibration.md` if review quality, assignment fit, or false-positive rate changed.
- A playbook when the session produced a repeatable tactic.

## Atlas's role

- Enforce retrieval before assigning non-trivial work.
- Keep retrieval focused; do not turn memory lookup into archaeology.
- Prefer exact file paths and evidence snippets over vague references.
- Make stale memory visible and fix it when it affects the work.
