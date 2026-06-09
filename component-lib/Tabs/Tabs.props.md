---
parent: "[[Tabs]]"
section: props
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/props
---

## Props

### `<Tabs>` (default export)

Package: `@8x8/oxygen-tabs` · Category: layout

| Name | Type | Default | Required | Description | Accepts |
|------|------|---------|----------|-------------|---------|
| `children` | `ReactNode` | — | ✅ | One or more `<Tab>` elements | [[Tab]] |
| `color` | `"light" \| "dark"` | — | | Color mode | — |
| `forwardedRef` | `object \| func` | `null` | ✅ | Component ref | — |

<!-- SKIP:GAP-008 manual="Check @8x8/oxygen-tabs source for color prop default on <Tabs>; document in props.md." -->

> **WARN-001:** `forwardedRef` is listed as required with a `null` default. This implies the component accepts a null ref gracefully, but the API is ambiguous — downstream type generation may emit a non-optional ref parameter.

---

### `<Tab>` (named export)

Package: `@8x8/oxygen-tabs` · Category: layout

| Name | Type | Default | Required | Description | Accepts |
|------|------|---------|----------|-------------|---------|
| `children` | `ReactNode` | — | ✅ | Tab label content | — |
| `color` | `"light" \| "dark"` | — | | Color mode | — |
| `value` | `any` | — | | Value passed to `onClick` handler | — |
| `isActive` | `boolean` | `false` | | Whether this tab is the active/selected tab | — |
| `isDisabled` | `boolean` | `false` | | Makes the tab non-interactive | — |
| `isStretched` | `boolean` | `false` | | Stretches tab to fill available space in `<Tabs>` | — |
| `onClick` | `(ev: React.MouseEvent, value: any) => void` | `noop` | | Click handler; called with event and the tab's `value` | — |
| `testId` | `string` | `'TABS'` | | `data-testid` attribute for automated testing | — |

<!-- SKIP:GAP-007 manual="Verify isStretched behaviour from @8x8/oxygen-tabs source or Storybook; update description if incorrect (currently inferred — MCP returned eslint-disable comment instead of real doc string)." -->
<!-- SKIP:GAP-008 manual="Check @8x8/oxygen-tabs source for color prop default on <Tab>; document in props.md." -->

---

## Figma design properties

### `tabs` component set (node `85651:78740`)

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `state` | Variant: `"rest" \| "hover"` | `"rest"` | Interaction state |
| `isSelected` | Variant: `"false" \| "true"` | `"false"` | Active/selected state (maps to `isActive` in code) |
| `isDisabled` | Variant: `"false" \| "true"` | `"false"` | Disabled state |
| `tabLabel` | Text | `"Label"` | Tab display label |
| `icon` | Boolean | `false` | Show an icon alongside the label |
| `selectIcon` | Instance swap | chevron icon | The icon component to render |
| `badge` | Boolean | `false` | Show a notification badge on the tab |
| `isFocus` | Boolean | `false` | Force focus ring visible (for prototyping) |
| `hasDropdown` | Boolean | `false` | Active when only this tab is visible; transforms tab into a popover trigger |

### `tabsDisclosure` component (node `85651:78793`)

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `badge` | Boolean | `false` | Show a notification badge on the disclosure button |

---

## Installation

```sh
yarn add @8x8/oxygen-tabs
# or
npm install @8x8/oxygen-tabs
```

**Registry prerequisite** — configure the 8x8 Artifactory registry:

```ini
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

```yaml
# .yarnrc.yml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
nodeLinker: node-modules
```

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
