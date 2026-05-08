---
component: Accordion
package: "@8x8/oxygen-accordion"
category: layout_overlay
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Accordion/props]]"
  - "[[Accordion/examples]]"
  - "[[Accordion/tokens]]"
  - "[[Accordion/accordion-figma]]"
  - "[[Accordion/accordion-audit]]"
tags:
  - oxygen
  - component/Accordion
  - role/accessibility
  - stage/spec_ready
  - category/layout_overlay
---
# Accordion — Accessibility

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accordion-figma.md](./accordion-figma.md)

---

> **Note:** No explicit accessibility annotations were found in the Figma file.
> The following guidance is inferred from the component's interactive nature,
> the WAI-ARIA Accordion pattern (APG 1.2), and the `translations` prop the
> component exposes.

---

## ARIA roles and attributes

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Accordion header | `<button>` | The header is rendered as a native button element |
| Collapsed state | `aria-expanded="false"` | Set on the header button |
| Expanded state | `aria-expanded="true"` | Set on the header button |
| Content panel | `role="region"` | The expanded content area |
| Content panel | `aria-labelledby` | Should reference the header button's ID |
| Disabled accordion | `aria-disabled="true"` | Matches the Figma `disabled` state |

---

## `translations` prop — aria-labels

Always provide meaningful translations for assistive technologies. Without them the
expand/collapse button has no accessible label beyond the title text.

```tsx
<Accordion
  title="Settings"
  translations={{
    expand: 'Expand Settings section',
    collapse: 'Collapse Settings section',
  }}
>
  ...
</Accordion>
```

For `AccordionGroup`, set `translations` at the group level as a default and override
per accordion where the context requires a more specific label.

---

## Keyboard interactions

| Key | Action |
|-----|--------|
| `Enter` / `Space` | Toggle accordion (when focus is on the header button) |
| `Tab` | Move focus to the next focusable element |
| `Shift + Tab` | Move focus to the previous focusable element |

---

## `expandTrigger` and focus management

The `expandTrigger` prop determines the focus target and affects the keyboard UX:

| Mode | Focus target | When to use |
|------|-------------|-------------|
| `'header'` (default) | Entire header row | Standard accordions with no interactive content after the title |
| `'arrow'` | Chevron icon only | When `contentAfterTitle` contains interactive elements (e.g. `IconButton`) that need their own tab stop |

Do not place interactive elements in `contentAfterTitle` when `expandTrigger="header"` —
they would be unreachable by keyboard and create a click conflict.

---

## Focus ring

A visible focus ring is applied via design tokens:

| Mode | Token | Resolved value |
|------|-------|----------------|
| Light | `--interactive/focus01` | `#0056e0` |
| Dark | `--interactive/focus01` | `#d7e3f9` |

The focus ring uses a `2px solid` border and meets WCAG 2.4.11 (Focus Appearance) contrast requirements when checked against the `--ui/ui06` background.

---

## Screen reader guidance

- The `title` prop serves as the accessible label for the toggle button — use descriptive values that reflect the hidden content.
- Collapsed content is hidden from the accessibility tree; only the header is announced.
- When `AccordionGroup` uses `hasFixedHeight`, only one accordion can be open at a time. Ensure screen reader users are made aware of this constraint through the surrounding UI (e.g. a descriptive label on the group container).
- The maximum nesting depth is **two levels** (design constraint). Deeper nesting creates navigation complexity for screen reader users — prefer tabs for deep hierarchies.

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.4.3 Contrast (Minimum) | ✅ | Token-based colors — verify resolved values meet 4.5:1 against backgrounds |
| 1.4.11 Non-text Contrast | ✅ | Focus ring uses `--interactive/focus01` |
| 2.1.1 Keyboard | ✅ | Header/arrow are focusable and keyboard-activatable |
| 2.4.3 Focus Order | ✅ | Tab order follows visual reading order |
| 2.4.7 Focus Visible | ✅ | Focus ring present in both light and dark modes |
| 4.1.2 Name, Role, Value | ⚠️ | Requires `translations` prop for meaningful aria-labels; default label values not confirmed from MCP data |

---

_Source: Oxygen MCP · Extracted 2026-04-28_
