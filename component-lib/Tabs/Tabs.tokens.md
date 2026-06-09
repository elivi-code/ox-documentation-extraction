---
parent: "[[Tabs]]"
section: tokens
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/tokens
---

## Tokens

Token values resolved via `figma_execute` + `getVariableByIdAsync` alias chain traversal on node `85651:78740` (UI-components → UI-Foundations library). Full primitive and dark-mode hex in [[Tabs.anatomy]].

---

### Color tokens

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
| Focus ring | `interactive/focus01` | `#0056e0` | 2px solid ring |
| Notification badge | `notification/notification01` | `#048284` | — |

> `tabsDisclosure` inherits the same tokens from `Icon Button`. Bottom border in rest state uses `ui/ui01`.

---

### Typography tokens

| Element | Token family | Size | Weight | Line-height | Letter-spacing |
|---------|-------------|------|--------|-------------|----------------|
| Tab label (unselected) | `typography/body01` | `14px` | `400` | `20px` | `-0.06px` |
| Tab label (selected — bold) | `typography/bodyBold01` | `14px` | `600` | `20px` | `-0.06px` |
| Disclosure label | `typography/labelBold01` | `12px` | `600` | `16px` | `0px` |

---

### Spacing

| Element | Property | Value |
|---------|----------|-------|
| `tabs` (default tab) | Padding (all sides) | `16px` |
| `tabs` (default tab) | Height | `52px` (HUG) |
| `tabsDisclosure` | Padding (all sides) | `6px` |
| `tabsDisclosure` | Size | `52 × 52px` |

---

### Token registry note

No dedicated `tab` component namespace exists in the Oxygen theme token registry as of extraction date. All tokens above are resolved semantic tokens from the Figma variable library (UI-components → UI-Foundations). Token wikilinks (e.g. `[[ui/ui01]]`) resolve when the `token-extract` pipeline runs.

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Tokens resolved 2026-05-05_
