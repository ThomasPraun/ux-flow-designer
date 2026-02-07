---
name: ux-flow-designer
description: "Design and document app user flows, screens, and use cases using Mermaid diagrams and HTML wireframes. Use when creating user flow diagrams (flowcharts, state diagrams, sequence diagrams), screen wireframes (HTML), use case documentation, screen maps, or when the user mentions 'flows', 'wireframes', 'user journey', 'screen map', 'navigation flow', 'use cases', 'app flow', 'screen layout', 'flujos', 'pantallas', 'casos de uso'. Bridges Product (PRD) and Visual Design phases. Outputs serve as input for ui-ux-pro-max. Optional Figma export when user explicitly requests it."
---

# UX Flow Designer

Bridge between Product (PRD/features) and Visual Design.
Generate user flow documentation, Mermaid diagrams, and HTML wireframes.

## Role and Context

- **Input**: PRD (`docs/product/prd.md`) or user-provided feature descriptions
- **Output**: Diagrams + wireframes in `docs/ux-flows/`
- **Downstream**: Outputs feed into `ui-ux-pro-max` for visual design
- **Standalone**: Usable independently or as saas-pipeline Phase 4 step 1

## Prerequisites

On every invocation, verify:

```
CHECK ~/.claude/skills/ui-ux-pro-max/ exists
  IF missing → READ references/install-commands.md, offer install

CHECK docs/product/prd.md exists
  IF missing → CHECK ~/.claude/skills/product-manager-toolkit/
    IF missing → READ references/install-commands.md, offer install
    OR accept direct user input as feature descriptions

IF user mentions "figma" or "export to figma" →
  READ references/figma-integration.md
  FOR each required MCP/plugin → verify installed, offer install if missing
```

## Workflow

Designing app flows involves these steps:

1. Extract use cases (from PRD or user input)
2. Generate Mermaid flow diagrams (screen map + per use case)
3. Generate HTML wireframes (per unique screen)
4. Consolidate into master handoff document

---

### Phase 1 — Use Case Extraction

Read `docs/product/prd.md` if it exists. If no PRD, ask user for feature list or use case descriptions.

For each use case, document:

| Field | Description |
|-------|-------------|
| ID | `UC-001`, `UC-002`, etc. |
| Name | Short descriptive name |
| Actors | Who participates (User, System, Admin, etc.) |
| Preconditions | What must be true before the flow starts |
| Main Flow | Numbered step-by-step sequence |
| Alternative Flows | Branches, error paths, edge cases |
| Postconditions | What is true after the flow completes |

Save to `docs/ux-flows/use-cases.md`.

Present the use case list to user for approval before proceeding. Do not advance to Phase 2 without explicit confirmation.

---

### Phase 2 — Mermaid Diagrams

Read `references/mermaid-patterns.md` for syntax patterns and best practices.

**Step 1: Master Screen Map**

Generate `docs/ux-flows/diagrams/screen-map.md` — a flowchart showing ALL screens and general navigation paths of the entire app.

**Step 2: Per Use Case Diagrams**

For each approved use case, generate 3 diagrams:

1. **Flowchart** (`graph TD`) — screen-to-screen navigation with decision nodes
2. **State diagram** (`stateDiagram-v2`) — app states (loading, error, success, idle, etc.)
3. **Sequence diagram** (`sequenceDiagram`) — frontend-backend interaction with HTTP methods

Save to `docs/ux-flows/diagrams/{use-case-id}/`:
- `flow.md` — flowchart
- `states.md` — state diagram
- `sequence.md` — sequence diagram

**Constraints:**
- Max 15-20 nodes per diagram
- Split into sub-flows if more complex (link with `click` or reference)
- Use `classDef` for consistent styling across diagrams

Generate index at `docs/ux-flows/diagrams/INDEX.md` listing all diagrams with links.

---

### Phase 3 — HTML Wireframes

For each unique screen identified in the flowcharts, generate an HTML file.

Use `assets/wireframe-template.html` as the base template.

**Requirements:**
- Self-contained: inline CSS only, no external dependencies
- Mobile-first: 375px viewport width
- Wireframe aesthetic: grays (`#f5f5f5` bg), dashed borders (`#ccc`), placeholder text (`#666`)
- Use template CSS classes: `.wf-header`, `.wf-input`, `.wf-button`, `.wf-card`, `.wf-nav`, `.wf-list-item`, `.wf-tab-bar`, `.wf-icon-placeholder`
- Include screen name and related use case in footer metadata

Save to `docs/ux-flows/wireframes/`.

Generate inventory at `docs/ux-flows/wireframes/INDEX.md`:
- Screen name
- File link
- Related use cases
- Key elements/components on the screen

---

### Phase 4 — Consolidation and Handoff

Generate master document `docs/ux-flows/UX-FLOWS.md`:

```markdown
# UX Flows — [App Name]

## Master Screen Map
Link to screen-map.md

## Screen Inventory
| Screen | Purpose | Wireframe | Use Cases |
|--------|---------|-----------|-----------|
| ...    | ...     | link      | UC-001    |

## Use Case Diagrams
### UC-001: [Name]
- Flow: link
- States: link
- Sequence: link

## Navigation Patterns
Summary of recurring navigation patterns (tab bar, back navigation,
modal flows, drawer menus, etc.)

## Open Questions
Design decisions and open questions for ui-ux-pro-max phase.
```

If Figma export requested: read `references/figma-integration.md` and follow the export workflow.

---

## Output Structure

```
docs/ux-flows/
├── UX-FLOWS.md                          # Master handoff document
├── use-cases.md                         # All use cases
├── diagrams/
│   ├── INDEX.md                         # Diagram index
│   ├── screen-map.md                    # Master app navigation
│   ├── uc-001-{name}/
│   │   ├── flow.md                      # Flowchart
│   │   ├── states.md                    # State diagram
│   │   └── sequence.md                  # Sequence diagram
│   └── ...
└── wireframes/
    ├── INDEX.md                         # Screen inventory
    ├── home.html
    ├── login.html
    └── ...
```

## Figma Export (Optional)

Only activate when user explicitly says "figma" or "export to figma".

Read `references/figma-integration.md` for the complete toolchain, required MCPs, plugins, and export workflow.

Never trigger Figma checks automatically. Never check for Figma MCPs unless requested.
