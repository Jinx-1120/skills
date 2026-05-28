---
name: architecture-review
description: Use when the user asks to review existing software architecture, find refactoring opportunities, improve module boundaries, consolidate code, improve seams, testability, or AI-navigability.
---

# Architecture Review

Find architecture changes that make the codebase easier to understand, test, and change. Do not implement during the review.

## Boundary

Use this skill for architecture review of existing code.

Do not use this skill for:

- Debugging or fixing a concrete failure. Use `diagnose`.
- Collecting requirements for a new feature. Use `grill-plan`.
- Writing a PRD. Use `to-prd`.
- Implementing a selected refactor. Use `implement`.

## Vocabulary

Use these terms consistently:

- `Module`: code with an interface and implementation.
- `Interface`: what callers must know, including types, invariants, ordering, config, and errors.
- `Implementation`: the code behind the interface.
- `Seam`: where behavior can change without editing all callers.
- `Adapter`: concrete implementation behind a seam.
- `Depth`: leverage behind a small interface.
- `Locality`: change and bugs concentrated in one place.

## Phase 1: Explore

- Identify whether the review is local to one project area or crosses project/package/service boundaries.
- Read the nearest applicable `AGENTS.md` or equivalent project instructions before judging structure.
- For cross-boundary reviews, name the producer, consumer, shared package, runtime, and deployment boundaries before judging structure.
- Read domain docs, ADRs, and `CONTEXT.md` if present.
- Trace real callers and data/control flow before judging structure.
- Note friction while exploring: bouncing across files, shallow pass-through modules, hidden coupling, hard-to-test behavior, duplicated invariants.

## Phase 2: Apply The Tests

For each suspected problem:

- Deletion test: if the module disappeared, would complexity vanish or reappear in callers?
- Interface test: is the interface smaller than the behavior it provides?
- Locality test: can a bug be fixed in one place?
- Seam test: is there more than one real adapter, or only a hypothetical abstraction?
- Testability test: can the behavior be tested through its public seam?

## Phase 3: Present Candidates

Return a short candidate list. Each candidate must include:

- Modules involved.
- Current friction.
- Proposed direction in plain language.
- Benefit in locality, depth, and testability.
- Risks or ADR conflicts.
- Recommendation strength: `Strong`, `Worth exploring`, or `Speculative`.

Do not propose interfaces in detail yet. End by asking which candidate the user wants to explore.

## Phase 4: Deepen Only After Selection

When the user selects a candidate:

- Walk constraints and callers.
- Define what lives behind the seam.
- Decide which tests should survive the refactor.
- Record durable domain terms or ADR decisions only when the user approves.
