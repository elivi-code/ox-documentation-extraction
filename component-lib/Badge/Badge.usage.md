---
parent: "[[Badge]]"
section: usage
---

## Usage guidelines

Guidelines derived from the Oxygen MCP documentation and component API.

<!-- STUB:GAP-006 source="If a '↳ Badge examples' page is created in the Figma file in the future, run figma-extract-usage for Badge and merge its pairs into badge-usage.md. No action available until Figma examples page exists." -->
> **Source gap:** No Figma "↳ Badge examples" page with Do/Don't card frames was found. The pairs below are **derived from MCP docs and the props API**, not Figma-sourced editorial content. Re-run `figma-extract-usage` and merge if an examples page is added.

### Counter badge

**Do — Pass only numeric values as children.** The `children` prop accepts numerical values only. Use whole numbers for counts up to two digits; use `"99+"` for overflow beyond that.

```tsx
<Badge>4</Badge>
<Badge>12</Badge>
<Badge>99+</Badge>
```

**Don't — Put non-numeric content in a counter badge.** Avoid icons, strings, or arbitrary text as `children`; the counter is sized and styled for numeric values and non-numeric content will overflow or render incorrectly.

```tsx
{/* Wrong */}
<Badge>New</Badge>
<Badge>★</Badge>
```

### Dot badge

**Do — Omit children to render a dot indicator.** A dot badge signals presence or activity without a count. Render it by passing no children and setting `size="small"`.

```tsx
<Badge size="small" />
```

**Don't — Add children to a dot badge.** Adding text or numbers to a `size="small"` badge turns it into a counter and breaks the dot affordance.

```tsx
{/* Wrong — makes it a counter, not a dot */}
<Badge size="small">1</Badge>
```

### Badge vs. AIBadge

**Do — Use AIBadge for AI-related features.** `AIBadge` renders a star icon alongside text and is purpose-built for AI feature labelling.

```tsx
import { AIBadge } from '@8x8/oxygen-badge';

<AIBadge />         {/* renders "AI" with star */}
<AIBadge>Beta</AIBadge>
```

**Don't — Use Badge to label AI features.** `Badge` is for notification counts and presence indicators. Using it for AI labels loses the semantic star icon and misrepresents the component's purpose.

```tsx
{/* Wrong */}
<Badge>AI</Badge>
```

### Conditional visibility

**Do — Render badge conditionally based on app state.** Badges should appear only when relevant. Permanently rendering an empty badge wastes DOM space and can confuse screen readers.

```tsx
{hasUnread && <Badge size="small" aria-hidden="true" />}
{unreadCount > 0 && <Badge>{unreadCount}</Badge>}
```

### Accessibility

**Do — Place the accessible count on the parent, hide the badge itself.** Badge is a passive display element. Use `aria-hidden="true"` on the badge and carry the count in the parent's `aria-label`. For dynamically-updated counts, add `aria-live="polite"` to the parent region, not the badge. See [[Badge.accessibility]].

```tsx
<IconButton
  icon={<BellIcon />}
  aria-label={`Notifications, ${count} unread`}
>
  <Badge isInner aria-hidden="true">{count}</Badge>
</IconButton>
```
