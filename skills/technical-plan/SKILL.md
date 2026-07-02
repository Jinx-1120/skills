---
name: technical-plan
description: "Use when requirements are mostly settled and technical design is needed for architecture, module/API boundaries, ownership, durable state, data flow, side effects, failure/recovery, observability, rollout, or tests. Also use when the user asks to restate or explain a design document in plain user-story language before planning."
---

# Technical Plan

Turn a confirmed requirements contract into a buildable technical plan. This skill designs the solution; it does not collect open-ended requirements, write the final PRD, split tasks, or implement code.

Use a risk-scaled architecture contract lens: keep simple work light, but make ownership, durable facts, runtime projections, failure semantics, and recovery explicit for data-facing, security-sensitive, external-system, multi-runtime, or side-effect-heavy work.

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

## Planning Depth

Choose the smallest depth that fits the risk:

- Light plan: local behavior, no durable state, no external side effects. Cover owner, public interface, errors, and test seam.
- Standard plan: shared API, workflow, stored data, reporting artifact, or cross-entry behavior. Add source of truth, writer, consumers, compatibility, freshness, and observability.
- Full contract plan: authorization, secrets, payments, destructive actions, provider integrations, queues, workers, multi-runtime behavior, or durable side effects. Add explicit ownership, persistent facts vs runtime projections, idempotency, ack/accept/commit/external-success boundaries, recovery, and fail-closed behavior.

If the user asks for a quick plan and the work is low-risk, do not expand into a full contract. If the selected depth exposes unresolved product decisions, hand back to `grill-plan` instead of turning assumptions into architecture.

## Intent Playback Mode

Use this mode when the user asks to restate, replay, or explain a design document so they can verify whether it matches their intent.

- Read the design document and any directly required linked context before summarizing.
- Do not review, redesign, or implement unless the user asks for that after the playback.
- Use the requested language. For Chinese requests, write natural Chinese.
- Avoid jargon and unexplained technical labels. Explain the design through users, scenarios, decisions, data/state changes, failure paths, and visible outcomes.
- Preserve every material detail: goals, non-goals, user stories, entry points, contracts, edge cases, errors, data freshness, operational behavior, rollout constraints, and open questions.
- Separate verified document content from assumptions or inferences.
- End by asking which parts do not match the user's intent before moving into planning.

## Phase 1: Load Or Reconstruct Requirements

- Identify the target project area and nearest applicable local instructions.
- Reconstruct the goal, accepted decisions, boundaries, rejected options, user corrections, entry points, consumers, data freshness rules, required artifacts, and open questions.
- Select the planning depth and state why only if it affects the plan shape.
- Treat the newest explicit user correction as authoritative.
- If a requirement is unclear but non-blocking, record it as an assumption.
- If a missing decision changes architecture, data contracts, security, rollout, or acceptance, stop and hand back to `grill-plan`.

## Phase 2: Ground In The Codebase

- Read the smallest code, docs, schema, routes, tests, ADRs, runtime evidence, or config needed to design against the real system.
- Batch independent reads and searches when several files are likely relevant.
- Before proposing implementation paths or new helpers, discover the existing utility surface relevant to the change: dependency utility packages from manifests/imports, project-level helpers such as `utils`, `lib`, `common`, or shared workspace packages, and module-level helper files near the target feature.
- Record whether each relevant utility should be reused, extended, wrapped, or deliberately rejected. If rejected, state the concrete mismatch; do not create duplicate parsing, formatting, validation, authorization, date/time, URL, SQL, retry, cache, or serialization logic by default.
- In monorepos, check package exports and shared workspace packages before inventing a local helper. In single-package projects, check project-wide helpers before module-local helpers, and module-local helpers before adding a new abstraction.
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

For standard and full contract plans, apply these checks where relevant:

