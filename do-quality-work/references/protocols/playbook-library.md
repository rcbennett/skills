# Protocol: Playbook Library

**Principle:** Repeated successful tactics should become reusable playbooks, not buried in session summaries.

## When to create or update a playbook

Create or update a playbook when:

- The team repeats the same diagnostic, review, deploy, verification, design, or research tactic.
- A session discovers a reliable sequence that prevents mistakes.
- An AAR identifies a missing reusable procedure.
- A persona's learning applies to more than one future session.
- A task is high-risk enough that the checklist should be explicit before the next attempt.

Do not create playbooks for one-off trivia, facts already obvious from code, or task status.

## Storage

Use project-level playbooks for cross-persona tactics:

```text
management/playbooks/<slug>.md
```

Use member-local playbooks only when the tactic is specific to that member:

```text
management/personas/<member-slug>/playbooks/<slug>.md
```

## Playbook format

```markdown
# <Playbook title>

**Owner:**
**Use when:**
**Do not use when:**
**Inputs needed:**
**Steps:**
**Verification:**
**Failure modes:**
**Related personas/protocols:**
**Last reviewed:**
**Review cadence:**
```

## Lifecycle

1. Draft from a validated session learning, AAR, or repeated task.
2. Use it in later sessions through `learning-retrieval.md`.
3. Update it when it prevents a mistake or fails to fit reality.
4. Retire it when it becomes obvious, obsolete, or contradicted by current project behavior.

## Atlas's role

- Promote repeated lessons into playbooks.
- Prefer playbooks over re-explaining the same process in final summaries.
- Keep playbooks short enough to execute.
- Link playbooks from persona memories when a member should use them by default.
