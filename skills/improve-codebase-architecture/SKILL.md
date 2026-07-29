---
name: improve-codebase-architecture
description: "Use when the user wants to scan existing code for deepening opportunities, design or improve a module's interface, choose where a seam or adapter belongs, compare alternative module shapes, make code more testable or AI-navigable, or produce a visual HTML architecture report; not for validating broad architecture findings or implementing the refactor."
---

# Improve Codebase Architecture

## Goal And Boundary

Design modules that return substantial capability through a small, coherent caller-facing interface. Optimize for caller leverage, maintenance locality, and a shape humans and agents can navigate without reconstructing hidden rules across many files.

Use the lightest relevant mode:

- `Discovery`: find and rank deepening, deletion, or consolidation opportunities.
- `Direct design`: improve a named module, interface, seam, or cluster.
- `Review-backed design`: continue from an `architecture-review` finding without re-proving settled evidence.
- `Report`: create a visual HTML survey or comparison when the artifact itself is requested.

This skill owns enough module-level evidence to rank discovery candidates, concrete interface alternatives, and a recommendation. Use `architecture-review` when the primary question is whether a broad or cross-system architecture concern is a valid finding. Product intent (`grill-plan`), concrete failures (`diagnose`), remaining system state and rollout (`technical-plan`), and production edits (`implement`) stay with their respective owners.

## Design Model

- **Module**: behavior with an interface and an implementation, from a function to a tier-spanning slice.
- **Interface**: everything a caller must know: entry points, types, invariants, ordering, errors, configuration, and material performance behavior.
- **Depth**: useful behavior hidden per unit of caller knowledge. Depth is not a line-count ratio.
- **Seam**: where behavior can vary without changing callers.
- **Adapter**: a concrete implementation at a seam justified by real variation or a protocol or ownership boundary.
- **Leverage and locality**: capability for callers and concentration of change, bugs, knowledge, and verification for maintainers.

A deep module may have many internal parts; callers should not need to learn them. If deleting a module makes complexity vanish, it was likely pass-through. If the same complexity reappears across callers, the module was providing depth.

Current and proposed module shapes are hypotheses. Their value depends on actual caller stories, change patterns, and dependency boundaries, not on architecture vocabulary or a preferred template.

## Evidence Context

Ground the design in the nearest instructions, domain language, ADRs, source, current callers, tests, dependencies, and runtime boundaries. Show what was read, sampled, inferred, or left uninspected.

For each candidate, identify:

- Caller burden today and the real story that suffers.
- Rules, side effects, configuration, or provider knowledge leaking through the interface.
- Repeated changes or bugs that would become local behind a better seam.
- What deletion, consolidation, or deepening removes rather than moves elsewhere.
- Evidence for and against the current structural hypothesis.

Churn and navigation friction are search signals, not findings on their own.

## Interface Design Contract

When dependencies matter, read [references/deepening.md](references/deepening.md) and classify them as in-process, local-substitutable, remote-but-owned, or truly external. That classification determines whether a seam stays internal, needs a port and adapter, or still requires real-runtime proof.

For a non-obvious or high-leverage choice, read [references/design-it-twice.md](references/design-it-twice.md) and compare enough materially different shapes to expose the actual tradeoff. Each serious option should make the following visible:

1. The complete interface a caller must learn and a realistic usage example.
2. Behavior and knowledge hidden behind the seam.
3. Dependency category and adapter strategy.
4. Deterministic test surface, stable protocol checks, and remaining integration or live proof.
5. Leverage, locality, migration cost, and explicit tradeoffs.

Recommend a design rather than returning an unranked menu. Explain why it is deeper for current callers, which old concepts or paths can disappear, and what future evidence would falsify the recommendation. A selected design that changes ownership or durable paths should carry cutover and old-path removal needs into `technical-plan`.

## Verification Boundary

Production ownership and interfaces come from real callers, protocols, and dependencies. Tests may exercise that justified interface or an independently useful deterministic responsibility; they do not create production variation by themselves.

Use strict fakes or fixtures only for stable serialization and protocol mapping, and state what they do not prove. Database, provider, service, deployment, and user-visible behavior retain explicit integration, read-back, staging, or live evidence requirements.

## Output And Completion

For discovery, lead with a short ranked candidate list containing evidence, caller burden, structural hypothesis, simpler direction, deletion opportunity, and recommendation strength.

For direct design, lead with the recommended interface, then show the meaningful alternatives, caller examples, hidden behavior, dependency strategy, test surface, migration or deletion needs, tradeoffs, and falsification signals.

For a requested visual artifact, read [references/html-report.md](references/html-report.md). Prefer concise inline design when presentation would not improve the decision.

The work is complete when the proposed interface hides more complexity than it introduces, the seam has a production or independently useful reason to exist, tests do not distort the production shape, the recommendation identifies what becomes local and removable, and cross-system decisions and proof gaps have a clear next owner.
