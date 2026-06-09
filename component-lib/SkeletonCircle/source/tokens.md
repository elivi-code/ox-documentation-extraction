---
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[SkeletonCircle/props]]"
  - "[[SkeletonCircle/examples]]"
  - "[[SkeletonCircle/accessibility]]"
  - "[[SkeletonCircle/SkeletonCircle-figma]]"
  - "[[SkeletonCircle/SkeletonCircle-audit]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/tokens
  - stage/blocked
  - category/feedback_status
---
# SkeletonCircle — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [SkeletonCircle-figma.md](SkeletonCircle-figma.md)

---

> **DATA GAP:** `get-theme-tokens` returned 0 matches for "skeleton". Token data below was extracted directly from the Figma design context (node `31984:56124`). The Figma Variables API and Desktop Bridge were both unavailable, so token names could not be resolved from the source library.

---

## Color tokens

| Element | Token | Light value | Dark value |
|---|---|---|---|
| Circle fill background | `--ui/ui02` | `#f4f3ee` | `#3d3d3d` |

### Animation tokens (from usage documentation)

The skeleton animation fades between two surface colors:

| Token | Role |
|---|---|
| `ui01` | Animation start color |
| `ui02` | Animation end color (same as fill background) |

---

## Spacing tokens

| Usage | Token | Value |
|---|---|---|
| Gap between skeleton elements | `spacing03` | 8px |

---

## Hardcoded values (flagged)

| Property | Value | Notes |
|---|---|---|
| Border radius | `100px` | Fully rounded — makes the element circular. Not bound to a token. |

---

## Size variants table

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

---

_Source: Oxygen MCP · Figma design context · Extracted 2026-05-05_
