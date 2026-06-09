---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: accessibility
role_description: "Accessibility specifications — ARIA roles, keyboard navigation, WCAG 2.1 AA"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu/props]]"
  - "[[PopoverMenu/examples]]"
  - "[[PopoverMenu/tokens]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-usage]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/accessibility
  - stage/blocked
  - category/overlays_contextual
---

# PopoverMenu — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> ⚠️ **Advisory — verification required (GAP-006):** All accessibility content in this file is **inferred** from the component type (disclosure + menu pattern) and the ARIA APG Menu Button pattern. No accessibility data was returned by the Oxygen MCP, and the Figma file contains no ARIA annotations. Content must be verified via DOM inspection of the rendered component before use in production documentation. See `PopoverMenu-audit.md` GAP-006.

> The Oxygen MCP returned no explicit accessibility documentation for `Popover` or `PopoverMenu`. The guidance below is inferred from the component type (disclosure + menu pattern) and WCAG 2.1 AA requirements.

---

## ARIA roles

| Element | Role | Notes |
|---|---|---|
| Trigger (e.g. `DropdownButton`) | `button` | Provided by the trigger component itself |
| Floating panel | `menu` or `dialog` | Depends on implementation; `PopoverMenu` wraps a list, likely `menu` |
| Menu items | `menuitem` | Each `ListItem` within the panel |
| Divider | `separator` | If `Divider` sub-component is used |
| Section header | `none` / `presentation` | Decorative grouping label; not interactive |

> **Data gap:** The MCP does not document which ARIA roles are applied by the component. Verify via DOM inspection or source review (`SOURCE_GAP`).

---

## Keyboard interactions

| Key | Behavior |
|---|---|
| `Enter` / `Space` | Opens the menu when focus is on the trigger |
| `Escape` | Closes the menu; returns focus to the trigger |
| `ArrowDown` | Moves focus to the next menu item |
| `ArrowUp` | Moves focus to the previous menu item |
| `Home` | Moves focus to the first menu item |
| `End` | Moves focus to the last menu item |
| `Tab` | Closes the menu and moves focus to the next focusable element |
| `Enter` (on item) | Activates the focused menu item |

> **Data gap:** No keyboard interaction spec was returned by the MCP. The pattern above follows the [ARIA Authoring Practices Menu Button pattern](https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/). Confirm actual implementation matches.

---

## Focus management

- When the menu opens, focus should move to the first menu item (or the menu container).
- When the menu closes (via `Escape`, item selection, or outside click), focus should return to the trigger element.
- The `isDisabled` prop should prevent the trigger from receiving focus or opening the menu.

---

## Screen reader guidance

- The trigger button should have a visible label or `aria-label` describing the menu's purpose.
- The floating panel should be announced as a menu when it opens.
- Disabled items should use `aria-disabled="true"` (not `disabled`) so they remain discoverable but not activatable.
- If `header` or `footer` content is used, ensure it does not create confusing reading order.

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Notes |
|---|---|---|
| 1.4.3 Contrast (Minimum) | Text ≥ 4.5:1, large text ≥ 3:1 | Menu item text and trigger button must meet contrast |
| 2.1.1 Keyboard | All functionality operable by keyboard | Menu must open, navigate, and close via keyboard |
| 2.1.2 No Keyboard Trap | Focus must not be trapped | `Escape` must dismiss menu and restore focus |
| 2.4.3 Focus Order | Logical focus sequence | Focus must enter the menu at the first item |
| 2.4.7 Focus Visible | Visible focus indicator | Menu items must show visible focus ring |
| 4.1.2 Name, Role, Value | All UI components have accessible name/role/state | Trigger button needs label; panel needs `role="menu"` |

---

_Source: Oxygen MCP (no explicit a11y data returned) · Inferred from component type · Extracted 2026-05-08_
