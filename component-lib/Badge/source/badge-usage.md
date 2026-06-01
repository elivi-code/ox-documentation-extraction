---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: usage
role_description: "Usage guidelines derived from extracted MCP docs — no Figma Do/Don't examples available"
pipeline_stage: extracted
pipeline_note: "Revised 2026-05-11 — fabricated Figma pairs removed; guidelines derived from examples.md, props.md, accessibility.md"
audit_verdict: null
siblings:
  - "[[Badge/props]]"
  - "[[Badge/examples]]"
  - "[[Badge/tokens]]"
  - "[[Badge/accessibility]]"
  - "[[Badge/badge-pui]]"
tags:
  - oxygen
  - component/Badge
  - role/usage
  - stage/extracted
  - category/data_display
---

<!-- SOURCE: Derived from Oxygen MCP (examples.md, props.md) and accessibility.md -->
<!-- NOTE: No Figma "↳ Badge examples" Do/Don't card frames were found. -->
<!-- This file does NOT contain Figma-extracted pairs. See Gaps section. -->
<!-- REVISED: 2026-05-11 -->
<!-- COMPONENT: Badge -->

# Badge — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

Usage guidelines derived from the Oxygen MCP documentation and component API.
No Figma Do/Don't examples page was found for Badge — see [Gaps](#gaps).

---

## Counter badge

### Do — Pass only numeric values as children

The `children` prop accepts **numerical values only**. Use whole numbers for counts up to two digits; use `"99+"` for overflow beyond that.

```tsx
<Badge>4</Badge>
<Badge>12</Badge>
<Badge>99+</Badge>
```

**Source:** `props.md` — `children` description: "Rendered element inside the badge (numerical value only)"

---

### Don't — Put non-numeric content in a counter badge

Avoid icons, strings, or arbitrary text as `children`. The counter badge is sized and styled for numeric values; non-numeric content will overflow or render incorrectly.

```tsx
{/* Wrong */}
<Badge>New</Badge>
<Badge>★</Badge>
```

---

## Dot badge

### Do — Omit children to render a dot indicator

A dot badge signals presence or activity without a count. Render it by passing no children and setting `size="small"`.

```tsx
<Badge size="small" />
```

---

### Don't — Add children to a dot badge

Adding text or numbers to a `size="small"` badge turns it into a counter and breaks the dot affordance.

```tsx
{/* Wrong — makes it a counter, not a dot */}
<Badge size="small">1</Badge>
```

---

## Badge vs. AIBadge

### Do — Use AIBadge for AI-related features

`AIBadge` renders a star icon alongside text and is purpose-built for AI feature labelling. It inherits all standard HTML `div` attributes.

```tsx
import { AIBadge } from '@8x8/oxygen-badge';

<AIBadge />         {/* renders "AI" with star */}
<AIBadge>Beta</AIBadge>
```

---

### Don't — Use Badge to label AI features

`Badge` is for notification counts and presence indicators. Using it for AI labels loses the semantic star icon and misrepresents the component's purpose.

```tsx
{/* Wrong */}
<Badge>AI</Badge>
```

---

## Conditional visibility

### Do — Render badge conditionally based on app state

Badges should appear only when relevant. Permanently rendering an empty badge wastes DOM space and can confuse screen readers.

```tsx
{hasUnread && <Badge size="small" aria-hidden="true" />}
{unreadCount > 0 && <Badge>{unreadCount}</Badge>}
```

---

## Accessibility

### Do — Place the accessible count on the parent, hide the badge itself

Badge is a passive display element. Use `aria-hidden="true"` on the badge and carry the count in the parent's `aria-label`.

```tsx
<IconButton
  icon={<BellIcon />}
  aria-label={`Notifications, ${count} unread`}
>
  <Badge isInner aria-hidden="true">{count}</Badge>
</IconButton>
```

For dynamically-updated counts, add `aria-live="polite"` to the parent region, not the badge itself.

**Source:** `accessibility.md`

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No "↳ Badge examples" page with Do/Don't card frames found in Figma. Guidelines above are derived from MCP docs and props API. If Figma examples are added in the future, re-run `figma-extract-usage` and merge. |
| Screenshots | SOURCE_GAP | No local PNG screenshots. No Figma nodes to reference. |

---

_Source: Oxygen MCP (`@8x8/oxygen-badge`) · Derived from examples.md, props.md, accessibility.md · Revised 2026-05-11_
