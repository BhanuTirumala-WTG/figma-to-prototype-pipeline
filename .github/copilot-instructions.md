# S&OP Exception Planning — Workspace Instructions

## Project Purpose
Build UI prototypes from Figma mockups for the S&OP Exception Planning application using the **Modern Harmony** design system exclusively.

---

## ⚙️ PROJECT CONFIG — Customize These Per Project

> **When plugging this agent system into a new project**, update the values below.
> Everything outside this section is reusable as-is.

### Project Name
`S&OP Exception Planning`

### Figma Source
- File key: `BijXxJ3HRcaEWoLQaiUbno`
- Default node: `3399:34987` ("Fix Exception" / "Capacity Planning Overview")

### Template File
- Reference prototype: `exception-planning/version-2.html`
- This is the "gold standard" file that `@ui-developer` copies structure from

### Output Directory
- Prototypes go in: `prototypes/`
- Draft file: `prototypes/draft.html`
- Versioned files: `prototypes/version-{n}.html`

### GitHub Repository
- Remote: `https://github.com/Bhanu-Tirumala-WTG/S-OP---Exception-planning.git`
- Default branch: `main`

---

## Tech Stack
- **HTML + React 18** via CDN (`unpkg.com`) — no npm, no build step
- **Tailwind CSS** via CDN (`cdn.tailwindcss.com`)
- **Babel Standalone** for in-browser JSX transpilation
- Single-file prototypes: everything self-contained in one `.html` file

## File Conventions
| Path | Purpose |
|------|---------|
| `prototypes/version-{n}.html` | Completed versioned prototypes |
| `prototypes/draft.html` | Work-in-progress during build pipeline |
| `exception-planning/version-2.html` | Reference baseline (current best version) |

## Design System — Modern Harmony ONLY

**CRITICAL**: This application uses ONLY the **Modern Harmony** design system. Never use Supply, Components [SUPPLY], or any other design system.

### Allowed Token Prefixes
| Prefix | Purpose | Example |
|--------|---------|---------|
| `--dec_color_*` | Color decision tokens | `--dec_color_text_label` |
| `--dec_text_*` | Typography tokens | `--dec_text_size_label_md` |
| `--dec_base_*` | Base layout tokens | `--dec_base_crn` (border-radius) |
| `--dec_element_*` | Element spacing | `--dec_element_hzpadding` |
| `--dec_grid-cell_*` | Grid cell layout | `--dec_grid-cell_hzpadding` |
| `--core_sp_*` | Core spacing primitives | `--core_sp_rem2` |
| `--core_color_*` | Core color primitives | `--core_color_transparent` |
| `--line-height-*` | Line height tokens | `--line-height-md` |

### FORBIDDEN Tokens (Supply DS — NEVER use)
| Supply Token | Modern Harmony Replacement |
|---|---|
| `--comp_df-button_*` | `--dec_element_*` |
| `--comp_color_error_*` | `--dec_color_error_*` |
| `--comp_color_warning_*` | `--dec_color_warning_*` |
| `--comp_color_info_*` | `--dec_color_info_*` |
| `--comp_app-header_*` | `--dec_color_surface_header`, `--dec_color_div_base` |
| `--comp_alert-cell_*` | `--dec_color_*` equivalents |
| `--comp_input-cell_*` | `--dec_color_*` equivalents |

### Typography
Font: **Switzer** (Light 300, Regular 400, Medium 500, Bold 700)

## Figma MCP Tools
- `#tool:mcp_com_figma_mcp_get_design_context` — Get code + screenshot for a node
- `#tool:mcp_com_figma_mcp_get_screenshot` — Capture a frame screenshot
- `#tool:mcp_com_figma_mcp_search_design_system` — Search DS components
- `#tool:mcp_com_figma_mcp_get_variable_defs` — Get design token definitions
- `#tool:mcp_com_figma_mcp_get_metadata` — Get file metadata

## Agent Pipeline

| Agent | Invoke With | Role |
|-------|-------------|------|
| `@orchestrator` | User entry point | Coordinates the full 7-stage pipeline |
| `@figma-reader` | Subagent only | Extracts design from Figma MCP |
| `@design-system-guardian` | Subagent only | Enforces DS compliance |
| `@ui-developer` | Subagent only | Builds the HTML prototype |
| `@qa-reviewer` | Subagent only | Checks bugs + accessibility |
| `@env-host` | Subagent only | Versions files + opens browser |
| `@github-manager` | User or subagent | Handles git commit, push, status |

### Quick Start
1. Open Copilot Chat → type `@orchestrator` → paste a Figma URL
2. Or use the slash command: `/build-from-figma {Figma URL}`
3. Or for git only: `@github-manager commit and push all changes`
