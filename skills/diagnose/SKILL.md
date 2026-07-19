---
name: diagnose
description: "Use when concrete evidence shows a user-visible behavior is wrong and root-cause work is needed: bugs, regressions, flaky or slow behavior, failed jobs, stale or wrong data, provider mismatches, deployment mismatches, or live incidents."
---

# Diagnose

Explain the actual failure through the real code, runtime, or data path. If the user also asked for a fix, apply the smallest safe correction and prove the original symptom changed; a diagnosis-only request does not authorize implementation.

## Boundary

Use this skill when work begins from an observed wrong behavior.

Do not use it for:

- A clear feature or refactor with no failure to explain. Use `implement`.
- Unsettled product requirements. Use `grill-plan`.
- Settled requirements that still need target design. Use `technical-plan`.
- Broad architecture review without a concrete symptom. Use `architecture-review`.

## Evidence Contract

- Start from the failed user story: action or job, expected result, actual result, environment, time window, data cutoff, and impact.
- Treat memory, code, logs, tests, dashboards, and screenshots as evidence with different freshness and scope.
- Prefer current live evidence for current-status claims. Local code, old logs, a green request, or a completed job do not prove the user-visible result is correct now.
- Distinguish `verified fact`, `inference`, `assumption`, and `unknown` whenever the distinction can change the conclusion.
- Keep every proposed cause falsifiable.

## Workflow

### 1. Orient and trace

- Read the nearest applicable instructions and stack files.
- Identify the concrete route, command, job, provider, table, artifact, or deployment that failed.
- Trace the shortest end-to-end path from input to user-visible output.
- For data problems, identify source of truth, writer, schedule, latest successful update, storage, consumer, freshness rule, and stale-data behavior.
- For external or durable side effects, separate transport acknowledgement, internal acceptance, durable commit, worker delivery, user-visible output, and external success.

### 2. Build a real feedback loop

Choose the cheapest signal that reaches the original failure:

1. Focused test at the behavior seam.
2. CLI or script replay with representative input.
3. HTTP/RPC replay against the relevant runtime.
4. Browser reproduction with console and network evidence.
5. Captured trace, artifact, or data-snapshot replay.
6. Bounded read-only production query or log check.

If no real loop is possible, name the missing evidence or access and continue with bounded static analysis; do not pretend a shallow substitute reproduced the bug.

### 3. Hypothesize adaptively

Start with the smallest useful hypothesis set. One strong hypothesis plus a disconfirming alternative is enough for a narrow bug; use a ranked 3-5 only when the evidence is genuinely ambiguous or the risk is high.

Express each material hypothesis as:

`If X is the cause, probe Z should produce Y.`

Include plausible non-code causes: stale data, missing migration, wrong config, wrong runtime version, failed deploy, permission denial, provider lag, partial backfill, clock/order mistakes, or zombie compatibility paths.

### 4. Probe and minimize

- Run one discriminating probe at a time.
- Capture the exact wrong output, error, timing, or state transition.
- Reduce the input while preserving the failure.
- Prefer targeted queries, debuggers, or logs over broad instrumentation.
- Remove temporary probes before delivery unless they are intentionally retained as diagnostics.

### 5. Fix only when authorized

When the request includes fixing or restoring behavior:

- Put a regression guard at the seam that reproduces the real pattern.
- Apply the smallest code, config, migration, data, provider, or deploy correction consistent with the root cause.
- Do not add unrelated features, abstractions, or compatibility paths.
- Re-run the minimized loop and the original unminimized symptom.
- Verify local, built, deployed, migrated, backfilled, and live-visible states separately when relevant.

If the safe fix requires new product, ownership, schema, rollout, or migration decisions, stop that slice and route it to `grill-plan` or `technical-plan`.

## Completion

For diagnosis-only work, report:

- Root cause and confidence.
- Evidence that distinguishes it from the strongest alternatives.
- Exact affected environment, time window, and freshness cutoff when relevant.
- Smallest safe next action and remaining proof gap.

For authorized fixes, also report:

- What changed.
- Regression or behavior-seam verification.
- Artifact/read-back verification.
- Current runtime or deployment verification, or the explicit reason it remains unverified.

Never collapse local correctness, artifact existence, and live success into one claim.
