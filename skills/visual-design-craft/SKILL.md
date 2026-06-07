---
name: visual-design-craft
description: "Use to raise interface visual quality and interaction craft for web, mobile, or desktop UI work: distinctive product UI, platform-aware patterns, responsive/adaptive layouts, complete states, and screenshot-backed polish; not for backend-only work, brand strategy, illustration-only work, or already-settled implementation without UI judgment."
---

# Visual Design Craft

Make product interfaces feel intentionally designed, platform-aware, and polished. This is a craft skill, not a requirements workflow. It improves the visual and interaction quality of UI work across web, mobile, and desktop surfaces.

## Boundary

Use this skill when the user asks to:

- Build or redesign a visible product interface, screen, prototype, dashboard, app, or tool.
- Make UI feel more polished, refined, native, premium, distinctive, or similar to a high-craft design agent output.
- Review or improve visual hierarchy, layout density, interaction states, responsive/adaptive behavior, or platform fit.
- Turn an existing rough UI into a shippable interface without changing the product contract.

Do not use this skill for:

- Backend-only, data-only, CLI-only, API-only, or infrastructure work.
- Brand strategy, logo systems, illustration-only assets, or marketing copy strategy.
- Unsettled product requirements. Use `grill-plan` first.
- Technical architecture decisions. Use `technical-plan`.
- Plain implementation with no UI judgment. Use `implement`.
- Bug symptoms or broken runtime behavior. Use `diagnose`.

## Platform Routing

Before designing or editing, identify the target surface from the user's request, project files, or existing stack.

- Web UI: read `references/web.md`.
- Mobile app UI: read `references/mobile.md`.
- Desktop app UI: read `references/desktop.md`.
- Cross-platform UI: read each relevant platform reference, then preserve the native expectations of each target instead of forcing one shared layout.

For build, redesign, polish, or review work, also read:

- `references/interaction-states.md` for required state coverage.
- `references/polish-check.md` before final verification.

If the platform cannot be inferred and choosing incorrectly would change the implementation stack, ask one concise question before editing.

## Core Principles

- Respect the existing product, design system, component library, and platform conventions first.
- Design the actual working surface, not a marketing page, unless the user explicitly asked for marketing.
- Prefer dense, scannable, task-focused layouts for operational tools; use expressive composition only when the product domain supports it.
- Create a clear hierarchy through spacing, typography, color, contrast, and grouping rather than decorative wrappers.
- Avoid generic AI-looking UI: one-note palettes, oversized cards, decorative gradient blobs, random glass effects, fake dashboards, and filler feature text.
- Use real content, realistic data shapes, and domain-specific labels when available.
- Cover loading, empty, error, success, disabled, selected, hover/focus/pressed, overflow, and permission/offline states that a real user would hit.
- Keep text inside its container at desktop, mobile, and constrained widths. Do not rely on viewport-scaled font sizes to hide overflow.
- Use icons and familiar controls where they improve recognition. Avoid text-only rounded rectangles for common tool actions when an established symbol exists.
- Build or review with accessibility in mind: keyboard paths, focus visibility, readable contrast, semantic controls, and target sizes.

## Workflow

1. Orient:
   - Read the nearest project instructions and relevant UI files.
   - Identify platform, stack, design system, target users, primary workflow, and constraints.
   - Note what must remain unchanged: routes, API contracts, state shape, copy meaning, component ownership, and product scope.

2. Choose the visual direction:
   - Name the intended interface character in concrete terms, such as quiet operations console, native mobile settings flow, editorial product page, creative builder, or compact desktop utility.
   - Tie visual choices to the domain and workflow. Do not add ornamental features just to make the screen look busy.

3. Implement or review the surface:
   - Use local components, tokens, icons, and layout primitives when they exist.
   - Keep repeated items, modals, and framed tools as cards when appropriate; do not nest cards or turn every section into a floating card.
   - Stabilize fixed-format UI with explicit dimensions, aspect ratios, grid tracks, or min/max constraints.
   - Make responsive or adaptive behavior explicit for the target platform.

4. State pass:
   - Apply `references/interaction-states.md`.
   - Add or verify the user-visible states that are plausible for the workflow.
   - Prefer local feedback for local actions instead of global page resets.

5. Polish pass:
   - Apply `references/polish-check.md`.
   - Inspect spacing, alignment, color balance, text fit, control affordance, focus order, and edge cases.
   - Remove decorative noise that does not support comprehension or interaction.

6. Verify:
   - Run the narrowest project verification command that exercises the changed UI.
   - Render the interface when possible and inspect screenshots at relevant sizes.
   - For web, use browser-based verification when a local target is available.
   - For mobile or desktop, use the configured simulator, preview, Storybook, screenshot test, or app run target when available.
   - If runtime rendering is unavailable, state that verification was static-only and name the remaining risk.

## Output

When delivering, report:

- What platform and surface were handled.
- What changed in visual hierarchy, layout, interaction states, and platform fit.
- What verification ran, including screenshot or runtime checks when available.
- Any residual risk, especially if mobile/desktop simulator or screenshot verification was not available.
