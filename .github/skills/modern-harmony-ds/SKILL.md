---
name: modern-harmony-ds
description: "Modern Harmony design system reference. Use when building UI components, auditing DS compliance, mapping Figma tokens to CSS variables, or checking if a token belongs to Supply vs Modern Harmony. Contains resolved color values, typography specs, component patterns, and forbidden token lists."
---

# Modern Harmony Design System

## When to Use
- Building new UI components that must match Figma mockups
- Auditing an HTML file for design system compliance
- Mapping raw hex values from Figma to CSS custom property names
- Checking whether a `--comp_*` token is Supply (forbidden) or Modern Harmony (allowed)
- Resolving a token name to its hex value or vice versa

## Quick Rules
1. **ALL colors** must use `var(--dec_color_*)` or `var(--core_color_*)` — never hardcoded hex
2. **ALL spacing** must use `var(--core_sp_*)` or `var(--dec_element_*)` or `var(--dec_grid-cell_*)`
3. **ALL border-radius** must use `var(--dec_base_crn)` (8px) or `var(--dec_pill_crn)` (16px)
4. **Font**: Switzer only — Light 300, Regular 400, Medium 500, Bold 700
5. **NEVER use Supply tokens** — any `--comp_df-button_*`, `--comp_color_error_*`, `--comp_alert-cell_*`, `--comp_input-cell_*`, `--comp_app-header_*` is forbidden

## Token Reference
See [Color Tokens](./references/color-tokens.md) for the complete token table with resolved hex values.

## Component Patterns
See [Component Patterns](./references/component-patterns.md) for exact CSS implementations of Button, Pill, Switch, Grid Header, Alert Cell, Input Cell, and App Header.

## Supply → Modern Harmony Mapping

When you encounter a Supply token, replace it:

| Supply Token (FORBIDDEN) | Modern Harmony Replacement |
|---|---|
| `--comp_df-button_hzpadding` | `--dec_element_hzpadding` (16px) |
| `--comp_df-button_vtpadding` | `--dec_element_vtpadding` (8px) |
| `--comp_color_error_cell_fill` | `--dec_color_error_subtle` (#fbece9) |
| `--comp_color_warning_cell_fill` | `--dec_color_warning_subtle` (#fff4e5) |
| `--comp_color_info_cell_fill` | `--dec_color_info_subtle` (#fff9e6) |
| `--comp_color_success_cell_fill` | `--dec_color_success_subtle` (#e8f5e9) |
| `--comp_app-header_fill` | `--dec_color_surface_header` (#ffffff) |
| `--comp_app-header_border` | `--dec_color_div_base` (#e5e5ec) |
| `--comp_app-header_height` | `--dec_app-header_height` (56px) |
| `--comp_alert-cell_padding` | `--dec_grid-cell_hzpadding` (12px) |
| `--comp_input-cell_padding` | `--dec_element_margin` (4px) |

## Audit Procedure

To audit an HTML file for DS compliance:

1. **Grep for forbidden prefixes**: Search for `comp_df-button`, `comp_color_error`, `comp_color_warning`, `comp_color_info`, `comp_app-header`, `comp_alert-cell`, `comp_input-cell`
2. **Check font family**: Must be `Switzer` — reject `Inter`, `Roboto`, `Arial`, `Helvetica`
3. **Check hardcoded colors**: Any hex value (#xxx) not inside a `:root {}` block is a violation
4. **Verify token existence**: Every `var(--token_name)` must correspond to a real MH token from the token reference
5. **Report**: Return `{severity, line, token, replacement}` for each violation
