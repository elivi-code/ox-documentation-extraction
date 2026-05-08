---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
siblings:
  - "[[Badge/props]]"
  - "[[Badge/tokens]]"
  - "[[Badge/accessibility]]"
  - "[[Badge/badge-pui]]"
tags:
  - oxygen
  - component/Badge
  - role/examples
  - stage/extracted
  - category/data_display
---
# Badge — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

---

## Basic counter badge

```tsx
import { Badge } from '@8x8/oxygen-badge';

// Single digit
<Badge>4</Badge>

// Double digit
<Badge>12</Badge>

// Overflow — use "+" when count exceeds two digits
<Badge>99+</Badge>
```

---

## Sizes

```tsx
<Badge size="small">2</Badge>
<Badge size="medium">2</Badge>   {/* default */}
<Badge size="big">2</Badge>
```

---

## Type variants

```tsx
<Badge type="primary">5</Badge>   {/* default — teal notification colour */}
<Badge type="secondary">5</Badge>
```

---

## Dot badge (no counter)

Use a badge without children and `size="small"` to render a dot indicator.

```tsx
<Badge size="small" />
```

---

## Inner badge (positioned inside wrapper)

Set `isInner` to have the badge absolutely positioned inside its parent container.

```tsx
<div style={{ position: 'relative', display: 'inline-block' }}>
  <IconButton icon={<BellIcon />} aria-label="Notifications, 4 unread" />
  <Badge isInner aria-hidden="true">4</Badge>
</div>
```

---

## Placement on an icon — top-right corner

```tsx
<div style={{ position: 'relative', display: 'inline-block' }}>
  <BellIcon />
  <Badge
    isInner
    style={{ position: 'absolute', top: 0, right: 0, transform: 'translate(50%, -50%)' }}
  >
    4
  </Badge>
</div>
```

---

## Placement on a list item — dot below, centred

```tsx
<div style={{ position: 'relative', display: 'inline-block' }}>
  <ListItem label="Meetings" />
  <Badge
    size="small"
    style={{ position: 'absolute', bottom: -4, left: '50%', transform: 'translateX(-50%)' }}
  />
</div>
```

---

## Conditional visibility

Badges are not permanently rendered — show them based on application state.

```tsx
{hasUnread && <Badge size="small" aria-hidden="true" />}

{meetingActive && (
  <Badge size="small" aria-hidden="true" />
)}
```

---

## AIBadge

```tsx
import { AIBadge } from '@8x8/oxygen-badge';

// Default label ("AI")
<AIBadge />

// Custom label
<AIBadge>Beta</AIBadge>

// With test ID
<AIBadge testId="my-ai-badge">AI</AIBadge>
```

---

## Storybook reference

From `Badge.documentation.stories.tsx`:

```tsx
<Badge>2</Badge>

<AIBadge>{aiBadgeChildren}</AIBadge>
```

---

_Source: Oxygen MCP (`@8x8/oxygen-badge`) · Figma node 2565:14 · Extracted 2026-04-29_
