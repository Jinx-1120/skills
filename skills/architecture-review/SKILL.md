---
name: architecture-review
description: "Use when existing code needs local, cross-boundary, plan-backed, or whole-project architecture review for structural drift, hidden ownership, duplicated rules, zombie paths, utility bypass, disproportionate complexity, testability, or operability; not for generating refactor options or implementing them."
---

# Architecture Review

## Goal And Boundary

Determine whether the current structure still fits real user, operator, and maintenance stories. Treat architecture as a set of falsifiable choices, not as a constraint that is correct merely because it already exists. Prefer evidence-backed subtraction and small accepted limitations over template architecture.

This is a review skill. It may validate or challenge a structural concern, but it does not design detailed target interfaces, schemas, migrations, or state machines and does not implement a refactor. Route concrete failures to `diagnose`, ambiguous product intent to `grill-plan`, interface or seam alternatives to `improve-codebase-architecture`, selected system design to `technical-plan`, and approved edits to `implement`.

## Scope And Evidence

Choose the smallest review scope that supports the claim: a local call chain, a cross-boundary path, conformance to an approved plan, or the whole project. Add authorization, persistence, idempotency, recovery, and operational analysis only where the story carries those risks.

Read the nearest applicable repository instructions, domain docs, ADRs, and plan or source artifacts before judging the structure; these establish intentional tradeoffs and constraints that code shape alone cannot reveal.

Build enough context for another reader to reproduce the judgment:

- Intent map: users, main stories, entry points, success and failure signals, non-goals, and accepted tradeoffs.
- Coverage map: packages, runtimes, callers, data/control flow, tests, docs, and what was read, sampled, inferred, or not inspected.
- Current evidence: deployed runtime or freshness proof for live, data, or operational claims.
- Evidence labels: verified fact, inference, assumption, and proof gap where the distinction changes the finding.

Review-only work leaves source artifacts and runtime content unchanged unless advancing an artifact is explicitly part of the request.

## Architecture Hypotheses

Owner placement, dependency direction, interface shape, adapter location, synchronization model, and compatibility paths are hypotheses about where complexity belongs. For a material hypothesis, identify:

- The user or maintenance benefit it is meant to provide.
- Evidence that it still provides that benefit.
- Counterevidence from recent changes, incidents, duplicated rules, boundary workarounds, test friction, or operational blind spots.
- A disposition: `not-material`, `retained`, `challenged`, `replace`, or `superseded`.

This prevents two opposite errors: protecting a bad original structure and proposing a refactor merely because a different style is fashionable.

## Review Lenses

Apply only lenses that can affect the current stories:

- `Ownership and locality`: one owner per fact, policy, and side effect; a change lands where that owner lives.
- `Main-flow clarity`: maintainers can follow the primary path without reconstructing pass-through layers or hidden state.
- `Depth and deletion`: interfaces hide meaningful complexity; deleting a layer removes concepts rather than scattering them into callers.
- `Duplication and utility leverage`: shared rules have one meaning and project or platform utilities are reused when they still fit.
- `Reality of seams`: production variation, a real protocol or ownership boundary, or a useful deterministic responsibility justifies the seam without relying on a test-only consumer.
- `Proportionality and operability`: owned state, branching, configuration, and coordination match current business complexity, and operators can see progress, freshness, stuck state, version, and final output.

For durable or external effects, also test the boundaries between cache and truth; acknowledgement, commit, delivery, and visible result; identity and idempotency; retry and reconciliation; and materially different failure classes.

## Finding Contract

A finding needs a current suffering story, concrete evidence, a named structural mechanism, and a simpler direction that removes, merges, narrows, or deliberately omits something. Existing use of a powerful library, an approved tradeoff, an active migration, or mere difference from a preferred style is not a finding by itself.

Rate recommendation strength as `Strong`, `Worth exploring`, or `Speculative`; a no-findings result is valid. For each finding, give the affected story and modules, evidence, structural mechanism, architecture disposition, simpler direction, tradeoff, and proof limit.

Lead the final result with the conclusion, then coverage, intent map, findings in impact order, and the narrowest next owner: deletion, deeper interface exploration, technical planning, diagnosis, or implementation.
