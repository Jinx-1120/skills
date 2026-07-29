---
name: grill-plan
description: "Use when a request's goal, scope, success criteria, user-visible behavior, or consequential choices are materially ambiguous and must converge before design or implementation."
---

# Grill Plan

## Goal

Turn genuine product ambiguity into the smallest decision-complete requirements contract. Resolve facts from evidence, make safe reversible assumptions, and involve the user only where their choice or authority changes the result.

Treat the current implementation as evidence about constraints, not as an automatic product requirement. The newest explicit user correction is authoritative.

## Scope

Use this skill when uncertainty is about what should be built or what outcome is acceptable. Adjacent work belongs to:

- `diagnose` for a concrete wrong behavior.
- `technical-plan` for settled behavior that still needs technical design.
- `implement` for a clear task ready to build.
- `to-prd` for a document based on accepted decisions.
- `architecture-review` for evidence-backed review of an existing structure.

Material product choices remain with the user. An end-to-end delivery request may continue into the next applicable skill once those choices are resolved and no new authority is required.

## Decision Model

Classify uncertainty by what can legitimately resolve it:

- `Discoverable fact`: repository, runtime, data, artifact, or current-source evidence can answer it.
- `Reversible assumption`: a project-native default preserves the requested outcome and can be changed cheaply.
- `Consequential choice`: alternatives change visible behavior, scope, ownership, security, cost, rollout, or an irreversible effect.
- `Missing authority`: the next action would affect an external system or person, or materially expand the request.

Investigate discoverable facts before asking. State a reversible assumption only when it matters to the result. Ask the smallest decision packet that lets work continue, with a recommendation, the meaningful alternatives, and why evidence cannot decide.

When an existing architecture or workflow conflicts with the accepted outcome, keep the outcome intact and label the implementation constraint as `challenged`; do not silently shrink the requirement to fit the current system.

## Requirements Contract

Reconstruct only the context the downstream reader needs:

- User or consumer and the capability they gain.
- Observable done criteria and behavior that must remain unchanged.
- Accepted decisions, boundaries, non-goals, and rejected options.
- Entry points, source of truth, freshness, artifacts, and failure behavior when relevant.
- Verified facts, assumptions, challenged implementation constraints, and open decisions.

Use a compact inline contract for small work. Persist a project-native artifact only when duration, risk, or handoff makes durable state useful. Relevant headings may include:

```markdown
## Outcome
## Done When
## Accepted Decisions
## Boundaries And Non-goals
## Data, Freshness, And Artifacts
## Assumptions And Challenged Constraints
## Open Decisions
## Next Owner
```

## Completion

The requirements are ready when no unresolved choice can silently change the user-visible result, success is observable, assumptions and evidence are distinguishable, and the next owner can proceed without reconstructing the conversation. If a real blocker remains, identify the decision owner and the smallest input needed.
