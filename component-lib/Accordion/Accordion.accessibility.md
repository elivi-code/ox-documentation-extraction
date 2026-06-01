---
parent: "[[Accordion]]"
section: accessibility
---

> **Note:** No explicit accessibility annotations in the Figma file. Guidance below is inferred from WAI-ARIA APG 1.2 and the `translations` prop the component exposes.

## ARIA roles and attributes

| Element | Role / Attribute | Notes |
|---|---|---|
| Accordion header | `<button>` | Rendered as native button (WARN-002 — inferred, not confirmed from source) |
| Collapsed | `aria-expanded="false"` | Set on header button |
| Expanded | `aria-expanded="true"` | Set on header button |
| Content panel | `role="region"` | Expanded content area |
| Content panel | `aria-labelledby` | References header button ID |
| Disabled | `aria-disabled="true"` | Matches Figma `disabled` state |
| Header button | `aria-controls` | WAI-ARIA APG recommends pointing to panel ID. Implementation not confirmed from source — verify before publishing. |

<!-- STUB:GAP-013 source="Designer should add ARIA role, focus order, and keyboard interaction annotations to the Figma Accordion component. Engineering should confirm aria-expanded, role=region, and aria-labelledby implementation." -->

---

## `translations` prop

Always provide meaningful translations for assistive technologies.

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

Set at `AccordionGroup` level as a default; override per accordion where context requires a more specific label.

<!-- STUB:GAP-012 source="Check @8x8/oxygen-accordion source or Storybook for default expand/collapse translation strings. Add defaults to Translations type in Accordion.props.md and confirm whether English-only or localised." -->

---

## Keyboard interactions

| Key | Action |
|---|---|
| `Enter` / `Space` | Toggle accordion (focus on header button) |
| `Tab` | Next focusable element |
| `Shift + Tab` | Previous focusable element |

---

## `expandTrigger` and focus management

| Mode | Focus target | When to use |
|---|---|---|
| `'header'` (default) | Entire header row | No interactive content after title |
| `'arrow'` | Chevron only | When `contentAfterTitle` contains interactive elements needing their own tab stop |

Do not place interactive elements in `contentAfterTitle` when `expandTrigger="header"` — they would be unreachable by keyboard.

---

## Focus ring

| Mode | Token | Value |
|---|---|---|
| Light | `--interactive/focus01` | `#0056e0` |
| Dark | `--interactive/focus01` | `#d7e3f9` |

`2px solid` border. Meets WCAG 2.4.11 against `--ui/ui06` background.

---

## Screen reader guidance

- `title` serves as the accessible label for the toggle button — use descriptive values.
- Collapsed content is hidden from the accessibility tree.
- With `AccordionGroup hasFixedHeight`, only one accordion can be open at a time — communicate this constraint in surrounding UI.
- Max nesting depth is **two levels**. Deeper nesting creates navigation complexity — prefer [[Tabs]] for deep hierarchies.

---

## WCAG 2.1 AA

| Criterion | Status | Notes |
|---|---|---|
| 1.4.3 Contrast | ✅ | Token-based — verify resolved values meet 4.5:1 |
| 1.4.11 Non-text Contrast | ✅ | Focus ring uses `--interactive/focus01` |
| 2.1.1 Keyboard | ✅ | Header/arrow focusable and activatable |
| 2.4.3 Focus Order | ✅ | Tab order follows visual reading order |
| 2.4.7 Focus Visible | ✅ | Focus ring in both modes |
| 4.1.2 Name, Role, Value | ⚠️ | Requires `translations` prop; defaults not confirmed (GAP-012) |
