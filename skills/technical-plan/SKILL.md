---
name: technical-plan
description: "Use when the desired behavior is mostly settled but implementation needs an end-to-end technical contract across architecture, ownership, durable state, data flow, failures, recovery, observability, rollout, migration, verification, and final module or API boundaries; also use to restate an existing design in plain user-story language. For focused alternative module interfaces or seam placement, use improve-codebase-architecture."
---

# Technical Plan

## Goal And Boundary

Design the smallest buildable system that satisfies the accepted outcome. Ground decisions in current repository or runtime evidence, user-approved constraints, or explicit assumptions, and make the contract self-contained for an implementer who did not see the earlier conversation.

Use `grill-plan` when product intent is still materially ambiguous, `diagnose` for an unexplained failure, `architecture-review` to establish whether a structural concern is real, `improve-codebase-architecture` for focused interface alternatives, `to-prd` for decision-faithful documentation without new design, and `implement` when the task is already buildable.

A planning-only request stops at the plan. An end-to-end delivery request may continue to implementation once the design is decision-complete and no new authority or review gate is required.

## Input Modes

- `Inline`: reconstruct the accepted outcome from the current request.
- `Artifact-backed`: use a supplied requirement, PRD, ADR, or design as the source contract.
- `Intent playback`: explain an existing design through users, scenarios, state changes, failures, and visible outcomes without silently reviewing or redesigning it.
- `Architecture correction`: preserve stable outcome and safety invariants while deciding which structural hypotheses are retained, replaced, or superseded.

For intent playback, separate source content from inference, preserve goals and non-goals, and identify concrete mismatches with the user's intent. The newest explicit correction wins over older assumptions.

## Proportional Depth

Choose the depth from the risk, not from a fixed template:

- `Light`: local behavior without durable state or external effects; settle owner, interface, errors, and verification.
- `Standard`: shared APIs, stored data, reports, or cross-entry workflows; add source of truth, consumers, freshness, compatibility, observability, and rollout.
- `Full contract`: authorization, secrets, destructive actions, external providers, queues, workers, migrations, or other durable effects; add identity, idempotency, confirmation, recovery, reconciliation, and fail-safe behavior.

## Planning Context

Establish the user-visible outcome, observable done criteria, accepted decisions, non-goals, rejected options, entry points, consumers, artifacts, compatibility, freshness, and open decisions. Label verified facts, inferences, assumptions, and unresolved choices.

Trace the real system far enough to identify current owners, callers, writers, readers, schemas, utilities, runtime boundaries, and deployment facts. Current data or deployment claims need exact environment and freshness evidence. Reuse or deliberately supersede project and platform utilities rather than inventing parallel rules for parsing, time, validation, authorization, retries, caching, or serialization.

Separate two kinds of contract:

- `Outcome invariants`: behavior, safety, authorization, durable facts, and user-visible guarantees that the design must preserve.
- `Structural hypotheses`: owner placement, dependency direction, synchronization, interface shape, adapter location, and compatibility paths that current evidence may retain or challenge.

For a challenged structure, record the evidence, chosen disposition, expected benefit, counterevidence, and future falsification signal. Do not make the current architecture permanent by calling it a requirement.

## Buildable System Contract

Cover only decisions needed to implement and verify the chosen depth:

- One owner for each fact, policy, side effect, and visible state.
- Public interfaces, schemas, errors, ordering, and compatibility.
- Durable truth versus cache, job, socket, UI, generated artifact, or transport observation.
- Data flow, identity, writer/reader ordering, freshness, idempotency, and side-effect boundaries.
- Failure classes, retry, replay, reconciliation, and unknown-after-side-effect behavior.
- Security, permissions, destructive-action boundaries, and secret handling.
- Logs, metrics, run identities, read-back, and operator-visible progress or stuck state.
- Rollout, migration or backfill, rollback, ownership cutover, temporary compatibility window, and old-path deletion.

Prefer deletion, reuse, and one clear owner over new indirection. A production seam needs a current caller, real variation, a protocol or ownership boundary, or a deterministic responsibility useful without a fake.

## Verification Contract

Design evidence at the boundary of each claim:

| Claim | Matching evidence |
| --- | --- |
| Deterministic rule | Focused test with realistic inputs and exact behavior |
| Stored fact or artifact | Durable read-back and completeness check |
| Dependency or side effect | Real integration, local-real smoke, staging, logs, or runbook |
| Deployment or current-status result | Intended version and original user-visible outcome observed live |

Fakes and fixtures may verify a stable protocol or deterministic mapping; they do not prove the dependency, orchestration, deployment, or final result. If real evidence is unavailable, keep the gap explicit and make the missing check repeatable instead of changing production ownership to satisfy a test.

For parsing and data boundaries, plan realistic upstream shapes and explicit malformed, missing, null, and blank behavior. Absence fails closed rather than becoming valid data such as a zero unless the public contract defines that meaning.

## Plan Artifact And Completion

Keep a simple plan inline. Persist a project-native artifact when duration, risk, migration, or handoff requires durable state. Use only relevant sections:

```markdown
## Outcome And Invariants
## Evidence And Assumptions
## Structural Hypotheses And Dispositions
## Architecture, Ownership, And Interfaces
## Data, Failure, Security, And Recovery
## Migration, Cutover, Rollback, And Deletion
## Observability And Verification
## Alternatives And Open Decisions
```

The plan is ready when accepted requirements map to decisions or explicit non-decisions, ownership and durable truth are unambiguous at the chosen depth, migration reaches one authoritative path and retires temporary ones, verification proves the user-visible outcome at the right evidence level, and every remaining question has a real decision owner.
