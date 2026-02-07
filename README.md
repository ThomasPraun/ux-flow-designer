# UX Flow Designer

Claude Code skill that bridges the gap between Product (PRD) and Visual Design by generating user flow documentation, Mermaid diagrams, and HTML wireframes.

## What It Does

Given a PRD or feature descriptions, this skill generates:

- **Use case documentation** — actors, flows, preconditions, postconditions
- **Mermaid diagrams** — flowcharts, state diagrams, and sequence diagrams per use case
- **Master screen map** — full app navigation overview
- **HTML wireframes** — mobile-first, self-contained, low-fidelity screen layouts
- **Handoff document** — consolidated index linking all artifacts

### Output Structure

```
docs/ux-flows/
├── UX-FLOWS.md              # Master handoff document
├── use-cases.md              # All use cases
├── diagrams/
│   ├── INDEX.md              # Diagram index
│   ├── screen-map.md         # Master app navigation
│   └── uc-001-{name}/
│       ├── flow.md           # Flowchart (graph TD)
│       ├── states.md         # State diagram (stateDiagram-v2)
│       └── sequence.md       # Sequence diagram
└── wireframes/
    ├── INDEX.md              # Screen inventory
    ├── home.html
    ├── login.html
    └── ...
```

## Installation

```bash
# Copy the skill to your Claude Code skills directory
cp -r ux-flow-designer ~/.claude/skills/
```

## Usage

The skill activates when you mention flows, wireframes, user journeys, screen maps, navigation flows, or use cases. Examples:

```
"Design the user flows for my task management app"
"Create wireframes for the onboarding flow"
"Generate a screen map for the app"
"Document the use cases from the PRD"
```

## Workflow

1. **Use Case Extraction** — Reads PRD or accepts feature descriptions, documents use cases, asks for approval
2. **Mermaid Diagrams** — Generates master screen map + 3 diagrams per use case (flow, states, sequence)
3. **HTML Wireframes** — Creates mobile-first wireframes per unique screen using the bundled template
4. **Consolidation** — Produces master handoff document linking all artifacts

## Skill Contents

```
ux-flow-designer/
├── SKILL.md                              # Skill definition and workflow
├── references/
│   ├── mermaid-patterns.md               # Mermaid syntax patterns and examples
│   ├── figma-integration.md              # Figma export toolchain (optional)
│   └── install-commands.md               # Related skills and tools
└── assets/
    └── wireframe-template.html           # HTML wireframe base template
```

## Optional Integrations

| Skill | Role | Required |
|-------|------|----------|
| `product-manager-toolkit` | Upstream: generates the PRD | No |
| `ui-ux-pro-max` | Downstream: visual design from wireframes | No |
| Figma MCPs + plugins | Export wireframes to Figma | No (only on request) |

## License

MIT