- Ownership: name the owning subsystem for each fact, policy, side effect, and externally visible state; name non-owners that may reference it but must not mutate it.
- Durable facts vs runtime projections: separate source-of-truth records from caches, sockets, jobs, process state, UI state, generated files, and transport observations.
- Identity and idempotency: define stable keys for entities, requests, inputs, outputs, retries, and side effects; avoid using one key to mean several domain concepts.
- Code contracts vs stored configuration: keep user-configurable policy small and declared; keep event semantics, privileged decisions, and cross-runtime invariants in code unless a user story requires configurability.
- Adapter boundaries: external adapters normalize provider input/output and expose declared capabilities; domain state, authorization, scheduling, and persistence stay with their owners.
- Failure semantics: distinguish malformed input, missing data, stale data, denied access, unsupported capability, retryable failure, dead letter, and unknown-after-side-effect.
- Confirmation boundaries: distinguish transport ack, internal acceptance, durable commit, actor or worker delivery, user-visible reply, and external provider success.
- Recovery and observability: define replay, reconciliation, read-back, diagnostics, run ids, and operator-visible stuck states for facts that must survive process death.

Do not over-design speculative abstractions. If a deeper review of existing module boundaries is needed, hand off that slice to `architecture-review`.

## Testing Strategy Contract

Design tests from first principles before listing test files:

- Classify the target code into pure functions, thin orchestration/business functions, and runtime verification paths.
- Pure functions must have code-level test cases when they carry meaningful rules: normalization, parsing, formatting, SQL or request builders, authorization predicates, visibility predicates, state transitions, payload mapping, and deterministic error selection.
- Functions that perform business side effects such as database queries, Redis/cache reads or writes, queue operations, file storage, SMS/email sends, external API calls, or provider workflows should not get extra mock-heavy unit tests merely to prove business correctness. Those tests usually verify the mock, not the real system.
- If a side-effecting function contains complex branching, design the implementation so the durable rule is extracted into a pure function or deterministic builder, then test that seam. Keep the side-effecting function thin: load trusted context, call the tested rule/builder, perform the real effect, and return the result.
- Verification for side-effecting behavior belongs in integration tests, staging or local-real smoke tests, read-back checks, migration/backfill validation, log inspection, or manual runbooks using real dependencies or project-approved test infrastructure.
- Do not present a mocked database, Redis, queue, or provider test as acceptance evidence for production behavior. If a fake is used for protocol-level or serialization checks, state exactly what it proves and what remains for real-runtime verification.
- The testing strategy section must separate code-level tests from runtime/read-back verification, and explicitly name skipped verification when no safe real environment exists.

## Phase 4: Technical Plan Artifact

For simple work, return the plan inline. For multi-turn, high-risk, or cross-skill work, write or request a checkpoint artifact. Prefer a user-provided path; otherwise use a project-local path such as `docs/<slug>.md` when writing is appropriate.

Use this structure:

```markdown
## Parent Requirements

Path or inline source summary.

## Requirement Coverage

Map each accepted decision, boundary, rejected option, entry point, artifact, and freshness rule to a technical decision or explicit non-decision.

## Architecture

## Ownership And State Contract

## Module And Interface Contracts

## Data And Artifact Flow

## Security And Safety Review

## Failure, Idempotency, And Recovery

## Observability And Operations

## Rollout And Migration

## Testing Strategy

## Alternatives Rejected

## Open Technical Questions

```

## Phase 5: Review Gate

Before finishing, verify:

- The plan does not contradict the requirements ledger.
- Every user-approved boundary and rejected option is preserved.
- Every known entry point and consumer is covered.
- Every technical decision has evidence, a repo pattern, or a stated assumption.
- The plan names relevant existing utility packages, project-level helpers, or module-level helpers considered for the implementation path, and explains any deliberate non-reuse.
- Standard and full contract plans identify owners, durable facts, runtime projections, and failure semantics instead of leaving them implicit.
- The plan does not widen configuration, provider-specific behavior, or runtime mechanism into a generic platform abstraction without a current user story.
- Open technical questions are truly blocking.
