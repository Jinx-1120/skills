---
name: technical-plan
description: "Use after requirements and boundaries are clear to design a target technical solution: architecture, module boundaries, interfaces, data flow, security and safety, observability, rollout or migration, and testing strategy."
---

# Technical Plan

Turn a confirmed requirements contract into a buildable technical plan. This skill designs the solution; it does not collect open-ended requirements, write the final PRD, split tasks, or implement code.

## Boundary

Use this skill when requirements are mostly settled but technical choices still need design.

Do not use this skill for:

- Requirement discovery or boundary negotiation. Use `grill-plan`.
- Debugging a concrete failure. Use `diagnose`.
- Writing the final PRD. Use `to-prd`.
- Splitting the work into implementation tasks. Use `task-breakdown`.
- Implementing the plan. Use `implement`.
- Broad architecture review without a target requirement. Use `architecture-review`.

## Input Modes

- Inline mode: if the current prompt or conversation contains enough requirement detail, reconstruct the minimal requirements contract and proceed.
- Artifact mode: if a requirements ledger, PRD, notes file, or prior plan path is provided, read it first and use it as the source of truth.
- High-risk no-artifact mode: if missing history, compaction, or conflicting assumptions would make the plan unreliable, stop and ask for the missing checkpoint or run `grill-plan`.

## Phase 1: Load Or Reconstruct Requirements

- Identify the target project area and nearest applicable local instructions.
- Reconstruct the goal, accepted decisions, boundaries, rejected options, user corrections, entry points, consumers, data freshness rules, required artifacts, and open questions.
- Treat the newest explicit user correction as authoritative.
- If a requirement is unclear but non-blocking, record it as an assumption.
- If a missing decision changes architecture, data contracts, security, rollout, or acceptance, stop and hand back to `grill-plan`.

## Phase 2: Ground In The Codebase

- Read the smallest code, docs, schema, routes, tests, ADRs, runtime evidence, or config needed to design against the real system.
- Batch independent reads and searches when several files are likely relevant.
- For cross-entry work, trace every UI, API, CLI, worker, import, automation, report, or export path that must honor the same contract.
- For data-facing work, trace source of truth, writer job, storage table or artifact, freshness signal, consumer path, stale-data behavior, and observability.
- For security-sensitive work, identify trust boundaries, credentials, permissions, destructive actions, external services, and data exposure risks.

## Phase 3: Design

Produce a plan that covers only decisions needed for implementation or acceptance:

- Architecture and module boundaries.
- Interfaces, schemas, state transitions, errors, and backward compatibility.
- Data flow, freshness, migration, and artifact contracts.
- Security and safety constraints.
- Observability: logs, metrics, run ids, status pages, manifests, or read-back checks.
- Rollout, compatibility, migration, and rollback.
- Test strategy at the right seams.
- Alternatives rejected and why.

Do not over-design speculative abstractions. If a deeper review of existing module boundaries is needed, hand off that slice to `architecture-review`.

## Phase 4: Technical Plan Artifact

For simple work, return the plan inline. For multi-turn, high-risk, or cross-skill work, write or request a checkpoint artifact. Prefer a user-provided path; otherwise use a project-local path such as `.codex/workflows/<date>-<slug>/technical-plan.md` when writing is appropriate.

Use this structure:

```markdown
## Parent Requirements

Path or inline source summary.

## Requirement Coverage

Map each accepted decision, boundary, rejected option, entry point, artifact, and freshness rule to a technical decision or explicit non-decision.

## Architecture

## Module And Interface Contracts

## Data And Artifact Flow

## Security And Safety Review

## Observability And Operations

## Rollout And Migration

## Testing Strategy

## Alternatives Rejected

## Open Technical Questions

## Next Skill

to-prd | task-breakdown | implement
```

## Phase 5: Review Gate

Before finishing, verify:

- The plan does not contradict the requirements ledger.
- Every user-approved boundary and rejected option is preserved.
- Every known entry point and consumer is covered.
- Every technical decision has evidence, a repo pattern, or a stated assumption.
- Open technical questions are truly blocking.
