---
parent: "[[Select]]"
section: tokens
component: Select
pipeline_stage: doc_rewrite
audit_verdict: NO
tags:
  - oxygen
  - component/Select
  - role/tokens
  - stage/doc_rewrite
---

<!-- STUB:GAP-011 source="Re-run get-theme-tokens with broader search terms: 'border', 'focus', 'error', 'disabled', 'interactive', 'input'. Also inspect the @8x8/oxygen-select package source to find which CSS variables / theme tokens are consumed. The MCP token search for 'select' returned only ui01 — all other state tokens (input border, focus ring, error colour, disabled opacity, popover shadow) are defined internally in the package's styled-components and are not exposed as standalone theme tokens." -->

## Confirmed tokens

| Token | Light value | Dark value | Reference | Usage |
|-------|-------------|------------|-----------|-------|
| `ui01` | `#EBEAE1` | `#666666` | `colorPalette.offwhite09` (light) / `colorPalette.gray05` (dark) | Selected state background colour for list items |

> Only `ui01` was returned by the MCP token search for "select". All other component-level tokens are consumed internally by the select package's styled-components.

## Sizes

| `size` prop | Figma label | Input height |
|-------------|-------------|-------------|
| `'small'` | Small | 76 px |
| `'default'` | Medium | 84 px |
| `'large'` | Large | 92 px |

## States × tokens (pending figma-extract)

| State | Visual indicator | Token / style |
|-------|-----------------|---------------|
| Rest | Default border | UNKNOWN — pending `Select-figma.md` |
| Hover | Highlighted border | UNKNOWN — pending `Select-figma.md` |
| Focus | Blue focus ring | UNKNOWN — pending `Select-figma.md` |
| Disabled | Reduced opacity, no interaction | UNKNOWN — pending `Select-figma.md` |
| Read-only | Muted appearance, non-editable | UNKNOWN — pending `Select-figma.md` |
| Error | Red border + error message below | UNKNOWN — pending `Select-figma.md` |
| Open | Elevated shadow on popover | UNKNOWN — pending `Select-figma.md` |
| Selected option | Option row background | `ui01` |

> ⚠️ "UNKNOWN — pending `Select-figma.md`" cells are not confirmed token names. Replace once `figma-extract Select` runs against node `2105:2` in file `5YihJ5WuDvnvrlrRMC4sBp`.

## Modes

| Mode | Description |
|------|-------------|
| Light | Default; white/light background |
| Dark | Inverted; dark background. `ui01` shifts from `#EBEAE1` → `#666666` |
