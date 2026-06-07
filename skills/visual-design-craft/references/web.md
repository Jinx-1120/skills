# Web UI Craft

Use this reference for browser-rendered interfaces: React, Next.js, Vite, plain HTML/CSS, dashboards, admin tools, SaaS apps, product pages, and web prototypes.

## Fit

- Build the usable experience as the first screen. Do not create a landing page when the user asked for an app, game, editor, dashboard, or tool.
- If a landing page is explicitly requested, make the brand, product, place, or object a first-viewport signal and leave a hint of the next section visible.
- For operational web apps, favor restrained density, strong scanability, predictable navigation, and repeated-use ergonomics.
- For games, creative tools, or editorial product experiences, use richer motion, imagery, and composition when it supports the subject.

## Layout

- Use responsive constraints: grids, min/max widths, aspect ratios, fixed toolbar dimensions, and stable row heights where needed.
- Keep section structure unframed unless an item, modal, repeated row, or tool genuinely needs a card.
- Avoid cards inside cards.
- Do not rely on viewport-width font scaling. Use normal responsive type steps and container-aware wrapping.
- Ensure text, icons, badges, and dynamic values cannot resize or shift fixed-format UI unexpectedly.

## Visual System

- Reuse existing tokens, components, icon libraries, and patterns before adding custom styling.
- Avoid one-note palettes dominated by one hue family, especially purple-blue gradients, beige/tan systems, dark slate-only systems, and espresso/orange themes.
- Use color for hierarchy and state, not as a substitute for layout.
- Prefer real product imagery or generated bitmap assets when the page needs visual material. Avoid vague abstract SVG decoration for product-focused hero work.

## Controls

- Use familiar controls: icon buttons for common tools, segmented controls for modes, toggles for binary settings, sliders or inputs for numeric values, tabs for views, and menus for option sets.
- Provide tooltips for unfamiliar icon-only actions.
- Make hover, focus, active, disabled, selected, loading, and error states visible.
- Keep hit areas practical and avoid tiny controls in dense toolbars.

## Verification

- Start or reuse the local dev server when the app requires one.
- Inspect desktop and mobile viewport screenshots.
- Check text fit, overlap, responsive navigation, focus visibility, and meaningful states.
- For canvas, WebGL, video, or image-heavy UI, confirm the rendered pixels are not blank and assets are framed correctly.
