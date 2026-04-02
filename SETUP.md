# Figma-to-Prototype Agent Pipeline

A portable multi-agent system for VS Code Copilot that converts Figma mockups into production-quality HTML prototypes, fully version-controlled on GitHub.

## What This Does

Give the `@orchestrator` agent a Figma URL → it coordinates 7 specialized agents to:

1. **Extract** the design from Figma (screenshots, layout, components, tokens)
2. **Annotate** every visual property with the correct design system token
3. **Build** a single-file HTML+React+Tailwind prototype
4. **Review** for DS violations, accessibility, layout bugs
5. **Fix** any critical/high issues (up to 3 auto-fix loops)
6. **Publish** as a versioned file + open in browser
7. **Commit** and push to GitHub

## Agents

| Agent | Role | User-Invocable |
|-------|------|----------------|
| `@orchestrator` | Pipeline coordinator — the main entry point | Yes |
| `@figma-reader` | Extracts design from Figma via MCP tools | No (subagent) |
| `@design-system-guardian` | Enforces design system compliance | No (subagent) |
| `@ui-developer` | Builds the HTML prototype | No (subagent) |
| `@qa-reviewer` | Reviews for bugs, a11y, DS violations | No (subagent) |
| `@env-host` | Versions files + opens browser | No (subagent) |
| `@github-manager` | Handles git commit, push, status | Yes |

## Quick Start (Current Project)

1. Open VS Code with this workspace
2. Open **Copilot Chat** (Ctrl+Shift+I / Cmd+Shift+I)
3. Type: `@orchestrator https://www.figma.com/design/BijXxJ3HRcaEWoLQaiUbno/...?node-id=3399-34987`
4. Watch the pipeline run through all 7 stages
5. Or use the slash command: `/build-from-figma {Figma URL}`

For git only: `@github-manager commit and push all changes`

## Plugging Into a New Project

### Step 1: Copy the `.github/` folder
Copy the entire `.github/` directory into your new project root:

```
your-new-project/
├── .github/
│   ├── copilot-instructions.md    ← EDIT THIS
│   ├── agents/
│   │   ├── orchestrator.agent.md
│   │   ├── figma-reader.agent.md
│   │   ├── design-system-guardian.agent.md
│   │   ├── ui-developer.agent.md
│   │   ├── qa-reviewer.agent.md
│   │   ├── env-host.agent.md
│   │   └── github-manager.agent.md
│   ├── skills/
│   │   ├── figma-extraction/SKILL.md
│   │   ├── modern-harmony-ds/
│   │   │   ├── SKILL.md
│   │   │   └── references/
│   │   │       ├── color-tokens.md
│   │   │       └── component-patterns.md
│   │   ├── prototype-qa/SKILL.md
│   │   └── git-workflow/SKILL.md
│   ├── instructions/
│   │   └── prototype-conventions.instructions.md
│   └── prompts/
│       └── build-from-figma.prompt.md
├── prototypes/          ← Output goes here
└── your-template.html   ← Your reference prototype
```

### Step 2: Edit `copilot-instructions.md`
Open `.github/copilot-instructions.md` and update the **⚙️ PROJECT CONFIG** section:

```markdown
### Project Name
`Your New Project Name`

### Figma Source
- File key: `YOUR_FIGMA_FILE_KEY`
- Default node: `YOUR_DEFAULT_NODE_ID`

### Template File
- Reference prototype: `path/to/your-template.html`

### Output Directory
- Prototypes go in: `prototypes/`

### GitHub Repository
- Remote: `https://github.com/YOUR_USER/YOUR_REPO.git`
- Default branch: `main`
```

### Step 3: Update Design System References (if different DS)
If your project uses a different design system than Modern Harmony:
1. Update `.github/skills/modern-harmony-ds/SKILL.md` with your DS rules
2. Update `references/color-tokens.md` with your token values
3. Update `references/component-patterns.md` with your CSS patterns
4. Update the "Allowed Token Prefixes" and "FORBIDDEN Tokens" tables in `copilot-instructions.md`

If your project also uses Modern Harmony, no changes needed.

### Step 4: Set Up Git
```bash
cd your-new-project
git init
git remote add origin https://github.com/YOUR_USER/YOUR_REPO.git
```

Or just ask: `@github-manager set up git for this project`

### Step 5: Create a Template Prototype
Build your first prototype manually or from Figma, and save it as the template file referenced in Step 2. This becomes the baseline that `@ui-developer` copies structure from for all future prototypes.

## Prerequisites

- **VS Code** with GitHub Copilot (Chat enabled)
- **Figma** account with access to the design files
- **Figma MCP** server configured in VS Code (provides `mcp_com_figma_mcp_*` tools)
- **Git** installed and configured with push access to your repository
- No Node.js or npm required — prototypes use CDN-loaded libraries

## File Structure

```
.github/
├── copilot-instructions.md          # Always-on workspace rules (edit per project)
├── agents/
│   ├── orchestrator.agent.md        # Main pipeline coordinator
│   ├── figma-reader.agent.md        # Figma MCP extraction
│   ├── design-system-guardian.agent.md  # DS compliance enforcement
│   ├── ui-developer.agent.md        # HTML prototype builder
│   ├── qa-reviewer.agent.md         # Quality assurance checker
│   ├── env-host.agent.md            # File versioning + browser preview
│   └── github-manager.agent.md      # Git commit/push/status
├── skills/
│   ├── figma-extraction/SKILL.md    # How to parse Figma URLs + extract designs
│   ├── modern-harmony-ds/           # Design system knowledge base
│   │   ├── SKILL.md                 # DS rules overview
│   │   └── references/
│   │       ├── color-tokens.md      # All token names → hex values
│   │       └── component-patterns.md # Copy-paste CSS for DS components
│   ├── prototype-qa/SKILL.md        # QA checklist for prototypes
│   └── git-workflow/SKILL.md        # Git operation procedures
├── instructions/
│   └── prototype-conventions.instructions.md  # Auto-applied to prototypes/**
└── prompts/
    └── build-from-figma.prompt.md   # /build-from-figma slash command
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Orchestrator doesn't find agents | Ensure `.github/agents/` files have correct YAML frontmatter |
| Figma MCP tools not available | Check Figma MCP server is running in VS Code settings |
| Git push fails | Run `@github-manager status` to diagnose |
| Wrong design system tokens | Update the DS skill files under `.github/skills/modern-harmony-ds/` |
| Prototype looks wrong | Check template file is correct in `copilot-instructions.md` |
