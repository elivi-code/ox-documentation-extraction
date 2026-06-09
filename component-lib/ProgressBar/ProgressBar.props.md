---
parent: "[[ProgressBar]]"
section: props
component: ProgressBar
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/ProgressBar
  - role/spoke
  - section/props
---

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-loaders

# npm
$ npm install @8x8/oxygen-loaders
```

> **Registry prerequisite:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc` (or equivalent `.yarnrc.yml` entry). 8x8 VPN access required.

## Import

```tsx
import { ProgressBar } from '@8x8/oxygen-loaders';
```

## Props

| Prop | Type | Default | Required | Description | Accepts |
|------|------|---------|----------|-------------|---------|
| `value` | `number` | `0` | false | Percentage of completed progress (0–100). When value reaches 100 the complete state is rendered (green fill, full track coverage). | — |
| `size` | `number \| string \| 'small' \| 'default' \| 'large'` | `'240px'` | false | Width of the progress bar; accepts named sizes or an explicit CSS dimension. When `fullWidth` is `true`, controls track height instead. | — |
| `text` | `string` | `''` | false | Text label displayed below the bar. Also satisfies the accessible name requirement; see [[ProgressBar.accessibility]]. | — |
| `fullWidth` | `boolean` | `false` | false | Stretches the bar to fill its container width. | — |
| `testId` | `string` | — | false | Test ID for automated testing (`data-testid`). | — |

### `size` named values

| Value | Description |
|-------|-------------|
| `'small'` | Compact track height |
| `'default'` | Standard track height |
| `'large'` | Enlarged track height |

When `fullWidth` is `true`, the `size` prop controls track height rather than container width.

<!-- STUB:GAP-002 source="Check @8x8/oxygen-loaders source or Storybook to determine pixel dimensions for small/default/large named sizes; add to size named values table" -->

> **WARN-002:** The `size` default `'240px'` may be the resolved pixel value of the `'default'` named size rather than a standalone default. Verify whether `size='default'` and `size='240px'` are equivalent before shipping docs.

## Theming

The Figma component set exposes a `mode` variant axis (`light` / `dark`). This variant has no corresponding Oxygen prop — light/dark theming is handled by the design-system `ThemeProvider` context, not at the component level.
