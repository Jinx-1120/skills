---
name: task-breakdown
description: "Use when an approved requirement or technical plan is too large, risky, or dependency-heavy to implement as one coherent slice and needs sequenced tasks with acceptance, verification, review, and rollout gates."
---

# Task Breakdown

Turn an approved contract into the fewest independently useful implementation slices. Use this skill only when sequencing reduces risk or improves reviewability; a clear small task should go directly to `implement`.

## Boundary

Do not use this skill to discover requirements, design architecture, write a PRD, diagnose failures, or edit code. Route those to `grill-plan`, `technical-plan`, `to-prd`, `diagnose`, or `implement`.

## Source Contract

Read the requirement, PRD, technical plan, or current conversation and reconstruct:

- Outcome and observable done criteria.
- Accepted decisions, non-goals, and rejected options.
- Architecture, ownership, data, compatibility, and rollout decisions.
- Entry points, consumers, artifacts, freshness rules, and verification matrix.
- Missing decisions that still block safe sequencing.

If the technical approach or acceptance behavior is not settled, hand back to the owning upstream skill instead of hiding design work inside tasks.

## Slicing Rules

- Prefer vertical slices that produce a reviewable capability or risk reduction.
- Put contracts, schemas, and migrations before consumers that depend on them.
- Put shared seams before feature adapters only when the seam has current consumers.
- Keep tests and read-back verification with the behavior they prove.
- Separate local implementation, migration/backfill, deployment, and live verification when they have different evidence or owners.
- Make temporary compatibility work include its removal condition and cleanup task.
- Do not create one task per file, layer, or engineering discipline unless that is the real dependency boundary.
- Avoid task lists so granular that the implementer must reconstruct the design.

## Task Contract

Each task must state:

- `Outcome`: independently useful result.
- `Scope`: included modules and explicit exclusions.
- `Dependencies`: prior contracts, data, or decisions.
- `Acceptance`: observable behavior, not activity.
- `Verification`: static, code, artifact/read-back, runtime, or live evidence required.
- `Review gate`: what must be checked before dependent work starts.
- `Rollback/removal`: when the slice changes durable state or adds a temporary path.

For simple work, return an ordered list inline. For multi-turn or handoff-heavy work, persist a project-native artifact with:

```markdown
## Source And Status
## Sequencing Rationale
## Dependency Map
## Tasks
## Cross-task Risks
## Deferred Work
## Completion Gate
```

## Coverage Gate

- Every accepted requirement maps to a task or explicit deferred item.
- Every non-goal remains out of scope.
- Every entry point, artifact, freshness rule, migration, and verification level has an owner.
- The first task is safe and useful on its own.
- The final task proves the end-to-end user outcome rather than only code completion.
