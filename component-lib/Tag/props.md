# Tag — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [Tag-figma.md](Tag-figma.md)

## Package

```
@8x8/oxygen-tag
```

### Installation

```sh
# yarn
$ yarn add @8x8/oxygen-tag

# npm
$ npm install @8x8/oxygen-tag
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
import { Tag } from '@8x8/oxygen-tag';
```

---

## Tag

A pill-shaped component used to label, categorize, or organize items using keywords. Supports two visual variants — Standard (with optional leading icon) and Avatar (with a fixed avatar image) — selected automatically by the presence of the `avatar` prop.

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | No | Component content (the label) |
| `variant` | `Variant` | `'default'` | No | Color variant (see values below) |
| `avatar` | `Pick<AvatarProps, 'name' \| 'src' \| 'isGroup'>` | — | No | When provided, renders an Avatar Tag instead of a Standard Tag |
| `action` | `React.MouseEventHandler<HTMLDivElement>` | — | No | Click handler for the remove (×) button. When provided, the close button is rendered (`type=withAction` in Figma) |
| `actionProps` | `React.HTMLAttributes<HTMLDivElement>` | — | No | Extra props applied to the remove-button `<div>` (e.g. `aria-label`, `data-*`) |
| `hasError` | `boolean` | `false` | No | Renders an error border around the tag. Maps to Figma `type=withActionError` (Avatar Tag) |
| `isFocused` | `boolean` | `false` | No | Forces the focused appearance — the focus ring becomes visible without keyboard interaction |
| `testId` | `string` | — | No | Value for the `data-testid` DOM attribute |

### `variant` values

The `Variant` type maps directly to the `color` axis in Figma:

| Value | Available on | Description |
|-------|--------------|-------------|
| `'default'` | Standard, Avatar | Neutral off-white (light) / neutral grey (dark) — the default tag appearance |
| `'blue'` | Standard, Avatar | Subtle blue background |
| `'grey'` | Standard, Avatar | Strong grey background with white text |
| `'red'` | Standard, Avatar | Subtle red — RAG status (Red) |
| `'yellow'` | Standard only | Subtle yellow — RAG status (Amber). **Not available on Avatar Tag.** |
| `'green'` | Standard only | Subtle green — RAG status (Green). **Not available on Avatar Tag.** |
| `'yellow-emphasis'` | Standard, Avatar | Solid yellow — emphasized warning |

> **Note:** Variant value enumeration is not returned by Oxygen MCP (`Variant` type alias).
> Values listed here are extracted from the Figma `color` variant axis.

### `avatar` shape

When provided, switches the Tag to **Avatar Tag** mode. The component uses these properties to render an `Avatar` on the leading edge.

| Property | Type | Description |
|----------|------|-------------|
| `name` | `string` | Used to generate avatar initials when `src` is not provided |
| `src` | `string` | URL of the avatar image |
| `isGroup` | `boolean` | Renders the avatar as a group avatar |

### `action` and `actionProps`

When `action` is set, the Tag renders a remove (×) button at the trailing edge.
The Figma `type=withAction` variant matches this state. Use `actionProps` to provide
the accessible label (`aria-label="Remove [tag]"`) and any data attributes.

### `hasError`

Adds a red error border (`error01`) around the tag. In Figma this is the
`type=withActionError` variant on Avatar Tag — confirm that this prop also affects
Standard Tag in code.

### `isFocused`

Programmatically renders the focused ring without requiring keyboard focus. Use sparingly
(e.g. when controlling focus from a parent select component).

---

## Variant matching: code vs Figma

| Figma variant axis | Code prop |
|---|---|
| `mode` (light/dark) | Inherited from theme provider — not a direct prop |
| `color` (default, blue, grey, red, yellow, green, yellow-emphasis) | `variant` |
| `type` (default, withAction, withActionError) | Combination of `action` (presence) and `hasError` |
| `icon?` boolean (Standard Tag only) | Implicit — pass an icon via `children` or use a wrapper |
| `↪ icon` instance swap | Pass an icon as the first child or via a slot pattern |
| `focus?` boolean | `isFocused` |
| Avatar/Standard form | Switched by `avatar` prop presence |

> **Gap:** The Oxygen Tag component appears to render its leading icon via `children` rather than a dedicated `icon` prop. Verify how an icon is supplied in code — it may be the first React element in `children`.

---

_Source: Oxygen MCP (`@8x8/oxygen-tag`) · Figma node 8083:8359 · Extracted 2026-05-01_
