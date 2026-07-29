---
name: implement
description: "Use when a clear feature, refactor, test, workflow, UI, API, schema, documentation, or selected task is ready to build with a coherent edit set and outcome-focused verification."
---

# Implement

## Goal And Authority

Carry a clear task from current-system evidence through a coherent edit and proportionate verification. Optimize for the smallest change that fully owns the requested behavior, not the smallest diff that leaves duplicated rules or incomplete entry points.

A build or fix request authorizes ordinary in-scope local edits and non-destructive validation. It does not authorize a materially different feature, destructive migration, external publication, production mutation, or unrelated cleanup.

Use `diagnose` for an unexplained failure, `grill-plan` for material product ambiguity, `technical-plan` for unsettled ownership, state, migration, or rollout, and the architecture skills when interface shape or structural validity is the unresolved work.

## Change Context

Establish enough context to act without turning a small task into a planning ceremony:

- User-visible outcome, downstream consumers, observable done criteria, and behavior that must remain unchanged.
- Input, output, errors, source of truth, persistence, freshness, artifacts, and side effects that matter to this change.
- In-scope entry points and any accepted compatibility, migration, rollout, or non-goal constraints.
- Current worktree, applicable instructions, owning module, callers, tests, utilities, and project-native commands.

Resolve discoverable facts from the repository or runtime. Make reversible project-native assumptions when they preserve the result; ask only when a missing decision changes behavior, data, security, compatibility, cost, authority, or an irreversible effect. Preserve unrelated user changes.

When a supplied plan or status artifact is part of the workflow, keep its transitions evidence-backed. Code completion does not imply approved, migrated, deployed, backfilled, or live.

## Coherent Edit

Place the change at the owner of the rule, fact, state, or side effect and cover every entry point that shares the contract. Reuse existing project and platform capabilities where they fit. New abstraction is justified by current duplication, locality, caller leverage, or a real seam—not by hypothetical variation or test convenience.

Treat the selected architecture as a working hypothesis. Evidence that a change needs a second owner, copied rule, boundary bypass, cross-layer dependency, or non-removable compatibility path may invalidate it. Resolve a local contradiction when that remains inside the accepted task; otherwise surface the evidence and the smallest design decision needed instead of layering a workaround onto the old structure.

Keep unrelated cleanup and speculative future requirements outside the edit.

## Comment And Documentation Mode

When comments, TSDoc, Rustdoc, docstrings, or equivalent documentation are the requested deliverable, preserve behavior unless code change is also in scope. Match project conventions and explain purpose, ownership, invariants, tradeoffs, or surprising edge cases for an experienced engineer. Names and signatures should carry obvious meaning; comments should not narrate syntax. Verify that a documentation-only pass did not alter behavior.

## Verification Contract

Match evidence to the claim and keep levels distinct:

1. `Static`: diff, types, schemas, links, or generated structure.
2. `Code`: focused tests, typecheck, lint, build, or deterministic scripts.
3. `Artifact/read-back`: reopen or query the durable output and check completeness.
4. `Runtime`: exercise the real local or staging UI, CLI, API, worker, database, or provider path.
5. `Live`: confirm the intended deployed version and original production-visible outcome.

Use the narrowest ladder that proves the requested outcome at its real boundary. A passing mock, successful request, completed job, created artifact, or green deployment proves only what it directly observed.

Deterministic rules and stable protocol mappings can use focused tests, strict fixtures, or fakes. Production interfaces remain shaped by real callers and dependencies; a test double does not justify exported dependency plumbing and does not prove orchestration, storage, provider, deployment, or visible behavior. When the real path is unavailable, retain a repeatable check and report the exact proof gap.

At parsing and data boundaries, use realistic upstream shapes and cover malformed, missing, null, and blank values according to the public contract. Fail closed rather than inventing valid data such as a zero unless that meaning is explicitly defined.

## Completion

Finish when the requested behavior exists across every in-scope entry point, verification matches the original acceptance and risk, architecture counterevidence has been resolved or surfaced, unrelated changes remain intact, and temporary probes are removed or intentionally retained.

Report the outcome, material changes, why ownership is coherent, evidence by level, and residual risk. Keep local, artifact, runtime, migration, deployment, and live claims separate.
