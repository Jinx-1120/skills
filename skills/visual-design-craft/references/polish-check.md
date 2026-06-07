# Polish Check

Use this reference before final delivery or when asked to review visual quality.

## High-Signal Issues

- Text overflows, overlaps, clips, or relies on tiny font sizes to fit.
- Buttons, badges, cards, or tabs change size unexpectedly when content or state changes.
- Visual hierarchy is created only by card borders, shadows, or gradients.
- The page reads as one hue family rather than a balanced product palette.
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

## Anti-Template Pass

Remove or revise:

- Decorative gradient blobs, bokeh, random glassmorphism, and ornamental SVG backgrounds.
- Fake metrics, fake dashboard widgets, and filler feature descriptions.
- Oversized headings inside compact panels or tool surfaces.
- Identical rounded cards repeated without hierarchy.
- UI text explaining how to use obvious controls instead of making the controls clear.

## Final Verification Questions

- Can the primary workflow be completed from the first visible screen?
- Does the interface still work at the smallest supported size?
- Do long labels, empty data, failed actions, and disabled controls look intentional?
- Does the design fit the platform rather than only looking good as a static screenshot?
- Did runtime or screenshot verification actually render the changed UI?
