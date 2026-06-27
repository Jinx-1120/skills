---
name: architecture-review
description: "Use when reviewing existing code architecture for whole-project structural drift, agent-built module mismatch, zombie compatibility paths, utility bypass, disproportionate complexity, refactoring opportunities, module boundaries, coupling, testability, or operability; not for designing a target solution from accepted requirements."
---

# Architecture Review

Find where existing code structure has drifted away from real user stories and become harder to understand, test, operate, or change. Prefer subtraction and small tradeoffs over additive architecture. Do not implement during the review.

## Boundary

Use this skill for architecture review of existing code.

Do not use this skill for:

- Debugging or fixing a concrete failure. Use `diagnose`.
- Collecting requirements for a new feature. Use `grill-plan`.
- Designing a target technical solution from accepted requirements. Use `technical-plan`.
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
- `Structural drift`: code that was locally reasonable when written, but now conflicts with the product's current shape.
- `Zombie path`: compatibility, fallback, transitional, or unused code with no current user, migration, or approved future need.

## Review Stance

- Start from real user stories and current product intent, not from architecture templates.
- Judge complexity by proportionality: structure should be no heavier than the essential business complexity it serves.
- Treat complexity as cognitive friction in the current system: extra state, branches, ownership ambiguity, duplicated invariants, pass-through layers, or hard-to-explain flows.
- Do not call a design complex only because it uses a powerful library, DSL, or runtime. A library can reduce project complexity when the project-owned code stays smaller and clearer.
- Look for subtraction opportunities before additive architecture. A small product or technical tradeoff may be worthwhile when it removes a large amount of branching or coordination.
- Do not reward speculative extensibility. Interfaces, event flows, permission chains, config engines, or adapters need current value, real runtime variants, or clear maintenance payoff.
- Do not treat approved future work or explicit design tradeoffs as dead code. Do flag unneeded compatibility layers, stale transitional code, and abandoned paths when the project has no current compatibility obligation.
- Do not punish a project for lacking enterprise-style audit, permissions, configurability, or indirection unless the current user stories require those properties.
- Treat "simple" as lower project-owned branching and clearer main flow, not as avoiding mature libraries or standard engines.
- For high-risk flows only, review fact ownership, persistence, confirmation boundaries, idempotency, and recovery. Do not apply that heavier lens to every local module.

## Anti-Template Self-Check

Before recording a finding, verify it is not template pressure:

- Is this complaint grounded in a current user story, code path, or operator pain?
- Would the proposed direction remove concepts, states, branches, or files, or only rearrange them?
- Does the project have more than one real runtime variant, adapter, policy, or caller that justifies the abstraction?
- Is the complexity project-owned, or mostly delegated to a mature library with a small local surface?
- Would a small product or technical tradeoff remove much more complexity than polishing the current shape?
- Are you asking for auditability, permissions, validation, events, or configuration because the product needs them, or because they look architecturally proper?

## Phase 1: Explore

- Identify whether the review is local to one project area or crosses project/package/service boundaries.
- Read the nearest applicable `AGENTS.md` or equivalent project instructions before judging structure.
- Build an intent map before judging code: real users, entry points, main path, failure paths, current non-goals, and acceptance signals.
- Decide the initial evidence set, then batch independent reads/searches for callers, interfaces, tests, docs, and ADRs.
- For cross-boundary reviews, name the producer, consumer, shared package, runtime, and deployment boundaries before judging structure.
- For whole-project reviews, create a coverage map before judging completeness: packages, modules, runtimes, entry points, docs/tests inspected, files read fully, files sampled, areas not inspected, and confidence limits. Do not claim full coverage without this evidence.
- Read domain docs, ADRs, and `CONTEXT.md` if present.
- Trace real callers and data/control flow before judging structure.
- Compare implementation structure against the intent map. Look for local optima, cross-module impedance, duplicated responsibilities, and places where code shape no longer matches business intent.
- Identify existing project utilities, shared packages, or platform helpers, then check whether bespoke code bypasses them without a current reason.
- For data or production systems, trace producer job, storage table or artifact, consumer path, schedule, freshness signal, and observability surface.
- For work built from a technical plan, compare implementation to the approved plan's ownership, state, failure, recovery, and test contracts. Treat approved tradeoffs as constraints, not findings.
- For work without a technical plan, infer the implicit design from real user stories and code paths, then flag where the code accidentally created multiple owners, hidden policies, duplicated concepts, or orphaned paths.
- Note friction while exploring: bouncing across files, shallow pass-through modules, hidden coupling, hard-to-test behavior, duplicated invariants.

