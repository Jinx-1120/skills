---
name: implement
description: "Use when a clear, approved task or selected task artifact is ready to implement with a minimal coherent edit set and focused verification: features, refactors, tests, workflows, UI/API/schema changes, code comments, doc comments, docstrings, or small commits. When implementation starts from a stateful source artifact, update its status truthfully."
---

# Implement

Implement one clear, approved task with the smallest coherent edit set, matching the target project's existing contracts and conventions.

## Boundary

Use this skill when the expected behavior is already clear enough to build.

Do not use this skill for:

- Unknown failures, regressions, flaky behavior, or root-cause work. Use `diagnose`.
- Ambiguous requirements or unsettled technical choices. Use `grill-plan`.
- Designing the technical solution. Use `technical-plan`.
- Turning a converged requirement into a PRD. Use `to-prd`.
- Splitting approved work into tasks. Use `task-breakdown`.
- Architecture opportunity discovery. Use `architecture-review`.

## Input Modes

- Inline mode: if the current prompt contains one clear approved task, proceed.
- Artifact mode: if a task breakdown, PRD, technical plan, or task file path is provided, read it first and implement only the selected task.
- High-risk no-artifact mode: if missing history or compaction makes the task boundary, acceptance checks, or verification gates unreliable, stop and ask for the missing checkpoint or run the upstream skill.

## Stateful Source Artifacts

When artifact mode uses a source document with an explicit status, progress marker, checklist gate, or frontmatter state such as `Status:`, `status:`, or `状态：`, treat that state as part of the implementation contract.

- Record the starting state before editing code.
- Before the final response, update the artifact to the truthful outcome: completed and verified, partially completed, blocked, needs review, local-only, or another project-native state.
- Do not leave a source artifact in `Draft`, unchecked, or stale progress when the selected task was actually completed.
- Do not mark an artifact done, accepted, or deployed when verification failed, work is partial, only local code changed, migration/backfill is missing, or live visibility was not proven.
- If the file is not writable or the status owner is unclear, state the exact pending status update instead of inventing a transition.

## Phase 0: Confirm The Work Area

- Identify the concrete project area before editing.
- Read the nearest applicable `AGENTS.md` or equivalent local instructions before editing.
- If the request is review, explanation, or planning only, do not edit code.
- If the user requested staged review gates, stop after each stage.
- Do not move current examples, entity names, prices, dates, or incident facts into durable rules or docs unless the user explicitly asks.

## Phase 1: Define The Contract

Before changing files, write down the contract you are preserving or changing:

- Input shape and validation.
- Output shape and error modes.
- Persistence, schema, artifact, CSV, API, or UI state expectations.
- Backward compatibility and default behavior.
- The real downstream consumer.
- All entry points that must honor the same behavior: UI, API, CLI, worker, import, automation, report, or export path.
- Source-of-truth and freshness expectations for data-facing work, including how stale, partial, or unavailable data should degrade.

If the requested change would add a feature, constraint, schema, or operational behavior the user did not ask for, ask first.

## Phase 2: Find The Local Pattern

- Use `rg` to find the real implementation path and neighboring examples.
- Before reading multiple files, decide the likely file/search set and batch independent reads/searches in parallel.
- Prefer existing helpers, module boundaries, test style, and naming.
- Derive commands from local instructions, `package.json`, `pyproject.toml`, `Cargo.toml`, lockfiles, or equivalent local files.
- Use the package manager and verification commands declared by the project; if not declared, infer them from nearby lockfiles and scripts.
- For production or data changes, inspect the current runtime/data path before editing when it is cheap and safe: latest snapshot, writer job, consumer query, logs, or artifact index.

## Phase 3: Edit In A Thin Slice

- Use `apply_patch` for manual edits. Read enough context first, then batch coherent edits instead of repeated micro-patches.
- Make the smallest edit that satisfies the contract.
- Keep business logic near its owning module; do not move project-owned runtime logic into skill files.
- Add an abstraction only when it reduces real duplication, improves locality, or creates a useful seam.
- Add comments only when a non-obvious block needs orientation, and match the language already used by nearby code.

## Test Boundary

Before adding or changing tests, classify the changed behavior:

