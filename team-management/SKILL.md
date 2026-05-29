---
name: team-management
description: Create and use role-specific team member personas, assign tasks to the best team members, identify missing team capabilities, assess team member performance, run Talent Planning reviews, and produce coaching or improvement plans. Use when Codex is asked to assemble an expert team, define personas for needed roles, assign work, route tasks to the right people, run a management or performance review process, review all current team members, evaluate how well team members are contributing, improve collaboration, identify where the team should expand, or determine what best practices, tools, techniques, and technologies a role should master.
---

# Team Management

## Operating Rule

Research the current best practices, tools, techniques, technologies, and role expectations before creating or assessing any persona. Prefer recent primary sources, vendor documentation, professional standards, reputable research, and credible practitioner writing. If browsing or live research is unavailable, state that the research is not current and make the uncertainty visible.

## Core Workflow

1. Clarify the objective, deliverable, product context, constraints, and decision horizon.
2. Identify the team capabilities required to achieve the objective. Separate essential roles from optional advisors.
3. Research each role before defining or assessing it. Capture what excellent current performance looks like for that role.
4. Create concise personas for the roles needed. Make each persona useful for execution, not theatrical.
5. Store project personas in `management/personas/` within the project or repo. Create the directory if it does not exist.
6. Assign every task to the best-fit team member or group of team members before work begins.
7. If no current team member is a good fit for a task, hire a new team member by creating the needed persona in `management/personas/` before proceeding.
8. Use the personas to review the work, plan execution, make decisions, or assess performance.
9. For performance assessment, compare observed behavior and outputs against the researched role standard, project goals, and explicit expectations.
10. For Talent Planning, review every current team member in `management/personas/`, make the identified changes directly to the affected persona files, summarize performance-review results, and identify where the team should be expanded with new members.
11. Produce concrete improvement actions with owners, timelines, practice loops, and measurable outcomes.

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

Keep personas specific to the actual objective. Avoid generic titles such as "strategist" unless the work truly needs that capability.

## Persona Storage

Keep personas used by a project in `management/personas/` relative to the project root. Use one Markdown file per persona unless the project already has a stronger convention. Prefer descriptive hyphen-case filenames such as `product-manager.md`, `security-reviewer.md`, or `fitness-domain-expert.md`.

When starting a team-management task in a project, inspect `management/personas/` first. Reuse and update existing personas when they remain valid, and create new personas only when a needed capability is missing or the current persona is materially stale.

## Task Assignment

No work should begin without an assigned team member. For every task, identify the owner or owner group that is most likely to produce the best outcome.

Assign tasks by matching:

- Task objective and expected deliverable.
- Required domain expertise, tools, techniques, and technologies.
- Required review lens, such as architecture, safety, UX, security, product, implementation, operations, or research.
- Current persona mission, decision rights, success signals, and known strengths.
- Risk profile, ambiguity, time sensitivity, and collaboration needs.
- Performance-review evidence when available.

Use one primary owner when accountability should be clear. Use a group when the task genuinely spans concerns, such as product plus UX, architecture plus security, or implementation plus domain correctness. Name the expected contribution of each member in the group.

If no current team member is a strong fit:

1. Do not assign the task to the closest weak fit by default.
2. Define the missing capability and why the current team cannot cover it well.
3. Research the current best practices, tools, techniques, and technologies for the needed role.
4. Hire the new team member by creating a persona in `management/personas/`.
5. Assign the task to the new persona, alone or with existing collaborators as appropriate.

Every task assignment should include the assigned member or group, why they are the best fit, expected output, collaborators or reviewers, and any capability gap or hiring decision.

## Talent Planning

Use Talent Planning when the user asks whether the team is complete, how the team is performing, who is missing, what capabilities are under-covered, or how to staff the next phase of work.

Talent Planning requires an in-depth review of the current team:

1. Treat `management/personas/` as the current team roster. Read every persona file before assessing the team.
2. Clarify the project phase, goals, risks, and upcoming workload.
3. Research current best practices, tools, techniques, and technologies for each represented role and each suspected missing role.
4. Run a performance review for every current team member/persona using the evidence available from project work, decisions, reviews, user feedback, and the persona's own stated mission.
5. Summarize each performance review result, including strengths, gaps, unknowns, and concrete improvement actions.
6. Map team capabilities against the project goals and identify over-covered, under-covered, and missing capabilities.
7. Recommend team expansion where a new member would materially improve quality, speed, safety, domain correctness, design, operations, or decision-making.
8. Make the identified changes directly in `management/personas/`: update existing persona files for changed responsibilities, expertise, decision rights, risks, success signals, improvement actions, or collaboration expectations; create new persona files for approved new team members.
9. For each proposed new member, define the role, mission, current expertise requirements, why the existing team cannot fully cover it, and the first work they should own.
10. Summarize the persona-file changes in the Talent Planning report, including files updated, files created, and the reason for each change.

Do not add new personas just to make the team look larger. Expansion recommendations must tie to evidence: recurring gaps, upcoming work, overloaded roles, risk concentration, missing expertise, or quality failures.

Talent Planning reports should not be the only place where changes live. The report is a summary and audit trail; the persona files are the source of truth that must be updated during the Talent Planning work.

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

## Useful References

For reusable output structures, read [persona-performance-templates.md](references/persona-performance-templates.md).
