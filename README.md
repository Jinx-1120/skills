# Codex Skills

Open-source skills for Codex-style coding agents. This repository can be
installed with the [`skills`](https://skills.sh) CLI from GitHub.

Repository: [Jinx-1120/skills](https://github.com/Jinx-1120/skills)

## Skills

| Skill | Purpose |
| --- | --- |
| `architecture-review` | Review existing architecture, module boundaries, refactoring opportunities, and testability. |
| `diagnose` | Diagnose bugs, regressions, flaky behavior, production issues, and wrong outputs through a real feedback loop. |
| `grill-plan` | Converge ambiguous requirements, user goals, boundaries, rejected options, and success criteria. |
| `implement` | Implement already-defined tasks with a narrow edit set and focused verification. |
| `task-breakdown` | Split approved requirements, PRDs, or technical plans into sequenced implementation tasks. |
| `technical-plan` | Design technical plans from settled requirements, including architecture, contracts, safety, rollout, and tests. |
| `to-prd` | Turn approved requirements or technical plans into a precise PRD or implementation brief. |
| `visual-design-craft` | Raise visual quality and interaction craft for web, mobile, or desktop product interfaces. |

## Workflow

For simple tasks, use the narrowest matching skill directly. For multi-turn or high-risk engineering work, prefer this sequence:

```text
grill-plan -> technical-plan -> to-prd -> task-breakdown -> implement
```

These skills support inline use for simple requests and checkpoint artifacts for longer work. When context loss would be risky, upstream skills should write or return a requirements ledger, technical plan, PRD, or task breakdown that downstream skills can reread.

`visual-design-craft` is a UI craft skill rather than part of the engineering workflow chain. Use it when the task is to design, review, or polish a visible product interface.

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
