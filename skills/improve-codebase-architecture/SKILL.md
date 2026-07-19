---
name: improve-codebase-architecture
description: "Use when the user wants to scan existing code for deepening opportunities, design or improve a module's interface, choose where a seam or adapter belongs, compare alternative module shapes, make code more testable or AI-navigable, or produce a visual HTML architecture report; not for validating broad architecture findings or implementing the refactor."
---

# Improve Codebase Architecture

Design deep modules: substantial behavior behind a small interface, placed at a clean seam and testable through that same interface. Optimize for leverage for callers, locality for maintainers, and a code shape that humans and agents can navigate without reconstructing hidden rules across many files.

## Modes And Boundary

Use the lightest mode that matches the request:

- `Discovery`: scan an area or codebase for deepening, deletion, or consolidation opportunities.
- `Direct design`: design or improve the interface and seam of a named module or cluster.
- `Review-backed design`: continue from an `architecture-review` finding without re-proving it unless new evidence contradicts it.
- `Report`: create a visual HTML survey or interface-comparison artifact when the user asks for one.

Direct design does not require a prior architecture finding or candidate-selection ceremony. This skill owns concrete alternative interfaces, seam placement, adapter strategy, and the recommendation among them.

Do not use it to:

- Decide whether a broad architecture concern is a valid finding. Use `architecture-review`.
- Diagnose a concrete broken behavior. Use `diagnose`.
- Resolve unsettled product goals or tradeoffs. Use `grill-plan`.
- Design cross-system durable state, schemas, migrations, recovery, security, or rollout after the module shape is chosen. Use `technical-plan`.
- Edit production code. Use `implement` after the design is accepted.

## Shared Vocabulary

Use these terms consistently for design roles. Preserve literal code identifiers and the project's domain language; do not rename real concepts merely to fit the glossary.

- **Module**: anything with an interface and an implementation, from a function or class to a package or tier-spanning slice.
- **Interface**: everything callers must know to use the module correctly: types, invariants, ordering, errors, configuration, and relevant performance characteristics. It is broader than a language `interface` or method list.
- **Implementation**: behavior hidden inside the module.
- **Depth**: leverage at the interface. A module is deep when callers get substantial behavior from a small interface; it is shallow when callers must understand nearly as much complexity as the implementation contains.
- **Seam**: the place where behavior can vary without editing callers; the location of the module's interface.
- **Adapter**: a concrete implementation that satisfies an interface at a seam.
- **Leverage**: capability returned to callers per unit of interface they must learn.
- **Locality**: change, bugs, knowledge, and verification concentrate in one place instead of spreading across callers.

Use `module`, `interface`, and `seam` for architecture analysis instead of drifting into vague synonyms such as component, service, API, or boundary. Quote actual code names when they matter.

## Deep Versus Shallow

```text
Deep module                         Shallow module
┌─────────────────────┐             ┌───────────────────────────────┐
│   Small interface   │             │        Large interface        │
├─────────────────────┤             ├───────────────────────────────┤
│                     │             │ Thin pass-through implementation│
│ Deep implementation │             └───────────────────────────────┘
│                     │
└─────────────────────┘
```

Do not measure depth as implementation lines divided by interface lines; that rewards padding. Judge the behavior and complexity callers no longer need to own.

## Core Principles

- **Depth belongs to the interface.** A deep module may contain many small internal parts and internal seams; callers should not have to learn them.
- **Apply the deletion test.** If deleting a module makes complexity vanish, it was likely pass-through. If the complexity reappears across many callers, the module was providing depth.
- **The interface is the test surface.** Callers and tests should cross the same seam. Repeatedly testing past it is evidence that the module has the wrong shape or the interface omits observable behavior.
- **One adapter suggests a hypothetical seam; two adapters make variation real.** Do not add a port merely to look decoupled. Production plus a justified test or alternate adapter can make the seam real, but that test adapter does not prove the production dependency works.
- **Design it more than once.** The first plausible interface is rarely the best. Compare materially different shapes before converging when the decision has real design leverage.
- **Use domain language to name the module.** Architecture vocabulary explains the role; project vocabulary explains the business concept.

