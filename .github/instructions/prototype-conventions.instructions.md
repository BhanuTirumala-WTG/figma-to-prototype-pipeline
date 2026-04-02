---
applyTo: "prototypes/**"
description: "Conventions for HTML prototype files in the prototypes/ folder. Use when creating or editing prototype .html files."
---

# Prototype File Conventions

## File Structure
Every prototype MUST follow this exact structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>{Project Name} - {Page Name} (v{N})</title>
  <!-- CDN scripts -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <style>
    /* ─── Design System Tokens ─── */
    :root { /* ALL CSS custom properties here */ }
    /* Component styles using var() references only */
  </style>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    /* React application */
  </script>
</body>
</html>
```

## CSS Variable Block
- ALL colors, spacing, radii, and typography sizes MUST be declared as CSS custom properties in `:root {}`
- NEVER use hardcoded hex values in JSX `style={}` or CSS classes — always reference `var(--token_name)`
- Exception: `#ffffff` and `#fff` for white are acceptable as fallbacks

## Component Naming
- React components: PascalCase (`AppHeader`, `DataGrid`, `AIAssistantPanel`)
- CSS classes prefixed with `ds-` for design-system components (`ds-btn`, `ds-pill`, `ds-switch`)
- Data constants: UPPER_SNAKE_CASE (`GRID_DATA`, `TIME_COLUMNS`)

## Version Numbering
- Files: `prototypes/version-{n}.html` where n increments from existing versions
- Draft: `prototypes/draft.html` (temporary, renamed on publish)
- Title tag includes version: `(v{N})`

## Version Switcher
Every prototype must include a `VersionSwitcher` component rendered immediately after `AppHeader` that links to all other versions in `prototypes/`.

## Template Reference
Read the template file specified in `.github/copilot-instructions.md` under "Template File" before building any new prototype. Copy that file's `:root {}` block, CDN links, and component class structure as your baseline.
