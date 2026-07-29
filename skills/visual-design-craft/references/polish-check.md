# Polish Check

Use this reference before final delivery or when asked to review visual quality.

## High-Signal Issues

- Text overflows, overlaps, clips, or relies on tiny font sizes to fit.
- Buttons, badges, cards, or tabs change size unexpectedly when content or state changes.
- Visual hierarchy depends on decoration because layout, typography, spacing, and alignment do not establish it.
- The palette does not distinguish hierarchy, state, or interaction clearly.
- Sections are framed as cards without a real interaction reason.
- Cards are nested inside cards.
- Marketing hero patterns appear in operational app surfaces.
- Icons are missing for common tool actions, or unfamiliar icon-only actions lack labels/tooltips.
- Hover/focus/pressed/selected/disabled states are missing or too subtle.
- Loading, empty, and error states have generic copy or break layout.
- Imagery is blurry, dark, cropped, stock-like, or unrelated to what the user needs to inspect.
- Spacing is inconsistent between similar groups, rows, controls, and panels.
- Dense areas lack alignment anchors, column rhythm, or predictable scan paths.
- Mobile layouts ignore safe areas, keyboard overlap, or tap target sizes.
- Desktop layouts ignore resizing, keyboard flow, menus, context actions, or pane behavior.

## Product-Specificity Pass

Reconsider any repeated visual habit that has no product or workflow reason: ornamental effects, identical containers, oversized headings, fake metrics or filler content, and explanatory copy standing in for a clear control. Keep a treatment when it supports hierarchy, state, affordance, platform fit, or deliberate brand character.

## Final Verification Questions

- Can the primary workflow be completed from the first visible screen?
- Does the interface still work at the smallest supported size?
- Do long labels, empty data, failed actions, and disabled controls look intentional?
- Does the design fit the platform rather than only looking good as a static screenshot?
- Did runtime or screenshot verification actually render the changed UI?