## Relationships

- Treat the complete surface a module presents to a caller role as one coherent interface.
- Measure depth against that interface, not against internal file or class count.
- Place the interface at a seam; let adapters satisfy it when real variation exists.
- Depth creates leverage for callers and locality for maintainers.

## Workflow

### 1. Ground the real caller problem

- Read the nearest applicable instructions, domain glossary, ADRs, and relevant source.
- Identify the user story, current callers, current interface facts, implementation cluster, tests, dependencies, and runtime boundaries.
- If no area was named, use recent change history and repeated navigation friction to prioritize likely hot spots; churn is a search signal, not proof of a problem.
- Record what was read fully, sampled, inferred, or left uninspected.

### 2. Assess the current shape

Ask:

- What must every caller know today: methods, parameters, ordering, errors, configuration, provider quirks, or performance constraints?
- Does understanding one behavior require bouncing across many shallow modules?
- Which rules or side effects leak through the current seam?
- Would deletion remove complexity or scatter it into callers?
- Do tests exercise observable behavior through the interface, or freeze internal wiring?
- Which change keeps recurring, and where would locality put it?

Keep a candidate only when deepening, consolidation, or deletion removes caller knowledge rather than moving it elsewhere.

### 3. Classify dependencies before placing the seam

When the module has I/O, cross-process, or external dependencies, read [references/deepening.md](references/deepening.md). Classify each dependency as in-process, local-substitutable, remote-but-owned, or truly external. Let that category determine whether the seam is internal, needs a port and adapters, or still requires real-runtime verification.

### 4. Design concrete alternatives

For a direct-design request or chosen candidate, concrete interface proposals are the work product, not a later handoff. When the shape is non-obvious or high-leverage, read [references/design-it-twice.md](references/design-it-twice.md).

Each proposed design must show:

1. The complete interface callers must learn, including invariants, ordering, errors, configuration, and material performance behavior.
2. A realistic usage example from an actual caller.
3. What behavior and knowledge move behind the seam.
4. Dependency category, port, and adapter strategy.
5. How tests use the same interface and what still needs integration or live proof.
6. Leverage, locality, AI-navigability, and explicit tradeoffs.

Compare alternatives before recommending one. Be opinionated: explain why the recommended interface is deeper, not merely different.

## Testability

- Accept dependencies at the appropriate internal seam instead of constructing them inside rules that need isolated testing.
- Return observable results from deterministic rules; isolate unavoidable side effects behind the module's owned orchestration.
- Prefer fewer entry points and simpler parameters when they preserve the real user stories.
- Replace shallow implementation-coupled tests only after interface-level tests cover the same meaningful behavior.
- Keep code-level adapter tests separate from integration, read-back, staging, or live evidence for the real dependency.

## Output

For discovery, present a short ranked candidate list with evidence, current caller burden, deepening direction, deletion opportunity, and recommendation strength. Lead with the top candidate.

For direct design, lead with the recommended interface, then compare the alternatives and show caller usage, hidden implementation, dependency strategy, test surface, and tradeoffs.

For an HTML artifact, read [references/html-report.md](references/html-report.md). Do not create a report when concise inline design is more useful.

## Completion And Handoff

Before finishing, verify that:

- The proposed module has one coherent caller-facing interface.
- The interface hides more complexity than it introduces.
- The seam corresponds to real variation or a justified dependency strategy.
- Tests can exercise meaningful behavior through the same interface callers use.
- The recommendation names what becomes more local and what can be deleted.
- Evidence limits and unresolved cross-system contracts are explicit.

Use `technical-plan` only for the broader state, schema, migration, recovery, security, observability, or rollout contract that remains after the module shape is selected. Use `implement` only after the user has asked to build the chosen design.
