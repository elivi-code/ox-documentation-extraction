---
parent: "[[Tooltip]]"
section: composition
---

## Composition

---

## Subcomponents

### `_Tip` — Arrow/pointer atom

The `_Tip` atom (Figma node `7987:8235`) is the directional arrow rendered on the tooltip container. It lives in the `Atoms` section (`29870:42882`) and is only rendered when `enableArrow` is `true`.

| Property | Value |
|----------|-------|
| Figma node | `7987:8235` |
| Size variant | `Small` (single size observed) |
| Controlled by | `enableArrow` prop on `<Tooltip>` |
| Token binding | Inherits background from Content container (`--ui/ui07`) |

The `_Tip` is a structural element with no independent interactivity. It exists solely to indicate directionality relative to the trigger.

---

## Related components

### [[Popover]]

Popover is the natural escalation path when Tooltip content becomes interactive, rich, or requires persistence. The usage guidelines define a clear boundary:

| When content is… | Use |
|-----------------|-----|
| Short hint, read-only, ≤140 chars | **Tooltip** |
| Rich text, links, buttons, or persistent | **Popover** |

Tooltip and Popover can be layered on the same trigger using a state progression (hover → Tooltip, click → Popover). See [[Tooltip.usage]] — "Tooltip and Popover working together".

### [[Modal]]

Modal is used when the content requires full user focus and blocks the page. Tooltip never blocks workflow; Modal always does.

### [[StaticTooltip]]

`StaticTooltip` (`@8x8/oxygen-static-tooltip`) renders the tooltip body in its always-visible, non-interactive state. Used for:
- Documentation screenshots
- Design alignment / Storybook demos
- Cases where tooltip content must be permanently visible without hover

`StaticTooltip` accepts `children` (confirmed). Full API is undocumented in the Oxygen MCP — see [[Tooltip.props]] GAP-009.

---

## Trigger element patterns

Tooltip is typically composed with:

| Trigger type | Notes |
|-------------|-------|
| `<IconButton>` | Most common use case — label the icon when no visible text exists |
| `<button>` | Augment visible label with additional context |
| Truncated `<span>` | Reveal full text of truncated content |
| `<th>` / column header | Explain abbreviations or technical terms in data tables |
| Disabled element | Explain why an element is disabled (use `includeWrapper` if needed) |

For triggers without forwardRef support (custom components), use `includeWrapper` to wrap in a `<span>`.

---

## Composition constraints

- **One tooltip per trigger.** Stacking multiple `<Tooltip>` instances on a single element is unsupported and produces conflicting `aria-describedby` bindings.
- **No nesting.** Tooltip should not be used inside other floating elements (Popover, Modal, SlideOut) — floating stacking context conflicts can result.
- **Touch accessibility.** Tooltip is hover/focus-triggered. For touch-primary surfaces, prefer always-visible helper text or Popover with `showOn="click"`.
