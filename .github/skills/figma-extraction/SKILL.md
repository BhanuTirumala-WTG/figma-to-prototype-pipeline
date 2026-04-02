---
name: figma-extraction
description: "Extract design context from Figma using MCP tools. Use when reading a Figma URL, parsing node IDs, fetching screenshots, getting component code, or building a DesignBrief from a Figma selection."
---

# Figma Design Extraction

## When to Use
- Given a Figma URL, need to extract the design structure
- Need to get screenshots and design tokens from a Figma frame
- Building a DesignBrief object from a Figma selection

## URL Parsing

Extract `fileKey` and `nodeId` from Figma URLs:

| URL Pattern | FileKey | NodeId |
|---|---|---|
| `figma.com/design/:fileKey/:name?node-id=:nodeId` | `:fileKey` | Convert `-` to `:` in nodeId |
| `figma.com/design/:fileKey/branch/:branchKey/:name` | Use `:branchKey` | From query param |
| `figma.com/file/:fileKey/...` | `:fileKey` | From query param |

**Example**: `https://www.figma.com/design/BijXxJ3HRcaEWoLQaiUbno/S-OP?node-id=3399-34987`
→ fileKey = `BijXxJ3HRcaEWoLQaiUbno`, nodeId = `3399:34987` (replace `-` with `:`)

## Extraction Procedure

### Step 1: Get Screenshot
Call `#tool:mcp_com_figma_mcp_get_screenshot` with fileKey and nodeId.
This gives you a visual reference of the entire frame.

### Step 2: Get Root Design Context
Call `#tool:mcp_com_figma_mcp_get_design_context` with fileKey and nodeId.
This returns:
- React + Tailwind reference code
- CSS custom properties and their resolved values
- Component descriptions and documentation links
- Screenshot of the specific node

### Step 3: Identify Child Components
From the root design context, identify distinct component nodes by looking at:
- `data-node-id` attributes in the returned code
- Component names in `data-name` attributes
- Key sections: App Header, Page Title, Toolbar, Grid, Panels

### Step 4: Get Child Design Context
For each major child component, call `#tool:mcp_com_figma_mcp_get_design_context` with its nodeId.
Prioritize these components:
1. App Header (navigation, search, user profile)
2. Page Title (breadcrumb styling)
3. Buttons, Pills, Switches (interactive elements)
4. Grid Header (column headers, hierarchy headers)
5. Grid Cells (data cells, alert cells, input cells)
6. Side panels (AI assistant, filters)

### Step 5: Search Design System
Call `#tool:mcp_com_figma_mcp_search_design_system` to find component definitions:
- Search for "Modern Components" patterns
- Search for "Modern UI Styles" color tokens
- Search for specific component names found in Step 3

### Step 6: Get Variable Definitions (optional)
Call `#tool:mcp_com_figma_mcp_get_variable_defs` to get design token collections.
Look for "Modern Color Tokens" and "Theme 2.0" collections.

## DesignBrief Structure

Return a structured brief with this shape:

```
DesignBrief:
  pageTitle: string           # e.g., "Capacity Planning Overview"
  dimensions: {w, h}          # Frame size
  layout: string              # e.g., "header + toolbar + grid + side-panel"
  screenshot: string          # URL from get_screenshot

  components[]:
    name: string              # e.g., "AppHeader", "DataGrid"
    nodeId: string            # Figma node ID
    figmaCode: string         # Raw React+Tailwind from get_design_context
    tokens[]:                 # CSS custom properties found
      name: string            # e.g., "--dec_color_text_label"
      value: string           # e.g., "#282828"
    description: string       # Component usage notes from Figma

  colorTokens[]:              # All unique tokens found across components
    name: string
    value: string
    source: string            # "Modern UI Styles", "Modern Components", etc.

  typography:
    fontFamily: string        # e.g., "Switzer"
    styles[]:                 # Font styles found
      name: string            # e.g., "Label/MD — Medium"
      weight: number
      size: string
      lineHeight: string

  assets[]:                   # Image/icon URLs (7-day expiry)
    name: string
    url: string
```

## Important Notes
- Figma asset URLs expire after 7 days — use SVG inline or recreate icons
- The React+Tailwind code from `get_design_context` is a REFERENCE, not production code
- Always check component descriptions for usage guidelines
- "Components [SUPPLY]" library items are from the WRONG design system — flag them for replacement
