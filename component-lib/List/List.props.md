---
parent: "[[List]]"
section: props
pipeline_stage: draft
tags:
  - component/List
  - role/props
---

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-list@<version>

# npm
$ npm install @8x8/oxygen-list@<version>
```

> **Version:** Replace `<version>` with the current release from Artifactory (`npm view @8x8/oxygen-list version` on the internal registry).

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
| `title` | `string` | — | No | HTML title attribute applied to the `<li>` element; appears as browser tooltip on hover; useful when item text is truncated |
| `isDisabled` | `boolean` | `false` | No | Marks the item as disabled |
| `isActive` | `boolean` | `false` | No | Marks the item as active/selected |
| `shouldWrapText` | `boolean` | — | No | When false, item text is clipped to a single line; when true (or unset), text wraps to multiple lines |
| `onClick` | `(e: React.MouseEvent<HTMLLIElement>) => void` | — | No | Click event handler |

<!-- STUB:GAP-004 source="Inspect @8x8/oxygen-list package exports and Storybook stories to confirm whether Destructive, Checkbox, Radio, Collapsible, Add Item, Sub Menu, and Remove Item variant patterns are achieved via child composition or undocumented props/exports; document findings here" -->

---

_Source: Oxygen MCP · Extracted 2026-05-08_
