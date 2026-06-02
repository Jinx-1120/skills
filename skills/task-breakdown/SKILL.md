---
name: task-breakdown
description: "Use after a requirement, PRD, or technical plan is approved to decompose work into sequenced implementation tasks with dependencies, acceptance criteria, verification gates, review gates, and deferred work."
---

# Task Breakdown

Turn an approved requirement, PRD, or technical plan into implementable task slices. This skill plans execution; it does not collect requirements, design new architecture, or edit code.

## Boundary

Use this skill when the intended behavior and technical approach are clear enough to sequence work.

Do not use this skill for:

- Requirement discovery or boundary negotiation. Use `grill-plan`.
- Technical solution design. Use `technical-plan`.
- PRD writing. Use `to-prd`.
- Debugging a concrete failure. Use `diagnose`.
- Implementing a task. Use `implement`.

## Input Modes

- Inline mode: if the current prompt or conversation contains enough approved scope and technical direction, reconstruct the minimal source contract and proceed.
- Artifact mode: if a requirements ledger, technical plan, PRD, or existing task list path is provided, read it first and use it as the source of truth.
- High-risk no-artifact mode: if missing history or compaction would make sequencing unreliable, stop and ask for the missing checkpoint or run the upstream skill.

## Phase 1: Load Or Reconstruct Source

- Identify the source requirement, PRD, or technical plan.
- Reconstruct accepted decisions, boundaries, rejected options, entry points, consumers, artifacts, freshness rules, rollout constraints, and verification gates.
- If the technical approach is not settled, hand off to `technical-plan`.
- If implementation acceptance is not clear, hand off to `to-prd` or `grill-plan` depending on the missing piece.

## Phase 2: Slice The Work

Create small coherent tasks that can be implemented and reviewed independently:

- Keep contract or schema changes before consumers.
- Keep migrations and compatibility work before behavior that depends on them.
- Keep shared seams before feature-specific adapters.
- Keep tests close to the behavior they validate.
- Avoid tasks that mix unrelated refactors, features, and operational changes.
- Separate local implementation from deployment or production verification when both matter.

## Phase 3: Output

For simple work, return the task list inline. For multi-turn, high-risk, or cross-skill work, write or request a checkpoint artifact. Prefer a user-provided path; otherwise use a project-local path such as `.codex/workflows/<date>-<slug>/task-breakdown.md` when writing is appropriate.

Use this structure:

```markdown
## Source

Path or inline summary of the requirement, PRD, or technical plan.

## Sequencing Rationale

## Tasks

### Task 1: <name>

- Goal:
- Scope:
- Files or modules:
- Dependencies:
- Acceptance checks:
- Verification:
- Review gate:

## Cross-task Risks

## Deferred Work

## Next Step

implement Task <n>
```

## Phase 4: Coverage Gate

Before finishing, verify:

- Every accepted requirement and technical decision maps to at least one task or an explicit deferred item.
- Every rejected option and non-goal remains out of scope.
- Every artifact, entry point, and freshness rule has an implementation or verification task.
- The first task is independently useful and safe to implement.
