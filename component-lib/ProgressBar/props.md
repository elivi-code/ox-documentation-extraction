---
component: ProgressBar
package: "@8x8/oxygen-loaders"
category: feedback_status
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[ProgressBar/examples]]"
  - "[[ProgressBar/tokens]]"
  - "[[ProgressBar/accessibility]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-usage]]"
  - "[[ProgressBar/ProgressBar-audit]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/props
  - stage/spec_ready
  - category/feedback_status
---
# ProgressBar — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [ProgressBar-usage.md](ProgressBar-usage.md)

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

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `number` | `0` | Percentage of completed progress (0–100) |
| `size` | `number \| string \| 'small' \| 'default' \| 'large'` | `'240px'` | Width of the progress bar; accepts named sizes or an explicit CSS dimension |
| `text` | `string` | `''` | Text label displayed below the progress bar |
| `fullWidth` | `boolean` | `false` | Stretches the bar to fill its container width |
| `testId` | `string` | — | Test ID for automated testing (`data-testid`) |

### `size` named values

| Value | Description |
|-------|-------------|
| `'small'` | Compact track height |
| `'default'` | Standard track height |
| `'large'` | Enlarged track height |

When `fullWidth` is `true`, the `size` prop controls track height rather than container width.

_Source: Oxygen MCP · Extracted 2026-05-05_
