---
component: Tag
package: "@8x8/oxygen-tag"
category: data_display
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Tag/props]]"
  - "[[Tag/examples]]"
  - "[[Tag/tokens]]"
  - "[[Tag/Tag-figma]]"
  - "[[Tag/Tag-audit]]"
tags:
  - oxygen
  - component/Tag
  - role/accessibility
  - stage/spec_ready
  - category/data_display
---
# Tag — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [Tag-figma.md](Tag-figma.md)

> **Note:** Oxygen MCP returned no explicit accessibility data for Tag, and Figma carries no
> accessibility annotations on the component. This page is inferred from the component's
> nature (passive display when `action` is absent; partially interactive when `action` is set
> on the close button) and from observed implementation patterns in the design context code.

---

## Component nature

Tag is a **dual-mode** component:

| Mode | Trigger | Interactivity |
|------|---------|---------------|
| **Display-only** | No `action` prop | Non-interactive — labels/categories. Should not receive focus. |
| **Partially interactive** | `action` prop set | The remove (×) button is interactive and focusable. The tag body itself remains non-interactive. |

The label content is never independently interactive — it is part of the visual label.

---

## ARIA guidance

### Display-only Tag (no `action`)

| Scenario | Recommendation |
|----------|----------------|
| Static category/status label | No ARIA role required. Text content is sufficient. |
| Status indicator (`variant="red"`/`"yellow"`/`"green"` for RAG) | Don't rely on color alone. Include the status word in the label or in a parent's accessible name. Optionally add `role="status"` if the status is dynamic. |
| Tag inside a list | Wrap in `<ul role="list">` and `<li>` — the parent provides the structure. |

### Tag with `action` (remove button)

The remove button is the focusable element. It must carry an accessible label.

| Scenario | Recommendation |
|----------|----------------|
| Standard remove action | Pass `aria-label` via `actionProps`: `actionProps={{ 'aria-label': 'Remove [Tag label]' }}`. |
| Used inside a Select multi-selection | Same as above — but ensure focus management returns to the Select when a tag is removed. |
| Focus state (`isFocused`) | Use sparingly. Only pass `isFocused={true}` when the parent component (e.g. Select) controls focus programmatically. |
| `hasError` state | The error is conveyed visually (red border). Surface the error condition in text via the parent or a live region — color alone is insufficient. |

### Avatar Tag — image accessibility

The Avatar inside an Avatar Tag must not duplicate the label. Best practice:

```tsx
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={removeHandler}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>
```

The Avatar's underlying `<img>` should have `alt=""` (decorative) when the label already names the user, or `alt="Josephine Lu"` if the avatar appears without a visible label.

---

## Keyboard interaction

| Key | Action | When |
|-----|--------|------|
| `Tab` | Move focus to the remove button | Only when `action` is set |
| `Tab` (again) | Move focus past the tag | After the remove button receives focus |
| `Enter` / `Space` | Activate the remove button (calls `action`) | When the remove button has focus |
| `Esc` | (No effect on Tag itself) | The parent component may close a popover or selection |

> The display-only Tag form (no `action`) is **not focusable** and has no keyboard interactions.

---

## Screen reader guidance

- For display-only tags, the screen reader simply reads the label text. No additional ARIA is required.
- For tags with a remove action, the screen reader reads the button as "Remove [label], button" — provided `aria-label` is set on `actionProps`.
- When `hasError` is true, ensure the error state is also conveyed in text (e.g. an adjacent error message), not only via color.
- When tags are removed from a list, announce the change in a polite live region attached to the parent list:

```tsx
<>
  <ul aria-label="Selected users">
    {tags.map((t) => (
      <li key={t.id}>
        <Tag
          avatar={{ name: t.name, src: t.avatar }}
          action={() => remove(t.id)}
          actionProps={{ 'aria-label': `Remove ${t.name}` }}
        >
          {t.name}
        </Tag>
      </li>
    ))}
  </ul>
  <span className="sr-only" aria-live="polite" aria-atomic="true">
    {announcement}
  </span>
</>
```

---

## Color and contrast

The Tag's color contrast varies by `variant`:

| `variant` | Text color | BG (light) | Contrast (light) | BG (dark) | Contrast (dark) |
|-----------|------------|-----------|------------------|-----------|-----------------|
| `default` | `#26252A` light / `#FFFFFF` dark | `#EBEAE1` | ~13:1 ✅ | `#666666` | ~5.7:1 ✅ |
| `blue` | `#26252A` light / `#292929` dark | `#CCDDF9` | ~12:1 ✅ | `#CCDDF9` | ~12:1 ✅ |
| `grey` | `#FFFFFF` (both) | `#6C6862` | ~5.4:1 ✅ | `#666666` | ~5.7:1 ✅ |
| `red` | `#26252A` light / `#292929` dark | `#F5D3D6` | ~12:1 ✅ | `#F5D3D6` | ~12:1 ✅ |
| `yellow` | `#26252A` / `#292929` | `#FEEFD1` | ~14:1 ✅ | `#FEEFD1` | ~14:1 ✅ |
| `green` | `#26252A` / `#292929` | `#D2F3E1` | ~13:1 ✅ | `#D2F3E1` | ~13:1 ✅ |
| `yellow-emphasis` | `#26252A` / `#292929` | `#F8AE1A` | ~9:1 ✅ | `#F8AE1A` | ~9:1 ✅ |

All variants meet **WCAG 2.1 AA** for normal text (≥ 4.5:1).

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Tag status |
|-----------|-------------|-------------|
| 1.4.3 Contrast (Minimum) | Text ≥ 4.5:1 | ✅ All variants pass (see table above) |
| 1.4.11 Non-text Contrast | UI components & states ≥ 3:1 | Focus ring (`focus01` on `ui06`): light `#0056E0` on `#FFFFFF` ≈ 8:1 ✅; dark `#D7E3F9` on `#171719` ≈ 13:1 ✅ |
| 1.3.1 Info and Relationships | Don't rely on color alone | RAG status colors must include text labels — never use color alone |
| 1.3.3 Sensory Characteristics | Don't rely on shape/color alone | Same as above |
| 2.1.1 Keyboard | All functionality reachable by keyboard | ✅ Remove button is keyboard-operable; display-only tags don't trap focus |
| 2.4.7 Focus Visible | Focus indicator is visible | ✅ Two-layer focus ring (border + inset shadow) provides clear visibility |
| 4.1.2 Name, Role, Value | Interactive components need accessible names | Required: `actionProps={{ 'aria-label': '…' }}` on the remove button |
| 4.1.3 Status Messages | Status changes announced without focus move | Required when removing tags dynamically — use `aria-live="polite"` |

---

## Common pitfalls

- **Missing `aria-label` on `actionProps`** — without it, the remove button is read as just "button". Always include the tag label in the action's `aria-label`.
- **Color-only RAG status** — `variant="red"` alone tells nothing to a non-sighted user. Always include explicit status text.
- **`hasError` without a textual error** — color/border alone is insufficient. Pair with an error message accessible to screen readers.
- **Avatar `alt` text duplicating the label** — leads to "Josephine Lu, image, Josephine Lu, button". Use empty `alt=""` when the visible label is already adjacent.
- **Removing a tag without announcing the change** — screen reader users don't see the visual update. Use a live region attached to the parent list.

---

_Source: Oxygen MCP (`@8x8/oxygen-tag`) · Figma node 8083:8359 · Inferred from component nature · Extracted 2026-05-01_