## Phase 2: Apply The Tests

For each suspected problem:

- Deletion test: if the module disappeared, would complexity vanish or reappear in callers?
- Interface test: is the interface smaller than the behavior it provides?
- Locality test: can a bug be fixed in one place?
- Seam test: is there more than one real adapter, or only a hypothetical abstraction?
- Testability test: can the behavior be tested through its public seam?
- Entry-point test: would every UI, API, worker, import, automation, or report path continue to honor the same contract?
- Operability test: can a future agent or operator tell whether data is fresh, a job is stuck, a deployed fix is live, or a report artifact is complete?
- User-story alignment test: does the structure make the main user stories easier to follow, or does it obscure them behind technical scaffolding?
- Proportionality test: is the architectural weight justified by current business complexity and current variants?
- Structural drift test: did independently built or heavily refactored modules become locally reasonable but globally mismatched?
- Subtraction test: what code, layer, compatibility path, or runtime variant could be removed by making one small acceptable tradeoff?
- Utility leverage test: is project-owned helper logic being reused, or are modules recreating it with extra branches and inconsistency?
- Global optimum test: is a proposed fix improving the underlying shape, or only patching symptoms inside a poor structure?
- Zombie path test: does this compatibility, fallback, old entry point, old field, unused adapter, or transitional branch have a current user, active migration, or approved future need?
- Duplication test: is the same business rule, state transition, normalization, or helper behavior implemented in multiple modules with slightly different meanings?
- Main-flow test: can a maintainer follow the primary user story in a mostly linear path, or must they reconstruct it from pass-through layers and callbacks?
- Small-tradeoff test: can a narrow accepted limitation remove enough coordination or branching to be worth considering?

For data, authorization, external integration, worker, queue, or durable side-effect paths, also apply a fact-contract check:

- Owner test: is there one writer for each fact, policy, externally visible state, and side effect?
- Runtime-state test: is temporary process, cache, socket, job, UI, or transport state being treated as durable truth?
- Confirmation-boundary test: are transport acknowledgement, internal acceptance, durable commit, worker delivery, user-visible output, and external success kept distinct?
- Idempotency/recovery test: can retries, crashes, or uncertain external sends create duplicate effects or unrecoverable states?
- Adapter-boundary test: do external adapters normalize inputs and declare capabilities without owning domain state, authorization, scheduling, or persistence?
- Failure-semantics test: are malformed, missing, stale, denied, unsupported, retryable, dead-lettered, and unknown-after-side-effect cases distinguishable where the user story needs them?

## Phase 3: Present Candidates

Return a short candidate list. Each candidate must include:

- User story or business intent affected.
- Modules involved.
- Current friction.
- Structural mismatch: how the code shape diverges from the user story or current product intent.
- Complexity source: state, branches, duplicated rules, cross-module navigation, pass-through layers, compatibility paths, utility bypass, speculative variants, or fact-boundary confusion.
- Proportionality judgment: why the complexity is or is not justified.
- Proposed direction in plain language.
- Simplification or tradeoff that makes the direction viable.
- Subtraction opportunity: code path, layer, compatibility branch, config surface, or runtime variant that may be removed.
- Benefit in locality, depth, and testability.
- Risks or ADR conflicts.
- Concrete file or behavior evidence that supports the finding.
- Coverage limits: important areas you did not inspect.
- If relevant, fact-contract evidence: unclear owner, mixed durable/runtime state, confused confirmation boundary, missing idempotency, adapter overreach, or collapsed failure semantics.
- Runtime or data-freshness evidence when the candidate depends on performance, production state, or scheduled data.
- Recommendation strength: `Strong`, `Worth exploring`, or `Speculative`.

Do not propose interfaces, schemas, migrations, or target state machines in detail yet. If the selected candidate needs those decisions, hand it to `technical-plan`. End by asking which candidate the user wants to explore.

## Phase 4: Deepen Only After Selection

When the user selects a candidate:

- Walk constraints and callers.
- Define what lives behind the seam.
- Decide whether the next step is direct simplification, `technical-plan`, or `implement`.
- Decide which tests should survive the refactor.
- Record durable domain terms or ADR decisions only when the user approves.
