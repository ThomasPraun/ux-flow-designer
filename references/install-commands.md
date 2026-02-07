# Install Commands

Tools, skills, and MCPs that ux-flow-designer can propose to the user.

## Auxiliary Skills

| Skill | Purpose | Phase | Install Command |
|-------|---------|-------|-----------------|
| ui-ux-pro-max | Downstream: visual design | After | `npx skills find ui-ux-pro-max` |
| product-manager-toolkit | Upstream: PRD | Before | `npx skills find product-manager-toolkit` |
| brainstorming | Ideation if no PRD | Before | `npx skills find brainstorming` |

## Figma MCPs (only if user requests Figma)

| MCP | Purpose | Install Command |
|-----|---------|-----------------|
| Figma Remote MCP | Read Figma designs | `claude mcp add --transport http figma https://mcp.figma.com/mcp` |
| figma-console-mcp | Write Figma designs | `npx figma-console-mcp` |
| Chrome DevTools MCP | Browser automation for Figma | `claude mcp add chrome-devtools npx chrome-devtools-mcp@latest` |

## Figma Plugins (only if user requests Figma)

| Plugin | Purpose | Install Command |
|--------|---------|-----------------|
| figma-friend | Write mode via browser | `/plugin marketplace add markacianfrani/claude-code-figma` |
| figma-design | Plugin API knowledge | `/plugin marketplace add manutej/luxor-claude-marketplace` |
| frontend-design | Visual output quality | `/plugin marketplace add anthropics/claude-code` |
