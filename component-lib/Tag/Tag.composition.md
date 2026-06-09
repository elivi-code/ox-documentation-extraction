---
parent: "[[Tag]]"
section: composition
component: Tag
package: "@8x8/oxygen-tag"
role: composition
pipeline_stage: doc_rewrite
audit_verdict: YES
siblings:
  - "[[Tag]]"
  - "[[Tag.props]]"
  - "[[Tag.anatomy]]"
  - "[[Tag.tokens]]"
  - "[[Tag.usage]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
tags: [component, data_display, role/composition]
---

## Sub-components

Tag composes two sub-components internally:

| Sub-component | Location | Triggered by |
|---|---|---|
| [[CloseButton]] | `packages/tag/src/components/CloseButton.tsx` | `action` prop presence |
| [[Avatar]] | `packages/avatar` | `avatar` prop presence |

### CloseButton

The × button rendered when `action` is set. Observed props (from Code Connect and Figma):
`action`, `isFocused`, `variant`, `tabIndex`, `actionProps`, `testId`.

The close button carries the focus ring — the tag body itself does not. See [[Tag.accessibility]] for keyboard and ARIA details.

### Avatar

The circular photo element rendered in Avatar Tag form. The Avatar sub-component:
- `size-24px`, `rounded-1000px`
- Fills the full tag height
- Always present when the `avatar` prop is set
- Accepts `name` (initials fallback), `src` (image URL), `isGroup`

For Avatar's own composition and accessibility rules, see [[Avatar]].

---

## Leading icon slot

Standard Tag includes an instance-swap slot for a leading icon (controlled by the `icon?` boolean in Figma):

| Property | Value |
|---|---|
| Default icon | `face-smile` (node 84161:245102) — "happy · face · smile · good · sentiment" |
| Rendered size | `iconSizeXS` — 16×16 px |
| Delivery mechanism | Via `children` (first `ReactElement`) — **unverified** against package source (GAP-001) |

<!-- STUB:GAP-003 source="Source verified code snippets from the internal Storybook (https://oxygen.8x8.dev/packages/release/latest/?path=/story/components-tag--guidelines) or the package README. Replace inferred examples with confirmed ones once available." -->

> The Oxygen MCP returned 0 clean Storybook examples for `@8x8/oxygen-tag` — the package exposes only a `TagDocumentation` Storybook wrapper. All code examples are constructed from observed props and Figma. Replace with verified snippets when available.

---

## Patterns

### Select multi-selection

Tag is the visual representation of each selected value inside a `Select` component when multi-selection is on. The Figma examples page documents this explicitly:

> "The tags used inside the select component when multiple selection is on."

Both Standard Tags and Avatar Tags are used in this context. Each rendered tag includes its own remove (×) button — the user deselects by activating the × button, which calls `e.stopPropagation()` to prevent the Select from re-opening.

```tsx
import { Select } from '@8x8/oxygen-select';
import { Tag } from '@8x8/oxygen-tag';

<Select
  multiple
  value={selectedUsers}
  onChange={setSelectedUsers}
  renderValue={(values) => (
    <div style={{ display: 'flex', gap: 'var(--spacing/spacing02)', flexWrap: 'wrap' }}>
      {values.map((user) => (
        <Tag
          key={user.id}
          avatar={{ name: user.name, src: user.avatar }}
          action={(e) => {
            e.stopPropagation();
            deselect(user.id);
          }}
          actionProps={{ 'aria-label': `Remove ${user.name}` }}
        >
          {user.name}
        </Tag>
      ))}
    </div>
  )}
/>
```

### RAG status pattern

Red / Amber (yellow) / Green tags as a status-indicator group. Documented in the Figma examples page:

> "RAG tags — Red · Amber (yellow) · Green"

Note: `variant="yellow"` in code corresponds to "Amber" in design conversation (audit WARN-003). Standard Tag only — Avatar Tag does not have `yellow` or `green` variants. See [[Tag.usage]] Pair 3 for full guidance.

```tsx
<div style={{ display: 'flex', gap: 'var(--spacing/spacing02)' }}>
  <Tag variant="red">Critical</Tag>
  <Tag variant="yellow">Warning</Tag>  {/* "Amber" in Figma */}
  <Tag variant="green">Healthy</Tag>
</div>
```

### Avatar Tag in messaging / To-fields

Avatar Tags with `action` appear in To-field inputs and messaging UIs where each selected recipient is represented as a removable pill. The public usage page's placement-02 image shows this pattern: "Josie Lu" and "Michael Jones" as Avatar Tag pills with their own × buttons inside a To-field.

---

## Tag list layout

When multiple tags appear together, lay them out with a flex container using `gap: var(--spacing/spacing02)` (4 px) — the same token used for internal spacing. See [[Tag.usage]] Pair 5 and [[Tag.tokens]] for token details.

```tsx
<div style={{ display: 'flex', gap: 'var(--spacing/spacing02)', flexWrap: 'wrap' }}>
  {items.map((item) => (
    <Tag
      key={item.id}
      action={() => remove(item.id)}
      actionProps={{ 'aria-label': `Remove ${item.label}` }}
    >
      {item.label}
    </Tag>
  ))}
</div>
```

---

_Source: Oxygen MCP · Figma node 8083:8359 · Examples page 52829:11107 · Extracted 2026-05-01_
