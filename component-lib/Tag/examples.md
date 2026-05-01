# Tag — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [Tag-figma.md](Tag-figma.md)

> **Note:** `get-component-examples` returned **0 clean examples** — the Tag package exposes
> only a `TagDocumentation` Storybook wrapper. The snippets below are constructed from the
> documented props (`@8x8/oxygen-tag` v current) and the Figma examples page (`52829:11107`).

---

## Basic Standard Tag

```tsx
import { Tag } from '@8x8/oxygen-tag';

<Tag>Tag</Tag>
```

---

## Standard Tag with leading icon

The leading icon is supplied via `children` (the first child element) — verify with the package source if a dedicated icon prop is required.

```tsx
import { Tag } from '@8x8/oxygen-tag';
import FaceSmileIcon from '@8x8/oxygen-icons/FaceSmile';

<Tag>
  <FaceSmileIcon />
  Happy
</Tag>
```

---

## Standard Tag with remove action

Adding an `action` handler renders the remove (×) button — Figma `type=withAction`.

```tsx
<Tag
  action={() => removeTag(id)}
  actionProps={{ 'aria-label': 'Remove Happy' }}
>
  Happy
</Tag>
```

---

## Color variants (Standard Tag)

```tsx
<Tag variant="default">Default</Tag>
<Tag variant="blue">Blue</Tag>
<Tag variant="grey">Grey</Tag>
<Tag variant="red">Red</Tag>           {/* RAG: Red */}
<Tag variant="yellow">Amber</Tag>      {/* RAG: Amber — Standard only */}
<Tag variant="green">Green</Tag>       {/* RAG: Green — Standard only */}
<Tag variant="yellow-emphasis">Warning</Tag>
```

---

## RAG status pattern

Red, Amber (yellow), Green tags as a status-indicator group. Documented in the Figma examples page.

```tsx
<>
  <Tag variant="red">Critical</Tag>
  <Tag variant="yellow">Warning</Tag>
  <Tag variant="green">Healthy</Tag>
</>
```

---

## Avatar Tag — basic

Passing the `avatar` prop switches the component to the Avatar Tag form.

```tsx
<Tag avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}>
  Josephine Lu
</Tag>
```

---

## Avatar Tag with remove action

```tsx
<Tag
  avatar={{ name: 'Josephine Lu', src: '/avatars/jlu.jpg' }}
  action={() => removeUser('jlu')}
  actionProps={{ 'aria-label': 'Remove Josephine Lu' }}
>
  Josephine Lu
</Tag>
```

---

## Avatar Tag — error state

Combines `action` + `hasError` to render an Avatar Tag with the red error border (Figma `type=withActionError`).

```tsx
<Tag
  avatar={{ name: 'Failed user', src: '/avatars/failed.jpg' }}
  action={() => retry('failed')}
  actionProps={{ 'aria-label': 'Retry Failed user' }}
  hasError
>
  Failed user
</Tag>
```

---

## Group avatar tag

```tsx
<Tag
  avatar={{ name: 'Marketing team', isGroup: true }}
>
  Marketing team
</Tag>
```

---

## Forced focus state

Useful when a parent (e.g. a multi-select Select) controls focus programmatically.

```tsx
<Tag
  isFocused
  action={handleRemove}
>
  Active selection
</Tag>
```

---

## Tag list with proper spacing

Per design specs, tags should be spaced **`$spacing02` (4px)** apart.

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

## Inside a Select with multi-selection

The Tag component is designed to appear inside a Select component when multi-selection is on (documented in the Figma examples page).

```tsx
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

---

## With test ID

```tsx
<Tag testId="user-tag-jlu" action={removeHandler}>
  Josephine Lu
</Tag>
```

---

## Storybook reference

From `Tag.documentation.stories.tsx`:

```tsx
export const TagDocumentation = (args) => (
  <>
    <Doc markdown>{README}</Doc>
    <Doc markdown>{example}</Doc>
    <ComponentSection>
      <Tag {...args} />
    </ComponentSection>
    <Doc markdown>{CHANGELOG}</Doc>
  </>
);
```

---

_Source: Oxygen MCP (`@8x8/oxygen-tag`) · Figma node 8083:8359 · Examples page 52829:11107 · Extracted 2026-05-01_
