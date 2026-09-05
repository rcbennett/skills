# Persona and Performance Templates

Use these templates only when structure helps the requested deliverable. The main team-management skill determines assess versus update mode; templates never authorize mutations. Omit empty or irrelevant fields. Engineering review and model routing remain owned by do-quality-work.

## Team Capability Map

| Capability | Needed for | Role/persona | Essential? | Evidence to inspect |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## Persona

Store each project team member in `management/personas/<member-slug>/persona.md`.

```markdown
### <Role Label>

**Role:**  
**Mission:**  
**Expertise:**  
**Decision Rights:**  
**Operating Style:**  
**Review Lens:**  
**Risks:**  
**Success Signals:**  
**Learning Practices:**
**Current Development Focus:**
**Calibration Signals:**
**Default Playbooks:**
```

## Member Directory

```text
management/personas/<member-slug>/
  persona.md
  learnings.md
  calibration.md
  playbooks/
```

Use `persona.md` as the canonical persona definition. Store durable member-specific lessons in `learnings.md` unless the project already uses a more specific learning-log convention inside the member directory. Store evidence about judgment quality and assignment fit in `calibration.md`. Store member-specific reusable tactics in `playbooks/`.

## Learning Log

```markdown
# Learnings

## <YYYY-MM-DD> - <Short lesson label>

**Source/Evidence:**
**Trigger:**
**Lesson:**
**Applies When:**
**Avoid When:**
**Behavior Change:**
**Confidence:** low / medium / high
**Supersedes:**
**Persona Update Needed:** yes/no
**Review Due:**
```

## Persona Calibration

```markdown
# Calibration

## <YYYY-MM-DD> - <Session or review label>

**Role in session:** owner / reviewer / advisor / executive
**Model/context:** when relevant and known
**Evidence:**
**Signal:** bug caught / bug missed / false positive / noisy review / strong assignment / weak assignment / verification gap
**Impact:**
**Adjustment:**
**Promote to persona.md:** yes/no
**Review Cadence:**
```

## Playbook

```markdown
# <Playbook title>

**Owner:**
**Use When:**
**Do Not Use When:**
**Inputs Needed:**
**Steps:**
**Verification:**
**Failure Modes:**
**Related Personas/Protocols:**
**Last Reviewed:**
**Review Cadence:**
```

## Research Log

| Role | Current practices/tools/techniques found | Sources | Confidence | Gaps |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## Performance Review

```markdown
### <Team Member or Persona>

**Scope Reviewed:**  
**Evidence Used:**  
**Overall Assessment:**  

| Dimension | Rating | Evidence | Improvement target |
| --- | --- | --- | --- |
| Role clarity and ownership |  |  |  |
| Judgment and decisions |  |  |  |
| Current expertise and tool fluency |  |  |  |
| Delivery reliability |  |  |  |
| Collaboration and communication |  |  |  |
| Risk management |  |  |  |
| Learning velocity |  |  |  |
| Team impact |  |  |  |
| Learning capture and self-improvement |  |  |  |
| Calibration trend and review signal quality |  |  |  |
| Playbook retrieval and reuse |  |  |  |
```

## Improvement Plan

| Gap | Why it matters | Practice loop | Tools/references | Success measure | Review cadence |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Task Assignment Plan

Use this only for coordination that benefits from a table. Ordinary execution uses the current owner; a concise dispatch is sufficient. Executive rationale is useful only when an existing executive role affects the assignment.

| Task | Executive routing rationale | Assigned owner(s) | Why best fit | Expected output | Collaborators/reviewers | Gap or hiring decision |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |

A bounded role brief can cover one-off expertise. Create a persistent member only in authorized team setup/update work for a demonstrated recurring need.

## Talent Planning Review

Use this for an in-depth review of the current team and expansion needs.

```markdown
# Talent Planning Review

**Project Phase:**  
**Goals Reviewed:**  
**Current Roster Source:** `management/personas/*/persona.md`
**Evidence Used:**  
**Research Performed:**  
**Executive Management Review (when relevant):**
**Coordination Evidence (when relevant):**

## Proposed Changes (assess mode) Or Applied Changes (update mode)

| Path | Proposed/applied change | Reason |
| --- | --- | --- |
| `management/personas/<member-slug>/persona.md` |  |  |
| `management/personas/<member-slug>/learnings.md` |  |  |
| `management/personas/<member-slug>/calibration.md` |  |  |
| `management/personas/<member-slug>/playbooks/<slug>.md` |  |  |
| `management/playbooks/<slug>.md` |  |  |

## Current Team Performance

| Team member/persona | Mission | Overall assessment | Strengths | Gaps | Improvement actions |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Calibration Summary

| Team member/persona | Strong signals | Weak signals | Assignment/review adjustment | Persona update? |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## Capability Coverage

| Capability | Current owner(s) | Coverage | Risk | Action |
| --- | --- | --- | --- | --- |
|  |  | over-covered / adequate / under-covered / missing |  |  |

## Expansion Recommendations

| Proposed role | Why needed | Expertise required | Current-team gap | First responsibilities | Priority |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Decisions

- Keep:
- Coach:
- Refocus:
- Add:
- Defer:
```

## Team Health Check

```markdown
# Team Health Check

**Scope:**
**Evidence:**

| Dimension | Rating | Evidence | Action |
| --- | --- | --- | --- |
| Surfaced uncertainty and dissent |  |  |  |
| Dependability |  |  |  |
| Structure and clarity |  |  |  |
| Scope and purpose clarity |  |  |  |
| Impact |  |  |  |
| Learning culture |  |  |  |
| Load and focus |  |  |  |
```

## Executive Retrospective

```markdown
# Executive Retrospective

**Scope:**
**Evidence:**

| Question | Finding | Action |
| --- | --- | --- |
| Did assignment quality improve outcomes? |  |  |
| Did review routing catch useful issues without avoidable noise? |  |  |
| Did members retrieve and apply prior learnings? |  |  |
| Did calibration or playbooks change future routing? |  |  |
| Did team health support improvement? |  |  |
| Which memories, protocols, playbooks, or staffing decisions need updates? |  |  |
```
