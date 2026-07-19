---
name: grill-plan
description: "Use when a request's goal, scope, success criteria, user-visible behavior, or consequential choices are materially ambiguous and must converge before design or implementation."
---

# Grill Plan

Turn real ambiguity into the smallest reliable requirements contract. Resolve facts with evidence first; ask the user only for choices that cannot be discovered and would materially change the result.

## Boundary

Use this skill when uncertainty is about what should be built or what outcome is acceptable.

Do not use it for:

- A concrete failure that needs root-cause work. Use `diagnose`.
- Settled requirements that need technical design. Use `technical-plan`.
- A clear task ready to build. Use `implement`.
- PRD drafting from already accepted decisions. Use `to-prd`.
- Architecture review of an existing system. Use `architecture-review`.

Do not implement while material product choices remain unresolved. If the user asked for end-to-end delivery and the contract becomes clear, continue to the downstream skill in the same task unless the user requested a review gate.

## Decision Policy

Classify each uncertainty before asking anything:

- `Discoverable fact`: inspect repository instructions, code, docs, schemas, tests, artifacts, logs, or current external sources.
- `Reversible assumption`: choose the safest project-native default, state it briefly when material, and continue.
- `Consequential decision`: ask because different answers change user-visible behavior, scope, data ownership, security, cost, rollout, or an irreversible action.
- `Missing authority`: stop when the next action would exceed the user's requested scope or affect an external system or person in a new way.

Do not ask the user to choose implementation details that the repository already answers. Do not turn low-risk uncertainty into a ceremony.

## Workflow

### 1. Reconstruct the outcome

Start from first principles:

- Who is the user or downstream consumer?
- What will they be able to do when this succeeds?
- What observable evidence means done?
- What must remain unchanged?
- What is explicitly out of scope?
- Which newest user correction overrides earlier assumptions?

For data, reports, or automation, also identify source of truth, time or freshness cutoff, stale/partial behavior, linked artifacts, and the action the output should enable.

### 2. Ground the request

- Read the nearest applicable `AGENTS.md` or equivalent instructions.
- Inspect the smallest evidence set that can resolve the uncertainty.
- Batch independent reads and searches.
- Separate verified facts, inferences, assumptions, and unresolved choices.
- For time-sensitive claims, use current evidence and record the exact date, environment, or data cutoff.

### 3. Resolve only blockers

Ask a compact decision packet only when needed. Group at most three related blocking choices and include:

- The decision in plain language.
- Your recommended default.
- The consequence of the main alternatives.
- Why repository or runtime evidence cannot decide it.

If no material blocker remains, do not ask for confirmation merely to restate the plan.

### 4. Produce the contract

Keep the contract proportional to the work. Include only relevant fields:

```markdown
## Outcome
## Done When
## Accepted Decisions
## Boundaries And Non-goals
## Entry Points And Consumers
## Data, Freshness, And Artifacts
## Failure Behavior
## Assumptions
## Open Decisions
## Next Skill
```

For multi-turn, high-risk, or handoff-heavy work, persist the contract in a user-provided path or a project-native workflow location. For small work, keep it inline.

## Completion Gate

Before handing off:

- No unresolved decision can silently change the user-visible result.
- Every material claim is marked as verified, inferred, assumed, or open.
- Success criteria are observable rather than subjective.
- Boundaries and rejected options survive the handoff.
- The next skill is the narrowest one that can finish the user's request.
