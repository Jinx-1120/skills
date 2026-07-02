---
name: architecture-review
description: "Use when existing code needs local, cross-boundary, or whole-project architecture review for structural drift from user stories, module mismatch, zombie compatibility paths, utility bypass, duplicated rules, disproportionate complexity, technical-plan implementation drift, coupling, testability, or operability; not for designing a new target solution. When the review is based on a stateful source artifact, update only the review-owned status truthfully."
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

## Review Mode

Choose the lightest mode that matches the user's request and evidence:

- `Local Review`: one module, feature, or call chain. Keep claims local and do not imply whole-project coverage.
- `Cross-Boundary Review`: multiple packages, services, runtimes, workers, shared utilities, or deployment boundaries. Name each boundary before judging the design.
- `Whole-Project Review`: the user asks to review a project as a whole. Produce coverage evidence before findings.
- `Plan-Backed Review`: code was built from a technical plan. Check implementation drift against approved ownership, state, failure, recovery, and test contracts without relitigating approved tradeoffs.
- `No-Plan Review`: no approved plan is available. Infer the implicit design from user stories and code paths, then look for accidental owners, hidden policies, repeated concepts, and orphaned paths.
- `High-Risk Fact Review`: an overlay for data, authorization, external integration, worker, queue, or durable side-effect paths. Add fact-contract checks only for those paths.

## Stateful Source Artifacts

When a review is based on a technical plan, design doc, review checklist, task file, or other source document with an explicit status, progress marker, checklist gate, or frontmatter state such as `Status:`, `status:`, or `状态：`, treat that state as part of the review output.

- Record the starting state before judging code.
- Before the final response, update only the state the review actually owns: reviewed, needs revision, findings filed, no findings, blocked by missing evidence, or another project-native review state.
- Do not mark implementation, approval, rollout, migration, or production visibility complete from a review-only pass.
- If the source artifact is still a draft plan, update the review/progress note without pretending the plan was approved unless the user explicitly approves it.
- If the file is not writable or the status owner is unclear, state the exact pending status update instead of inventing a transition.

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

## Complexity Sources

Use these labels when they clarify a finding:

- `Zombie path`: dead compatibility, fallback, transitional, or old entry-point code.
- `Duplicated rule`: the same business rule, state transition, or normalization exists in multiple places.
- `Local optimum`: a module is reasonable alone but makes the whole project harder to understand or change.
- `Cross-boundary impedance`: two modules, packages, or runtimes expose mismatched concepts or contracts.
- `Utility bypass`: code recreates existing project utilities, shared packages, or platform helpers without a current reason.
- `Pass-through layer`: a layer mostly forwards calls, errors, or config without adding meaningful depth.
- `Speculative variant`: an abstraction exists for future variants that do not currently exist.
- `Hidden owner`: ownership of a fact, policy, side effect, or user-visible state is unclear.
- `Fact-boundary confusion`: durable truth, runtime state, transport acknowledgement, or external success is mixed together.
- `Config, audit, or permission overreach`: non-core control surfaces add more branching than the current user story needs.

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

## Non-Findings

Do not report something as an architecture problem solely because:

- It is approved future work with a credible path to use.
- It is an explicit design tradeoff already accepted by the project.
- It uses a mature library, standard engine, DSL, runtime, or external service behind a small local surface.
- It lacks enterprise audit, permission, validation, or configuration features that the current user stories do not need.
- It is a naming, formatting, or style preference without user-story impact or maintenance friction.
- It is temporarily unused but tied to an active migration, rollout, or documented follow-up.
- A side-effecting business function lacks mock-based unit tests, if its deterministic rules are covered at pure seams and its real behavior is intended for integration, staging, read-back, or live verification.

## Anti-Template Self-Check

Before recording a finding, verify it is not template pressure:

- Is this complaint grounded in a current user story, code path, or operator pain?
- Would the proposed direction remove concepts, states, branches, or files, or only rearrange them?
- Does the project have more than one real runtime variant, adapter, policy, or caller that justifies the abstraction?
- Is the complexity project-owned, or mostly delegated to a mature library with a small local surface?
- Would a small product or technical tradeoff remove much more complexity than polishing the current shape?
- Are you asking for auditability, permissions, validation, events, or configuration because the product needs them, or because they look architecturally proper?

## Finding Quality Gate

Before presenting a candidate, make sure it has:

- A current user story, operator scenario, or maintenance task that suffers.
- Concrete file, behavior, runtime, or data evidence.
- A clear complexity mechanism from the complexity-source labels above.
- A reason it is not a non-finding, approved tradeoff, or known future path.
- A simpler direction that removes, merges, narrows, or accepts a small limitation.
- A recommendation strength with confidence and risk.

Use recommendation strength consistently:

- `Strong`: user-story impact, code evidence, complexity mechanism, and simplification path are all clear.
- `Worth exploring`: evidence suggests real drift, but more caller, runtime, data, or product context is needed.
- `Speculative`: the concern is a design hunch. Keep it separate from primary findings and state what evidence would change it.

