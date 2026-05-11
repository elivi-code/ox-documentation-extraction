---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - usage
  - pui
siblings:
  - "[[Badge/examples]]"
  - "[[Badge/tokens]]"
  - "[[Badge/accessibility]]"
  - "[[Badge/badge-pui]]"
  - "[[Badge/badge-usage]]"
tags:
  - oxygen
  - component/Badge
  - role/props
  - stage/extracted
  - category/data_display
---
# Badge — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Package

```
@8x8/oxygen-badge
```

### Installation

```sh
# yarn
$ yarn add @8x8/oxygen-badge

# npm
$ npm install @8x8/oxygen-badge
```

> **Registry required (8x8 VPN needed):**
>
> `.npmrc`:
> ```
> @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
> ```
>
> `.yarnrc.yml`:
> ```yaml
> npmScopes:
>   8x8:
>     npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
> nodeLinker: node-modules
> ```

### Import

```tsx
import { Badge, AIBadge } from '@8x8/oxygen-badge';
```

---

## Badge

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | No | Rendered element inside the badge (numerical value only) |
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

---

## AIBadge

A specialised badge for AI-related features. Displays a star icon alongside text content. Inherits all standard HTML `div` attributes (`className`, `style`, `onClick`, etc.).

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | `'AI'` | No | Content to display next to the star icon |
| `testId` | `string` | `'AI_BADGE'` | No | Value for the `data-testid` DOM attribute |

---

## Figma design variants vs. code props

The Figma design file uses a `type` prop with values `counter | dot | mention`. These map to code usage as follows:

| Figma `type` | Code equivalent |
|---|---|
| `counter` | `<Badge size="medium">{count}</Badge>` — pill with numeric children |
| `dot` | `<Badge size="small" />` — no children |
| `mention` | `<Badge size="medium">@</Badge>` or rendered with an `@` icon as children |

---

_Source: Oxygen MCP (`@8x8/oxygen-badge`) · Figma node 2565:14 · Extracted 2026-04-29_
