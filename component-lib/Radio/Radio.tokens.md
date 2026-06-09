---
parent: "[[Radio]]"
section: tokens
---

## Spacing tokens

| Token | Value | Usage |
|-------|-------|-------|
| `$spacing(2)` | `8px` | Gap between Radio Button items in a `RadioGroup` |

> Confirmed via Figma node 50606:93474.

---

## Per-state token bindings

The component exposes 8 states (Rest, Hover, IsFocused, IsDisabled × IsChecked/Unchecked) but no dedicated per-state colour, border, or shadow token bindings were returned by the Oxygen MCP token search. The authoritative bindings (rest border, selected fill, focus ring colour, disabled border/fill) require Figma variable inspection.

<!-- STUB:GAP-003 source="Run /figma-extract Radio against UI-components nodes 51776:2800 / 50606:93474 to capture per-state colour, border, and shadow token bindings for all 8 Radio states. Depends on GAP-001 (Radio-figma.md absent)." -->

---

## Dark mode

The component renders correctly in both light and dark themes. Theming is handled automatically by the Oxygen design system token layer — no extra configuration is needed.
