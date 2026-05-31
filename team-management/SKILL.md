---
name: team-management
description: Create and use role-specific team member personas, assign tasks to the best team members, maintain per-member persona directories, learning records, calibration records, and playbooks, use an executive persona for assignment and management improvement, convert legacy file-based personas, identify missing team capabilities, assess team member performance and team health, run Talent Planning reviews and executive retrospectives, and produce coaching or improvement plans. Use when Codex is asked to assemble an expert team, define personas for needed roles, assign work, route tasks to the right people, run a management or performance review process, review all current team members, evaluate how well team members are contributing, improve collaboration, identify where the team should expand, or determine what best practices, tools, techniques, and technologies a role should master.
---

# Team Management

## Operating Rule

Research the current best practices, tools, techniques, technologies, and role expectations before creating or assessing any persona. Prefer recent primary sources, vendor documentation, professional standards, reputable research, and credible practitioner writing. If browsing or live research is unavailable, state that the research is not current and make the uncertainty visible.

## Core Workflow

1. Clarify the objective, deliverable, product context, constraints, and decision horizon.
2. Identify the team capabilities required to achieve the objective. Separate essential roles from optional advisors.
3. Research each role before defining or assessing it. Capture what excellent current performance looks like for that role.
4. Create concise personas for the roles needed. Make each persona useful for execution, not theatrical.
5. Store each team member in `management/personas/<member-slug>/persona.md` within the project or repo. Create the directory if it does not exist.
6. Convert any legacy top-level persona files in `management/personas/` to member directories before treating the roster as current.
7. Ensure the executive persona exists, read it before assigning work, and use it to guide task routing, team structure, and management improvement.
8. Assign every task to the best-fit team member or group of team members before work begins.
9. If no current team member is a good fit for a task, hire a new team member by creating the needed member directory and `persona.md` before proceeding.
10. Use the personas and member learnings to review the work, plan execution, make decisions, or assess performance.
11. Use calibration evidence before trusting a reviewer, owner, or executive judgment on high-impact work.
12. After meaningful work, store durable learnings in the responsible member's directory and update `persona.md` when the learning should change that member's skills or operating model.
13. Promote repeated tactics into playbooks instead of leaving them buried in learning logs.
14. For performance assessment, compare observed behavior and outputs against the researched role standard, project goals, explicit expectations, the member's learning history, and calibration evidence.
15. For Talent Planning, review every current team member in `management/personas/`, run a team-health check when relevant, make the identified changes directly to the affected member directories, summarize performance-review results, and identify where the team should be expanded with new members.
16. Produce concrete improvement actions with owners, timelines, practice loops, and measurable outcomes.

## Research Requirements

For each role, gather enough current context to answer:

- What outcomes the role is accountable for.
- Which best practices currently distinguish strong performance.
- Which tools, techniques, frameworks, standards, or technologies the role should know.
- Which failure modes are common for the role.
- Which adjacent roles the persona must collaborate with.
- Which evidence would prove the role is performing well.

Include source links and retrieval dates when the final answer depends on live research. If the task is internal, combine external research with repo, project, or organization-specific evidence.

## Persona Format

Define each persona with:

- `Name`: A short role label, not a fictional backstory.
- `Role`: The job the persona performs on this team.
- `Mission`: The outcome this persona protects.
- `Expertise`: The current best practices, tools, techniques, and technologies they should command.
- `Decision Rights`: What this persona can decide or strongly influence.
- `Operating Style`: How they should evaluate work and communicate.
- `Review Lens`: Questions they ask when evaluating plans, designs, code, strategy, or execution.
- `Risks`: Blind spots, overreach risks, or conflicts with other roles.
- `Success Signals`: Observable evidence that the persona is helping.
- `Learning Practices`: How the persona captures durable lessons and improves its own work.
- `Current Development Focus`: Skills, judgment, habits, or knowledge the member is actively improving.
- `Calibration Signals`: Evidence that should change future trust, assignment, or review routing for this persona.
- `Default Playbooks`: Reusable tactics this persona should retrieve before relevant work.

Keep personas specific to the actual objective. Avoid generic titles such as "strategist" unless the work truly needs that capability.

## Persona Storage

Keep personas used by a project in `management/personas/` relative to the project root. Store each team member in a descriptive hyphen-case subdirectory:

```text
management/personas/
  executive/
    persona.md
    learnings.md
    calibration.md
    playbooks/
  product-manager/
    persona.md
    learnings.md
    calibration.md
    playbooks/
  security-reviewer/
    persona.md
    learnings.md
    calibration.md
    playbooks/
```

The canonical persona definition for a member must live in that member's `persona.md`. Store durable member-specific lessons in the same subdirectory, defaulting to `learnings.md` unless the project already uses a more granular learning-log convention inside the member directory. Store evidence about judgment quality, false positives, missed issues, noisy reviews, and assignment fit in `calibration.md`. Store repeated member-specific tactics in `playbooks/`; use project-wide `management/playbooks/` for tactics shared across personas.

