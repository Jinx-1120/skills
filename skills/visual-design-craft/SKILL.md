---
name: visual-design-craft
description: "Use when a web, mobile, or desktop product interface needs distinctive visual design, platform-aware interaction, responsive or adaptive layout, complete states, or screenshot-backed polish and verification."
---

# Visual Design Craft

Make the working product surface feel intentional, clear, and native to its context. Judge quality through the real workflow and rendered pixels, not styling vocabulary.

## Modes And Boundary

- `Build/redesign`: implement the requested visible surface and verify it.
- `Polish`: preserve product behavior while improving hierarchy, layout, states, and interaction craft.
- `Review`: inspect and report evidence-backed issues; do not edit unless the user asked for changes.

Do not use this skill for backend-only work, brand strategy, logo systems, illustration-only assets, unsettled product requirements, or plain implementation with no UI judgment. Route those to the relevant requirements, implementation, or asset skill.

## Platform Routing

Infer the surface from the request and project evidence:

- Web: read `references/web.md`.
- Mobile: read `references/mobile.md`.
- Desktop: read `references/desktop.md`.
- Cross-platform: read each relevant reference and preserve native expectations instead of forcing one shared layout.

For build, redesign, polish, or review work, also read `references/interaction-states.md`; read `references/polish-check.md` before final delivery.

Ask about platform only when it cannot be discovered and the answer changes the implementation stack or interaction model.

## Visual Acceptance Contract

Before editing, identify:

- Target user and primary task.
- Platform, viewport/window classes, input methods, and accessibility needs.
- Existing design system, components, tokens, icons, and product constraints.
- Routes, copy meaning, data contracts, and behaviors that must remain unchanged.
- Current rendered baseline when the app can run.
- Observable visual done criteria, including states and sizes.

Use real domain content and data shapes. Do not invent dashboard metrics, product features, or filler copy to make a mockup look complete.

## Craft Principles

- Design the usable surface first; do not substitute a marketing hero for an app, editor, dashboard, or tool.
- Build hierarchy with composition, typography, spacing, color, contrast, and alignment before adding containers or effects.
- Prefer platform and product conventions over generic AI aesthetics.
- Avoid nested cards, one-hue palettes, decorative gradient blobs, random glass, ornamental SVGs, oversized panel headings, and text that explains obvious controls.
- Use familiar controls and icons when they improve recognition; label unfamiliar icon-only actions.
- Keep dense operational surfaces scannable and expressive surfaces purposeful.
- Make keyboard, touch, focus, selection, resizing, safe areas, and text overflow part of the design rather than cleanup.

## Workflow

### 1. Inspect and capture the baseline

- Read project instructions and the smallest relevant UI/component/state files.
- Run or reuse the configured preview when possible.
- Capture representative screenshots before substantial changes when a baseline exists.
- Record current defects as user-visible effects: what task becomes confusing, slow, inaccessible, or visually unstable.

### 2. Choose one coherent direction

Name the intended character in domain terms, such as quiet operations console, native settings flow, focused research workstation, or editorial product page. Tie each major visual choice to the workflow; do not add ornamental features to signal creativity.

### 3. Build the surface

- Reuse local components, tokens, layout primitives, and icons.
- Stabilize fixed-format UI with explicit constraints, grids, aspect ratios, and min/max behavior.
- Make responsive or adaptive behavior explicit.
- Keep feedback local to the action when possible.
- Preserve realistic empty, long, missing, zero, stale, and permission-limited data.

### 4. Complete interaction states

Apply `references/interaction-states.md`. Cover only plausible states, including loading, empty, error, success, disabled, focus, hover/pressed, selected, overflow, permission, offline, and stale/partial data where relevant.

### 5. Render, compare, and iterate

- Run the narrowest code verification for the changed surface.
- Inspect screenshots at representative compact and large sizes.
- Compare against the baseline for hierarchy, alignment, text fit, affordance, state clarity, and platform fit.
- Use browser, simulator, preview, Storybook, or screenshot tests when available.
- Iterate on visible defects; do not stop after the first render merely because code checks pass.

If rendering is unavailable, state that verification is static-only and list the exact missing runtime checks.

## Delivery

Lead with the improved user workflow. Report:

- Platform and surface.
- Visual direction and material changes.
- States and responsive/adaptive behavior covered.
- Code verification and screenshot/runtime evidence.
- Remaining risk, especially untested sizes, input methods, or platform runtimes.
