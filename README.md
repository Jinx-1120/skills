# Agent Skills

Portable, evidence-first skills for tool-using coding agents. Each skill follows the open [Agent Skills specification](https://agentskills.io/specification) and keeps one canonical `SKILL.md` workflow that can be consumed by Codex, Claude Code, OpenClaw, Hermes, and other compatible clients.

## Design Target

The skills are designed for high-capability agents without depending on a particular model, tool namespace, invocation syntax, or installation root. They give the model room to investigate and reason, but make completion auditable through four shared rules:

1. **Outcome before procedure.** Define the user-visible result, boundaries, and observable done criteria; do not micro-script reasoning that the model can perform.
2. **Evidence before questions.** Resolve repository, runtime, data, and current external facts with tools. Ask only for consequential choices or missing authority.
3. **Adaptive depth.** Scale planning, hypotheses, artifacts, and verification to risk. The workflow stages are optional, not a mandatory pipeline.
4. **Truthful completion.** Keep static checks, code checks, artifact/read-back evidence, runtime evidence, and live/deployed evidence distinct.

This design reflects a practical operating preference: current evidence beats memory, exact dates and freshness matter, user corrections override earlier assumptions, and recommendations should end in an executable action or a precise blocker.

## Skills

| Skill | Use it when |
| --- | --- |
| `architecture-review` | Existing code needs evidence-backed review for structural drift, hidden ownership, duplicated rules, zombie paths, utility bypass, disproportionate complexity, testability, or operability. |
| `diagnose` | A concrete user-visible behavior is wrong and the real code, runtime, deployment, provider, or data path must explain it. Fix only when requested. |
| `grill-plan` | Goal, scope, success, or a consequential product choice is materially ambiguous and cannot be settled from evidence alone. |
| `improve-codebase-architecture` | The user wants to find deepening opportunities or directly design and compare module interfaces, seams, adapters, test surfaces, and simpler code shapes. |
| `implement` | A feature, refactor, test, UI, API, schema, workflow, or documentation task is clear enough to build and verify. |
| `task-breakdown` | Approved work is too large, risky, or dependency-heavy for one coherent implementation slice. |
| `teach` | The user wants multi-session learning through a mission, trusted sources, a real project, practice, feedback, and demonstrated progress. |
| `technical-plan` | Desired behavior is mostly settled but needs an end-to-end technical contract across ownership, state, data, failure, recovery, migration, rollout, and final boundaries, or an existing design needs plain user-story playback. |
| `to-prd` | Accepted requirements and approved technical decisions need a precise PRD, implementation brief, or consultation brief. |
| `visual-design-craft` | A web, mobile, or desktop product surface needs platform-aware visual design, complete states, and screenshot-backed iteration. |

## Routing, Not Ceremony

Choose the narrowest skill that owns the current uncertainty:

```text
material product ambiguity  -> grill-plan
concrete wrong behavior     -> diagnose
current architecture review -> architecture-review
module/interface/seam design -> improve-codebase-architecture
target technical decisions  -> technical-plan
decision-faithful artifact  -> to-prd
large approved sequencing   -> task-breakdown
clear implementation        -> implement
visible interface craft     -> visual-design-craft
stateful learning           -> teach
```

An end-to-end task may use several skills in one run. Do not stop for ceremonial approval between stages when the user already requested delivery, no material decision remains, and no new authority is required. Conversely, review-only, diagnosis-only, and planning-only requests do not authorize implementation.

## Evidence Levels

Skills use a common completion vocabulary:

- `Static`: source, diff, types, schema, links, or generated structure inspected.
- `Code`: tests, typecheck, lint, build, or deterministic scripts passed.
- `Artifact/read-back`: the saved row, file, report body, index, or external object was reopened and checked.
- `Runtime`: the real local or staging UI, CLI, API, worker, database, or provider path behaved correctly.
- `Live`: the intended deployed version and original production-visible result were confirmed.

A lower level never proves a higher one. A green request, completed job, created artifact, passing mock, or successful deployment does not by itself prove the user's final result.

## Repository Layout

Each independently installable skill lives under `skills/<name>/`:

- `SKILL.md`: the portable discovery metadata and canonical workflow.
- Optional `references/`, `scripts/`, and `assets/`: progressively loaded resources belonging to the portable skill.
- Optional `agents/openai.yaml`: a Codex UI adapter. Other clients ignore it, and it is not part of the skill's validity or behavior contract.

Do not duplicate a skill body for different clients. Client-specific metadata may improve presentation or installation, but the behavior must remain in the shared `SKILL.md` and relative resources.

## Client Compatibility

The portable core is the same for every client; only discovery roots and manual invocation differ:

| Client | Common discovery locations | Invocation |
| --- | --- | --- |
| Codex | `.agents/skills/<name>`, `$CODEX_HOME/skills/<name>`, or `~/.codex/skills/<name>` | Automatic matching or `$name` |
| Claude Code | `~/.claude/skills/<name>` or `.claude/skills/<name>` | Automatic matching or `/name` |
| OpenClaw | `<workspace>/skills/<name>`, `.agents/skills/<name>`, `~/.agents/skills/<name>`, or `~/.openclaw/skills/<name>` | Automatic matching; slash exposure follows OpenClaw configuration |
| Hermes | `.hermes/skills/<name>`, `~/.hermes/skills/<category>/<name>`, or a configured external skill directory | Natural matching or `/name` |

These paths are installation concerns, not instructions that belong inside a skill. Claude Code, OpenClaw, and Hermes read the standard `SKILL.md` directly; they do not need replicas of `agents/openai.yaml`.

## Validate

Use the specification's reference validator when available rather than maintaining a second, narrower schema:

```sh
for skill in skills/*; do
  [ -f "$skill/SKILL.md" ] && skills-ref validate "$skill"
done
```

Also run the skill's own scripts or tests, `git diff --check`, and a native discovery smoke test for every client whose compatibility is being claimed. Vendor validators are supplementary and apply only to that vendor's adapter.

## Install

The [`skills`](https://skills.sh) CLI can install from [Jinx-1120/skills](https://github.com/Jinx-1120/skills):

```sh
npx skills@latest add Jinx-1120/skills
```

List available skills:

```sh
npx skills@latest add Jinx-1120/skills --list
```

Install one skill:

```sh
npx skills@latest add Jinx-1120/skills --skill diagnose
```

Install the same skill globally for the four target clients:

```sh
npx skills@latest add Jinx-1120/skills \
  --global \
  --skill diagnose \
  --agent codex \
  --agent claude-code \
  --agent openclaw \
  --agent hermes-agent
```

You can also place or link an individual `skills/<name>` directory into any discovery root listed above. Prefer a client's native installer when it provides provenance, update, or security checks. Client commands evolve independently, so the portable package does not encode one client's private installer syntax.

## Credits

The deep-module vocabulary and design principles in `improve-codebase-architecture` are adapted from Matt Pocock's [`codebase-design`](https://github.com/mattpocock/skills/tree/e9fcdf95b402d360f90f1db8d776d5dd450f9234/skills/engineering/codebase-design) skill under the MIT License.

## License

MIT
