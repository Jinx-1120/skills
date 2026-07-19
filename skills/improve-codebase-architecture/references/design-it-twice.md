# Design It Twice

Use this reference when a chosen module or cluster has more than one plausible interface. The purpose is to prevent the first reasonable idea from becoming the design by default.

## Frame The Design Space

Before proposing interfaces, state:

- The actual callers and their most important stories.
- The constraints every design must satisfy.
- Everything callers currently need to know.
- The dependency categories and likely seam choices.
- The behavior that should move behind the interface.
- A small illustrative call sketch that grounds the problem without implying a preferred answer.

## Produce Independent Alternatives

Create at least three materially different designs. Draft each one far enough to be usable before comparing them.

Useful constraints include:

1. **Minimum interface:** target one to three entry points and maximize leverage per entry point.
2. **Common caller:** make the dominant user story trivial while keeping exceptional behavior explicit.
3. **Flexible variation:** support the known variants without exposing implementation detail or speculative extension points.
4. **Port and adapter:** use when a remote-owned or truly external dependency creates a real seam.

Use subagents only when the user or applicable instructions explicitly request parallel agent work. In that mode, give each agent the same evidence and a different design constraint. Otherwise, generate the alternatives in one task while keeping the constraints independent.

## Required Shape For Each Design

1. Complete caller-facing interface: types, methods, parameters, invariants, ordering, errors, configuration, and material performance behavior.
2. Realistic usage example from a current caller.
3. Behavior and knowledge hidden in the implementation.
4. Dependency and adapter strategy.
5. Interface-level test examples and remaining runtime proof.
6. Tradeoffs: where depth, leverage, and locality improve, and where the design stays thin.

## Compare And Recommend

Present the alternatives sequentially, then compare them by:

- Depth at the interface.
- Caller simplicity and misuse resistance.
- Locality of future changes and bugs.
- Seam placement and adapter reality.
- Test surface and runtime verification burden.
- Migration cost and compatibility pressure.
- AI-navigability: how much context a future agent needs to use or change the module safely.

Recommend one design or a deliberate hybrid. Explain why it is deeper for the current callers; do not return an unranked menu.

