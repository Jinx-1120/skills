---
name: grill-plan
description: Use before PRD or implementation when a project request, plan, design, or technical approach is ambiguous, underspecified, risky, or needs requirement and solution convergence.
---

# Grill Plan

Converge an unclear request into a buildable requirement and technical direction before PRD writing or implementation.

## Boundary

Use this skill before `to-prd` when the requirement or approach is not settled.

Do not use this skill for:

- Debugging a concrete failure. Use `diagnose`.
- Implementing an already clear task. Use `implement`.
- Writing the final PRD document. Use `to-prd`.
- Broad review of existing architecture without a target plan. Use `architecture-review`.

## Rules

- Ask one question at a time.
- Provide your recommended answer with each question.
- If the answer can be found by reading code, docs, schema, tests, or runtime evidence, inspect those instead of asking.
- Do not start implementation during grilling.
- Default to at most 5 high-leverage questions. Stop sooner once the remaining choices no longer block PRD or implementation.

## Phase 1: Ground The Question

- Identify the target project area or cross-boundary workflow.
- Read the nearest applicable `AGENTS.md` or equivalent local instructions and the smallest relevant docs/code needed to avoid asking questions the repo already answers.
- Restate the current goal, the uncertain decisions, and your recommended default.

## Phase 2: Decision Tree

Walk the plan through these branches:

1. Goal: what user-visible outcome must change?
2. Scope: what is explicitly out of scope?
3. Consumer: who or what uses the output?
4. Contract: what input/output/state/error shape must hold?
5. Data: what source of truth, freshness, and migration path apply?
6. Failure modes: what can go wrong and how should it surface?
7. Test seam: where can behavior be verified without testing internals?
8. Rollout: how will the change be released, observed, and reverted?
9. Alternatives: what simpler option was rejected, and why?

Skip branches that are irrelevant or already answered by repository evidence.

## Phase 3: Output

When the tree is resolved, summarize:

- Agreed decisions.
- Remaining open questions.
- Recommended technical direction.
- Implementation gates.
- Verification gates.

If the discussion reveals architecture debt, suggest `architecture-review`. If it resolves into a buildable requirement, hand off to `to-prd` when the user wants a document, or `implement` when the user wants direct execution.