- Pure functions with meaningful rules should get focused code-level tests. This includes deterministic builders, normalizers, parsers, formatters, visibility predicates, state transitions, request or SQL command construction, and payload mapping.
- Side-effecting business functions that query databases, read or write Redis/cache, enqueue jobs, touch storage, send SMS/email, call external providers, or depend on live runtime state should not get new mock-heavy unit tests just for coverage. Mocking those dependencies usually proves only that the mock was wired to the implementation.
- If important logic is trapped inside a side-effecting function, first extract the deterministic rule or command builder behind a small seam and test that pure seam. Keep the side-effecting function as thin orchestration.
- Do not reshape production code solely to satisfy a mock test. Add a seam only when it also improves locality, removes duplication, clarifies ownership, or matches an existing project pattern.
- Protocol-level fakes or local test servers are acceptable only when they verify stable serialization, transport, or adapter contracts. State their limits; they are not proof that the real business dependency behaved correctly.
- For side-effecting behavior, prefer existing integration harnesses, local-real smoke tests, staging checks, read-back queries, log checks, or documented manual verification. If none can be run safely, say so and name the remaining production risk.
- Preserve existing valuable tests. Remove or rewrite low-value mock tests only when the task clearly includes test cleanup or the test blocks the correct design.

## Comment And Doc Pass

Use this mode only when the user explicitly asks to add comments, TSDoc, Rustdoc, docstrings, or equivalent documentation.

- Assume the reader is a strong engineer with several years of full-stack experience and practical experience with the relevant SDKs or runtime, but not this codebase's intent, tradeoffs, and edge cases.
- Write simple English that non-native speakers can understand, unless the project already uses another language consistently.
- Use the documentation convention of the language and project, without limiting the pass to TypeScript or Rust: TSDoc, JSDoc, Rustdoc, Python docstrings, Go doc comments, Java/Kotlin doc comments, shell comments, or the local equivalent.
- Add a comment whenever that reader cannot quickly understand the purpose or reason by looking at the code, name, and surrounding context.
- Prefer explaining why the code exists, what user or system contract it protects, and which tradeoff or edge case forced the shape. Avoid restating obvious code behavior.
- Write function-level comments before function declarations when the function's purpose and use are not immediately and unambiguously clear from the name and signature.
- Omit function-level comments for obvious getters, setters, tiny local helpers, and functions whose name and signature fully explain their role.
- Use narrative style for function documentation, such as "Builds the request payload..." rather than imperative style, such as "Build the request payload...".
- If a function uses a clever, subtle, or unusual technique, explain the rough approach or reason at the function documentation site when that helps the reader understand the implementation.
- Add inline explanatory comments for clever, obscure, important, surprising, or edge-case-driven blocks. Keep them close to the code they explain.
- Preserve behavior during comment-only passes. Do not refactor or change contracts unless the user explicitly asked for that too.
- Remove stale, misleading, or redundant comments when found.

## Phase 4: Verify

Run verification that matches risk:

- Narrow test for the changed seam.
- Typecheck/lint/build command from the project instructions.
- Browser, CLI, API, DB, or log check when the behavior is runtime-facing.
- For production-facing fixes, verify local behavior and deployed/live behavior separately. Do not describe a local fix as live unless current runtime evidence confirms it.
- For report or artifact workflows, verify every bound output: primary file, index or manifest, reader/export copy, links, and date/freshness fields.
- For implementation from a PRD, design doc, or task artifact, verify outcome alignment: accepted intent, user stories, edge cases, contracts, and non-goals are reflected in the final behavior, not merely in the implementation steps.
- For stateful source artifacts, verify the final status or progress entry matches the actual implementation and verification evidence.
- Keep code-level test evidence and runtime/read-back evidence separate in your judgment. Do not let mocked side-effect tests substitute for real verification when the user story depends on persistence, caches, queues, providers, or deployed behavior.

If verification cannot run, explain why and state the remaining risk.

## Phase 5: Deliver

Final response should include:

- What changed.
- Why this location and shape matched the contract.
- Verification results.
- Source artifact status update, when artifact mode used a stateful document.
- Exact environment, data date, freshness window, or deployment state when those facts matter.
- Residual risk or skipped verification.

If a plan or checklist was created, close it out before the final response.

When committing, stage only related files and keep unrelated dirty worktree changes out.
