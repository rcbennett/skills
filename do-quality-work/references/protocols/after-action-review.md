# Protocol: After Action Review

**Principle:** A team learns fastest when surprises become explicit process changes. Review the work, not the person.

## When to run one

Run an After Action Review when any of these happen:

- A failure, regression, false blocker, missed requirement, or avoidable rework occurred.
- The result differed materially from the plan.
- A task produced a durable lesson for multiple personas.
- A review exposed a weak protocol, stale memory, or wrong assignment.
- A milestone, release, deploy, or Talent Planning review completes.
- The executive persona sees the same failure mode repeat.

For routine low-risk work, the normal session learning summary is enough.

## Review questions

Answer these with evidence:

1. What was supposed to happen?
2. What actually happened?
3. What explains the difference?
4. What worked and should be repeated?
5. What should change before the next similar session?
6. Which persona memories, protocols, playbooks, or project docs need updates?

## Output shape

Use a compact report:

```markdown
# After Action Review: <short title>

**Date:**
**Scope:**
**Participants / personas:**
**Evidence inspected:**

## Expected

## Actual

## Causes

## Repeat

## Change

| Action | Owner | Where it lands | Due / review cadence |
| --- | --- | --- | --- |
|  |  |  |  |

## Memory and protocol updates

- Persona memories:
- Protocols:
- Playbooks:
- Project docs:
```

Store project AARs in `management/reviews/after-action/<YYYY-MM-DD>-<slug>.md` when the review needs an audit trail. For smaller findings, update the affected persona memories and summarize the AAR in the final response.

## Rules

- Be blameless and specific. "The handoff lacked verification evidence" is useful; "the reviewer was sloppy" is not.
- Do not manufacture root causes. Use `unknown` when evidence is thin.
- AARs must produce changes, not just narratives.
- If the AAR identifies a protocol gap, update or propose the protocol change before calling the loop closed.

## Atlas's role

- Trigger AARs when failure patterns repeat or a session's outcome differs from the plan.
- Ensure action items have owners and storage locations.
- Verify that persona memories, calibration, and playbooks actually get updated.
