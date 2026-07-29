---
name: visual-design-craft
description: "Use when a web, mobile, or desktop product interface needs to be designed, redesigned, polished, or reviewed for distinctive visual quality, platform-aware interaction, responsive or adaptive layout, complete states, accessibility, or screenshot-backed evidence."
---

# Visual Design Craft

## Goal And Modes

Make a working product surface feel intentional, clear, and native to its platform. Judge quality through the real user workflow, interaction states, and rendered pixels rather than styling vocabulary.

- `Build/redesign`: implement a requested visible surface and verify it.
- `Polish`: preserve behavior while improving hierarchy, layout, states, and interaction craft.
- `Review`: report screenshot-backed issues; edit only when change is requested.

Backend-only work, brand systems, illustration-only assets, unresolved product intent, and plain implementation without UI judgment belong to their narrower skills.

## Problem Layer

Identify the layer that owns the observed problem:

- `Visual`: hierarchy, typography, spacing, color, alignment, imagery, or density.
- `Interaction`: affordance, feedback, input method, state transition, or platform convention.
- `Information architecture`: grouping, navigation, priority, or workflow sequence.
- `Product or technical architecture`: missing capability, wrong ownership, data contract, latency model, or system behavior.

Improve the layers inside the request. Do not use visual polish to conceal a broken workflow or system contract; surface the deeper owner and route unresolved product or technical decisions to the appropriate requirements, architecture, or implementation skill.

## Platform Context

Infer the surface from the request and project evidence, then read the relevant guide:

- Web: [references/web.md](references/web.md)
- Mobile: [references/mobile.md](references/mobile.md)
- Desktop: [references/desktop.md](references/desktop.md)

For every product-surface build, redesign, polish, or review, read [references/interaction-states.md](references/interaction-states.md) and apply the states the product can actually produce. Read [references/polish-check.md](references/polish-check.md) before final delivery. Cross-platform work preserves each platform's expectations rather than forcing one layout everywhere.

## Acceptance Context

Before editing, understand the target user and primary task, platform and size classes, input methods and accessibility needs, existing design system and components, product behavior and data contracts that must remain stable, current rendered baseline, and observable visual done criteria.

Use real domain content and realistic data shapes. Missing, long, empty, zero, stale, partial, error, and permission-limited states matter only where the product can actually produce them.

## Craft Contract

Choose one coherent visual direction grounded in the product's domain and repeated-use workflow. Let composition, typography, spacing, contrast, color, and alignment establish hierarchy. Containers, effects, imagery, and motion earn their place by clarifying grouping, state, affordance, or brand character.

Reuse project components, tokens, icons, and layout primitives when they fit. Preserve platform conventions, responsive or adaptive behavior, keyboard and touch interaction, safe areas, focus, selection, resizing, and text overflow in proportion to the surface.

The result should feel specific to this product without inventing features, metrics, or copy merely to make the screen look complete.

## Rendered Verification

Use the configured preview, browser, simulator, Storybook, screenshot target, or app runtime when available. Capture a baseline for meaningful redesigns, inspect representative compact and large sizes, and compare hierarchy, alignment, text fit, affordance, state clarity, and platform fit. Iterate on visible defects after code checks pass.

When rendering is unavailable, identify the work as static-only and name the exact runtime, size, input, or state checks still missing.

## Delivery

Lead with the improved user workflow. Report the platform and surface, visual direction, material changes, states and sizes covered, code and rendered evidence, deeper issues handed to another owner, and residual visual or runtime risk.
