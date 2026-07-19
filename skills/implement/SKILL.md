---
name: implement
description: "Use when a clear feature, refactor, test, workflow, UI, API, schema, documentation, or selected task is ready to build with a coherent edit set and outcome-focused verification."
---

# Implement

Carry a clear task through inspection, editing, verification, and truthful handoff. Optimize for the smallest coherent change, not the smallest diff at the expense of correctness.

## Boundary

Use this skill when the expected behavior is clear enough to build.

Do not use it for:

- Unknown failures that need root-cause work. Use `diagnose`.
- Materially ambiguous goals or behavior. Use `grill-plan`.
- Unsettled architecture, ownership, state, or rollout design. Use `technical-plan`.
- Deep-module/interface design or architecture review. Use `improve-codebase-architecture` or `architecture-review`.

A build request authorizes normal in-scope implementation steps, including focused tests and local verification. It does not authorize a materially different feature, destructive migration, external publication, production mutation, or unrelated cleanup.

## Operating Contract

- Lead from the user-visible outcome and define what done means.
- Inspect repository evidence before asking questions.
- Make safe, reversible, project-native assumptions when they do not change the requested result.
- Ask only when a missing choice would materially change behavior, data, security, compatibility, cost, or an irreversible action.
- Continue until the requested outcome is implemented and proportionately verified, or a concrete blocker remains.
- Preserve unrelated user changes and do not overwrite a dirty worktree casually.

## Workflow

### 1. Establish the change contract

For simple work, keep this mental and concise. For higher-risk work, write down:

- Input, output, and error behavior.
- User-visible and downstream consumer expectations.
- Source of truth, persistence, freshness, and artifact effects.
- Entry points that must stay consistent: UI, API, CLI, worker, import, automation, report, or export.
- Compatibility, migration, rollout, and non-goals.
- Observable acceptance evidence.

If a supplied PRD, plan, or task artifact has status, record its starting state. Update it only when that transition is part of the requested workflow, and never mark deployed, migrated, backfilled, approved, or live without matching evidence.

### 2. Find the real local pattern

- Read the nearest applicable instructions and inspect worktree state.
- Use `rg` to find the owning module, callers, tests, utilities, and neighboring patterns.
- Batch independent reads and searches.
- Derive commands from project manifests, lockfiles, and local documentation.
- For runtime or data-facing work, inspect the current writer, consumer, artifact, data snapshot, or runtime path when cheap and safe.

### 3. Edit a coherent slice

- Use the owning module and existing helpers before adding new abstractions.
- Change all in-scope entry points that share the contract.
- Add an abstraction only when it removes real duplication, improves locality, or creates a current useful seam.
- Avoid speculative compatibility, unrelated cleanup, and project-specific facts in reusable rules.
- Add comments or docstrings only when requested or when a non-obvious invariant would otherwise be easy to break. Explain why, not obvious syntax.

### Comment and documentation mode

When the user explicitly asks for comments, TSDoc, Rustdoc, docstrings, or equivalent documentation:

- Preserve behavior unless the request also includes a code change.
- Match the project's language and documentation convention.
- Write for an experienced engineer who knows the runtime but not this codebase's intent.
- Explain purpose, invariants, tradeoffs, ownership, and surprising edge cases; do not narrate obvious syntax.
- Add function-level documentation only when the name and signature do not make the role clear.
- Keep inline comments next to genuinely subtle blocks and remove stale or misleading comments encountered in scope.
- Verify that a comment-only pass did not alter behavior.

### 4. Verify by evidence level

Choose the narrowest sufficient ladder and keep levels distinct:

1. `Static`: inspect diff, types, schemas, links, or generated structure.
2. `Code`: focused tests, typecheck, lint, build, or deterministic scripts.
3. `Artifact/read-back`: reopen the file, query the stored row, inspect the report body/index, or fetch the saved object.
4. `Runtime`: exercise the real local or staging UI, CLI, API, worker, provider, or database path.
5. `Live`: confirm the deployed version and original production-visible outcome when the request includes live completion.

Do not claim a higher level from lower-level evidence. A passing mock, HTTP 200, completed job, created file, or green deployment status is not automatically proof of the final user-visible result.

## Test Boundary

- Test meaningful deterministic rules as pure seams: parsing, normalization, builders, formatting, authorization predicates, state transitions, payload mapping, and deterministic error selection.
- Keep side-effecting orchestration thin and prefer real integration, local-real smoke, staging, read-back, log, or runbook evidence over mock-heavy business tests.
- Use protocol fakes only for stable serialization or adapter contracts and state what they do not prove.
- Do not reshape production code only to satisfy a mock.

## Completion

Before finishing:

- The requested behavior exists across every in-scope entry point.
- Verification matches the risk and the original acceptance evidence.
- User changes and unrelated files remain intact.
- Temporary probes and artifacts are removed or intentionally documented.
- Source artifact status is truthful when updated.
- Any skipped runtime, deployment, migration, backfill, or live check is named as residual risk.

Report what changed, why this shape fits the contract, verification by evidence level, and remaining risk. Do not present local work as live work.
