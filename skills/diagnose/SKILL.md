---
name: diagnose
description: "Use when concrete evidence shows a user-visible behavior is wrong and root-cause work is needed: bug, regression, flaky or slow behavior, production/live incident, failed job, stale/partial/wrong data, wrong output, provider/API mismatch, deployment/environment mismatch, or unknown cause. Trace the real runtime/data path to the smallest safe fix or truthful downgrade, verify the original symptom, and update any stateful source artifact truthfully."
---

# Diagnose

Find the real cause of a broken behavior, then apply the smallest safe fix that removes it or restores a truthful user-visible state. This skill owns bug diagnosis, incident-style troubleshooting, data freshness failures, live/runtime mismatches, and problem fixes.

## Boundary

Use this skill when the work begins from evidence that something is wrong.

Do not use this skill for:

- Implementing a clear feature or approved task. Use `implement`.
- Requirement discovery or boundary negotiation. Use `grill-plan`.
- Requirements are mostly settled but the target technical design still needs architecture, ownership, state, rollout, or test decisions. Use `technical-plan`.
- Writing a PRD. Use `to-prd`.
- Broad architecture review without a concrete failure, or deeper structural review after a root cause points to coupling, hidden ownership, zombie paths, utility bypass, or disproportionate complexity. Use `architecture-review`.

## Operating Stance

- Start from the user story that failed: who did what, what should have happened, what happened instead, where it happened, and when it happened.
- Treat logs, tests, code, dashboards, and memory as evidence, not as the user's problem statement. Current live evidence beats old logs, local code, previous smoke tests, and memory.
- Name the suspected path early, but keep every suspected cause falsifiable until tested.
- Prefer a small fix, data repair, migration, config correction, deploy correction, or truthful downgrade over adding new architecture during diagnosis.
- For ordinary local bugs, keep the loop light. For data-facing, external-system, worker, queue, multi-runtime, security-sensitive, or durable side-effect bugs, add a fact-boundary check only where it can prevent a wrong fix.

## Stateful Source Artifacts

When diagnosis starts from an incident note, failure report, runbook, technical plan, task file, or other source document with an explicit status, progress marker, checklist gate, or frontmatter state such as `Status:`, `status:`, or `状态：`, treat that state as part of the user-visible outcome.

- Record the starting state before probing.
- Before the final response, update the artifact to the truthful diagnosis outcome: fixed and verified, mitigated, local-only, needs deploy, needs migration, needs backfill, blocked, unreproduced, or another project-native state.
- Do not mark an issue resolved when the fix is only local, not deployed, not migrated, not backfilled, not visible in the live runtime, or not verified through the original symptom.
- If the diagnosis hands off to `technical-plan` or `architecture-review`, update the source artifact or its notes to show the concrete next state and evidence.
- If the file is not writable or the status owner is unclear, state the exact pending status update instead of inventing a transition.

## Phase 0: Orient

- Identify the concrete project area, then read the nearest applicable `AGENTS.md` or equivalent local instructions and stack files.
- Batch independent orientation reads and searches when possible: instructions, stack files, nearby docs, tests, and relevant logs.
- Read nearby domain docs, ADRs, or `CONTEXT.md` if they exist.
- Write a short symptom contract: user action or job, expected result, actual result, environment, time window, data cutoff, and visible impact.
- Name the suspected UI, API, CLI, worker, job, provider, database, artifact, or deployment path, but do not treat the suspicion as fact.
- For live-status questions, current production evidence has priority over local code, old logs, memory, or earlier smoke tests.
- For data freshness symptoms, identify the source of truth, table or artifact, writer job, schedule, upstream source, latest update timestamp, consumer path, stale-data behavior, and observability surface before fixing code.
- For multi-runtime or side-effect symptoms, identify the owner of the fact or side effect, the durable record, runtime projections, transport acknowledgements, user-visible outputs, and external provider success signals well enough to avoid mixing them up.

## Phase 1: Build The Feedback Loop

Create the fastest agent-runnable pass/fail signal that reaches the real bug, not a shallow substitute.

Try feedback loops in this order:

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

For user-visible runtime crashes, first reach the concrete route, screen, command, job, or report that failed. Do not merge different pages, jobs, providers, or stacks into one root cause until the current evidence proves they share one.

