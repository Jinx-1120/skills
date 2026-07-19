---
name: architecture-review
description: "Use when existing code needs local, cross-boundary, plan-backed, or whole-project architecture review for structural drift, hidden ownership, duplicated rules, zombie paths, utility bypass, disproportionate complexity, testability, or operability; not for generating refactor options or implementing them."
---

# Architecture Review

Determine whether the current structure still fits real user stories and operating needs. Review from evidence and first principles; prefer subtraction and small tradeoffs over template architecture.

## Boundary

This is a review skill. Do not implement the refactor or design detailed target interfaces, schemas, migrations, or state machines.

Use another skill when the task is primarily:

- A concrete broken behavior: `diagnose`.
- Ambiguous requirements: `grill-plan`.
- Deep-module, interface, seam, or before/after design options: `improve-codebase-architecture`.
- A selected cross-system design involving durable state, schemas, migration, recovery, or rollout: `technical-plan`.
- An approved refactor ready to build: `implement`.

## Review Modes

Choose the smallest scope that supports the claim:

- `Local`: one module, feature, or call chain.
- `Cross-boundary`: several packages, runtimes, services, workers, or storage boundaries.
- `Plan-backed`: compare implementation with an approved technical contract.
- `Whole-project`: review the repository as a system and show coverage before claiming completeness.
- `High-risk overlay`: add fact, authorization, persistence, idempotency, and recovery checks only to data, security, external-integration, queue, worker, or durable-side-effect paths.

## Evidence And Coverage

- Read the nearest applicable instructions, domain docs, ADRs, and source artifact when present.
- Build an intent map: users, main stories, entry points, success signals, failure paths, non-goals, and accepted tradeoffs.
- Trace real callers and data/control flow before judging module shape.
- For whole-project work, inventory packages, runtimes, entry points, tests, and docs; mark what was read fully, sampled, inferred, or not inspected.
- For live, data, or operational claims, include current runtime or freshness evidence. Static code alone cannot prove deployed health or current data.
- Preserve the distinction between verified facts, inferences, assumptions, and proof gaps.

Do not update source artifacts during a review unless the user asked the review to advance that artifact or the project explicitly makes review status part of the requested workflow. Otherwise report the truthful pending transition.

## First-principles Tests

Apply only the tests that fit the user story:

- `Ownership`: Is one subsystem clearly responsible for each fact, policy, and side effect?
- `Main flow`: Can a maintainer follow the primary story without reconstructing many pass-through layers?
- `Locality`: Can a rule change or bug fix land in one place?
- `Depth`: Is the public interface substantially smaller than the behavior it owns?
- `Duplication`: Are rules, normalization, state transitions, or helpers implemented with competing meanings?
- `Utility leverage`: Is project code recreating an existing project or platform utility without a current reason?
- `Reality of seams`: Does an abstraction serve current adapters, callers, runtimes, or tests rather than speculative variants?
- `Deletion`: Would removing a layer eliminate concepts or merely push them into every caller?
- `Proportionality`: Is project-owned state, branching, configuration, and coordination justified by current business complexity?
- `Operability`: Can an operator determine freshness, progress, stuck state, deployed version, and completed output?

For high-risk paths, also check:

- Durable truth versus cache, process, UI, job, generated-file, or transport state.
- Ack, accept, commit, delivery, user-visible result, and external-success boundaries.
- Stable identity, idempotency, retry, reconciliation, and unknown-after-side-effect handling.
- Distinct malformed, missing, stale, denied, unsupported, retryable, dead-lettered, and unknown failures.

## Non-findings

Do not report a problem solely because the code:

- Uses a powerful library or standard engine behind a small local surface.
- Lacks enterprise audit, permission, configuration, or indirection that no current story needs.
- Contains an approved tradeoff, active migration, or credible near-term path.
- Differs from a preferred style without user or maintenance impact.
- Verifies side-effecting behavior with real integration/read-back checks instead of mock-heavy unit tests.

## Finding Gate

Keep a candidate only when it has:

- A current user, operator, or maintenance story that suffers.
- Concrete code, runtime, data, or navigation evidence.
- A named complexity mechanism such as hidden owner, duplicated rule, pass-through layer, zombie path, utility bypass, fact-boundary confusion, or speculative variant.
- A simpler direction that removes, merges, narrows, or accepts a small limitation.
- A clear proof limit, risk, and recommendation strength.

Use `Strong`, `Worth exploring`, or `Speculative`. Do not inflate severity to make a review look productive; a no-findings result is valid.

## Output

Lead with the conclusion, then provide:

1. `Coverage`: reviewed, sampled, and uninspected areas.
2. `Intent map`: the stories and constraints used for judgment.
3. `Findings`: ordered by user impact and evidence strength.
4. `Recommended next step`: direct deletion, deeper exploration, technical planning, diagnosis, or implementation.

For each finding, include only:

- User story and modules affected.
- Evidence and structural mechanism.
- Why the current complexity is disproportionate or risky.
- Simpler direction and subtraction opportunity.
- Tradeoff or ADR conflict.
- Coverage/proof limit and recommendation strength.
