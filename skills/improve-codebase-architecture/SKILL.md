---
name: improve-codebase-architecture
description: "Use when the user wants architecture improvement or refactoring opportunity discovery in an existing codebase, especially shallow modules that could become deeper modules, visual before/after candidates, or an HTML architecture report; not for validating architecture findings, diagnosing failures, designing a selected solution, writing PRDs, or implementing refactors."
---

# Improve Codebase Architecture

Find architecture improvement opportunities in existing code and present them as visual before/after candidates. This is a workshop skill for exploring how code could become deeper, easier to test, and easier for future agents to navigate. It does not decide whether a suspected architecture problem is a review finding, and it does not implement the refactor.

## Boundary

Use this skill when the user asks to:

- Find refactoring or architecture improvement opportunities.
- Identify shallow modules that could become deeper modules.
- Explain before/after architecture options visually.
- Produce an HTML architecture improvement report.
- Continue from an `architecture-review` candidate into a visual exploration of possible simplifications.

Do not use this skill for:

- Validating whether an architecture finding is real. Use `architecture-review`.
- Debugging a concrete broken behavior. Use `diagnose`.
- Converging ambiguous product requirements. Use `grill-plan`.
- Designing the selected technical solution in detail. Use `technical-plan`.
- Writing a PRD or third-party consultation brief. Use `to-prd`.
- Splitting approved work into tasks. Use `task-breakdown`.
- Editing code or implementing a refactor. Use `implement`.

## Input Modes

- Inline mode: if the prompt names a code area and asks for improvement opportunities, inspect the relevant code and proceed.
- Review-backed mode: if an `architecture-review` candidate is provided, treat it as input evidence and visualize improvement directions without re-litigating the finding unless new evidence contradicts it.
- Report mode: if the user asks for a visual or HTML report, create a self-contained report artifact and give the absolute path.
- High-uncertainty mode: if the target area, current user story, or desired report scope is unclear enough to change the exploration, ask one blocking question or route to `grill-plan`.

## Vocabulary

Use these terms consistently:

- `Module`: code with an interface and implementation.
- `Interface`: what callers must know, including types, invariants, ordering, config, and errors.
- `Implementation`: the code behind the interface.
- `Seam`: where behavior can change without editing all callers.
- `Adapter`: concrete implementation behind a seam.
- `Depth`: leverage behind a small interface.
- `Deep module`: a module whose interface is much smaller than the behavior it owns.
- `Shallow module`: a module whose interface is nearly as complex as its implementation.
- `Leverage`: many callers or behaviors benefit from one small interface.
- `Locality`: bugs and changes concentrate in one place.

Do not let vocabulary override local domain language. Use `CONTEXT.md`, docs, ADRs, and existing code names for business concepts when they exist.

## Improvement Stance

- Start from the current user story and code navigation friction, not from a generic refactoring template.
- Prefer deepening, deletion, and consolidation over adding new layers.
- Treat a seam as real only when there is more than one current adapter, caller shape, runtime variant, or test need that benefits from it.
- Do not call for a new abstraction merely because the current code is untidy.
- Do not turn an improvement opportunity into a review finding unless `architecture-review` has established the evidence and impact.
- Respect existing ADRs and approved tradeoffs. Surface an ADR conflict only when current friction is strong enough to justify reopening it.
- Do not automatically write `CONTEXT.md`, ADRs, or durable project documents. Offer that only after the user selects a candidate and the decision is durable.

## Phase 1: Orient

- Read the nearest applicable `AGENTS.md` or equivalent local instructions.
- Read `CONTEXT.md`, domain docs, and relevant ADRs if present.
- Identify the target user story, entry points, modules, callers, tests, and important runtime boundaries.
- Build a compact coverage note: files read fully, files sampled, docs or ADRs used, and areas not inspected.
- If the request came from `architecture-review`, preserve the candidate's evidence, recommendation strength, and coverage limits.

Use subagents only when the environment supports them and the scope is broad enough to justify an independent exploration pass. If subagents are unavailable, inspect the code directly and state the coverage limits.

## Phase 2: Find Improvement Candidates

Look for candidates where a visual before/after would help the user choose a direction:

- Shallow modules whose interfaces expose nearly the same complexity as their implementations.
- Call chains where understanding one concept requires bouncing across many small modules.
- Pass-through modules that add little depth and force callers to learn extra names.
- Leaky seams where callers know implementation details, provider quirks, or ordering rules.
- Pure functions extracted for unit tests while real bugs live in orchestration with weak locality.
- Bespoke helpers that bypass existing project utilities and spread similar behavior.
- One-adapter seams that exist for speculative variants rather than current value.
- Repeated rules or normalization paths that could move behind one deeper interface.

Apply these tests before keeping a candidate:

- Deletion test: if the module disappeared, would complexity concentrate or only move into callers?
- Interface test: would the proposed direction make the interface smaller than the behavior it owns?
- Locality test: would future bugs or rule changes land in one place?
- Adapter test: is there more than one real adapter, runtime variant, caller shape, or test need?
- Test surface test: can important behavior be tested through a public seam instead of internal wiring?
- Tradeoff test: does a small limitation or product tradeoff remove enough coordination to be worth discussing?

## Phase 3: Present Candidates

For quick explorations, return candidates inline. For visual/report requests, create an HTML report.

Each candidate must include:

- Title naming the deepening or consolidation.
- Files or modules involved.
- Current friction.
- Before shape: why the current module is shallow, leaky, or low-locality.
- After direction: what becomes deeper, deleted, or consolidated.
- Benefit in depth, leverage, locality, and test surface.
- Subtraction opportunity: wrappers, compatibility paths, duplicated rules, config surfaces, or speculative variants that may go away.
- ADR or approved-tradeoff conflict, if any.
- Coverage limits and evidence.
- Recommendation strength: `Strong`, `Worth exploring`, or `Speculative`.

Do not propose detailed interfaces, schemas, migrations, or target state machines in this skill. If the selected direction needs those decisions, hand off to `technical-plan`.

## HTML Report

When creating a report:

- Read `references/html-report.md` before writing the HTML.
- Write a single self-contained HTML file to the OS temp directory, such as `<tmpdir>/improve-codebase-architecture-<timestamp>.html`.
- Resolve the temp directory from `$TMPDIR`, falling back to `/tmp` on Unix-like systems or `%TEMP%` on Windows when applicable.
- Include coverage, candidate cards, before/after diagrams, and a top recommendation.
- Use Mermaid only when graph, sequence, or dependency structure is clearer than hand-built HTML or SVG.
- If using CDN assets such as Tailwind or Mermaid, state that the report needs network access for full styling or diagram rendering. If offline viewing matters, use inline CSS and simple SVG/HTML diagrams.
- Do not require opening a GUI app. Open the report only when the environment permits it; otherwise provide the absolute path.

## Phase 4: Selection And Handoff

After presenting candidates, ask which candidate the user wants to explore.

Route the selected next step narrowly:

- Use `grill-plan` if the product goal, scope, or tradeoff is still unsettled.
- Use `technical-plan` if the direction is chosen and module/API/state/test decisions are needed.
- Use `task-breakdown` if an approved plan already exists and needs sequencing.
- Use `implement` only when the selected refactor is already clear and approved.
- Use `architecture-review` if the user wants to challenge whether the candidate is a real architecture finding.
- Use `diagnose` if exploration reveals a concrete failing behavior that needs root-cause work.

When the user rejects a candidate for a durable reason that future agents should not rediscover, offer to record an ADR or project-native note. Do not write durable project records without approval.
