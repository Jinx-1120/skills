# Deepening Modules Safely

Use this reference after selecting a shallow cluster that has dependencies. The dependency category determines where the seam belongs, which adapters are justified, and what tests can prove.

## Dependency Categories

### 1. In-process

Pure computation or in-memory state with no I/O.

- Merge or reorganize freely when that creates a deeper interface.
- Test behavior directly through the new interface.
- Do not add an adapter merely for internal structure.

### 2. Local-substitutable

I/O with a faithful local implementation, such as an embedded database, local test server, or temporary filesystem.

- Keep the substitutable dependency behind an internal seam.
- Exercise the deep module through its external interface with the local implementation running.
- Do not expose the internal seam to callers just because tests use it.

### 3. Remote but owned

An internal service, queue, or API controlled by the same organization.

- Define a port only when current production variation requires it or when a protocol or ownership boundary creates an anti-corruption need independently of tests.
- Keep domain behavior in the deep module and transport normalization in the production HTTP, RPC, or queue adapter. Do not inject an in-memory transport solely to unit test orchestration.
- Test deterministic rules with representative inputs, then verify module orchestration and the real transport contract through a faithful local runtime, integration, staging, or read-back check.

### 4. Truly external

A third-party provider that the project does not control.

- Put third-party protocol details behind a narrow production adapter. Add a project-owned port only when a current ownership boundary or real provider variation gives it production value by reducing caller knowledge independently of a fake.
- Use a strict protocol fake or fixture only to verify serialization, response normalization, and error mapping. Reject unexpected interactions and state what the fake does not prove.
- Test domain decisions as deterministic rules. Use sandbox, integration, read-back, staging, or live checks to prove orchestration and real provider behavior.

## Seam Discipline

- One production adapter may justify an internal anti-corruption seam when a real protocol or ownership boundary exists; it does not automatically justify an exported project-owned port.
- A test adapter never creates production variation or justifies an exported interface, dependency parameter, registry, or pass-through layer.
- Keep internal seams owned by the module. Test them directly only when they isolate a deterministic responsibility that remains useful without a fake.
- Put policy and domain behavior inside the deep module; keep adapters focused on transport and normalization.
- Do not let a provider adapter become the owner of domain state, authorization, scheduling, or persistence.

## Replace, Do Not Layer Tests

- Add tests at the deepened module's interface before deleting old coverage.
- Assert observable outcomes, errors, and side-effect commands rather than internal call order.
- Remove shallow-module tests when the new interface tests cover the same behavior and the old tests only freeze implementation.
- Preserve tests that still protect a distinct protocol, serialization, migration, or runtime contract.
- Do not replace database, provider, query, or service orchestration with a fake router that branches on SQL, table, URL, or query text and returns handwritten business outcomes.
- A test should survive internal refactoring. If every internal move rewrites it, the test is probably crossing the wrong seam.
- Keep interface-level code evidence separate from real dependency and deployment evidence.
