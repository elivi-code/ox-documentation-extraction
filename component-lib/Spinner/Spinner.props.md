---
parent: "[[Spinner]]"
section: props
component: Spinner
package: "@8x8/oxygen-loaders"
pipeline_stage: draft
siblings:
  - "[[Spinner]]"
  - "[[Spinner.anatomy]]"
  - "[[Spinner.tokens]]"
  - "[[Spinner.usage]]"
  - "[[Spinner.accessibility]]"
  - "[[Spinner.platform]]"
  - "[[Spinner.composition]]"
tags:
  - oxygen
  - component/Spinner
  - role/props
---

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

<!-- SKIP:GAP-003 manual="All defaults show '—' — verify actual defaults from @8x8/oxygen-loaders source before populating the Default column" -->

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `size` | `number \| keyof typeof spinnerSize` | No | — | Size of the spinner. Accepted string keys: `"small"`, `"default"`, `"large2x"`. Can also accept a raw number. |
| `strokeWidth` | `number` | No | — | Width of the spinner stroke. |
| `hasAnimation` | `boolean` | No | — | Whether the spinner plays its rotation animation. |
| `text` | `string` | No | — | Supporting text displayed alongside the spinner. |
| `testId` | `string` | No | — | Test ID for automated testing (`data-testid`). |

<!-- SKIP:GAP-002 manual="strokeWidth and hasAnimation have empty descriptions — verify behaviour from @8x8/oxygen-loaders source or Storybook before writing descriptions" -->

### `spinnerSize` key values

From usage examples the following named sizes are available:

| Key | Description |
|-----|-------------|
| `"small"` | Inline / compact contexts (cards, dropdowns, overflow menus) |
| `"default"` | General purpose — typical full-page or section loading |
| `"large2x"` | Large spaces requiring a visually prominent spinner |

<!-- CONFLICT:GAP-011 finding="large2x: documented in code (spinnerSize enum, Storybook examples) but absent from Figma component set — Figma only defines default and small; one source is stale — verify whether large2x Figma variant exists in a different file, was intentionally removed, or was renamed" HUMAN DECISION REQUIRED -->

<!-- CONFLICT:GAP-010 finding="isInverted: Figma component set exposes isInverted as a first-class variant axis (values: no/yes) for placement on dark/coloured backgrounds; the React component (@8x8/oxygen-loaders) has no isInverted prop — unclear whether (a) theme/surface context auto-handles inversion, (b) an isInverted prop is missing from the package, or (c) design-only intent requiring consuming teams to apply CSS/theming" HUMAN DECISION REQUIRED -->

_Source: Oxygen MCP · Extracted 2026-05-05_
