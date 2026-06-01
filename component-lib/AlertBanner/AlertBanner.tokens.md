---
parent: "[[AlertBanner]]"
component: AlertBanner
section: tokens
role: spoke-tokens
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/tokens
  - stage/rewritten
---

# AlertBanner — Tokens

## Color tokens

Token values confirmed via `figma_execute` + `getVariableByIdAsync` alias chain traversal on node `13899:15489` (UI-components → UI-Foundations library).

### Banner container background

| Semantic token | Primitive | Hex (Light) | Hex (Dark) | Notes |
|---------------|-----------|-------------|------------|-------|
| `warning/warning01` | `color/yellow/yellow06` | `#f8ae1a` | `#f8ae1a` | Same in both modes — the amber background is intentionally fixed; no mode switch |

<!-- CONFLICT:CONFLICT-002 finding="Raw fill #F8AE1A matches alertYellow dark-mode value exactly (colorPalette.yellow06). Oxygen theme registry documents alertYellow as a data-visualisation token (graphs, bars, quality indicators) — not an AlertBanner component token. Figma extraction (2026-05-05) confirms warning/warning01 → color/yellow/yellow06 as the binding; design system token owner must confirm canonical name and resolve namespace overlap with alertYellow." HUMAN DECISION REQUIRED -->

### Text and icon

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Title / message text | `text/textColor07` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray02` | `#292929` |
| Warning icon fill | `icon/icon08` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray02` | `#292929` |
| Action button (secondary) | `actions/action02` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray08` | `#c2c2c2` |
| Close / dismiss icon | `text/textColor09` | `color/pure/white` | `#ffffff` | `color/pure/black` | `#000000` |

Dark text and icon on the fixed amber background ensure contrast in both modes. The close-icon token flips white↔black to accommodate mode-specific contexts.

## Typography tokens

| Element | Token family | Size | Weight | Line-height | Letter-spacing |
|---------|-------------|------|--------|-------------|----------------|
| Message body | `typography/body01/` | `14px` | `400` | `20px` | `-0.06px` |
| Action label | `typography/labelBold01/` | `12px` | `600` | `16px` | `0px` |

## Spacing values

| Property | Value | Variant |
|----------|-------|---------|
| Padding (horizontal) | 16 px | all |
| Padding (vertical) | 12 px | all |
| Gap between elements | 16 px | breakpoint ≥ 576 (horizontal layout) |
| Gap between elements | 8 px | breakpoint < 576 (vertical layout) |

<!-- STUB:GAP-009 source="After Variables API access is restored (GAP-005), map padding-H 16px, padding-V 12px, gap-desktop 16px, gap-mobile 8px to Oxygen spacing scale tokens (e.g. space-3, space-4). Currently raw px values with no token binding confirmed." -->

## Related semantic tokens (data-viz scope, not component tokens)

Listed for completeness — these `alert*` tokens were returned when searching "alert" in the Oxygen registry but are scoped to data-visualisation (graphs, quality indicators), not AlertBanner. The CONFLICT-002 marker above tracks the naming overlap.

| Token | Light | Dark | Description |
|-------|-------|------|-------------|
| `alertGreen` | `#127440` | `#189B55` | Green data-viz quality indicators |
| `alertRed` | `#CB2233` | `#F24D5F` | Red data-viz quality indicators |
| `alertYellow` | `#BC841C` | `#F8AE1A` | Yellow data-viz quality indicators |

<!-- STUB:GAP-008 source="Search the Oxygen token registry with wider terms (warning, notification, feedback) and confirm whether a dedicated AlertBanner-namespaced token exists. If absent, note explicitly in this section." -->