When starting a team-management task in a project, inspect `management/personas/` first. Reuse and update existing member directories when they remain valid, and create new members only when a needed capability is missing or the current persona is materially stale.

## Legacy Persona Conversion

Treat top-level Markdown persona files in `management/personas/` such as `product-manager.md` or `security-reviewer.md` as legacy storage. Before assessing the roster or assigning work:

1. Create `management/personas/<filename-without-extension>/`.
2. Move the current persona definition into `management/personas/<member-slug>/persona.md`, preserving the existing content unless it is clearly stale or malformed.
3. Create `management/personas/<member-slug>/learnings.md` when the member has durable lessons to store or when new work creates them.
4. Create `management/personas/<member-slug>/calibration.md` when performance, review, or assignment-fit evidence exists.
5. Update any roster, assignment, or Talent Planning references from the old file path to the new `persona.md` path.
6. Remove the old top-level persona file from the active roster after verifying the new `persona.md` contains the current definition.

Do not keep both the old file and the new `persona.md` as competing sources of truth.

## Member Learning and Persona Improvement

Every team member is responsible for remembering durable lessons from its own work. After meaningful execution, review, failure analysis, user feedback, or research, decide whether a learning belongs in that member's directory.

Record a learning when it changes how the member should make decisions, review work, communicate, use tools, avoid a failure mode, collaborate, or judge success. Include the date, source or evidence, lesson, expected behavior change, and any follow-up review cadence. Do not store secrets, credentials, private user data, or transient task status as learnings.

Update the member's `persona.md` when a learning changes their mission, expertise, decision rights, operating style, review lens, risks, success signals, learning practices, or current development focus. Keep one-off notes in `learnings.md`; promote durable behavior changes into `persona.md`.

## Calibration and Playbooks

Use `calibration.md` to track evidence about a member's judgment quality over time. Record real issues caught, real issues missed, false positives, noisy findings, verification gaps, rework caused or prevented, assignment fit, and whether prior calibration changed later behavior.

Use calibration before assigning high-impact work or selecting reviewers. Do not treat calibration as blame; use it to route work, add reviewers, adjust development focus, and improve the persona. Promote calibration findings into `persona.md` only when they change durable responsibilities, risks, review lens, success signals, or development focus.

Use playbooks for repeatable tactics. Create or update a project-level `management/playbooks/<slug>.md` when a tactic applies to multiple personas. Create or update `management/personas/<member-slug>/playbooks/<slug>.md` when it is specific to one member. Each playbook should state when to use it, when not to use it, required inputs, steps, verification, failure modes, related personas/protocols, and review cadence.

## Executive Persona

Maintain an executive team member at `management/personas/executive/persona.md`. If it is missing and task assignment or Talent Planning is in scope, create it before assigning work.

The executive persona owns team-level management: clarifying priorities, choosing task owners, identifying capability gaps, balancing speed and quality, coordinating reviews, deciding when to hire new personas, and improving how the team is managed. The executive does not replace specialist owners; it improves assignment quality and management decisions.

Before assigning tasks, read the executive persona and its learnings. Use the executive persona to:

- Review the task list and decide whether the team structure fits the objective.
- Select owners and reviewers using each member's persona, learning history, calibration evidence, current development focus, playbooks, and performance evidence.
- Identify when a task needs a new team member instead of a weak-fit assignment.
- Record management lessons in `management/personas/executive/learnings.md`.
- Update `management/personas/executive/persona.md` when the team learns a better way to assign, coach, review, coordinate, or improve team performance.
- Run executive retrospectives when a milestone completes, an AAR exposes a management gap, team-health signals weaken, or assignment/review quality drifts.

## Task Assignment

No work should begin without an assigned team member. For every task, identify the owner or owner group that is most likely to produce the best outcome.

The executive persona participates in task assignment by default. Include the executive's routing rationale or management decision in the assignment, even when the executive is not the primary owner of the actual deliverable.

Assign tasks by matching:

- Task objective and expected deliverable.
- Required domain expertise, tools, techniques, and technologies.
- Required review lens, such as architecture, safety, UX, security, product, implementation, operations, or research.
- Current persona mission, decision rights, success signals, and known strengths.
- Member learning history, current development focus, and relevant improvement actions.
- Calibration evidence, especially false positives, missed issues, useful review signal, and assignment-fit history.
- Applicable member or project playbooks.
- Executive persona guidance on priority, staffing, collaboration, and management risk.
- Risk profile, ambiguity, time sensitivity, and collaboration needs.
- Performance-review evidence when available.

Use one primary owner when accountability should be clear. Use a group when the task genuinely spans concerns, such as product plus UX, architecture plus security, or implementation plus domain correctness. Name the expected contribution of each member in the group.

If no current team member is a strong fit:

1. Do not assign the task to the closest weak fit by default.
2. Define the missing capability and why the current team cannot cover it well.
3. Research the current best practices, tools, techniques, and technologies for the needed role.
4. Hire the new team member by creating `management/personas/<member-slug>/persona.md`.
5. Assign the task to the new persona, alone or with existing collaborators as appropriate.

