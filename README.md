---
title: "OX Documentation Extraction — Workspace Guide"
description: "Project overview, directory structure, workflow steps, and navigation guide"
role: workspace_guide
workspace: OX Documentation Extraction
last_updated: 2026-05-08
tags:
  - oxygen
  - navigation
  - readme
---
# OX Documentation Extraction

A documentation-only workspace for the **Oxygen (OX) design system** (`@8x8/oxygen-*`). This project produces structured markdown documentation for Oxygen UI components by composing multiple data sources (component APIs, Figma designs, Platform UI infrastructure, and accessibility specifications).

## What This Is

This is **not** a source code repository. There is no build, test suite, or package to deploy. The work product is comprehensive, audited markdown documentation under [`component-lib/`](component-lib/) that serves as the canonical reference for Oxygen components.

## Project Structure

```text
OX Documentation Extraction/
├── index.md                        # ← START HERE — all 37 components with file links
├── pipeline-status.md              # Quick status table for AI orientation (8K)
├── component-map.yaml              # Full detail map: scores, verdicts, cross-links
├── components-to-extract.md        # Progress tracker (28 / 34 complete)
├── CLAUDE.md                       # AI instructions and workflow conventions
└── component-lib/
    └── {ComponentName}/
        ├── props.md                # Component API and prop definitions
        ├── examples.md             # Usage examples and code snippets
        ├── tokens.md               # Design tokens (colors, spacing, typography)
        ├── accessibility.md        # A11y specs and ARIA guidance
        ├── {component}-figma.md    # Design system specs from Figma
        ├── {component}-usage.md    # Do/Don't editorial guidance (optional)
        ├── {component}-pui.md      # Platform UI integration notes (optional)
        ├── {component}-audit.md    # Documentation gap report
        └── {component}-spec.md     # Final merged specification
```

### Navigation files

| File | Purpose | When to use |
|------|---------|-------------|
| [`index.md`](index.md) | All components grouped by category, every file linked | Browsing in Obsidian |
| [`pipeline-status.md`](pipeline-status.md) | Compact status table — stage, verdict, blocker per component | AI orientation; quick status check |
| [`component-map.yaml`](component-map.yaml) | Full detail — audit scores, gap counts, cross-file links, wiki-links | Deep lookups on a specific component |
| [`components-to-extract.md`](components-to-extract.md) | Strike-through progress tracker | Updating after each completed component |

Every `.md` file in `component-lib/` has YAML frontmatter with `component`, `role`, `pipeline_stage`, `audit_verdict`, `siblings` (wiki-links to related files), and `tags` — making them filterable in Obsidian Dataview and self-describing when opened standalone.

## The Workflow

Documentation for each component progresses through three stages:

### 1. Extract (Parallel)

Gather data from multiple sources:

- **`oxygen-mcp-extract`** → `props.md`, `examples.md`, `tokens.md`, `accessibility.md`
- **`figma-extract`** → `{component}-figma.md` + screenshot
- **`figma-extract-usage`** → `{component}-usage.md` (if Examples page exists)
- **`pui-mcp-extract`** → `{component}-pui.md` (if applicable)

### 2. Audit

Run **`doc-audit`** to produce `{component}-audit.md`. This report:

- Scores documentation completeness across 7 dimensions
- Flags gaps as `DOC_GAP` (auto-fixable), `SOURCE_GAP` (upstream work needed), or `CONFLICT` (human decision)
- Decides whether rewrite can proceed

### 3. Rewrite

Run **`doc-rewrite`** to produce `{component}-spec.md`, the final canonical documentation. Only proceeds if audit verdict is `YES`.

## Progress Tracking

See [`pipeline-status.md`](pipeline-status.md) for a quick visual summary of all 37 components by stage. See [`components-to-extract.md`](components-to-extract.md) for the master list with a `Progress: N / 34 complete` counter. After each component finishes extraction + audit, mark it done and bump the counter.

## Setup

### Prerequisites

- Claude Code or compatible AI development environment
- MCP servers configured in `.claude/settings.local.json`:
  - **figma-console** (required for Figma extraction)
  - **workshop-mcp** (project-specific configuration)

- Claude.ai connected tools:
  - **oxygen-mcp** — component APIs, props, examples, tokens, icons
  - **platform-ui-mcp** — Platform UI docs and events integration

### Getting Started

1. Check [`CLAUDE.md`](CLAUDE.md) for project conventions and detailed instructions
2. Review [`components-to-extract.md`](components-to-extract.md) to see what needs documentation
3. For each component, run the extraction → audit → rewrite pipeline in order

## Key Conventions

- **Don't invent file content.** If a token resolves to an opaque ID, flag it as a gap—don't guess.
- **Cross-link within components** using relative paths: `[props.md](props.md)`, `[{component}-figma.md]`
- **Deprecated packages** are struck through in the component list—skip extraction unless asked.
- **`.pen` files** are encrypted—use `pencil` MCP tools, never `Read` or `Grep`.

## Documentation Output

Each component's final output is a merged specification (`{component}-spec.md`) that combines:

- Complete prop documentation with types and defaults
- Usage examples and patterns
- Design token mappings
- Accessibility guidelines
- Design system visuals and variants
- Application-layer integration guidance (where applicable)

This creates a single source of truth for developers and designers using Oxygen components.

## Contributing

When documenting a new component:

1. **Extract** all available sources in parallel
2. **Audit** the gaps and resolve conflicts
3. **Rewrite** to produce the final spec
4. Update [`components-to-extract.md`](components-to-extract.md) with ✅ and bump progress

For detailed instructions, see [`CLAUDE.md`](CLAUDE.md).

## Questions?

This workspace uses Claude Code skills and MCP servers. Refer to `CLAUDE.md` for technical setup and workflow details.
