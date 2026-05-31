# Protocol: Learning As We Go

**Principle:** Every work session is a learning event. What we discover must outlive the session, or we'll rediscover it next month.

## What every team member does

At the end of any non-trivial work session, before the final response, the owner answers three questions. A work session means completing the instruction in the user's prompt, not each individual task executed inside that session.

1. **What did I learn that wasn't obvious from the code?**
   Surprising behavior, hidden constraints, a library quirk, a decision someone made three commits ago that matters now.
2. **Where does this learning belong?**
   In code (a comment that explains a non-obvious *why*), in project docs, in persona memories, in memory, or in `decisions.md`.
3. **Did I invalidate anything we already believed?**
   A stale assumption in `decisions.md`, a persona's "owns" list that's wrong, a memory that should be updated or deleted.

If the answer to #1 is "nothing," that's a valid answer, but the owner must say so in the session summary.

## Structured learning entry

Use this structure for durable persona or project learnings:

```markdown
## <YYYY-MM-DD> - <Short lesson label>

**Source/Evidence:**
**Trigger:**
**Lesson:**
**Applies when:**
**Avoid when:**
**Behavior change:**
**Confidence:** low / medium / high
**Supersedes:**
**Promote to persona.md:** yes/no
**Review due:**
```

Keep entries short. If the same lesson applies across multiple future sessions, consider promoting it into a playbook.

## Where learnings land

Match the learning to the right home. More than one may apply.

| Kind of learning | Home |
|---|---|
| Why the code does something non-obvious | Inline comment (one line, WHY only) |
| A product scope or per-platform status change | `requirements.md` + `PROJECT_STATE.md` |
| An architectural or library choice, and the reason | `decisions.md` (short ADR entry) |
| A shared model or service shape changed | `data_structures.md` |
| A recurring user preference, correction, or validated judgment call | Active Codex memory update mechanism, or the project's documented memory policy |
| A persona's responsibilities, skills, review lens, or watch-outs shifted | `management/personas/<member-slug>/persona.md` |
| A persona learned a durable tactic, caution, preference, or coordination pattern | `management/personas/<member-slug>/learnings.md` |
| A persona's review quality, assignment fit, false positives, or missed issues changed trust | `management/personas/<member-slug>/calibration.md` |
| A repeated tactic became a reusable procedure | `management/playbooks/<slug>.md` or `management/personas/<member-slug>/playbooks/<slug>.md` |
| A new repeatable process | A new or updated protocol under `management/protocols/` |
| A tactic or style norm that isn't a process | `management/conventions/` (create when needed) |

## Learning lifecycle

1. Capture new lessons in the narrowest useful home.
2. Reuse them through [learning-retrieval.md](learning-retrieval.md) before future work.
3. Promote repeated, validated behavior changes from `learnings.md` into `persona.md`.
4. Promote repeatable tactics into playbooks when they would save future work or prevent mistakes.
5. Record judgment-quality evidence in `calibration.md`, not in the persona narrative.
6. Supersede or delete lessons that prove wrong. Do not archive false guidance as if it were still useful.
7. Review stale persona memories during Talent Planning, AARs, and executive retrospectives.

## What does NOT belong in memory or docs

- Facts already derivable from the current code, git history, or existing docs
- Ephemeral task state ("currently working on X")
- Debugging recipes whose fix is already in the diff
- Learnings that turn out to be wrong — those get *deleted*, not archived

## Atlas's role

- Before final response, require one session-level learning assessment for the completed prompt, not a separate learning ritual after every subtask.
- Before accepting returned work from a subagent, ask: "what did you learn, and where does it live now?"
- Reject "done" claims that don't address the three questions when the work session warranted it.
- Update persona memories directly when a learning changes the persona's durable behavior, skills, risks, review lens, coordination style, or management practice.
- Create or update calibration and playbooks when the learning belongs there instead of in the persona narrative.
- Periodically prune: stale memory records, outdated persona entries, and `decisions.md` entries that history has overturned. A doc that lies is worse than no doc.

## Subagent briefs

Every subagent brief for non-trivial work includes:

> When you finish the prompt-level work session, include a short **Learnings** section: what was surprising, where it should live (code / docs / memory / persona memories), and anything we previously believed that this invalidates. If nothing was surprising, say so.

## Signals that learning isn't happening

- Two tasks in a row rediscover the same quirk.
- A persona's `persona.md` or `learnings.md` hasn't been touched in months despite the area being worked heavily.
- `decisions.md` entries disagree with the code and nobody has noticed.
- Memory records cite files or functions that no longer exist.

Any of these is a protocol-level bug and Atlas fixes it.
