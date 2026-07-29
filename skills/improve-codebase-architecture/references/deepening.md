# Deepening Modules With Dependencies

Use this reference after selecting a shallow cluster whose dependencies affect seam placement or verification.

## Dependency Categories

### In-process

Pure computation or in-memory state has no I/O boundary. Merge or reorganize it when that creates a deeper interface, test behavior directly, and keep adapters out of the design.

### Local-substitutable

A faithful local implementation exists, such as an embedded database, local server, or temporary filesystem. Keep the substitution behind the module and exercise the public interface with the local dependency running; callers do not need to see the internal seam.

### Remote but owned

The organization controls the service, queue, or API. A port is useful when current production variation, protocol stability, or ownership separation makes it a real anti-corruption boundary. Keep domain policy in the module and transport normalization in the adapter. Verify deterministic rules locally and the owned protocol through a faithful runtime, integration, staging, or read-back check.

### Truly external

A third party controls the dependency. Hide provider protocol details behind a narrow adapter. Add a project-owned port only when provider variation or an ownership boundary reduces real caller knowledge. Strict fixtures or fakes may prove serialization, normalization, and error mapping; sandbox, integration, read-back, staging, or live evidence proves orchestration and provider behavior.

## Seam And Evidence Contract

- A real protocol or ownership boundary may justify one internal adapter; it does not automatically justify a public port.
- A test double can exercise an already justified contract but cannot create production variation or justify caller-visible dependency plumbing.
- Deterministic policy belongs inside the deep module; adapters stay focused on transport and normalization rather than owning domain state, authorization, scheduling, or persistence.
- Interface-level tests protect observable outcomes. Preserve separate checks for distinct serialization, migration, dependency, deployment, and user-visible contracts.
- When a test must understand internal wiring or reproduce business outcomes inside a fake dependency, treat that as evidence that the seam or evidence level is wrong.

Deepening is complete only when caller knowledge shrinks, meaningful behavior remains covered, obsolete shallow paths can be removed, and claims about real dependencies retain matching real-path evidence.