Every task assignment should include the assigned member or group, the executive's assignment rationale, why the assigned owner is the best fit, expected output, collaborators or reviewers, and any capability gap or hiring decision.

## Talent Planning

Use Talent Planning when the user asks whether the team is complete, how the team is performing, who is missing, what capabilities are under-covered, or how to staff the next phase of work.

Talent Planning requires an in-depth review of the current team:

1. Treat `management/personas/` as the current team roster. Convert legacy file-based personas first, then read every member's `persona.md` and relevant learning records before assessing the team.
2. Clarify the project phase, goals, risks, and upcoming workload.
3. Research current best practices, tools, techniques, and technologies for each represented role and each suspected missing role.
4. Use the executive persona to evaluate whether task assignment, coaching, review routing, staffing, calibration, playbook reuse, and team-management practices are improving.
5. Run a team-health check when collaboration, staffing, learning quality, or management effectiveness is in scope. Assess psychological safety, dependability, structure and clarity, meaning, impact, learning culture, and load/focus.
6. Run a performance review for every current team member/persona using the evidence available from project work, decisions, reviews, user feedback, learning records, calibration records, and the persona's own stated mission.
7. Summarize each performance review result, including strengths, gaps, unknowns, and concrete improvement actions.
8. Map team capabilities against the project goals and identify over-covered, under-covered, and missing capabilities.
9. Recommend team expansion where a new member would materially improve quality, speed, safety, domain correctness, design, operations, or decision-making.
10. Make the identified changes directly in `management/personas/`: update existing `persona.md` files for changed responsibilities, expertise, decision rights, risks, success signals, learning practices, calibration signals, default playbooks, improvement actions, or collaboration expectations; create new member directories and `persona.md` files for approved new team members.
11. Store durable lessons from the review in the affected member directories, including executive management lessons in `management/personas/executive/learnings.md`.
12. Update `calibration.md` when the review changes trust in a member's judgment, reviewer quality, owner fit, or management decisions.
13. Promote repeated team tactics into `management/playbooks/` or member-local `playbooks/`.
14. For each proposed new member, define the role, mission, current expertise requirements, why the existing team cannot fully cover it, and the first work they should own.
15. Summarize the member-directory changes in the Talent Planning report, including directories updated, files created, files converted, calibration updates, playbooks created, and the reason for each change.

Do not add new personas just to make the team look larger. Expansion recommendations must tie to evidence: recurring gaps, upcoming work, overloaded roles, risk concentration, missing expertise, or quality failures.

Talent Planning reports should not be the only place where changes live. The report is a summary and audit trail; member directories are the source of truth that must be updated during the Talent Planning work.

## Executive Retrospectives and Team Health

Run an executive retrospective when a milestone completes, repeated rework appears, an AAR exposes a management gap, team-health signals weaken, or the team structure changes materially.

The executive retrospective asks:

1. Did assignment quality improve outcomes?
2. Did review routing catch meaningful issues without creating avoidable noise?
3. Did team members retrieve and apply relevant prior learnings?
4. Did calibration or playbooks change future routing or execution?
5. Did the team have enough psychological safety, dependability, role clarity, meaning, impact, learning culture, and focus to improve?
6. Which persona memories, calibration records, playbooks, protocols, or staffing decisions need updates?

Store durable executive retrospectives in `management/reviews/executive-retrospectives/<YYYY-MM-DD>-<slug>.md` when an audit trail is useful. Otherwise update the affected member directories and summarize the retrospective in the final report.

## Performance Assessment

Assess performance against evidence, not vibes. Use observed deliverables, decisions, execution behavior, communication artifacts, stakeholder feedback, and measurable outcomes.

Rate each relevant dimension as `strong`, `adequate`, `needs improvement`, or `unknown`:

- Role clarity and ownership.
- Quality of judgment and decisions.
- Current expertise and tool fluency.
- Delivery reliability.
- Collaboration and communication.
- Problem discovery and risk management.
- Learning velocity and adaptability.
- Impact on the team's objective.
- Quality of learning capture and persona self-improvement.
- Calibration trend and review signal quality.
- Playbook creation, retrieval, and reuse where applicable.

Call out `unknown` areas instead of inventing evidence.

## Improvement Planning

For each gap, provide:

- The specific behavior or capability gap.
- Why it matters to the objective.
- The current best-practice target.
- A concrete coaching action or practice loop.
- Tools, techniques, references, or training to use.
- A measurable success criterion.
- A review date or cadence.

Prefer small, inspectable improvement loops over broad advice. Make recommendations respectful, direct, and actionable.

When an improvement action changes how a member should operate, update that member's `persona.md`. When an improvement action creates a reusable lesson but does not yet change the persona definition, record it in the member's `learnings.md`.

When an improvement action changes future assignment or reviewer trust, update `calibration.md`. When it creates a repeatable tactic, update a playbook.

## Useful References

For reusable output structures, read [persona-performance-templates.md](references/persona-performance-templates.md).
