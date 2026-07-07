# Codex Skills

Open-source skills for Codex-style coding agents. This repository can be
installed with the [`skills`](https://skills.sh) CLI from GitHub.

Repository: [Jinx-1120/skills](https://github.com/Jinx-1120/skills)

## Skills

| Skill | Purpose |
| --- | --- |
| `architecture-review` | Review existing code architecture for user-story drift, module mismatch, zombie paths, utility bypass, duplicated rules, plan implementation drift, and disproportionate complexity. |
| `diagnose` | Diagnose concrete user-visible failures, stale/wrong data, runtime issues, and production incidents through the real path to a verified minimal fix or truthful downgrade. |
| `grill-plan` | Converge ambiguous requirements, user goals, boundaries, rejected options, and success criteria. |
| `improve-codebase-architecture` | Find and visualize architecture improvement opportunities, especially shallow modules that could become deeper modules, with before/after candidates. |
| `implement` | Implement already-defined tasks, requested code comments, doc comments, and docstrings with a narrow edit set and outcome verification. |
| `task-breakdown` | Split approved requirements, PRDs, or technical plans into sequenced implementation tasks. |
| `teach` | Teach a new skill or concept over multiple sessions in a stateful learning workspace. |
| `technical-plan` | Design technical plans from settled requirements, or restate design documents in plain user-story language before planning. |
| `to-prd` | Turn approved requirements or technical plans into a precise PRD, implementation brief, or third-party consultation brief. |
| `visual-design-craft` | Raise visual quality and interaction craft for web, mobile, or desktop product interfaces. |

## Workflow

For simple tasks, use the narrowest matching skill directly. For multi-turn or high-risk engineering work, prefer this sequence:

```text
grill-plan -> technical-plan -> to-prd -> task-breakdown -> implement
```

These skills support inline use for simple requests and checkpoint artifacts for longer work. When context loss would be risky, upstream skills should write or return a requirements ledger, technical plan, PRD, or task breakdown that downstream skills can reread. When a checkpoint or source artifact has an explicit status, downstream skills treat that status as part of the contract and update it truthfully before finishing.

`visual-design-craft` is a UI craft skill rather than part of the engineering workflow chain. Use it when the task is to design, review, or polish a visible product interface.

`improve-codebase-architecture` is an architecture improvement workshop skill rather than a review-finding validator. Use `architecture-review` to decide whether an architecture problem is real, then use `improve-codebase-architecture` when visual before/after candidates would help choose a refactoring direction.

`teach` is a productivity skill rather than part of the engineering workflow chain. Use it when the user wants to learn a new topic over multiple sessions in a workspace with a mission, resources, lessons, references, and learning records.

Each skill contains:

- `SKILL.md`: the skill instructions and frontmatter used by Codex.
- `agents/openai.yaml`: display metadata and the default prompt for agent UIs.

## Install

Install from GitHub with:

```sh
npx skills@latest add Jinx-1120/skills
```

List the skills in the repository before installing:

```sh
npx skills@latest add Jinx-1120/skills --list
```

Install one skill:

```sh
npx skills@latest add Jinx-1120/skills --skill diagnose
```

Install globally for Codex:

```sh
npx skills@latest add Jinx-1120/skills --global --agent codex
```

## License

MIT
