---
parent: "[[Button]]"
section: composition
component: Button
package: "@8x8/oxygen-button"
tags: [oxygen, component/Button, role/composition, section/composition]
---

# Button — Composition

How `Button` composes with its sibling exports and neighbouring components.

---

## Sibling exports (same package)

| Component | Relationship | Notes |
|-----------|-------------|-------|
| `ButtonGroup` | Container | Wraps multiple `Button`s with shared `spacing` and `align`. Used for dialog and form action rows. |
| `DropdownButton` | Variant component | Button that opens a menu; pair with `Popover`/`PopoverMenu`. Supports `fullWidth`. |
| `IconButton` | Variant component | Compact icon-only trigger; always pair with `[[Tooltip]]` for an accessible name. |

## Slotted content

| Slot | Accepts | Via |
|------|---------|-----|
| Leading icon | Any `@8x8/oxygen-icon` component | `iconLeft` prop / Figma `Swap Icon L` |
| Trailing icon | Any `@8x8/oxygen-icon` component | `iconRight` prop / Figma `Swap Icon R` |
| Circular content | A single `Icon` child | `isCircular` + `children` |

## Common patterns

- **Action rows / dialogs** — `ButtonGroup` of Text + Secondary + Primary (see [[Button.usage]] Pair 1).
- **Split control** — `ButtonGroup` of a `Button` + `DropdownButton` (Pair 6).
- **Icon trigger** — `IconButton` wrapped in `[[Tooltip]]` (Pair 4).
- **Forms** — submit `Button` with `type="submit"`; keep enabled and show inline errors (Pair 7).

## Related (peer) components

- `[[Tooltip]]` — supplies the accessible name for icon-only buttons.
- `[[Popover]]` / `PopoverMenu` — typically opened by `DropdownButton`.
- `[[TextLink]]` — use for navigation instead of a button.
