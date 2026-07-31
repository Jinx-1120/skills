---
name: diagnose
description: "Use when concrete evidence shows a user-visible behavior is wrong and root-cause work is needed: bugs, regressions, flaky or slow behavior, failed jobs, stale or wrong data, provider mismatches, deployment mismatches, or live incidents."
---

# Diagnose

## Outcome And Boundary

Reconstruct the failed user story from trajectory evidence, derive the root cause step by step, report the reasoning, and propose a repair that prevents recurrence.

Treat requests, responses, traces, logs, events, state transitions, writes, reads, configuration, deployment state, and the relevant code path as trajectory evidence. Preserve the exact environment, version, time window, and data cutoff because evidence from another path or time cannot prove this failure.

A diagnosis request authorizes investigation and a repair proposal, not edits or operational changes. Implement the repair only when the user explicitly asks.

Use another skill when the work is primarily a clear feature (`implement`), unsettled product intent (`grill-plan`), target technical design (`technical-plan`), or broad architecture review without a concrete symptom (`architecture-review`).

## Reconstruct The Trajectory

- State the action, authoritative expected behavior, actual result, impact, and evidence boundary.
- Rebuild the ordered path from entry point to user-visible result. At each relevant hop, record the input, decision or transformation, output or durable state, responsible owner, and supporting evidence.
- Include every material deviation in the bounded story, not only the first visible error. Keep causally related deviations in the chain and record unrelated problems separately.
- Keep verified facts distinct from inferences, assumptions, and proof gaps. Prefer evidence captured from the failing path over nearby tests, dashboards, or successful status signals.
- If the real path cannot be observed or replayed, name the missing artifact or access and continue with bounded static analysis without presenting it as runtime proof.

## Derive The Root Cause

Reason through the trajectory one causal link at a time:

1. Identify the condition that immediately produced each deviation and cite the evidence for that link.
2. Ask what produced that condition, then repeat until reaching the responsible code, configuration, data, deployment, or ownership rule.
3. Test the chain counterfactually: if the proposed cause were removed or corrected, would the downstream deviations still occur?
4. Challenge the strongest alternative explanations with the smallest high-signal probe that would distinguish them.

Call something a root cause only when it is an ownership-level condition supported by the observed trajectory and correcting it breaks the causal chain without relying on downstream compensation. Do not rename a symptom, final error, or easiest edit as the root cause. If the evidence supports independent causes, report them separately instead of forcing one explanation.

## Report

Lead with the conclusion, then provide:

- The failed user story, impact, and evidence freshness boundary.
- The ordered trajectory and step-by-step causal chain from observed deviation to root cause.
- The root cause and its owner, confidence, decisive evidence, strongest rejected alternatives, and remaining proof gaps.
- A concrete repair proposal and how to verify it.

## Repair Proposal

Use a New Jersey-style constraint: solve the proven problem completely with the simplest mechanism that fits the existing architecture. Do not generalize for hypothetical cases.

- Fix the violated rule at its existing owner or source of truth, rather than masking a downstream symptom.
- Prefer a direct change, deletion, or reuse of an existing seam over a new abstraction, state machine, configuration layer, framework, or compatibility path.
- Make the smallest coherent change, not merely the fewest changed lines: cover every entry point affected by the proven cause while leaving unrelated cleanup outside scope.
- State the exact changes, deliberately untouched scope, tradeoffs, risks, and any decision that cannot be made from evidence.
- Verify by replaying the original trajectory and checking the changed owner's affected callers, writers, readers, and failure paths for new deviations. Do not use a mock or local success to claim a runtime, data, provider, or deployment failure is fixed.
