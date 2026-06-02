---
name: implement
description: Use when the user asks to implement an already defined feature, approved task, refactor, test, workflow change, API/schema contract change, UI change, or small commit in a software project.
---

# Implement

Implement one clear, approved task with the smallest coherent edit set, matching the target project's existing contracts and conventions.

## Boundary

Use this skill when the expected behavior is already clear enough to build.

Do not use this skill for:

- Unknown failures, regressions, flaky behavior, or root-cause work. Use `diagnose`.
- Ambiguous requirements or unsettled technical choices. Use `grill-plan`.
- Turning a converged requirement into a PRD. Use `to-prd`.
- Architecture opportunity discovery. Use `architecture-review`.

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

## Phase 4: Verify

Run verification that matches risk:

- Narrow test for the changed seam.
- Typecheck/lint/build command from the project instructions.
- Browser, CLI, API, DB, or log check when the behavior is runtime-facing.
- For production-facing fixes, verify local behavior and deployed/live behavior separately. Do not describe a local fix as live unless current runtime evidence confirms it.
- For report or artifact workflows, verify every bound output: primary file, index or manifest, reader/export copy, links, and date/freshness fields.

If verification cannot run, explain why and state the remaining risk.

## Phase 5: Deliver

Final response should include:

- What changed.
- Why this location and shape matched the contract.
- Verification results.
- Exact environment, data date, freshness window, or deployment state when those facts matter.
- Residual risk or skipped verification.

If a plan or checklist was created, close it out before the final response.

When committing, stage only related files and keep unrelated dirty worktree changes out.
