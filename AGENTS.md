# Repository Instructions

## Scope

These instructions apply to the whole repository.

## Working Principles

- Reason from the requested user outcome and first principles. Treat uncertain facts with skepticism and use tools to resolve them when possible.
- Prefer current repository, runtime, data, and official-source evidence over memory or assumptions.
- Separate verified facts, inferences, assumptions, and unresolved proof gaps when they can change a conclusion.
- Preserve unrelated user changes and avoid broad rewrites without evidence that they improve the skill system.
- Keep reusable skills model-agnostic and free of local paths, current incidents, entity names, dates, prices, or environment-specific facts.
- Do not spawn subagents unless the user or applicable instructions explicitly request delegation or parallel agent work.

## Portability Contract

- Treat `skills/<name>/SKILL.md` and its directly referenced resources as the portable skill. Follow the [Agent Skills](https://agentskills.io/specification) format rather than any one client's private conventions.
- Keep `name` and `description` as the required discovery metadata. Use optional standard frontmatter only when it carries real portable value; never reject a standard field merely because one client ignores it.
- Express workflows in capabilities such as inspect files, search text, edit safely, run commands, browse current sources, ask for a consequential choice, or delegate when available. Do not require a vendor-specific tool name, channel, invocation sigil, model, or filesystem root.
- Reference bundled files with paths relative to the skill root. Do not put `${CLAUDE_SKILL_DIR}`, `{baseDir}`, `${HERMES_SKILL_DIR}`, `$CODEX_HOME`, or equivalent client placeholders in the portable body.
- Keep one canonical workflow. Do not fork the skill body into Codex, Claude Code, OpenClaw, Hermes, or model-specific copies.
- Treat client extensions as optional adapters. In particular, `agents/openai.yaml` is Codex UI metadata: keep it when useful, but never require it for skill validity or let it constrain the portable `SKILL.md` contract.

## Editing Skills

- Read the available skill-authoring guidance before creating or substantially updating a skill, while treating client-specific packaging advice as optional adapter guidance.
- Treat `description` as the trigger contract: front-load when the skill applies and keep workflow details in the body.
- Keep each skill narrow. Route adjacent work explicitly rather than creating a mega-skill.
- Give a strong model outcomes, boundaries, evidence rules, and completion checks; avoid rigid micro-steps that add no safety or repeatability.
- Use progressive disclosure. Add references or scripts only when they reduce repeated context or make fragile work deterministic.
- When public trigger semantics or routing changes, synchronize `SKILL.md` with the relevant repository catalog text. Refresh a client adapter only when that adapter exists and the change makes it stale.
- Review-only work must not silently edit runtime content. Implementation requests should continue through proportionate verification while safe in-scope work remains.

## Validation

Before reporting a skill change complete:

1. Validate each changed skill against the Agent Skills specification, preferably with `skills-ref validate` when it is available.
2. Run any bundled script or deterministic check affected by the change.
3. Run client-specific validation only for adapters or runtime-compatibility claims in scope; a client validator must not redefine the portable core.
4. Run `git diff --check`.
5. Inspect the final diff for trigger drift, broken relative references, accidental machine-specific content, and vendor-specific assumptions in the portable body.
6. If claiming discovery in a particular client, verify that client's actual discovery or parser behavior rather than inferring it from repository layout.
