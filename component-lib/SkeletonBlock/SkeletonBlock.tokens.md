---
parent: "[[SkeletonBlock]]"
section: tokens
---

## Tokens

<!-- STUB:GAP-005 source="Resolve ui01 and --ui/ui02 from the UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on Block variant nodes, or request Variables API access." -->
<!-- STUB:GAP-006 source="Enable Variables API access (Enterprise plan) or connect Desktop Bridge to resolve token bindings from the primary library. Re-run figma-extract once available. Depends on GAP-005." -->

> **SOURCE GAP (GAP-005 / GAP-006):** The Figma Variables API (Enterprise plan required) and Desktop Bridge were both unavailable during extraction. Token names are documented via CSS custom property fallbacks from design context, not from the authoritative token library. Token names could have aliases not captured here.

---

## Color tokens

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Block background fill | `--ui/ui02` | `#f4f3ee` | `#3d3d3d` |

### Animation tokens

The skeleton animation fades between two surface colors:

| Token | Role |
|-------|------|
| `ui01` | Animation start color — fades from here |
| `ui02` | Animation end color — same as fill background |

The animation "alternates the colors from `ui01` to `ui02`" to create a smooth in/out fade effect. `ui01` does not appear in the Figma node properties for this component set and its resolved value is unknown.

---

## Spacing tokens

| Usage | Token | Value |
|-------|-------|-------|
| Gap between stacked text skeleton lines | `spacing03` | 8px |

> **WARN-002:** `spacing03` (8px) is sourced from OX usage documentation. It is not confirmed as an enforced CSS token value within the `@8x8/oxygen-skeletons` package — it may be a spacing guideline rather than a hardcoded value the component itself enforces.

---

## Hardcoded values

<!-- STUB:GAP-008 source="Check UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) for a border-radius token at 6px. If one exists, update both tokens.md and SkeletonBlock-figma.md. Depends on GAP-006." -->

| Property | Value | Notes |
|----------|-------|-------|
| Border radius | `6px` | Hardcoded in Figma — no token binding found (GAP-008). May correspond to an Oxygen border-radius token. |
| Width | `362px` | Representative width in the component set frame. In practice fills the container. |