## Phase 1: Explore

- Choose the review mode before judging the design. Upgrade scope only when the evidence or user request requires it.
- Read the nearest applicable `AGENTS.md` or equivalent project instructions before judging structure.
- Build an intent map before judging code: real users, entry points, main path, failure paths, current non-goals, approved tradeoffs, and acceptance signals.
- Decide the initial evidence set, then batch independent reads/searches for callers, interfaces, tests, docs, and ADRs.
- For cross-boundary reviews, name the producer, consumer, shared package, runtime, and deployment boundaries before judging structure.
- For whole-project reviews, create a coverage map before judging completeness: packages, modules, runtimes, entry points, docs/tests inspected, files read fully, files sampled, areas not inspected, and confidence limits. Do not claim full coverage without this evidence.
- For local reviews, keep evidence and output scoped to the local path unless a real caller or shared contract forces a wider review.
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
- Testing-boundary test: are deterministic rules separated enough to test as pure functions, while database, Redis, queue, provider, storage, or other side-effecting business paths are verified through real-runtime checks instead of low-value mocks?

For data, authorization, external integration, worker, queue, or durable side-effect paths, also apply a fact-contract check:

- Owner test: is there one writer for each fact, policy, externally visible state, and side effect?
- Runtime-state test: is temporary process, cache, socket, job, UI, or transport state being treated as durable truth?
- Confirmation-boundary test: are transport acknowledgement, internal acceptance, durable commit, worker delivery, user-visible output, and external success kept distinct?
- Idempotency/recovery test: can retries, crashes, or uncertain external sends create duplicate effects or unrecoverable states?
- Adapter-boundary test: do external adapters normalize inputs and declare capabilities without owning domain state, authorization, scheduling, or persistence?
- Failure-semantics test: are malformed, missing, stale, denied, unsupported, retryable, dead-lettered, and unknown-after-side-effect cases distinguishable where the user story needs them?

When judging testability:

- Treat pure functions and deterministic builders as the primary code-level test seam. Missing tests for meaningful pure rules can be a finding when it increases regression risk.
- Do not require mock-heavy unit tests around business functions whose purpose is to query or mutate databases, Redis/cache, queues, storage, or external providers. Flag those tests when they freeze implementation details, duplicate the production query in mock form, or create false confidence without exercising the real boundary.
- If a side-effecting function is hard to verify because it also owns complex rules, review that as a design issue: extract the rule into a pure seam or narrow deterministic builder, then leave the side-effecting path thin.
- For production-facing side effects, look for integration, staging, smoke, read-back, log, or runbook evidence. If none exists, report the missing real-runtime verification rather than asking for more mocks.

## Phase 3: Present Candidates

Return results in this order when scope is cross-boundary or whole-project:

- `Coverage`: what was read fully, sampled, inferred, or not inspected.
- `Intent Map`: the main user stories, entry points, non-goals, approved tradeoffs, and success signals used for judgment.
- `Candidates`: the short finding list.
- `Suggested Next Step`: direct simplification, `technical-plan`, `implement`, `diagnose`, or `grill-plan`.

For local reviews, keep the same content but shorten sections that would add no value.

Each candidate must include:

- User story or business intent affected.
- Modules involved.
- Current friction.
- Structural mismatch: how the code shape diverges from the user story or current product intent.
- Complexity source: state, branches, duplicated rules, cross-module navigation, pass-through layers, compatibility paths, utility bypass, speculative variants, or fact-boundary confusion.
- Proportionality judgment: why the complexity is or is not justified.
- Why it is not a non-finding, approved tradeoff, or credible future path.
- Proposed direction in plain language.
- Simplification or tradeoff that makes the direction viable.
- Subtraction opportunity: code path, layer, compatibility branch, config surface, or runtime variant that may be removed.
- Benefit in locality, depth, and testability.
- Risks or ADR conflicts.
- Concrete file or behavior evidence that supports the finding.
- Coverage limits: important areas you did not inspect.
- If relevant, fact-contract evidence: unclear owner, mixed durable/runtime state, confused confirmation boundary, missing idempotency, adapter overreach, or collapsed failure semantics.
- Runtime or data-freshness evidence when the candidate depends on performance, production state, or scheduled data.
- Recommendation strength: `Strong`, `Worth exploring`, or `Speculative`, with the reason for that strength.

Do not propose interfaces, schemas, migrations, or target state machines in detail yet. If the selected candidate needs those decisions, hand it to `technical-plan`. End by asking which candidate or next step the user wants to pursue.

## Phase 4: Deepen Only After Selection

When the user selects a candidate:

- Walk constraints and callers.
- Define what lives behind the seam.
- Decide whether the next step is direct simplification, `technical-plan`, `implement`, `diagnose`, or `grill-plan`.
- Decide which tests should survive the refactor.
- Record durable domain terms or ADR decisions only when the user approves.
