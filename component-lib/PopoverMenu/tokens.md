---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: tokens
role_description: "Design token bindings — colors, spacing, typography per component state"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu/props]]"
  - "[[PopoverMenu/examples]]"
  - "[[PopoverMenu/accessibility]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-usage]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/tokens
  - stage/blocked
  - category/overlays_contextual
---

# PopoverMenu — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

The Oxygen MCP returned **no theme tokens** for the `popover` component family (`totalMatches: 0` for search term "popover").

This is a `SOURCE_GAP` — popover panel styling (background, border, shadow, radius) likely relies on shared surface/elevation tokens from the UI-Foundations token library rather than component-scoped tokens. These tokens are not individually exposed via the MCP's `get-theme-tokens` endpoint for this package.

**Recommended audit action:** Resolve actual token names via the Figma UI-Foundations library (file key `iVY5nI8JAxM05Apnnvozzs`) using `figma_execute` + `getVariableByIdAsync` on the Popover/PopoverMenu Figma nodes.

---

## Variants and sizes

No variant or size tokens were returned by the MCP. The `PopoverMenu` does not expose a `size` or `variant` prop — the panel dimensions are controlled via:

- `maxHeight` (numeric prop, pixels)
- `placement` (positional, not dimensional)

There are no documented color variants or size tokens at this time (`SOURCE_GAP`).

---

_Source: Oxygen MCP · Extracted 2026-05-08_
