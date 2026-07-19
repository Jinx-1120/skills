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

- Define a port at the seam only when production transport and a justified alternate adapter create real variation.
- Keep domain behavior in the deep module; inject an HTTP, RPC, queue, or in-memory adapter for transport.
- Test rules and orchestration through the module interface, then verify the real transport contract separately.

### 4. Truly external

A third-party provider that the project does not control.

- Inject the provider capability behind a narrow port.
- Use a test adapter to verify the module's decisions, serialization expectations, and failure handling.
- Treat the adapter test as code-level evidence only. Use sandbox, integration, read-back, staging, or live checks to prove the real provider behavior.

## Seam Discipline

- One production adapter alone usually does not justify a project-owned port.
- Production plus a meaningful local, test, or alternate adapter can make the seam real.
- Internal seams may serve the module's own implementation and tests without becoming caller-facing interface.
- Put policy and domain behavior inside the deep module; keep adapters focused on transport and normalization.
- Do not let a provider adapter become the owner of domain state, authorization, scheduling, or persistence.

## Replace, Do Not Layer Tests

- Add tests at the deepened module's interface before deleting old coverage.
- Assert observable outcomes, errors, and side-effect commands rather than internal call order.
- Remove shallow-module tests when the new interface tests cover the same behavior and the old tests only freeze implementation.
- Preserve tests that still protect a distinct protocol, serialization, migration, or runtime contract.
- A test should survive internal refactoring. If every internal move rewrites it, the test is probably crossing the wrong seam.
- Keep interface-level code evidence separate from real dependency and deployment evidence.

