---
parent: "[[Badge]]"
section: props
---

## Package

```
@8x8/oxygen-badge
```

```tsx
import { Badge, AIBadge } from '@8x8/oxygen-badge';
```

## Badge props

| Name | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | No | Numerical value or overflow string only. Use whole numbers (e.g. `4`, `12`) or `'99+'` for counts exceeding two digits. Do not pass icons, arbitrary text, or other ReactNode content. |
| `type` | `'primary' \| 'secondary'` | `'primary'` | No | Visual/colour variant of the badge |
| `size` | `'small' \| 'medium' \| 'big'` | `'medium'` | No | Size of the badge |
| `isInner` | `boolean` | `false` | No | When `true`, renders the badge inside its parent wrapper (absolute positioning) |
| `testId` | `string` | `'BADGE'` | No | Value for the `data-testid` DOM attribute |

### `type` values

| Value | Description |
|-------|-------------|
| `'primary'` | Default teal (`notification01`) badge — used for notification counts and dot indicators |
| `'secondary'` | Alternative style variant |

### `size` values

| Value | Description |
|-------|-------------|
| `'small'` | Smallest badge — used for dot-only indicators |
| `'medium'` | Default size — standard notification count |
| `'big'` | Largest size |

### `isInner`

When `true` the badge is absolutely positioned inside its parent wrapper element. Set to `false` (default) when you want to position the badge yourself via CSS.

## AIBadge props

A specialised badge for AI-related features. Displays a star icon alongside text content. Inherits all standard HTML `div` attributes (`className`, `style`, `onClick`, etc.).

| Name | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | `'AI'` | No | Content to display next to the star icon |
| `testId` | `string` | `'AI_BADGE'` | No | Value for the `data-testid` DOM attribute |

## Figma design variants vs. code props

The Figma design file uses a `type` prop with values `counter | dot | mention`. These map to code usage as follows:

| Figma `type` | Code equivalent |
|---|---|
| `counter` | `<Badge size="medium">{count}</Badge>` — pill with numeric children |
| `dot` | `<Badge size="small" />` — no children |
| `mention` | `<Badge size="medium">@</Badge>` or rendered with an `@` icon as children |
