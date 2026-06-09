---
component: Tabs
package: "@8x8/oxygen-tabs"
category: layout_overlay
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_complete
pipeline_note: "Canonical spec written — pipeline complete"
audit_verdict: YES
siblings:
  - "[[Tabs/props]]"
  - "[[Tabs/examples]]"
  - "[[Tabs/accessibility]]"
  - "[[Tabs/Tabs-figma]]"
  - "[[Tabs/Tabs-pui]]"
  - "[[Tabs/Tabs-audit]]"
  - "[[Tabs/Tabs-spec]]"
tags:
  - oxygen
  - component/Tabs
  - role/tokens
  - stage/spec_complete
  - category/layout_overlay
---
# Tabs — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [Tabs-figma.md](Tabs-figma.md)

## MCP token search results

A search for `"tab"` in `get-theme-tokens` returned **no component-specific tab tokens** — only generic active-state tokens unrelated to the Tabs component.

<!-- No dedicated tab token namespace exists in the Oxygen theme token registry as of extraction date. -->

---

## Color & token bindings

Token values resolved via `figma_execute` + alias chain traversal on node `85651:78740` (UI-components → UI-Foundations library). Full primitives and dark-mode values in [Tabs-figma.md](Tabs-figma.md) §Color & token bindings.

<!-- GAP-001: applied — variable IDs replaced with semantic token names from Tabs-figma.md §Color & token bindings -->

| Element | Semantic token | Hex (Light) | Notes |
|---------|---------------|-------------|-------|
| Bottom border — rest/unselected | `ui/ui01` | `#ebeae1` | 1px |
| Bottom border — hover | `text/textColor01` | `#26252a` | 1px |
| Bottom border — selected | `actions/action01` | `#0056e0` | **2px** |
| Bottom border — disabled | `interactive/disabled02` | `#c8c8bd` | 1px |
| Label text — rest | `text/textColor01` | `#26252a` | — |
| Label text — secondary/muted | `text/textColor02` | `#6c6862` | Tab group label or tab count context |
| Label text — disabled | `interactive/disabled02` | `#c8c8bd` | — |
| Icon fill | `icon/icon01` | `#26252a` | — |
| Focus ring | `interactive/focus01` | `#0056e0` | 2px solid |
| Notification badge | `notification/notification01` | `#048284` | — |

> The selected state uses a **2px** bottom border; all other states use **1px**.

### Typography tokens

| Element | Token family | Size | Weight | Line-height | Letter-spacing |
|---------|-------------|------|--------|-------------|----------------|
| Tab label (unselected) | `typography/body01` | `14px` | `400` | `20px` | `-0.06px` |
| Tab label (selected — bold) | `typography/bodyBold01` | `14px` | `600` | `20px` | `-0.06px` |
| Disclosure label | `typography/labelBold01` | `12px` | `600` | `16px` | `0px` |

---

## Spacing (from Figma layout)

| Element | Property | Value |
|---------|----------|-------|
| `tabs` (default tab) | Padding (all sides) | `16px` |
| `tabs` (default tab) | Height | `52px` (HUG) |
| `tabsDisclosure` | Padding (all sides) | `6px` |
| `tabsDisclosure` | Size | `52 × 52px` |

---

## No OX-registered tab-specific tokens

The Oxygen theme token search returned no entries scoped to the `tab` component namespace. The color values above are derived from Figma variable bindings and may correspond to shared semantic tokens (e.g. `border03`, `interactive01`) — the full token name resolution requires access to the Figma variable library.

---

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
