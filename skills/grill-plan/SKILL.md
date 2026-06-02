---
name: grill-plan
description: "Use to discuss and converge ambiguous requirements before solution design: user goals, success criteria, scope, non-goals, rejected options, user corrections, entry points, and requirements-ledger checkpoints."
---

# Grill Plan

Converge an unclear request into a buildable requirements contract before technical planning, PRD writing, task breakdown, or implementation.

## Boundary

Use this skill when the requirement boundary is not settled.

Do not use this skill for:

- Debugging a concrete failure. Use `diagnose`.
- Designing the technical solution after requirements are clear. Use `technical-plan`.
- Splitting an approved plan into implementation tasks. Use `task-breakdown`.
- Implementing an already clear task. Use `implement`.
- Writing the final PRD document. Use `to-prd`.
- Broad review of existing architecture without a target plan. Use `architecture-review`.

## Input Modes

- Inline mode: if the current prompt or conversation is enough, reconstruct the minimal contract in the response and proceed.
- Artifact mode: if the user provides a ledger, PRD, plan, or notes path, read it first and treat it as the current source of truth.
- High-risk no-artifact mode: if missing history, compaction, or ambiguity would make the boundary unreliable, ask for the missing blocking decision or create a requirements ledger before continuing.

## Rules

- Ask one question at a time.
- Provide your recommended answer with each question.
- If the answer can be found by reading code, docs, schema, tests, or runtime evidence, inspect those instead of asking.
- Ask only questions that block PRD or implementation; convert non-blocking uncertainty into assumptions or out-of-scope notes.
- Do not start implementation during grilling.
- If the user explicitly asks to discuss first or says not to edit yet, keep the whole turn in plan mode until they approve implementation.
- Default to at most 5 high-leverage questions. Stop sooner once the remaining choices no longer block PRD or implementation.
- Do not produce a detailed architecture or implementation design. Capture technical constraints only as inputs for `technical-plan`.
- Keep durable rules abstract. Do not promote current examples, one-off entity names, or temporary market/runtime facts into evergreen docs unless the user asks.

## Phase 1: Ground The Question

- Identify the target project area or cross-boundary workflow.
- Read the nearest applicable `AGENTS.md` or equivalent local instructions and the smallest relevant docs/code needed to avoid asking questions the repo already answers.
- Batch the first evidence pass when multiple docs, schema, routes, or tests are likely relevant.
- When data, reports, or automation are involved, identify the source of truth, latest freshness signal, and required linked artifacts before asking about behavior.
- Restate the current goal, the uncertain decisions, and your recommended default.

## Phase 2: Decision Tree

Walk the requirement through these branches:

1. Goal: what user-visible outcome must change?
2. Scope: what is explicitly out of scope?
3. Consumer: who or what uses the output?
4. Contract: what input/output/state/error shape must hold?
5. Entry points: which UI, CLI, automation, worker, import, or API paths must honor the same contract?
6. Data: what source of truth, freshness cutoff, stale-data downgrade, and migration path apply?
7. Failure modes: what can go wrong and how should it surface?
8. Test seam: where can behavior be verified without testing internals?
9. Rollout: how will the change be released, observed, and reverted?
10. Alternatives: what simpler option was rejected, and why?

Skip branches that are irrelevant or already answered by repository evidence.

## Phase 3: Requirements Ledger

When the tree is resolved, output a requirements ledger. For multi-turn, high-risk, or cross-skill work, write or request a checkpoint artifact. Prefer a user-provided path; otherwise use a project-local path such as `.codex/workflows/<date>-<slug>/requirements-ledger.md` when writing is appropriate.

Use this structure:

```markdown
## Status

draft | user-approved | superseded

## Goal

## Success Criteria

## Accepted Decisions

## Boundaries And Non-goals

## Rejected Options

## User Corrections

## Entry Points And Consumers

## Data And Freshness

## Required Artifacts

## Open Questions

## Next Skill

technical-plan | to-prd | task-breakdown | implement
```

If unresolved technical choices remain, hand off to `technical-plan`. If only documentation is needed, hand off to `to-prd`. If the work is already small and clear, hand off to `implement`.
