# Interaction States

Use this reference during build, redesign, polish, or review work. Cover states that are plausible for the product surface; do not invent unrelated states.

## Required State Scan

- Initial/loading: skeletons, progress, optimistic UI, disabled controls, or deferred content.
- Empty: first-use empty, filtered-empty, permission-empty, and no-results variants when they differ.
- Error: validation errors, network failures, failed actions, retry, and user-correctable messages.
- Success: saved, sent, completed, copied, imported, synced, or submitted states.
- Disabled: unavailable controls should explain why when the reason is not obvious.
- Focus: keyboard-visible focus for links, inputs, menus, buttons, tabs, and custom controls.
- Hover/pressed: pointer feedback for clickable controls on platforms that support it.
- Selected/current: active nav, selected row, selected item, checked option, expanded panel.
- Overflow: long labels, long numbers, missing avatars, zero values, many tags, many rows, and narrow containers.
- Permission/offline/stale: blocked access, offline mode, stale data, partial sync, and expired sessions when relevant.

## State Quality Rules

- Keep state changes local when the user's action is local.
- Do not replace useful content with a spinner when partial content can remain visible.
- Pair destructive actions with confirmation, undo, or a clearly recoverable path.
- Make validation errors specific to the field or action.
- Keep state text short and action-oriented.
- Do not use placeholder educational copy to describe obvious UI behavior inside the product.

## Review Output

When reviewing, list missing states as concrete user-visible failures, not generic checklist items. Include the file, component, or screen where each state belongs.
