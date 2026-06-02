---
name: diagnose
description: "Use when work starts from a symptom or failure: bug, regression, flaky behavior, performance issue, production/live issue, stale or wrong data, wrong output, or unknown root cause."
---

# Diagnose

Find the root cause of a broken behavior, then apply the smallest fix that removes it. This skill owns bug diagnosis, incident-style troubleshooting, and problem fixes.

## Boundary

Use this skill when the work begins from evidence that something is wrong.

Do not use this skill for:

- Implementing a clear feature or approved task. Use `implement`.
- Collecting requirements or choosing a technical approach. Use `grill-plan`.
- Writing a PRD. Use `to-prd`.
- Broad architecture opportunity review without a concrete failure. Use `architecture-review`.

## Phase 0: Orient

- Identify the concrete project area, then read the nearest applicable `AGENTS.md` or equivalent local instructions and stack files.
- Batch independent orientation reads and searches when possible: instructions, stack files, nearby docs, tests, and relevant logs.
- Read nearby domain docs, ADRs, or `CONTEXT.md` if they exist.
- Name the user-visible symptom and the suspected runtime path, but do not treat the suspicion as fact.
- For live-status questions, current production evidence has priority over local code, old logs, memory, or earlier smoke tests.
- For data freshness symptoms, identify the table or artifact, writer job, schedule, upstream source, latest update timestamp, and consumer path before fixing code.

## Phase 1: Build The Feedback Loop

Create the fastest agent-runnable pass/fail signal that reaches the bug.

Try seams in this order:

1. Failing test at the real behavior seam.
2. CLI command or script with fixture input.
3. HTTP/RPC replay against a local or deployed service.
4. Browser automation for UI, console, and network symptoms.
5. Captured trace replay: payload, log, event stream, artifact, or data snapshot.
6. Throwaway harness around the smallest real module path.
7. Repeated loop for flaky bugs to raise reproduction rate.
8. Read-only production log/query check when the bug only exists in production.

Do not proceed to broad hypotheses without a loop. If no loop is possible, state what you tried and what artifact or access is needed.

For current production checks, inspect the current pod/job/artifact and a bounded recent time window first, then aggregate current error codes or stale records. Do not rely on a historical error class until the current window proves it is still present.

## Phase 2: Reproduce And Minimize

- Confirm the loop produces the same failure the user described.
- Run it more than once, or enough times to make a flaky failure debuggable.
- Minimize the input while preserving the failure.
- Capture the exact error, wrong output, timing, or state transition.
- Distinguish broken logic from stale, partial, unavailable, or mis-timestamped data. When "latest" data matters, use explicit update or ingestion ordering instead of arbitrary samples.

## Phase 3: Hypothesize

Write 3 to 5 ranked hypotheses before changing code.

Each hypothesis must predict an observation:

`If X is the cause, then Y will change when I test Z.`

Discard vague hypotheses that cannot be falsified. Share the ranking when the user may have domain context, but keep moving if the next probe is cheap.

## Phase 4: Instrument

- One probe per hypothesis.
- Prefer debugger, REPL, targeted query, or targeted log over broad logging.
- Tag temporary logs with a unique prefix like `[DEBUG-1234]`.
- For performance regressions, measure first: timing harness, profiler, query plan, or benchmark.
- If output is large, preserve the exact failing line plus useful head/tail context, then narrow the next probe instead of dumping everything.

## Phase 5: Fix And Lock

- Put the regression test at the seam that reproduces the real bug pattern.
- If the available seam is too shallow, document that architecture gap instead of writing a false-confidence test.
- Apply the smallest fix that makes the minimized loop pass.
- Do not add unrelated features, constraints, schema changes, or operational behavior while fixing the bug.
- Re-run the original, unminimized loop.
- For deployed systems, separately verify whether the fix is merely local, built, deployed, and visible in the live runtime.

## Phase 6: Cleanup And Report

Before declaring done:

- Original repro no longer fails.
- Regression test or equivalent verification passes.
- Temporary debug logs and harnesses are removed or clearly isolated.
- The final explanation states root cause, fix, verification, and residual risk.
- Include exact environment, time window, data cutoff, and current/live status when they affected the diagnosis.
- If the bug was hard to lock down because of coupling or missing seams, hand off to `architecture-review`.
- If repeated probes stop producing new observations, stop the loop and report the blocker with the evidence already gathered.
