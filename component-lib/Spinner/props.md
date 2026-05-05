# Spinner — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
$ yarn add @8x8/oxygen-loaders

# npm
$ npm install @8x8/oxygen-loaders
```

**Registry prerequisite** — add to `.npmrc` (npm) or `.yarnrc.yml` (yarn) before installing:

```
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

> VPN required: you must be connected to the 8x8 VPN to access the private Artifactory registry.

## Import

```tsx
import { Spinner } from '@8x8/oxygen-loaders';
```

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `size` | `number \| keyof typeof spinnerSize` | No | — | Size of the spinner. Accepted string keys: `"small"`, `"default"`, `"large2x"`. Can also accept a raw number. |
| `strokeWidth` | `number` | No | — | Width of the spinner stroke. |
| `hasAnimation` | `boolean` | No | — | Whether the spinner plays its rotation animation. |
| `text` | `string` | No | — | Supporting text displayed alongside the spinner. |
| `testId` | `string` | No | — | Test ID for automated testing (`data-testid`). |

### `spinnerSize` key values

From usage examples the following named sizes are available:

| Key | Description |
|-----|-------------|
| `"small"` | Inline / compact contexts (cards, dropdowns, overflow menus) |
| `"default"` | General purpose — typical full-page or section loading |
| `"large2x"` | Large spaces requiring a visually prominent spinner |

_Source: Oxygen MCP · Extracted 2026-05-05_
