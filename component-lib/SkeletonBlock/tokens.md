# SkeletonBlock — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [SkeletonBlock-figma.md](SkeletonBlock-figma.md)

---

> **DATA GAP:** `get-theme-tokens` returned 0 matches for "skeleton". Token data below was extracted directly from the Figma design context (node `31984:56109`). The Figma Variables API and Desktop Bridge were both unavailable, so token names could not be resolved from the source library.

---

## Color tokens

| Element | Token | Light value | Dark value |
|---|---|---|---|
| Block / Text fill background | `--ui/ui02` | `#f4f3ee` | `#3d3d3d` |

### Animation tokens (from usage documentation)

The skeleton animation fades between two surface colors:

| Token | Role |
|---|---|
| `ui01` | Animation start color |
| `ui02` | Animation end color (same as fill background) |

The animation "alternates the colors from `ui01` to `ui02`" to create a smooth in/out fade effect.

---

## Spacing tokens

| Usage | Token | Value |
|---|---|---|
| Gap between text skeleton lines | `spacing03` | 8px |

---

## Hardcoded values (flagged)

The following values appear in the Figma design context without token references:

| Property | Value | Notes |
|---|---|---|
| Border radius | `6px` | Not bound to a token; may correspond to a border radius token |
| Width | `362px` | Representative width in the component set frame; in practice fills the container |

---

## Variants / sizes table

### SkeletonBlock

| Size value | Height | Replaces |
|---|---|---|
| `40px - heading02` | 40px | `heading02` text style |
| `28px - heading01` | 28px | `heading01` text style |
| `24px - bulletList01` | 24px | `bulletList01` text style |
| `22px - body02` | 22px | `body02` text style |
| `20px - body01` | 20px | `body01` text style |
| `16px - label01` | 16px | `label01` text style |
| `custom - image` | 240px | Image / block-level element |

### SkeletonCircle (from usage documentation)

| Size value | Diameter |
|---|---|
| `xlarge` | 80px |
| `large` | 48px |
| `medium` | 40px |
| `small` | 32px / 28px |
| `xsmall` | 24px / 22px / 20px / 16px |

---

_Source: Oxygen MCP · Figma design context · Extracted 2026-05-05_
