# Figma Integration

Only load this file when user explicitly requests Figma export.

## Table of Contents

- [Required MCPs](#required-mcps)
- [Claude Code Plugins](#claude-code-plugins)
- [Export Workflow](#export-workflow)
- [Limitations](#limitations)

---

## Required MCPs

| MCP | Capability | Install Command |
|-----|------------|-----------------|
| Figma Remote MCP (official) | READ: read designs, extract tokens, screenshots | `claude mcp add --transport http figma https://mcp.figma.com/mcp` |
| figma-console-mcp (community) | WRITE: create/modify frames, components, auto-layout | `npx figma-console-mcp` (requires Figma Desktop Bridge Plugin) |
| Chrome DevTools MCP | Browser automation for figma-friend | `claude mcp add chrome-devtools npx chrome-devtools-mcp@latest` |
| Composio Figma MCP (optional) | FEEDBACK: comment management | Requires Composio account |

## Claude Code Plugins

| Plugin | Purpose | Install |
|--------|---------|---------|
| figma-friend | Direct Figma Plugin API access via browser (WRITE) | `/plugin marketplace add markacianfrani/claude-code-figma` then `/plugin install figma-friend` |
| figma-design | Deep Figma Plugin API knowledge | `/plugin marketplace add manutej/luxor-claude-marketplace` then `/plugin install figma-design@luxor-claude-marketplace` |
| frontend-design (Anthropic) | Improve visual output quality | `/plugin marketplace add anthropics/claude-code` then `/plugin install frontend-design@claude-code-plugins` |

---

## Export Workflow

### Prerequisites

1. Figma Professional seat ($15/month minimum)
2. All required MCPs installed and configured
3. Chrome browser available (for figma-friend)

### Steps

1. **Verify toolchain**
   - Check each MCP from the table above is installed
   - Check each plugin is installed
   - Offer install commands for any missing tool
   - Abort if user declines required tools

2. **Prepare Figma project**
   - Open Figma in Chrome via `chrome-devtools` MCP
   - Create or select target Figma file
   - Set up page structure matching the screen inventory

3. **Convert wireframes**
   - For each HTML wireframe in `docs/ux-flows/wireframes/`:
     - Read the HTML file
     - Create a Figma frame (375px width, mobile)
     - Apply auto-layout matching the wireframe structure
     - Use placeholder rectangles for images
     - Set text content from wireframe

4. **Apply design tokens** (if design system exists)
   - Read existing design tokens via Figma Remote MCP
   - Map wireframe classes to design tokens
   - Apply colors, typography, spacing

5. **Organize and link**
   - Group frames by use case flow
   - Add flow connections between screens
   - Name all frames matching screen inventory

---

## Limitations

| Limitation | Detail |
|------------|--------|
| figma-console-mcp remote (SSE) | Read-only; write requires local NPX mode |
| figma-friend | Requires Chrome open with Figma — not headless |
| Figma API rate limits | Tier 1 limits with Dev seat; Professional recommended |
| Auto-layout fidelity | Complex CSS layouts may not map 1:1 to Figma auto-layout |
| No offline mode | All Figma operations require active internet connection |
| Plugin stability | Community plugins (figma-console-mcp, figma-friend) may have breaking updates |
