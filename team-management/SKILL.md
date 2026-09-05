---
name: team-management
description: Assign specialist work, create or maintain project personas, assess team capability and review quality, and improve coordination from evidence. Use for requested team setup, role routing, performance assessment, or recurring capability gaps; routine single-owner work needs no roster administration.
---

# Team Management

## Choose the mode before acting

Respect current user scope and authorization. Use [do-quality-work](../do-quality-work/SKILL.md) for engineering design, review gates, verification, model choice, and completion; this skill owns role fit and team administration. It does not add another review matrix or override safety/project gates.

- **Execute or route:** the current agent is the default accountable owner. Reuse relevant personas when specialist judgment or multiple decision owners matter. A bounded role brief can supply one-off expertise; no persistent persona, executive file, roster conversion, or research campaign is required merely to begin work.
- **Assess:** inspect the current roster and evidence and report findings. A review or Talent Planning request alone does not authorize persona edits, file migration, hiring, or learning writes. Recommend precise changes without applying them unless the user also asks to improve or update the team.
- **Update or reorganize:** when authorized, edit only the affected roles and references. Create, merge, refocus, or retire roles according to real capability needs. Apply requested improvements directly rather than requesting the same authorization again.

Infer mode from the full request. Do not turn an assessment into implementation, or leave an authorized update as advice only. Ask only if a material scope choice remains unresolved; one question at a time with A/B/C options when useful.

## Assignment and model choice

Inspect only the relevant `management/personas/` definitions, learnings, calibration, and playbooks. If an existing executive persona materially helps routing or team assessment, read it; do not create one solely to assign a task. Keep one accountable integration owner even when several contributors participate.

For a substantive assignment, specify the expected result, boundary, relevant evidence, decision rights, acceptance, and collaborators. A short dispatch is sufficient; no separate assignment ledger is required. Match expertise and observed judgment to the actual risk. Do not equate a role label with independent execution or demonstrated competence.

Use [model-selection.md](../do-quality-work/references/protocols/model-selection.md) for capability, reasoning effort, context, and total-cost tradeoffs. When suitability is uncertain, favor a more capable model. Required independent review may use a fresh capable agent or an authorized external reviewer. Do not route review to a weak model merely because it is cheap or different.

Delegate only concrete independent work whose benefit justifies coordination, plus required reviews. Routine deterministic steps and process waiting should normally use direct tools. A missing persistent role does not imply a missing runtime capability; use a clear temporary brief. Create a durable role only when requested or when an authorized team update addresses a demonstrated recurring gap.

## Research when it changes role guidance

Research current role practices when creating a role, materially updating stale expertise, or deciding something affected by changing tools or standards. Prefer primary sources and relevant project evidence. Reuse still-applicable, dated source-backed guidance for routine assignments and local fit assessment; inspect actual deliverables before general role literature.

Capture only what changes the role's outcomes, practices, failure modes, collaboration, or evidence of success. State uncertainty if needed current research is unavailable. Include sources and retrieval dates for conclusions that depend on research. Do not infer expertise from a persona's self-description alone.

## Persona storage and lifecycle

Use existing project conventions. The default canonical definition is `management/personas/<member-slug>/persona.md`. Create auxiliary files only when there is content worth preserving:

```text
management/personas/<member-slug>/
  persona.md
  learnings.md       # surprising reusable lessons, when needed
  calibration.md     # evidence of judgment/assignment quality, when needed
  playbooks/         # validated repeated tactics, when needed
```

Keep a persona concise: role/mission, expertise, decision rights, review lens, risks, observable success signals, and relevant development focus. Link learning or playbooks instead of repeating them. Use [persona-performance-templates.md](references/persona-performance-templates.md) only when its structure improves the requested deliverable, and omit empty fields.

Legacy top-level persona files can be read in place during execution or assessment. Convert only during authorized reorganization: verify the source, move its current definition into the member directory, update inbound references, verify preservation, and remove the competing old definition. Do not overwrite an existing member directory or unrelated work. Keep one canonical definition.

Consider merging, narrowing, or retiring overlapping roles before adding another. Require evidence such as repeated missed risks, upcoming work needing distinct expertise, or conflicting decision rights. Preserve useful lessons and update current references when retiring a role; do not proliferate roles to make the team look complete.

## Performance and Talent Planning

For an explicitly comprehensive team assessment, read every current persona and relevant evidence. For a scoped fit question, inspect only affected roles. Assess project goals, upcoming work, actual deliverables, user feedback, and prior calibration. Use `strong`, `adequate`, `needs improvement`, or `unknown`; missing evidence is unknown, not failure.

Focus on role clarity, judgment, delivery reliability, architecture/maintainability outcomes, useful review findings, missed defects, false positives, rework, handoff quality, and whether prior lessons improved later work. Do not reward number of findings, personas, tests, or learning artifacts. Record the model/context and task evidence when relevant; a persona name alone is not a stable predictor of ability.

Summarize strengths, material gaps, overlap, and the smallest improvement actions with owners and observable success criteria. Add a review date only when a follow-up is useful. A team-wide executive review is appropriate for repeated routing failures or substantial coordination changes, not every milestone by default.

For agent teams, assess observable behavior: disclosure of uncertainty, legible handoffs, surfaced dissent, ownership conflicts, duplicate effort, and correction of mistakes. Do not infer human feelings, motivation, or psychological safety from generated role narratives. Use team-health guidance only when coordination evidence warrants it.

In assess mode, proposed changes stay recommendations. In authorized update mode, apply affected persona, calibration, playbook, and reference changes and report actual results. Do not let templates expand the scope.

## Learn proportionately

Use one session-level assessment under do-quality-work. Preserve only a surprising fact that changes future behavior, with evidence, applicability, and the resulting adjustment. Choose one canonical home: code/docs for system facts, `learnings.md` for role-specific lessons, `calibration.md` for judgment evidence, or a playbook for validated repeated procedures. Link elsewhere as needed.

Promote lessons into persona behavior only when evidence justifies it. Supersede incorrect guidance within authorized scope and preserve history when the repository requires it. Persistent memory writes always follow the active memory policy. Do not automatically write every lesson to several files or treat an old modification date as proof that learning failed.

Report the requested result and material gaps. Name owners, model choices, or administrative changes only when they affect the decision or handoff.
