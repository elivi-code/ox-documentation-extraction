---
parent: "[[Breadcrumbs]]"
section: tokens
---

<!-- STUB:GAP-001 source="Check @8x8/oxygen-breadcrumbs source stylesheet or raise with the Oxygen team to expose component tokens via the MCP theme-tokens endpoint." -->
> **No MCP-registered tokens (GAP-001):** `get-theme-tokens` returned 0 results for `breadcrumb`. No Oxygen theme tokens are registered against this component in the MCP. The MCP is the authoritative registry; the names below are **Figma design context** (CSS variable references), not confirmed registry entries. Verify against `@8x8/oxygen-tokens` before implementation.

## Color tokens

> Confidence: Figma design context (not MCP-registered). Only **rest-state** bindings resolved.

| Token | Collection | Light | Dark | Element(s) |
|-------|------------|-------|------|------------|
| `--actions/action08` | actions | `#0056e0` | `#99bbf3` | Link label (`_Text link breadcrumb`, rest); ellipsis button (rest) |
| `--interactive/active07` | interactive | `#0045b3` | `#0056e0` | Ellipsis button — menu open / active |
| `--text/textcolor01` | text | `#26252a` | `white` | `/` separator; current-page label |
| `--ui/ui01` | ui | `#ebeae1` | — | Overflow Menu border (light mode only; dark is hardcoded `#666`) |

<!-- STUB:GAP-003 source="Access the shared Oxygen token library for Figma file 5YihJ5WuDvnvrlrRMC4sBp (file key iVY5nI8JAxM05Apnnvozzs; use figma_execute + getVariableByIdAsync). Retrieve hover/active/focus token names for the breadcrumb link atom (node 20648:30062) and ellipsis atom (node 22076:37746); update this table." -->
> **Hover / active / focus bindings unresolved (GAP-003):** The Figma file has 0 local variables — all tokens come from a shared library inaccessible via this file's Variables API. Only rest-state values were returned. The state atoms exist (nodes `20648:30062`, `22076:37746`) but their hover/active/focus fill bindings were not resolved.

### Hardcoded (no token binding) — Overflow Menu container

| Property | Light | Dark |
|----------|-------|------|
| Background | `white` | `#171719` |
| Border | `#ebeae1` (`--ui/ui01`) | `#666` (hardcoded) |
| Box shadow | `0px 1px 2px 0px rgba(41,41,41,0.25)` | `0px 1px 2px 1px #141414` |
| Border radius | `6px` | `6px` |
| Width / padding-y | `160px` / `9px` | `160px` / `9px` |

## Typography tokens

| Token | Size | Weight | Line height | Letter spacing | Element(s) |
|-------|------|--------|-------------|----------------|------------|
| `--typography/body01/*` | 14 px | 400 | 20 px | −0.06 px | All text (links, separator, current page) |

## Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE — Overflow Menu shadow is hardcoded (see above). -->

_Source: [[Breadcrumbs/tokens]] · [[Breadcrumbs/Breadcrumbs-figma]] · Oxygen MCP + Figma MCP · Extracted 2026-04-30_