## Phase 2: Reproduce And Minimize

- Confirm the loop produces the same failure the user described.
- Run it more than once, or enough times to make a flaky failure debuggable.
- Minimize the input while preserving the failure.
- Capture the exact error, wrong output, timing, or state transition.
- Distinguish broken logic from stale, partial, unavailable, or mis-timestamped data. When "latest" data matters, use explicit update or ingestion ordering instead of arbitrary samples.
- For "success" states, read back the result the user needs: rendered page, returned payload, generated artifact, database row, report body, provider timestamp, or live deployment version. Do not treat HTTP success, job completion, schema presence, or a green status as proof that the user-visible output is correct.

## Phase 3: Hypothesize

Write 3 to 5 ranked hypotheses before changing code.

Each hypothesis must predict an observation:

`If X is the cause, then Y will change when I test Z.`

Discard vague hypotheses that cannot be falsified. Share the ranking when the user may have domain context, but keep moving if the next probe is cheap.

Include non-code causes when plausible: stale data, missing migration, wrong config, wrong runtime version, failed deploy, provider freshness, permission denial, time/order assumptions, partial backfill, or an old compatibility path. Do not call something architecture drift unless it is tied to the concrete failure.

## Phase 4: Instrument

- One probe per hypothesis.
- Prefer debugger, REPL, targeted query, or targeted log over broad logging.
- Tag temporary logs with a unique prefix like `[DEBUG-1234]`.
- For performance regressions, measure first: timing harness, profiler, query plan, or benchmark.
- If output is large, preserve the exact failing line plus useful head/tail context, then narrow the next probe instead of dumping everything.
- For data, external integration, worker, queue, or durable side-effect bugs, use targeted probes to distinguish:
  - Durable truth vs cache, process state, UI state, generated files, or transport observations.
  - Transport acknowledgement, internal acceptance, durable commit, worker delivery, user-visible result, and external provider success.
  - Malformed input, missing data, stale data, denied access, unsupported capability, retryable failure, dead letter, and unknown-after-side-effect.

## Phase 5: Fix And Lock

- Put the regression test or equivalent guard at the seam that reproduces the real bug pattern.
- If the available seam is too shallow, document that architecture gap instead of writing a false-confidence test.
- Apply the smallest fix that makes the minimized loop pass and matches the root cause. The fix may be code, config, migration, data repair, provider correction, deploy correction, or a truthful stale/partial-data downgrade.
- Do not add unrelated features, constraints, schema changes, abstractions, compatibility paths, or operational behavior while fixing the bug.
- If the correct fix requires target architecture, ownership, state, rollout, or migration decisions beyond the bug, stop and hand that slice to `technical-plan`.
- Re-run the original, unminimized loop.
- For deployed systems, separately verify whether the fix is merely local, built, deployed, and visible in the live runtime.
- For data and artifacts, separately verify freshness, completeness, consumer visibility, and any index, manifest, or report update that the user relies on.

## Phase 6: Cleanup And Report

Before declaring done:

- Original repro no longer fails.
- Regression test or equivalent verification passes.
- Temporary debug logs and harnesses are removed or clearly isolated.
- The final explanation states root cause, fix, verification, and residual risk.
- Include exact environment, time window, data cutoff, and current/live status when they affected the diagnosis.
- Any stateful source artifact status has been updated, or the skipped update and reason are stated.
- If the fix is local-only, not deployed, not migrated, not backfilled, or not visible in the live runtime, say that plainly.
- If the bug was hard to lock down because of coupling, hidden owners, duplicated rules, zombie paths, utility bypass, missing seams, or weak operability, hand off to `architecture-review` with the concrete evidence gathered during diagnosis.
- If repeated probes stop producing new observations, stop the loop and report the blocker with the evidence already gathered.

## Failure Modes To Avoid

- Do not continue an old implementation plan after the user provides a concrete runtime error; diagnose the current failure first.
- Do not mistake "the code has a schema/feature" for "the database, deploy, provider, or runtime is initialized and serving it."
- Do not mistake a successful request, completed job, or non-empty metadata for fresh, complete, user-usable output.
- Do not infer current production health from local behavior, old logs, or prior memory.
- Do not turn diagnosis into an architecture review unless the structural issue is needed to explain or safely fix the concrete failure.
