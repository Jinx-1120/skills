# Mobile App UI Craft

Use this reference for iOS, Android, React Native, SwiftUI, Flutter, Kotlin/Compose, mobile web app shells, and mobile-first product screens.

## Fit

- Respect platform conventions before applying generic web design ideas.
- Design for touch, small screens, intermittent attention, one-handed use, and constrained text.
- Prefer clear navigation stacks, tabs, sheets, lists, and forms that match the platform.
- Do not force desktop dashboards or wide data grids into mobile layouts. Summarize, drill down, or use progressive disclosure.

## Layout

- Account for safe areas, status bars, home indicators, notches, keyboard overlays, and bottom navigation.
- Keep primary actions reachable. Avoid placing critical actions only in dense top-right toolbars.
- Use minimum practical touch targets, adequate spacing, and clear pressed states.
- Plan for dynamic type, localization, long names, zero data, and slow network states.
- Treat scroll as a first-class layout tool, but avoid hiding required actions below ambiguous endings.

## Interaction

- Use gestures only when they have visible affordances or platform precedent.
- Provide non-gesture alternatives for destructive or important actions.
- Make permission prompts, offline states, background refresh, retries, and partial sync visible when relevant.
- Keep destructive actions guarded by platform-appropriate confirmation or undo patterns.

## Visual System

- Follow native typography scale, elevation/material behavior, controls, and spacing where the framework provides them.
- Use imagery and illustration sparingly unless the app domain benefits from it.
- Avoid tiny text, low-contrast secondary text, and decorative detail that becomes noise on small screens.

## Verification

- Use simulator, preview, Storybook, screenshot tests, or the app run target when configured.
- Inspect at least one compact and one larger phone size when possible.
- Check keyboard overlap, safe-area clipping, dynamic text, tap target size, and long-content scroll behavior.
- If no mobile runtime is available, state that the pass is static and list the missing simulator or screenshot checks.
