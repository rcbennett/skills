# Decisions

## 2026-07-23: Add preservation-first workspace and document lifecycle

**Status:** accepted

**Decision:** Make clean-as-you-go reconciliation part of `do-quality-work`. Track the task-owned or explicitly adopted workspace delta, preserve unique work before cleanup, maintain durable source-of-truth documents as reality changes, and close/archive completed work artifacts under the repository's existing convention. Define clean as no unexplained task-owned residue or stranded unique content, not a globally empty repository.

**Context:** Complex work routinely creates branches, worktrees, stashes, temporary/generated artifacts, implementation plans, reports, and review documents. The prior skill required a clean handoff but did not define artifact ownership, safe source-control retirement, document authority, blocked-work preservation, or when an active artifact should become historical. This allowed hidden local work and stale active-looking documents to accumulate.

**Options considered:** Keep cleanup as an implied final step; require every task to leave a globally empty repository and archive all completed documents; use proportional checkpoint reconciliation with preservation-first deletion guards and explicit document roles.

**Rationale:** A task-owned delta avoids full-repository ceremony on small work while still preventing task-created residue. Preservation checks protect local-only and squash-merged branch content, and semantic document roles keep plans/reports from competing with current designs, READMEs, requirements, runbooks, decisions, and project-state documents.

**Consequences:** `SKILL.md`, `implementation-planning.md`, the implementation-plan template, and the protocol index now route relevant work through `workspace-and-document-lifecycle.md`. Material plans track workspace/document disposition and closeout evidence. Pre-existing or unrelated state is protected by default, blocked work receives a resumable preservation packet, and destructive cleanup requires exact targets plus preservation or regenerability evidence.

**Verification:** The skill package, Markdown links, UI metadata, semantic cleanup assertions, and working diff passed validation. Forward tests correctly required preservation/content proof for a completed squash-merged refactor, retained a blocked branch/worktree/stash/evidence packet without premature archival, and kept a narrow direct fix from inventorying or touching unrelated pre-existing state.

**Revisit trigger:** Revisit if agents still strand work in local branches/stashes, archive canonical documents, leave completed plans looking active, or turn routine changes into exhaustive repository inventories and artifact ledgers.

## 2026-07-23: Add architecture-gated durable implementation planning

**Status:** accepted

**Decision:** Add a three-tier workflow to `do-quality-work`: direct implementation for narrow reversible changes, a durable checkpoint plan for material coordinated work, and an approved architecture design followed by a durable plan when system shape or ownership changes. Treat the design as the canonical system-shape artifact, the decision record as concise rationale, and the plan as the living execution-control surface.

**Context:** Detailed checkpoint plans had improved sequencing, scope control, handoffs, evidence tracking, and reversibility on complex cross-platform refactors, but the skill only described plan review rather than when to create or maintain a repository plan. Its design guidance also did not reliably gate implementation on a verified current architecture, explicit ownership, alternatives, migration, failure handling, or approval. Requiring the same artifacts for a narrow fix would recreate the ceremony and slow progress that the skill is intended to prevent.

**Options considered:** Keep plans and design notes optional and chat-based; require a design and plan for every production change; use conditional architecture and planning gates with a no-document path for narrow work.

**Rationale:** Conditional gates preserve speed while giving architecture-shaping work durable control. Architecture-first and cross-platform forward tests produced clear ownership, migration, rollback, parity, and first-slice decisions; a narrow-fix test remained a patch plus focused evidence and an owner spot-check after proportionality wording was tightened.

**Consequences:** `SKILL.md`, `design-first.md`, `implementation-planning.md`, `plan-review.md`, `code-review.md`, and `cross-platform-parity.md` now define the design-to-plan-to-execution lifecycle. New architecture and implementation-plan templates bind baselines, review revisions, decisions, checkpoints, separate implementation/validation status, evidence, rollback, and receipts. Material cross-platform consolidation must adjudicate existing divergence before selecting canonical behavior. Plans stay current at checkpoint boundaries and return to design review when responsibilities or contracts change; direct local work creates no design or plan artifact.

**Verification:** The skill package validator, internal Markdown file/heading-link audit, generated UI-metadata checks, semantic assertions, and `git diff --check` passed. Architecture-heavy offline sync, narrow local correction, and shared cross-platform policy-refactor forward tests all passed after delta review of their material findings.

**Revisit trigger:** Revisit if plans become retrospective transcripts, review or artifact duplication outweighs coordination value, narrow fixes accumulate ceremony, implementation repeatedly drifts from approved architecture, or the gates miss material ownership, migration, safety, or platform constraints.

