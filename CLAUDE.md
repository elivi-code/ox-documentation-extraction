# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this workspace is

A documentation-only workspace for the **Oxygen (OX) design system** (`@8x8/oxygen-*`). There is no source code, build, or test suite. The work product is structured markdown under [component-lib/](component-lib/), produced by composing several MCP servers and skills.

Track progress in [components-to-extract.md](components-to-extract.md) — 37 components across 8 categories (34 tracked in that file; Badge, Radio, and Toaster are the additional three), with a `Progress: N / 34 complete` counter at the top. **After each component finishes extraction + audit, strike through the row and bump the counter** (this is a standing user instruction, also captured in memory).

## Per-component output layout

Each component lives in `component-lib/{ComponentName}/`. Filenames are produced by specific skills and consumed by later stages:

| File | Source skill | Notes |
| --- | --- | --- |
| `props.md`, `examples.md`, `tokens.md`, `accessibility.md` | `oxygen-mcp-extract` | Always lowercase, no component prefix. |
| `{component}-figma.md` + `figma-screenshot-{component}.png` | `figma-extract` | Casing of the prefix is inconsistent across existing folders (e.g. `Avatar-figma.md` vs `accordion-figma.md`) — match the casing already used in the folder rather than changing it. |
| `{component}-pui.md` | `pui-mcp-extract` | Only present when the component has Platform UI infra concerns (notifications, navigation, session, event bus). Many components don't need one. |
| `{component}-usage.md` | `figma-extract-usage` | Do/Don't editorial guidance from a Figma "{Component} — Examples" page. Often missing. |
| `{component}-usage.html` | `figma-extract-usage` | HTML render of the usage examples; produced alongside `-usage.md`. |
| `{component}-audit.md` | `doc-audit` | YAML-frontmatter gap report scoring 7 dimensions (props, examples, tokens, accessibility, figma, usage, pui). Required input for `doc-rewrite`. |
| `{component}-spec.md` | `doc-rewrite` | Canonical merged spec — final pipeline output. |

## Navigation files

Before starting any pipeline work, read `pipeline-status.md` — one read gives instant orientation on every component's current state.

| File | When to use |
| --- | --- |
| [`pipeline-status.md`](pipeline-status.md) | **First stop for AI orientation** — compact stage/verdict/blocker table for all 37 components |
| [`index.md`](index.md) | All components grouped by category with wiki-links to every file |
| [`component-map.yaml`](component-map.yaml) | Full detail: audit scores, gap counts, cross-file links; use for deep lookups on a specific component |

## The extract → audit → rewrite pipeline

The skills are designed to be run in this order for each component:

1. **Extract** in parallel (when MCPs are connected):
   - `oxygen-mcp-extract` → `props.md`, `examples.md`, `tokens.md`, `accessibility.md`
   - `figma-extract` → `{component}-figma.md` + screenshot
   - `figma-extract-usage` → `{component}-usage.md` (skip if no Examples page exists)
   - `pui-mcp-extract` → `{component}-pui.md` (skip if component has no application-layer concerns)
2. **Audit** with `doc-audit` → `{component}-audit.md`. The frontmatter classifies every gap as `DOC_GAP` (auto-fixable), `SOURCE_GAP` (needs upstream Figma/MCP work), or `CONFLICT` (human decision). The `verdict:` field decides whether rewrite can proceed.
3. **Rewrite** with `doc-rewrite` once the audit verdict is `YES` → `{component}-spec.md`. `CONFLICT` gaps must be resolved before rewrite runs.

When a user asks to "document X", route to the skill that fits the current stage — don't replay earlier steps if their outputs already exist.

### Quick command reference

Since this workspace has no build/test suite, "commands" are skill invocations:

```bash
# Start extraction for a component (run as parallel batch)
/oxygen-mcp-extract <ComponentName>
/figma-extract <ComponentName>
/figma-extract-usage <ComponentName>
/pui-mcp-extract <ComponentName>

# Audit after extraction completes
/doc-audit <ComponentName>

# Rewrite once audit verdict is YES
/doc-rewrite <ComponentName>

# Update progress tracking (manual)
# Edit components-to-extract.md: strike through row, bump counter
```

### Before each skill: MCP verification

SessionStart hook prints an availability reminder. Before starting any extraction skill, verify these MCPs are accessible:

- **OX MCP** — Test: `mcp__oxygen-mcp__list-components` (should return component list)
- **PUI MCP** — Test: `mcp__platform-ui-mcp__pui-list` (should return Platform UI packages)
- **Figma Console** — Test: `mcp__figma-console__figma_navigate` with file URL (should navigate; auth failures block figma-extract)

If any MCP is unavailable, tell the user before proceeding. The settings allow list includes most common tool calls, reducing permission prompts.

## MCP servers (and the SessionStart check)

Project-level (in `.claude/settings.local.json`):

- **figma-console** — write/execute against Figma (variants, screenshots, variables). Required by `figma-extract`, `figma-extract-usage`, `figma-draw`.
- **workshop-mcp** — project-specific.

Available via claude.ai:

- **oxygen-mcp** — `mcp__oxygen-mcp__*` tools for Oxygen docs/props/examples/tokens/icons.
- **platform-ui-mcp** — `mcp__platform-ui-mcp__*` tools for PUI docs and events.
- **pencil** — `.pen` design files (only needed if a `.pen` file is in scope).

A SessionStart hook prints an MCP-availability reminder. Before starting any extraction skill, do a lightweight probe (e.g. `mcp__oxygen-mcp__list-components`) and tell the user if any required MCP is missing — `figma-extract` in particular **must stop and report** on auth failure rather than emitting partial data.

## Progress tracking (standing instruction)

After each component finishes extraction + audit (the extract → audit pipeline):

1. Open [components-to-extract.md](components-to-extract.md)
2. Find the component's row
3. Strike it through: change `| ComponentName |` to `| ~~ComponentName~~ |`
4. Bump the `Progress: N / 34 complete` counter at the top

The counter reflects how many components have completed the full extract + audit pipeline (ready for or past rewrite). This is a visual tracking mechanism for ongoing work.

## Conventions worth knowing

- **Don't invent file content.** If a Figma variable resolves to an opaque ID (`20136:253`) rather than a semantic token name, the audit's job is to flag it as a `DOC_GAP`/`SOURCE_GAP` — don't guess `border03`.
- **Cross-links inside component files** point to siblings (`[props.md](props.md)`, `[{component}-figma.md]`). When renaming, update the "See also" lines in all sibling files.
- **Deprecated packages** are struck through in `components-to-extract.md` headers (e.g. `~~card~~`). Don't extract those unless explicitly asked.
- **Never use `Read` or `Grep` on `.pen` files** — they're encrypted; use the `pencil` MCP tools.
- **Every `.md` under `component-lib/`** carries YAML frontmatter with `component`, `role`, `pipeline_stage`, `audit_verdict`, `siblings` (wiki-links to related files), and `tags`. Files are filterable in Obsidian Dataview and self-describing when opened standalone.
