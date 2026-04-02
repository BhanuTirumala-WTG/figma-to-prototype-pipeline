# Modern Harmony — Component CSS Patterns

Exact CSS implementations derived from the Figma "Modern Components" library. Every component uses ONLY `var()` references to MH tokens.

## DS Button (`.ds-btn`)

```css
.ds-btn {
  font-family: var(--core_typeface_switzer);
  font-weight: 500;
  font-size: var(--dec_text_size_label_md);
  line-height: var(--line-height-md);
  letter-spacing: 0.07px;
  padding: var(--dec_element_vtpadding) var(--dec_element_hzpadding);
  border-radius: var(--dec_base_crn);
  border: 1px solid var(--dec_color_disabled_border);
  background: var(--dec_color_disabled_subtle);
  color: var(--dec_color_text_label);
  cursor: pointer;
}
.ds-btn:hover { background: var(--dec_color_surface_secondary); }

/* Primary variant */
.ds-btn-primary {
  background: var(--dec_color_secondary_strong);
  color: #ffffff;
  border-color: var(--dec_color_secondary_strong);
}
.ds-btn-primary:hover { background: var(--dec_color_secondary_foreground); }
```

## DS Pill (`.ds-pill`)

```css
.ds-pill {
  font-family: var(--core_typeface_switzer);
  font-weight: 400;
  font-size: var(--dec_text_size_label_sm);
  line-height: var(--line-height-md);
  letter-spacing: 0.07px;
  padding: 4px 12px;
  border-radius: var(--dec_pill_crn);
  border: 1px solid var(--dec_color_secondary_base);
  background: var(--dec_color_secondary_base);
  color: var(--dec_color_secondary_text);
  cursor: pointer;
}
.ds-pill.active {
  background: var(--dec_color_secondary_strong);
  color: #ffffff;
  border-color: var(--dec_color_secondary_strong);
}
/* Severity variants */
.ds-pill-critical { background: var(--dec_color_error_subtle); border-color: #f5c6c0; color: var(--dec_color_error_foreground); }
.ds-pill-high { background: var(--dec_color_warning_subtle); border-color: #fde0b0; color: var(--dec_color_warning_foreground); }
.ds-pill-medium { background: var(--dec_color_info_subtle); border-color: #fde68a; color: var(--dec_color_info_foreground); }
.ds-pill-low { background: #fefce8; border-color: #fde047; color: #854d0e; }
```

## DS Switch

```css
.ds-switch {
  width: 48px;
  height: 24px;
  border-radius: var(--dec_switch_crn);
  padding: 2px;
  cursor: pointer;
  display: flex;
  align-items: center;
}
.ds-switch.on {
  background: var(--dec_color_switch_selected);
  justify-content: flex-end;
}
.ds-switch.off {
  background: #c4c4c4;
  justify-content: flex-start;
}
.ds-switch-knob {
  width: 20px;
  height: 20px;
  border-radius: 20px;
  background: var(--dec_color_switch_indicator);
  box-shadow: 0px 1px 2px 0px rgba(25,34,61,0.12),
              0px 1px 3px 0px rgba(25,34,61,0.24);
}
```

Knob shadow uses `rgba(25,34,61,...)` — this is the MH shadow primitive, NOT a hardcoded color.

## Grid Header Cell (`.ds-header-cell`)

```css
.ds-header-cell {
  background: var(--dec_color_header-cell_fill);
  border: 0.5px solid var(--dec_color_grid-cell_border);
  font-family: var(--core_typeface_switzer);
  font-weight: 500;
  font-size: var(--dec_text_size_label_md);
  line-height: var(--line-height-md);
  letter-spacing: 0.07px;
  color: var(--dec_color_text_label);
  padding: var(--core_sp_rem2) var(--dec_grid-cell_hzmargin);
}
```

## Grid Data Cell (`.ds-data-cell`)

```css
.ds-data-cell {
  border: 0.5px solid var(--dec_color_grid-cell_border);
  font-family: var(--core_typeface_switzer);
  font-weight: 400;
  font-size: var(--dec_text_size_label_md);
  line-height: var(--line-height-md);
  letter-spacing: 0.07px;
  padding: var(--core_sp_rem3) var(--dec_grid-cell_hzpadding);
}
```

## Alert Cell Variants

```css
.cell-alert-critical {
  background: var(--dec_color_error_subtle);
  color: var(--dec_color_error_foreground);
}
.cell-alert-high {
  background: var(--dec_color_warning_subtle);
  color: var(--dec_color_warning_foreground);
}
.cell-alert-medium {
  background: var(--dec_color_info_subtle);
  color: var(--dec_color_info_foreground);
}
.cell-alert-low {
  background: #fefce8;
  color: #854d0e;
}
```

Alert cells display a small flag icon in the top-right corner. The flag uses `currentColor` so it inherits the foreground color.

## Input Cell (editable)

```css
/* Alternating row background */
background: var(--dec_color_grid_alt-row);
/* Inner border when focused */
border: 1px solid var(--dec_color_grid-input-cell_border);
/* Inner padding */
padding: var(--dec_element_margin);
```

## App Header

```css
header {
  height: var(--dec_app-header_height);
  background: var(--dec_color_surface_header);
  border-bottom: 1px solid var(--dec_color_div_base);
  display: flex;
  align-items: center;
  padding: 0 20px;
  justify-content: space-between;
}
```

### Header Elements
- **Logo**: 28x28px, `var(--dec_color_secondary_strong)` background, 8px border-radius
- **Nav breadcrumb**: Switzer Regular 12px, `var(--dec_color_text_secondary)`
- **Search input**: border `var(--dec_color_disabled_border)`, radius `var(--dec_base_crn)`
- **Assistant button**: `.ds-btn-primary` pattern
- **Avatar**: 32x32px circle, `var(--dec_color_secondary_base)` background

## Page Title

```css
/* Breadcrumb level 1 — Light */
font-family: var(--core_typeface_switzer);
font-weight: 300;
font-size: 30px;
line-height: 32px;
letter-spacing: -0.3px;
color: var(--dec_color_text_label);

/* Current page — Medium */
font-weight: 500;
/* Same size/line-height */
```

Separator: `›` character in `var(--dec_color_text_secondary)`.
