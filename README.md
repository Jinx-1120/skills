# Codex Workflow Skills

Open-source workflow skills for Codex-style coding agents. This repository can
be installed with the [`skills`](https://skills.sh) CLI from GitHub.

Repository: [Jinx-1120/skills](https://github.com/Jinx-1120/skills)

## Skills

| Skill | Purpose |
| --- | --- |
| `architecture-review` | Review existing architecture, module boundaries, refactoring opportunities, and testability. |
| `diagnose` | Diagnose bugs, regressions, flaky behavior, production issues, and wrong outputs through a real feedback loop. |
| `grill-plan` | Converge ambiguous requirements, designs, or technical approaches before PRD or implementation work. |
| `implement` | Implement already-defined tasks with a narrow edit set and focused verification. |
| `to-prd` | Turn converged requirements or planning context into a precise PRD or implementation brief. |

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
