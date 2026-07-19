---
name: to-prd
description: "Use when accepted requirements and optional technical decisions need to become a precise PRD, implementation brief, or self-contained third-party consultation brief without inventing new requirements or architecture."
---

# To PRD

Produce a decision-faithful document that another person or agent can use without reconstructing the conversation.

## Boundary

Use this skill after requirements are sufficiently settled.

Do not use it for:

- Discovering materially ambiguous goals. Use `grill-plan`.
- Making target architecture, ownership, state, rollout, or test-design decisions. Use `technical-plan`.
- Debugging or fixing a failure. Use `diagnose`.
- Sequencing approved implementation work. Use `task-breakdown`.
- Implementing the document. Use `implement`.

A PRD may record approved technical decisions, but it must not invent them to appear complete.

## Source Contract

Before drafting, reconstruct and label:

- Goals, users, and observable success criteria.
- Accepted decisions and defaults.
- Newest user corrections.
- Boundaries, non-goals, and rejected options.
- Entry points, consumers, linked artifacts, data/freshness rules, rollout constraints, and verification gates.
- Approved technical decisions, if supplied.
- Assumptions and unresolved blockers.

Use repository evidence to clarify wording, not to silently override accepted decisions. If missing history or a material product choice makes the document unreliable, ask only for that blocker or route to `grill-plan`.

## Artifact Modes

- `PRD`: user-facing problem, behavior, acceptance, and boundaries.
- `Implementation brief`: compact contract for a clear engineering change.
- `External consultation brief`: self-contained background, current design, constraints, tradeoffs, evidence, and precise questions for a third party.
- `Revision`: preserve stable identifiers and accepted content; show what changed and why.

Scale the document to its consumer. Do not force every low-risk task into a long template.

## Drafting Workflow

1. Read the nearest applicable instructions and supplied source artifacts.
2. Inspect the smallest relevant code, schema, tests, docs, and user-facing flows.
3. Separate confirmed facts, accepted decisions, assumptions, and open questions.
4. Draft from the user's problem and observable outcome, then add contracts and constraints.
5. Trace every major requirement to conversation, source artifact, repository evidence, or an explicit assumption.
6. Run a coverage pass against the source contract.

Use relevant sections from this structure:

```markdown
## Problem And Audience
## Outcome
## Done When
## Accepted Decisions And Boundaries
## User Stories
## Contracts And Failure Behavior
## Data, Freshness, And Artifacts
## Approved Implementation Decisions
## Verification And Rollout
## Out Of Scope
## Open Questions
## Source Trace
```

For an external consultation brief, also include current solution, known tradeoffs, evidence limits, rejected options, and the exact advice requested.

## Quality Gate

- Every accepted decision appears once in a clear owning section.
- Every rejected option and non-goal stays excluded.
- Every entry point, consumer, artifact, freshness rule, and verification gate is covered.
- No technical decision lacks an approved source.
- Open questions remain questions rather than disguised defaults.
- `Done When` is observable by the downstream implementer or reviewer.
- The document is self-contained for its intended reader.

If this document is an intermediate step in an end-to-end request and no approval decision remains, hand off to the next skill without inventing a ceremonial approval. Do not label the PRD user-approved until the user actually approves it.
