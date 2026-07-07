---
name: to-prd
description: "Use to convert approved requirements and optional technical plans into a PRD, implementation brief, or self-contained third-party consultation brief with accepted decisions, boundaries, contracts, source trace, and coverage checks; do not invent new requirements or architecture."
---

# To PRD

Turn converged requirements and optional technical-plan evidence into a precise requirement document. This skill writes the PRD; it does not collect open-ended requirements or invent the technical design.

## Boundary

Use this skill after `grill-plan` or `technical-plan`, or directly when the scope is already clear.

Do not use this skill for:

- Debugging or fixing a broken behavior. Use `diagnose`.
- Exploring ambiguous requirements or technical choices. Use `grill-plan`.
- Designing architecture, module boundaries, security posture, rollout, or testing strategy from requirements. Use `technical-plan`.
- Splitting approved work into implementation tasks. Use `task-breakdown`.
- Implementing the PRD. Use `implement`.
- Architecture improvement or refactoring opportunity discovery. Use `improve-codebase-architecture`.
- Validating whether an architecture problem is real. Use `architecture-review`.

## Input Modes

- Inline mode: if the current prompt or conversation is enough, reconstruct the minimal requirements contract and proceed.
- Artifact mode: if a requirements ledger, technical plan, notes file, or existing PRD path is provided, read it first and use it as the source of truth.
- High-risk no-artifact mode: if missing history or compaction makes accepted decisions unreliable, stop and ask for the missing checkpoint or run `grill-plan` before drafting.

## External Consultation Brief Mode

Use this mode when the user wants a complete draft they can send to a third party for review or discussion.

- Make the document self-contained. Assume the reader has no prior conversation context.
- Preserve source-trace discipline: separate confirmed facts, accepted decisions, rejected options, assumptions, and open questions.
- Include enough background for useful advice without leaking unrelated implementation noise.
- Cover: audience and review goal, project background, current user stories, current solution, constraints, non-goals, existing architecture or document summary, known tradeoffs, rejected options, candidate improvements, risks, and specific questions for the third party.
- Do not turn open questions into decisions. Do not invent architecture to make the brief feel complete.
- Prefer a long draft when needed; the success criterion is that the user can forward it without adding missing context.

## Phase 1: Reconstruct The Source Contract

Before drafting, build a compact source ledger from the provided artifacts and available conversation:

- Explicit user goals and success criteria.
- Accepted decisions and defaults.
- Rejected options, non-goals, and "do not do this" boundaries.
- User corrections that override earlier assistant assumptions.
- Required entry points, consumers, data freshness rules, artifacts, tests, and rollout constraints.
- Approved technical-plan decisions, if one exists.
- Open questions that still block implementation or acceptance.

Use the newest explicit user correction as authoritative when conversation history conflicts. Do not reintroduce rejected options through "reasonable defaults." If compaction or missing history prevents a reliable ledger, state the gap and ask only for the missing blocking boundary instead of drafting a PRD that pretends the scope is complete.

## Phase 2: Ground In The Codebase

- Identify the target project area, then read the nearest applicable `AGENTS.md` or equivalent local instructions.
- Explore existing implementation, docs, schema, routes, scripts, tests, and user-facing flows as needed.
- Batch independent evidence gathering when several files or searches are obviously needed.
- Use domain vocabulary from existing docs when available.
- Separate verified facts from assumptions.
- Check the codebase evidence against the source ledger. Repository patterns can refine PRD wording, but they must not silently drop, reverse, or invent user-approved boundaries or technical-plan decisions.
- If outputs are archived, indexed, copied, exported, or consumed by automation, treat those linked artifacts as part of the requirement rather than a follow-up detail.
- If a blocking decision is missing, stop drafting and run `grill-plan` to converge it first.

## Phase 3: Draft The PRD

Use this structure:

```markdown
## Problem Statement

Describe the user's problem from the user's perspective.

## Solution

Describe the intended behavior from the user's perspective.

## Accepted Decisions And Boundaries

List settled decisions, explicit non-goals, rejected options, and user corrections that constrain the PRD.

## User Stories

Numbered stories covering normal path, edge cases, error states, permissions, data freshness, and operational visibility where relevant.

## Contracts

List input/output shapes, state transitions, persistence, API/schema/CSV/artifact contracts, freshness/cutoff fields, stale or partial-data behavior, linked artifact updates, and backward compatibility expectations.

## Implementation Decisions

List only implementation decisions already approved in the requirements ledger, technical plan, or repository evidence. Do not invent architecture here. Avoid brittle file paths unless the file path is itself a decision.

## Testing Decisions

Describe what behavior must be tested, which seams are appropriate, and what prior tests in the repo are comparable.

## Out Of Scope

List explicitly excluded work and future ideas.

## Open Questions

Include only questions that block implementation or acceptance.

## Source Trace

Map each major requirement and boundary to conversation decisions, repository evidence, or assumptions. Keep it concise; its purpose is coverage, not audit noise.
```

## Phase 4: Coverage Review Gate

Before presenting the PRD, compare it against the source ledger and technical plan:

- Every accepted decision appears in the PRD.
- Every rejected option or explicit non-goal appears in `Accepted Decisions And Boundaries` or `Out Of Scope`.
- Every known entry point, consumer, artifact, freshness rule, and verification gate is represented.
- Every implementation blocker is either resolved in the PRD or listed as an open question.
- Every technical decision included in the PRD traces back to an approved source.

End with the exact decisions the user should approve before coding, including entry points, source-of-truth choices, freshness expectations, and verification gates. If the user asked for stepwise implementation, turn the PRD into reviewable phases with acceptance checks for each phase.
