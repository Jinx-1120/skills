# HTML Report Guidance

Use this reference when `$improve-codebase-architecture` needs to create a visual report. Keep the report useful as an artifact the user can reopen later, but do not let presentation replace evidence.

## Report Shape

Create a single HTML file in the OS temp directory. Include:

- Header: repository or area name, date, scope, and coverage summary.
- Legend: module, interface, seam, adapter, leakage, deep module, shallow module.
- Candidates: one visual card per improvement opportunity.
- Top recommendation: the candidate to explore first and why.
- Handoff: the next skill or decision needed after the user selects a candidate.

If the environment can safely open a GUI file viewer, open the report. Otherwise provide the absolute path.

## Candidate Card

Each candidate card should contain:

- Title: short and action-oriented, such as `Deepen Order intake`.
- Recommendation strength: `Strong`, `Worth exploring`, or `Speculative`.
- Files: monospaced list of the most relevant files.
- Before / After: side-by-side diagrams.
- Problem: one or two sentences naming the current friction.
- Direction: one or two sentences naming what gets deeper, deleted, or consolidated.
- Wins: short bullets in terms of depth, leverage, locality, and test surface.
- Evidence: concrete files, callers, tests, or docs used.
- Coverage limit: what was not inspected.
- ADR or tradeoff note when relevant.

## Diagram Patterns

Choose the diagram style that explains the candidate fastest:

- Mermaid flowchart: dependency graphs, call flow, worker flow, or before/after sequences.
- Boxes and arrows: when Mermaid layout hides the important shape.
- Cross-section: many thin pass-through layers becoming one deeper module.
- Mass diagram: interface surface area nearly matching implementation size.
- Call-graph collapse: scattered helper calls becoming internals of one module.

Do not make every card use the same diagram type. If prose has to explain the diagram at length, redraw the diagram.

## Styling

- Prefer readable, static HTML with restrained color.
- Use one accent color plus red for leakage and amber for warnings.
- Keep diagrams compact enough to compare before and after without excessive scrolling.
- Avoid decorative dashboard styling; this is an engineering artifact.
- If using Tailwind or Mermaid from CDNs, mention that full rendering needs network access. Use inline CSS when offline viewing matters.

## Language

Use the skill vocabulary consistently:

- module
- interface
- implementation
- depth
- deep
- shallow
- seam
- adapter
- leverage
- locality

Use project domain terms from `CONTEXT.md`, ADRs, docs, or code. Do not rename business concepts to match a generic architecture template.

## Minimal Scaffold

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Architecture improvement - {{area}}</title>
    <style>
      body { margin: 0; font-family: ui-sans-serif, system-ui, sans-serif; background: #f8fafc; color: #0f172a; }
      main { max-width: 1120px; margin: 0 auto; padding: 48px 24px; }
      article { background: #fff; border: 1px solid #e2e8f0; border-radius: 8px; padding: 24px; margin: 24px 0; }
      code { font-family: ui-monospace, SFMono-Regular, Menlo, monospace; }
      .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; }
      .diagram { min-height: 260px; border: 1px solid #e2e8f0; border-radius: 8px; padding: 16px; background: #f8fafc; }
      .strong { color: #047857; }
      .explore { color: #b45309; }
      .speculative { color: #475569; }
    </style>
  </head>
  <body>
    <main>
      <header>
        <h1>Architecture improvement - {{area}}</h1>
        <p>{{coverage summary}}</p>
      </header>
      <section id="candidates">
        {{candidate cards}}
      </section>
      <section id="top-recommendation">
        {{top recommendation}}
      </section>
    </main>
  </body>
</html>
```
