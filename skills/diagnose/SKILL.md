---
name: diagnose
description: "Use when concrete evidence shows a user-visible behavior is wrong and root-cause work is needed: bugs, regressions, flaky or slow behavior, failed jobs, stale or wrong data, provider mismatches, deployment mismatches, or live incidents."
---

# Diagnose

Explain every material deviation in the failed user story through the real project architecture, runtime, or data path. If the user also asked for a fix, apply the smallest architecture-aligned correction that resolves the causally related anomaly set, then verify both the original problem and the affected surface; a diagnosis-only request does not authorize implementation.

## Boundary

Use this skill when work begins from an observed wrong behavior.

Do not use it for:

- A clear feature or refactor with no failure to explain. Use `implement`.
- Unsettled product requirements. Use `grill-plan`.
- Settled requirements that still need target design. Use `technical-plan`.
- Broad architecture review without a concrete symptom. Use `architecture-review`.

## Evidence Contract

- Start from the failed user story: action or job, authoritative expected behavior, actual result, environment, time window, data cutoff, and impact.
- Maintain a bounded anomaly set containing every material mismatch observed in that story or discovered on its affected architecture path. Track each anomaly as unexplained, explained, resolved, or out of scope.
- Include newly discovered anomalies when they are causally related or fall inside the change's affected surface. Record independent unrelated problems separately instead of silently expanding the repair.
- Treat memory, code, logs, tests, dashboards, and screenshots as evidence with different freshness and scope.
- Prefer current live evidence for current-status claims. Local code, old logs, a green request, or a completed job do not prove the user-visible result is correct now.
- Distinguish `verified fact`, `inference`, `assumption`, and `unknown` whenever the distinction can change the conclusion.
- Keep every proposed cause falsifiable. Do not force several anomalies into one root cause when the evidence shows independent defects.

## Workflow

Scale the working notes to the incident. A narrow bug may need only a few lines; a multi-runtime, data, or live incident may need an anomaly table and explicit architecture map.

### 1. Establish the problem and anomaly set

- Read the nearest applicable instructions and stack files.
- Identify the concrete route, command, job, provider, table, artifact, or deployment involved.
- Confirm the expected behavior from the newest user correction and the relevant product, code, schema, test, data, or operational contract.
- Reproduce the original story with the highest-fidelity practical signal and capture all material deviations: wrong output, missing or stale data, errors, timing, state transitions, side effects, and inconsistent observability.
- Keep the set bounded to the failed story and its affected architecture surface; do not turn diagnosis into a repository-wide cleanup.

### 2. Map anomalies to the real architecture

- Trace the relevant end-to-end paths from input to user-visible output and compare expected with actual state at their boundaries.
- Identify the owning module or subsystem, source of truth, shared rules, callers, writers, readers, runtime version, and deployment or configuration for each anomaly.
- For data problems, identify source of truth, writer, schedule, latest successful update, storage, consumer, freshness rule, and stale-data behavior.
- For external or durable side effects, separate transport acknowledgement, internal acceptance, durable commit, worker delivery, user-visible output, and external success.
- Group anomalies as a shared cause, cascading symptoms, contributing conditions, or independent defects. A first incorrect boundary is a localization clue, not a stopping condition; continue until every in-scope anomaly has an evidence-backed explanation or an explicit proof gap.

### 3. Build a discriminating feedback loop

Choose the signal with the best combination of fidelity to the original problem, ability to distinguish competing causes, and execution cost. Candidate loops, without a fixed priority order, include:

- Focused test at an existing production interface or independently meaningful deterministic boundary with realistic input.
- CLI or script replay with representative input.
- HTTP/RPC replay against the relevant runtime.
- Browser reproduction with console and network evidence.
- Captured trace, artifact, or data-snapshot replay.
- Bounded read-only production query or log check.

- Before each probe, state which anomalies or competing causes it distinguishes and what each possible result would mean.
- After each probe, update the anomaly statuses and causal model; do not keep accumulating evidence that changes no decision.
- Start with the smallest useful hypothesis set. One strong hypothesis plus a disconfirming alternative is enough for a narrow bug; use a ranked 3-5 only when the evidence is genuinely ambiguous or the risk is high.
- Express each material hypothesis as:

