# Tabs — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [figma.md](figma.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-tabs

# npm
$ npm install @8x8/oxygen-tabs
```

**Registry prerequisite** — you must configure the 8x8 Artifactory registry before installing:

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

---

## `<Tabs>` (default export)

Package: `@8x8/oxygen-tabs` · Category: layout

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | ✅ | Component content (one or more `<Tab>` elements) |
| `color` | `"light" \| "dark"` | — | | Color mode |
| `forwardedRef` | `object \| func` | `null` | ✅ | Component ref |

---

## `<Tab>` (named export)

Package: `@8x8/oxygen-tabs` · Category: layout

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | ✅ | Tab content |
| `color` | `"light" \| "dark"` | — | | Color mode |
| `value` | `any` | — | | Value returned to `onClick` handler |
| `isActive` | `boolean` | `false` | | Whether this tab is the active/selected tab |
| `isDisabled` | `boolean` | `false` | | Whether this tab is non-interactive |
| `isStretched` | `boolean` | `false` | | Stretches tab to fill available space in `<Tabs>` |
| `onClick` | `(ev: React.MouseEvent, value: any) => void` | `noop` | | Click handler; called with the event and the tab's `value` |
| `testId` | `string` | `'TABS'` | | `data-testid` attribute value for automated testing |

---

## Figma design properties (`tabs` component set)

These are the Figma-side component properties (used when prototyping with the Figma component, node `85651:78740`):

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `state` | Variant: `"rest" \| "hover"` | `"rest"` | Interaction state |
| `isSelected` | Variant: `"false" \| "true"` | `"false"` | Active/selected state (maps to `isActive` in code) |
| `isDisabled` | Variant: `"false" \| "true"` | `"false"` | Disabled state |
| `tabLabel` | Text | `"Label"` | Tab display label |
| `icon` | Boolean | `false` | Show an icon alongside the label |
| `selectIcon` | Instance swap | icon node | The icon component to render |
| `badge` | Boolean | `false` | Show a notification badge on the tab |
| `isFocus` | Boolean | `false` | Force focus ring visible (for prototyping) |
| `hasDropdown` | Boolean | `false` | Active when only this tab is visible; transforms tab into a popover trigger |

## Figma design properties (`tabsDisclosure` component)

Overflow "more" button component (node `85651:78793`):

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `badge` | Boolean | `false` | Show a notification badge on the disclosure button |

---

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
