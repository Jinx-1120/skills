---
name: diagnose
description: "Use when concrete evidence shows a user-visible behavior is wrong and root-cause work is needed: bugs, regressions, flaky or slow behavior, failed jobs, stale or wrong data, provider mismatches, deployment mismatches, or live incidents."
---

# Diagnose

## Goal And Authority

Explain every material deviation in the failed user story through the real code, runtime, deployment, or data path. Keep the investigation bounded, but do not stop at the first incorrect boundary while related anomalies remain unexplained.

A diagnosis-only request ends with findings and the safest next action. If the user also asked to fix or restore behavior, apply the smallest ownership-correct repair and prove both resolution and safety across the affected surface.

Use another skill when the work is primarily a clear feature (`implement`), unsettled product intent (`grill-plan`), target technical design (`technical-plan`), or broad architecture review without a concrete symptom (`architecture-review`).

## Incident Context

Anchor the work in a failed user story:

- Action, request, or job and its authoritative expected behavior.
- Actual result, environment, runtime version, time window, data cutoff, and impact.
- Entry points, source of truth, durable facts, side effects, and user-visible output involved.

Maintain a bounded anomaly set for every material mismatch in that story or its affected architecture path. Track each anomaly as `unexplained`, `explained`, `resolved`, or `out of scope`. Include newly found anomalies when they are causally related; record independent problems separately.

Evidence has scope and freshness. Code, tests, logs, dashboards, screenshots, artifacts, and live queries are not interchangeable. Current-status claims need current evidence, and verified facts remain distinct from inferences, assumptions, and proof gaps.

## Causal Model

Trace the relevant path from input to visible result and locate each anomaly against its real owners, callers, writers, readers, shared rules, configuration, and deployment state. For data or durable effects, distinguish acknowledgement, acceptance, durable commit, delivery, read-back, and external success.

Group anomalies as shared causes, cascading symptoms, contributing conditions, or independent defects. Treat existing seams, owners, and dependency directions as hypotheses: repeated workarounds, duplicated rules, boundary bugs, or incompatible writers may show that the current structure is part of the cause.

Keep material causes falsifiable. A useful probe distinguishes competing explanations or changes the next action. Choose it by fidelity to the original failure, discriminating power, risk, and cost; examples include focused interface tests, realistic replay, runtime requests, browser evidence, captured artifacts, and bounded live queries. Use the smallest hypothesis set the evidence supports rather than a fixed count.

Reduce inputs while preserving the failure and prefer targeted evidence over broad instrumentation. If the real path cannot be exercised, state the missing access or artifact and continue with bounded static analysis without upgrading that substitute into runtime proof.

## Repair Contract

When a fix is authorized:

- Correct the owner of the violated rule, fact, state, or side effect and cover every affected entry point.
- Resolve a shared cause once; use separate repairs when evidence shows independent causes.
- Place regression evidence at an existing production interface or a deterministic responsibility that remains meaningful without a fake.
- Keep production ownership and interfaces shaped by real callers and dependencies, not by a test double.
- Keep unrelated cleanup, speculative abstractions, and compatibility paths outside the repair.

A fake can prove deterministic policy or a stable protocol mapping; it cannot prove a database, provider, deployment, or user-visible path. Preserve an explicit, repeatable real-path check when that dependency is unavailable.

If the safe repair requires a new product decision, ownership model, schema, migration, or rollout contract, surface that decision and route the unresolved slice to `grill-plan` or `technical-plan` instead of hiding it inside a workaround.

## Completion Evidence

For diagnosis, report the anomaly set, causal relationships, architectural owners, confidence, evidence against the strongest alternatives, exact environment and freshness boundary, and remaining proof gaps.

For an authorized repair, add two distinct verification results:

1. `Resolution`: replay the minimized case and the original story; every in-scope anomaly is resolved or truthfully left as a proof gap.
2. `Affected surface`: derive adjacent checks from the changed owner, rules, callers, writers, readers, entry points, and deployment path; look for newly introduced anomalies in proportion to risk.

Keep local, built, artifact/read-back, runtime, migrated, deployed, and live evidence distinct. The problem is `fixed` only when the original story and all in-scope anomalies pass at the evidence level the claim requires; otherwise report partial repair, mitigation, or the exact blocker.
