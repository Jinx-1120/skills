# Desktop App UI Craft

Use this reference for Electron, Tauri, WebView wrappers, SwiftUI/AppKit, WinUI, WPF, Qt, native Linux UI, and cross-platform desktop apps.

## Fit

- Treat desktop apps as tools for repeated work, multitasking, resizable windows, keyboard control, and persistent state.
- Respect the host platform: macOS, Windows, and Linux differ in window chrome, menus, shortcuts, spacing, materials, tray behavior, and native controls.
- If the app is Electron, Tauri, or a WebView, preserve desktop expectations instead of shipping a website in a window.

## Layout

- Design for multiple window sizes: compact, default, large, and full-screen when relevant.
- Keep navigation predictable: sidebars, command palettes, menus, inspectors, panes, and status bars should serve real workflows.
- Avoid oversized hero sections and marketing composition inside an app window.
- Use density carefully. Desktop can carry more information, but alignment, grouping, and keyboard flow must stay clear.
- Make split panes, resizers, tables, toolbars, and inspectors stable under content changes.

## Interaction

- Support keyboard shortcuts, focus order, selection states, context menus, drag/drop, undo/redo, and copy/paste when the workflow expects them.
- Surface save/sync/run status without blocking the whole window unnecessarily.
- Keep destructive or irreversible actions confirmable and recoverable where possible.
- Design empty, loading, error, offline, stale, and permission states in the same layout as the normal workflow.

## Visual System

- Use native controls, materials, and platform typography when the framework supports them.
- Keep custom chrome restrained and functional.
- Iconography should match the platform and task. Avoid playful or decorative icons in serious productivity tools.
- Avoid web-card-heavy dashboards unless the app is explicitly an analytics product and cards represent real repeated objects.

## Verification

- Run the app, preview, Storybook, or screenshot target when available.
- Inspect at compact/default/large window sizes.
- Check menu/shortcut affordances, focus visibility, pane resizing, text overflow, disabled states, and high-density content.
- If no desktop runtime is available, state that verification is static and identify the missing run or screenshot target.
