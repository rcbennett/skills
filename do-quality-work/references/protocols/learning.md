# Protocol: Learning As We Go

**Principle:** Every task is a learning event. What we discover must outlive the task, or we'll rediscover it next month.

## What every team member does

On any non-trivial task, before marking it complete, the owner answers three questions:

1. **What did I learn that wasn't obvious from the code?**
   Surprising behavior, hidden constraints, a library quirk, a decision someone made three commits ago that matters now.
2. **Where does this learning belong?**
   In code (a comment that explains a non-obvious *why*), in project docs, in a persona, in memory, or in `decisions.md`.
3. **Did I invalidate anything we already believed?**
   A stale assumption in `decisions.md`, a persona's "owns" list that's wrong, a memory that should be updated or deleted.

If the answer to #1 is "nothing," that's a valid answer — but the owner should have asked.

## Where learnings land

Match the learning to the right home. More than one may apply.

| Kind of learning | Home |
|---|---|
| Why the code does something non-obvious | Inline comment (one line, WHY only) |
| A product scope or per-platform status change | `requirements.md` + `PROJECT_STATE.md` |
| An architectural or library choice, and the reason | `decisions.md` (short ADR entry) |
| A shared model or service shape changed | `data_structures.md` |
| A recurring user preference, correction, or validated judgment call | Memory at `~/.claude/projects/-Users-rob-dev-TerraFlo/memory/` |
| A persona's responsibilities or watch-outs shifted | The persona file under `management/personas/` |
| A new repeatable process | A new or updated protocol under `management/protocols/` |
| A tactic or style norm that isn't a process | `management/conventions/` (create when needed) |

## What does NOT belong in memory or docs

- Facts already derivable from the current code, git history, or existing docs
- Ephemeral task state ("currently working on X")
- Debugging recipes whose fix is already in the diff
- Learnings that turn out to be wrong — those get *deleted*, not archived

## Atlas's role

- Before accepting returned work from a subagent, ask: "what did you learn, and where does it live now?"
- Reject "done" claims that don't address the three questions when the task warranted it.
- Periodically prune: stale memory records, outdated persona entries, and `decisions.md` entries that history has overturned. A doc that lies is worse than no doc.

## Subagent briefs

Every subagent brief for non-trivial work includes:

> When you finish, include a short **Learnings** section: what was surprising, where it should live (code / docs / memory / persona), and anything we previously believed that this invalidates. If nothing was surprising, say so.

## Signals that learning isn't happening

- Two tasks in a row rediscover the same quirk.
- A persona file hasn't been touched in months despite the area being worked heavily.
- `decisions.md` entries disagree with the code and nobody has noticed.
- Memory records cite files or functions that no longer exist.

Any of these is a protocol-level bug and Atlas fixes it.