## 2026-05-31: Reconcile backup-only governance protocols with current learning system

**Status:** accepted

**Decision:** Merge the backup-only `do-quality-work` governance protocols back into the current skill while preserving the newer learning-retrieval, AAR, persona-calibration, playbook, and team-health protocol structure already present in this directory.

**Context:** `../skills.bak` contained protocol files and routing for council review, red-team review, steelman review, pre-mortem review, decision records, slice sizing, and completion commits that were absent from the current tracked skill tree. The current tree contained newer learning and persona-improvement protocols not present in the backup, so a direct overwrite would have regressed current behavior.

**Options considered:** Keep the current tracked skill unchanged; overwrite from `../skills.bak`; merge only the backup-only governance material into the current skill.

**Rationale:** The missing governance protocols were previously accepted operating rules and are still complementary to the newer learning/calibration system. A targeted merge restores important-decision, adversarial-review, operational-readiness, durable-decision, and slice-sizing behavior without losing the current session-learning improvements.

**Consequences:** Future use of `do-quality-work` should route important and high-risk decisions through the restored governance protocols and still report learning retrieval, AAR, calibration, playbook, team-health, and session-learning outcomes.

**Verification:** Compare backup and current skill trees, merge missing files and routing, validate skill structure, audit internal Markdown links, and commit the reconciled skill.

**Revisit trigger:** Revisit if the merged protocol surface becomes too heavy for ordinary work, if completion commits conflict with a caller's workflow, or if future skill syncs again drop accepted protocols.

## 2026-05-24: Add slice-size and verification-overhead rule

**Status:** accepted

**Decision:** Add a first-class Slice Size And Overhead Rule to `do-quality-work`, update the verification-toolchain protocol to distinguish micro-slices, capability packets, and broader checkpoints, and require non-trivial work reports to state the chosen slice size when it affects risk, overhead, or progress.

**Context:** A CommonThread Phase 4 review showed that the work was safe and well evidenced, but recent commits were becoming too small relative to the cost of live probes, rollups, generated docs, review, credential scans, and build verification. The older right-time verification rule handled when to run tests, but did not force a decision about whether the unit of work was large enough to justify the full evidence loop.

**Options considered:** Keep the existing right-time verification rule unchanged; reduce verification rigor globally; add a slice-sizing rule that preserves rigor while batching related low/medium-risk work into coherent capability packets.

**Rationale:** Verification rigor is still required before commits, releases, deploys, and parity claims, but excessive ceremony around tiny low-risk changes slows meaningful progress. Explicit slice sizing lets agents use micro-slices for high-risk or hard-to-debug work while batching related changes that share a domain, fixture set, rollback path, reviewer group, and verification envelope.

**Consequences:** Future work should report whether it used a micro-slice, capability packet, or broader checkpoint. Expensive evidence generation and broad verification should normally run at packet/checkpoint boundaries, while targeted checks run during iteration. Agents must not batch unrelated work just to reduce overhead.

**Verification:** Updated `SKILL.md`, `references/protocols/verification-toolchain.md`, `references/protocols/README.md`, and `agents/openai.yaml`; then inspected the edited files for the new rule and output contract.

**Revisit trigger:** Revisit if capability packets become too broad to debug or rollback, if micro-slices again dominate low-risk work, or if the added reporting requirement creates more ceremony than clarity.

## 2026-05-21: Add adversarial, alternative, operational, and decision-record protocols

**Status:** accepted

**Decision:** Add first-class `red-team.md`, `steelman.md`, `pre-mortem.md`, and `decision-record.md` protocols to the `do-quality-work` skill, wire them into `SKILL.md`, and expose them in the bundled protocol README.

**Context:** The existing skill covered plan, design, code, verification, model selection, claim checking, parity, learning, and council review. It did not explicitly require adversarial challenge, charitable review of serious alternatives, production-failure forecasting, or durable decision capture.

**Options considered:** Keep relying on council review alone; add only red-team and steelman; add red-team, steelman, pre-mortem, and decision-record together.

**Rationale:** Council review asks for weaknesses and opportunities, but explicit protocols make the trigger and output contract clearer. Adding the four protocols together covers downside risk, competing-path reasoning, operational readiness, and future traceability without making every small task heavier.

**Consequences:** Important decisions and high-risk work now have more explicit gates. Small reversible edits can still skip these protocols when they would add ceremony without improving the result.

**Verification:** Validated by direct inspection and skill validation after the protocol files were added.

**Revisit trigger:** Revisit if the added protocols are skipped in practice, produce too much ceremony for routine work, or fail to catch release, safety, security, or decision-traceability problems.
