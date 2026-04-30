# AlertBanner — Tokens

> **See also:** [alert-banner-figma.md](./alert-banner-figma.md) · [props.md](./props.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Summary

No dedicated AlertBanner-specific design tokens were found in the Oxygen theme registry.
The component's amber background colour matches the value of the `alertYellow` dark-mode
token, but that token is documented as scoped to **data-visualisation** use, not to the
AlertBanner component directly.

> ⚠ The Variables API was inaccessible during extraction (requires Figma Desktop Bridge
> or elevated REST token permissions). Token bindings could not be confirmed. All values
> below are raw hex colours derived from the Figma component reconstruction.

---

## Banner background

| Token | Light value | Dark value | Palette reference |
|-------|------------|------------|------------------|
| `alertYellow` ¹ | `#BC841C` | `#F8AE1A` | light → `colorPalette.yellow04` · dark → `colorPalette.yellow06` |

¹ The Figma reconstruction shows `#F8AE1A` for **all** variants (light and dark). This
matches only the **dark-mode** resolved value of `alertYellow`. Two interpretations:
1. The component intentionally uses a single fixed amber (dark variant) in all modes.
2. Variables were not resolved in the API response — the light-mode background may alias
   to `alertYellow` light (`#BC841C`) but was not surfaced.

**Action required:** Confirm with the design team whether the banner uses a fixed amber
or a mode-adaptive token.

---

## `alert*` semantic tokens (data-visualisation scope)

These tokens were found in the Oxygen theme registry when searching "alert". They are
documented as **data-visualisation** tokens (graphs, bar charts, quality indicators) and
are not AlertBanner-component tokens. Listed here for completeness only.

| Token | Light | Dark | Description |
|-------|-------|------|-------------|
| `alertGreen` | `#127440` | `#189B55` | Green for data viz quality indicators |
| `alertRed` | `#CB2233` | `#F24D5F` | Red for data viz quality indicators |
| `alertYellow` | `#BC841C` | `#F8AE1A` | Yellow for data viz quality indicators |

---

## Spacing / layout values (raw — no tokens confirmed)

| Property | Value | Variant |
|----------|-------|---------|
| Padding (horizontal) | 16 px | all |
| Padding (vertical) | 12 px | all |
| Gap between elements | 16 px | breakpoint ≥ 576 px (horizontal layout) |
| Gap between elements | 8 px | breakpoint < 576 px (vertical layout) |

No spacing tokens were confirmed for these values. They may map to Oxygen spacing scale
tokens (e.g. `space-4`, `space-3`) — verify against the spacing token catalogue.

---

## Missing tokens (gaps)

| Property | Raw value | Gap |
|----------|-----------|-----|
| Banner background | `#F8AE1A` | No confirmed token binding; possible `alertYellow` (data-viz) — needs design confirmation |
| Padding H | 16 px | No confirmed spacing token |
| Padding V | 12 px | No confirmed spacing token |
| Gap (desktop) | 16 px | No confirmed spacing token |
| Gap (mobile) | 8 px | No confirmed spacing token |
| Text colour | unknown | Inner layers not returned by API |
| Icon colour | unknown | Inner layers not returned by API |

---

_Source: Oxygen MCP · figma-console MCP · Extracted 2026-04-28_
