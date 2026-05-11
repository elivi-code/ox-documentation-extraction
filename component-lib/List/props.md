---
component: List
package: "@8x8/oxygen-list"
category: data_display
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - pui
  - audit
siblings:
  - "[[List/examples]]"
  - "[[List/tokens]]"
  - "[[List/accessibility]]"
  - "[[List/List-figma]]"
  - "[[List/List-pui]]"
  - "[[List/List-audit]]"
tags:
  - oxygen
  - component/List
  - role/props
  - stage/blocked
  - category/data_display
---

# List — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-list

# npm
$ npm install @8x8/oxygen-list
```

> **Registry prerequisite:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc` (or equivalent in `.yarnrc.yml`). VPN required.

## Import

```tsx
import { List, ListItem } from '@8x8/oxygen-list';
```

---

## `List`

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | Yes | Rendered item content; should be `ListItem` components |
| `isGroup` | `boolean` | `false` | No | Styles the list as a group |
| `isOrdered` | `boolean` | `false` | No | Renders an ordered list |
| `withBackground` | `boolean` | `false` | No | Applies a background to the list |
| `theme` | `ListTheme` | _(Oxygen theme provider)_ | No | Theme object; defaults come from `@8x8/oxygen-config` and `@8x8/oxygen-constants` via the internal theme provider |

---

## `ListItem`

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | Yes | Item content |
| `title` | `string` | — | No | Title attribute for the item element |
| `isDisabled` | `boolean` | — | No | Marks the item as disabled |
| `isActive` | `boolean` | — | No | Marks the item as active/selected |
| `shouldWrapText` | `boolean` | — | No | Controls whether text wraps inside the item |
| `onClick` | `(e: React.MouseEvent<HTMLLIElement>) => void` | — | No | Click event handler |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
