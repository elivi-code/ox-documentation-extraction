---
parent: "[[SkeletonCircle]]"
section: tokens
component: SkeletonCircle
role: spoke
pipeline_stage: draft
tags:
  - oxygen
  - component/SkeletonCircle
  - role/tokens
  - stage/draft
---

<!-- source: figma-only -->

> **DATA GAP:** `get-theme-tokens` returned 0 matches for "skeleton". Token data below was extracted from the Figma design context (node `31984:56124`). The Figma Variables API and Desktop Bridge were both unavailable during extraction, so token names could not be resolved from the source library.

<!-- STUB:GAP-005 source="Resolve --ui/ui02 and ui01 from UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on Circle variant nodes." -->

<!-- STUB:GAP-006 source="Enable Variables API or connect Desktop Bridge; re-run figma-extract on node 31984:56124 to confirm all token bindings from source library. Depends on GAP-005." -->

---

## Color tokens

| Element | Token | Light value | Dark value |
|---|---|---|---|
| Circle fill background | `--ui/ui02` | `#f4f3ee` | `#3d3d3d` |

> Token name sourced from CSS fallback values in Figma design context — not confirmed from the UI-Foundations source library. Both `SkeletonBlock` and `SkeletonCircle` share this fill token.

### Animation tokens

The skeleton animation fades between two surface colors:

| Token | Role | Notes |
|---|---|---|
| `ui01` | Animation start color | Referenced in usage documentation; not present in Figma node properties |
| `ui02` | Animation end color (same as fill background) | Extracted from CSS fallback |

---

## Spacing tokens

| Usage | Token | Value | Notes |
|---|---|---|---|
| Gap between skeleton elements in a layout | `spacing03` | 8px | Sourced from usage documentation only — unconfirmed as an enforced CSS value in `@8x8/oxygen-skeletons` |

---

## Hardcoded values (flagged)

| Property | Value | Notes |
|---|---|---|
| Border radius | `100px` | Fully rounded — makes the element circular. No token binding found in Figma. |

<!-- STUB:GAP-009 source="Check UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) for a full-rounded border-radius token. Update this table and SkeletonCircle.anatomy.md if one exists. Depends on GAP-006." -->

---

## Size variants (dimensional reference)

| Size value | Diameter | Size label |
|---|---|---|
| `80px - xlarge` | 80px | xlarge |
| `48px - large` | 48px | large |
| `40px - medium` | 40px | medium |
| `32px - small` | 32px | small |
| `28px - small` | 28px | small |
| `24px - xsmall` | 24px | xsmall |
| `22px - xsmall` | 22px | xsmall |
| `20px - xsmall` | 20px | xsmall |
| `16px - xsmall` | 16px | xsmall |

> Diameter values are enforced by the `size` Figma axis; not bound to spacing tokens.

---

_Source: Oxygen MCP (0 token results) · Figma design context · Extracted 2026-05-05_
