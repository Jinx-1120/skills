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

Create the fewest materially different designs needed to expose the real tradeoff. Two strong alternatives are often enough; add another only when it represents a distinct caller, ownership, or dependency choice. Draft every retained option far enough that a caller could use it and a maintainer could judge what moves behind it.

Useful perspectives include a minimum interface, the dominant caller story, known production variation, and a real protocol or ownership boundary. These are design lenses, not a required set.

When parallel delegation is available and authorized, independent designers may receive the same evidence with different design lenses. Keep the expected answer and the other alternatives hidden so agreement is evidence rather than coordination.

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

Recommend one design or a deliberate hybrid. Explain why it is deeper for current callers, what can be deleted, and which future change or failure pattern would invalidate the choice; do not return an unranked menu.
