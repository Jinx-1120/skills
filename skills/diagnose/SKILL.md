---
name: diagnose
description: "Use when a problem needs deep root-cause analysis from trajectory data and a simple, root-cause repair proposal."
---

# Diagnose

Deeply analyze the available trajectory data: logs, traces, requests and responses, state transitions, configuration, deployment facts, and the code path they exercise. Reconstruct what happened hop by hop, citing the observed value at each hop, and reason through the causal chain step by step until you reach the root cause. Keep verified observations distinct from inferences; do not present a mock, a nearby passing test, or a green status as evidence about the failing path.

Before naming the root cause, check it against the evidence:

- Counterfactual: if this condition were corrected, would the observed deviation disappear?
- Alternatives: name the other plausible explanations the trajectory suggests and say what evidence rules each one out, rather than ignoring them.
- Owner: the root cause is the rule, fact, state, or side effect that was violated, not the last error message or the easiest place to patch.

A diagnosis request authorizes investigation and a repair proposal. Do not edit code or change systems unless the user explicitly asks for the fix.

Report the conclusion first, then the trajectory and causal chain, the root cause with its owner and confidence, the rejected alternatives, and any remaining proof gaps.

Provide a repair proposal that fixes the root cause instead of masking its symptoms. Follow the New Jersey ("Worse Is Better") style for the repair: keep the implementation and interface simple, prefer a limited but basically correct solution over consistency, completeness, or generality that adds unnecessary complexity, and reuse an existing owner or helper before introducing anything new. Simplicity applies to the mechanism, not to coverage: the proposal must cover every call site that shares the proven cause, and it must say how the repair would be verified against the original trajectory.
