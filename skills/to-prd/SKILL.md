---
name: to-prd
description: Use when converting an already converged project requirement, grill-plan result, current conversation, or approved scope into a precise PRD or implementation brief.
---

# To PRD

Turn converged context and codebase evidence into a precise requirement document. This skill writes the PRD; it does not collect open-ended requirements.

## Boundary

Use this skill after `grill-plan` when important decisions needed convergence, or directly when the scope is already clear.

Do not use this skill for:

- Debugging or fixing a broken behavior. Use `diagnose`.
- Exploring ambiguous requirements or technical choices. Use `grill-plan`.
- Implementing the PRD. Use `implement`.
- Architecture opportunity discovery. Use `architecture-review`.

## Phase 1: Ground In The Codebase

- Identify the target project area, then read the nearest applicable `AGENTS.md` or equivalent local instructions.
- Explore existing implementation, docs, schema, routes, scripts, tests, and user-facing flows as needed.
- Use domain vocabulary from existing docs when available.
- Separate verified facts from assumptions.
- If a blocking decision is missing, stop drafting and run `grill-plan` to converge it first.

## Phase 2: Draft The PRD

Use this structure:

```markdown
## Problem Statement

Describe the user's problem from the user's perspective.

## Solution

Describe the intended behavior from the user's perspective.

## User Stories

Numbered stories covering normal path, edge cases, error states, permissions, data freshness, and operational visibility where relevant.

## Contracts

List input/output shapes, state transitions, persistence, API/schema/CSV/artifact contracts, and backward compatibility expectations.

## Implementation Decisions

List module-level decisions, interfaces to change, schema changes, API contracts, and important constraints. Avoid brittle file paths unless the file path is itself a decision.

## Testing Decisions

Describe what behavior must be tested, which seams are appropriate, and what prior tests in the repo are comparable.

## Out Of Scope

List explicitly excluded work and future ideas.

## Open Questions

Include only questions that block implementation or acceptance.
```

## Phase 3: Review Gate

End with the exact decisions the user should approve before coding. If the user asked for stepwise implementation, turn the PRD into reviewable phases with acceptance checks for each phase.
