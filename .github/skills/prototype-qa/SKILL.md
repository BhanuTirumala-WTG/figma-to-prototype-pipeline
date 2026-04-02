---
name: prototype-qa
description: "QA checklist for HTML prototypes. Use when reviewing a built prototype for bugs, accessibility issues, design system token violations, Supply DS contamination, layout problems, or interaction state coverage."
---

# Prototype QA Checklist

## When to Use
- After a prototype HTML file is built or updated
- When auditing an existing prototype for quality
- Before publishing/versioning a prototype

## Checklist

### 1. Design System Token Compliance

**Supply Token Grep** — Search the file for these FORBIDDEN patterns:
```
--comp_df-button_
--comp_color_error_
--comp_color_warning_
--comp_color_info_
--comp_app-header_
--comp_alert-cell_
--comp_input-cell_
```
If ANY match is found → **CRITICAL** violation. Report with line number and replacement token.

**Hardcoded Color Check** — Scan all `style={}` JSX and CSS rules for raw hex values not inside `:root {}`:
- Allowed: `#ffffff`, `#fff`, `rgba(...)` for shadows
- Forbidden: Any other hex color outside `:root {}`

**Font Family Check** — The ONLY allowed font is `Switzer`. Search for:
- `Inter` → CRITICAL (replace with Switzer)
- `Roboto`, `Arial`, `Helvetica` → CRITICAL
- `sans-serif` alone → WARNING (must be fallback after Switzer)

### 2. Accessibility

- [ ] All `<img>` tags have `alt` attributes
- [ ] Interactive elements are `<button>` or `<a>`, not `<div>` with click handlers
- [ ] Color contrast: error text (#981e15) on error bg (#fbece9) meets WCAG AA (4.5:1)
- [ ] Focus states: interactive elements show visible focus ring
- [ ] `lang="en"` on `<html>` tag
- [ ] Semantic HTML: `<header>`, `<main>`, `<table>` used correctly

### 3. Layout & Structure

- [ ] Page doesn't overflow horizontally at 1440px viewport
- [ ] Grid frozen columns don't overlap scrollable columns
- [ ] VersionSwitcher component exists below AppHeader
- [ ] Grid has sticky headers (position: sticky)
- [ ] Scrollbar styling applies (`.scrollbar-thin`)

### 4. Interaction States

- [ ] Buttons have hover states
- [ ] Grid cells have hover highlight
- [ ] Alert cells show severity colors
- [ ] Editable cells focus state works (click to edit)
- [ ] Switch toggles change visual state
- [ ] Pills show active/inactive states

### 5. Data Integrity

- [ ] All grid data rows render (count matches GRID_DATA length)
- [ ] Number formatting uses `.toLocaleString()` (comma separators)
- [ ] Null values display as `-` not blank or "null"
- [ ] Time columns match TIME_COLUMNS constant

### 6. AI Features (if applicable)

- [ ] AI panel opens/closes without layout shift
- [ ] Chat messages render with proper styling (user vs assistant)
- [ ] AI suggestion cards show severity colors
- [ ] Cell tooltip appears on alert cell click
- [ ] Toast notifications appear and auto-dismiss

## Severity Levels
| Level | Meaning | Example |
|-------|---------|---------|
| CRITICAL | Blocking, must fix before publish | Supply token found, wrong font |
| HIGH | Visual mismatch with Figma | Wrong color value, broken layout |
| LOW | Minor, polish item | Missing hover state, alignment off by 1px |

## Output Format
Return issues as a structured list:
```
[
  { severity: "CRITICAL", location: "line 42, :root block", issue: "Uses --comp_color_error_cell_fill (Supply token)", fix: "Replace with --dec_color_error_subtle" },
  { severity: "HIGH", location: "AppHeader component", issue: "Font family set to Inter", fix: "Change to Switzer" },
  ...
]
```
