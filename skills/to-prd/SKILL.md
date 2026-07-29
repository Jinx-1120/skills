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

Reconstruct the context needed by a reader with no conversation history, and keep unlike claims visibly separate:

- `User requirement`: requested behavior, audience, and observable success.
- `Outcome invariant`: behavior, safety, or compatibility that must survive implementation choices.
- `Current implementation fact`: evidence about today's system, not automatically a requirement.
- `Approved decision`: a product or technical choice the user or source artifact has accepted.
- `Provisional hypothesis`: an unapproved structural assumption that still needs evidence or a decision.
- `Open question`: missing input whose alternatives materially change the result.

Also preserve the newest user corrections, non-goals, rejected options, entry points, consumers, artifacts, freshness, rollout constraints, and verification gates. Repository evidence may clarify wording but cannot silently override an accepted decision. Route a materially unresolved product choice to `grill-plan` rather than disguising it as a default.

## Artifact Modes

- `PRD`: user-facing problem, behavior, acceptance, and boundaries.
- `Implementation brief`: compact contract for a clear engineering change.
- `External consultation brief`: self-contained background, current design, constraints, tradeoffs, evidence, and precise questions for a third party.
- `Revision`: preserve stable identifiers and accepted content; show what changed and why.

Scale the document to its consumer. Do not force every low-risk task into a long template.

## Drafting Contract

Use the nearest instructions, supplied artifacts, and the smallest relevant repository evidence to make the document self-contained. Lead from the user's problem and observable outcome, then add contracts and constraints. Every material statement should trace to the request, a source artifact, current evidence, an approved decision, or an explicitly labeled hypothesis. Scale detail to the downstream reader and risk.

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
- No current implementation fact or provisional hypothesis is promoted into a requirement.
- Open questions remain questions rather than disguised defaults.
- `Done When` is observable by the downstream implementer or reviewer.
- The document is self-contained for its intended reader.

If this document is an intermediate step in an end-to-end request and no approval decision remains, hand off to the next skill without inventing a ceremonial approval. Do not label the PRD user-approved until the user actually approves it.
