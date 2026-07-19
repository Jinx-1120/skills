---
name: technical-plan
description: "Use when the desired behavior is mostly settled but implementation needs an end-to-end technical contract across architecture, ownership, durable state, data flow, failures, recovery, observability, rollout, migration, verification, and final module or API boundaries; also use to restate an existing design in plain user-story language. For focused alternative module interfaces or seam placement, use improve-codebase-architecture."
---

# Technical Plan

Design the smallest buildable solution that satisfies the accepted outcome. Ground every important decision in repository evidence, a user-approved constraint, or an explicit assumption.

## Boundary

Use this skill for target technical design, including plain-language playback of an existing design before planning.

Do not use it for:

- Materially ambiguous goals or scope. Use `grill-plan`.
- A concrete failure that needs root-cause work. Use `diagnose`.
- Broad review of whether current architecture is problematic. Use `architecture-review`.
- Focused exploration of deep-module interfaces, seam placement, or alternative module shapes. Use `improve-codebase-architecture`.
- PRD writing without new technical decisions. Use `to-prd`.
- A clear task ready to build. Use `implement`.

For a planning-only request, stop at the plan. For an end-to-end build request, treat planning as an internal phase and continue to implementation when no material decision requires user authority or a requested review gate.

## Input Modes

- `Inline`: reconstruct the minimum accepted requirements from the current request.
- `Artifact-backed`: read the supplied requirements ledger, PRD, design, ADR, or notes as the source contract.
- `Intent playback`: explain an existing design through users, scenarios, state changes, failures, and visible outcomes before judging or extending it.
- `Blocked`: route back to `grill-plan` only when a missing product decision changes the architecture or acceptance result.

Treat the newest explicit user correction as authoritative. Mark verified facts, inferences, assumptions, and unresolved decisions separately.

### Intent playback mode

When the user asks to restate or explain an existing design:

- Read the design and directly required linked context before summarizing.
- Explain it through users, scenarios, decisions, state changes, failures, and visible outcomes in the user's requested language.
- Preserve goals, non-goals, entry points, contracts, edge cases, freshness, rollout constraints, and open questions.
- Separate document content from your inference.
- Do not review, redesign, or implement unless the user asks for that next step.
- End with the concrete places where the design may not match the user's intent, or say that no mismatch is evident from the available source.

## Planning Depth

Choose the lightest depth that fits the risk:

- `Light`: local behavior with no durable state or external effect. Cover owner, interface, errors, and verification seam.
- `Standard`: shared API, workflow, stored data, report, or cross-entry behavior. Add source of truth, writer/consumers, freshness, compatibility, observability, and rollout.
- `Full contract`: authorization, secrets, destructive actions, provider integrations, queues, workers, multi-runtime state, migrations, or durable side effects. Add identity, idempotency, confirmation boundaries, recovery, reconciliation, and fail-safe behavior.

Do not expand a low-risk change into a platform design. Do not hide a high-risk contract behind a light checklist.

## Workflow

### 1. Establish the accepted outcome

Reconstruct:

- User-visible outcome and observable done criteria.
- Accepted decisions, boundaries, non-goals, and rejected options.
- Entry points, consumers, linked artifacts, and compatibility constraints.
- Source-of-truth and freshness rules.
- Material open decisions.

### 2. Ground in the real system

- Read the nearest applicable instructions, relevant code, manifests, schemas, tests, ADRs, and runtime evidence.
- Batch independent exploration.
- Trace every in-scope UI, API, CLI, worker, import, automation, report, or export path.
- Discover project and platform utilities before proposing new parsing, time, validation, auth, URL, SQL, retry, cache, or serialization logic.
- Record whether an existing utility is reused, extended, wrapped, or rejected, and why.
- For current data or deployment claims, include exact environment, date, and freshness evidence rather than relying on old code or memory.

### 3. Design from ownership outward

Cover only decisions needed to build and verify:

- Owning module or subsystem for each fact, policy, side effect, and user-visible state.
- Public interfaces, schemas, errors, and backward compatibility.
- Durable facts versus caches, jobs, sockets, UI state, generated files, and transport observations.
- Data flow, writer/reader ordering, freshness, migration, and artifact contracts.
- Stable identities and idempotency keys.
- Ack, accept, durable commit, delivery, user-visible result, and external-success boundaries.
- Failure classes, retry, replay, reconciliation, and unknown-after-side-effect behavior.
- Security boundaries, permissions, destructive actions, and secret handling.
- Logs, metrics, run ids, read-back checks, and operator-visible stuck states.
- Rollout, compatibility window, migration/backfill, rollback, and removal of temporary paths.

Prefer deletion, reuse, and one clear owner over additional indirection. Add a seam only for a current caller, adapter, runtime, or test need.

### 4. Design verification before file tasks

Use a verification matrix:

| Contract | Evidence | Environment | Pass condition |
| --- | --- | --- | --- |
| Deterministic rule | Focused test | Local | Exact expected behavior |
| Stored/artifact result | Read-back | Local/staging | Durable output is complete and linked |
| Side-effect path | Integration/smoke | Real dependency | User-visible result is observed |
| Deployment claim | Live check | Production | Correct version and original outcome are visible |

Test pure rules at code level. Keep side-effecting orchestration thin and verify it through real integration, staging, read-back, logs, or runbooks. A mock is not production evidence.

## Plan Artifact

Keep simple plans inline. Persist multi-turn, high-risk, or handoff-heavy plans at a user-provided or project-native path.

Use only relevant sections:

```markdown
## Outcome And Parent Requirements
## Evidence And Assumptions
## Requirement Coverage
## Architecture And Ownership
## Interfaces And Data Flow
## Failure And Recovery
## Security And Safety
## Observability
## Rollout, Migration, And Rollback
## Verification Matrix
## Alternatives Rejected
## Open Decisions
```

## Review Gate

Before finishing:

- Every accepted requirement, entry point, artifact, and freshness rule maps to a technical decision or explicit non-decision.
- Ownership and durable truth are unambiguous at the chosen risk depth.
- No decision is justified only by generic best practice.
- Existing utilities and approved tradeoffs are preserved or deliberately superseded.
- Verification proves the user-visible outcome at the right evidence level.
- Remaining questions are genuinely blocking and assigned to the correct decision owner.