`If X is the cause, probe Z should produce Y.`

- Include plausible non-code causes: stale data, missing migration, wrong config, wrong runtime version, failed deploy, permission denial, provider lag, partial backfill, clock/order mistakes, or zombie compatibility paths.
- Capture the exact wrong output, error, timing, or state transition.
- Reduce the input while preserving the failure.
- Prefer targeted queries, debuggers, or logs over broad instrumentation.
- If no real loop is possible, name the missing evidence or access and continue with bounded static analysis; do not claim that a shallow substitute reproduced the bug. For database, provider, or query failures, a mock-backed test does not reproduce dependency behavior: use captured input only to guard deterministic parsing or policy, and keep a real-path probe in the acceptance evidence.

### 4. Fix the problem at its architectural owner

When the request includes fixing or restoring behavior:

- Before editing, ensure the anomaly set and affected surface are sufficiently understood, the causal model explains every in-scope anomaly or names its proof gap, the strongest alternatives have been tested proportionately, and the owning module or operational control is identified.
- Choose the smallest coherent correction at the owner of the violated rule, fact, state, or side effect. Minimize project-owned concepts and blast radius, not merely changed lines.
- Resolve a shared cause once for every in-scope entry point instead of patching each symptom. If the anomalies have independent causes, apply the smallest coherent set of separate corrections rather than inventing one root cause.
- Put a regression guard at an existing production interface or an independently meaningful deterministic boundary that reproduces the real pattern.
- Do not add a client or provider interface, injectable dependency, registry, or pass-through parameter solely for that regression guard.
- Do not add unrelated features, abstractions, or compatibility paths.

If the safe fix requires new product, ownership, schema, rollout, or migration decisions, stop that slice and route it to `grill-plan` or `technical-plan`.

### 5. Verify resolution, then verify safety

Run two distinct passes:

1. `Resolution verification`
   - Re-run the minimized reproducer and the original unminimized story.
   - Re-check every in-scope anomaly, including user-visible output, data freshness and completeness, state transitions, durable side effects, and read-back.
   - Reopen diagnosis when a causally related anomaly remains; do not mark the task fixed because only the headline symptom disappeared.
2. `Affected-surface verification`
   - Derive the impact surface from the changed architectural owner, shared rules, callers, writers, readers, entry points, and deployment path.
   - Exercise relevant adjacent contracts, edge and failure paths, focused and broader tests, build or type checks, runtime integration, and live read-back in proportion to risk.
   - Look explicitly for newly introduced anomalies. Keep this pass bounded by the real change impact rather than testing the entire repository by default.
   - Return to architecture mapping and repair when a new related anomaly appears; record an unrelated problem separately instead of hiding it or silently expanding scope.

Verify local, built, deployed, migrated, backfilled, and live-visible states separately when relevant. Remove temporary probes before delivery unless they are intentionally retained as diagnostics.

## Completion

For diagnosis-only work, report:

- The anomaly set and the status of every in-scope anomaly.
- The causal model: shared causes, cascading symptoms, contributing conditions, and independent defects, with confidence.
- The architectural owners and evidence distinguishing the model from the strongest alternatives.
- Exact affected environment, time window, and freshness cutoff when relevant.
- Smallest safe next action and remaining proof gap.

For authorized fixes, also report:

- What changed.
- Why the change is the smallest ownership-correct repair and which anomalies and entry points it covers.
- Resolution verification for the original story and every in-scope anomaly.
- Affected-surface verification and the evidence that no new problem was found.
- Artifact/read-back verification.
- Current runtime or deployment verification, or the explicit reason it remains unverified.

Do not call the problem fixed while an in-scope anomaly is unresolved, resolution verification has not replayed the original story, or affected-surface verification is missing. Report partial repair, mitigation, or the exact proof gap instead. Never collapse local correctness, artifact existence, runtime behavior, and live success into one claim.
