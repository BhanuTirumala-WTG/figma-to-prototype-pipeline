# Figma to Prototype

UI prototypes for the applications using Modern Harmony design system, built from Figma mockups using a multi-agent Copilot pipeline.

## How to Use

1. Open this workspace in VS Code
2. Open Copilot Chat
3. Type `@orchestrator` and paste a Figma URL — the pipeline handles everything
4. Or use: `@github-manager commit and push all changes`

See [SETUP.md](SETUP.md) for the full guide, including how to plug this system into a new project.

## Agent Pipeline

| Stage | Agent | What It Does |
|-------|-------|-------------|
| 1 | `@figma-reader` | Extracts design from Figma |
| 2 | `@design-system-guardian` | Maps tokens to Modern Harmony DS |
| 3 | `@ui-developer` | Builds HTML+React prototype |
| 4 | `@qa-reviewer` | Checks bugs, a11y, DS compliance |
| 5 | `@orchestrator` | Auto-fixes issues (up to 3 loops) |
| 6 | `@env-host` | Versions file + opens browser |
| 7 | `@github-manager` | Commits and pushes to GitHub |

## Tech Stack

- HTML + React 18 + Tailwind CSS (all via CDN, no build step)
- Modern Harmony Design System (Switzer font, `--dec_*` tokens)
- Figma MCP for design extraction
- Git for version control
