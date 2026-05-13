---
component: Label
package: "@8x8/oxygen-label"
category: data_display
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - pui
  - audit
siblings:
  - "[[Label/examples]]"
  - "[[Label/tokens]]"
  - "[[Label/accessibility]]"
  - "[[Label/Label-figma]]"
  - "[[Label/label-pui]]"
  - "[[Label/label-usage]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/props
  - stage/blocked
  - category/data_display
---
# Label — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [label-usage.md](label-usage.md)

## Installation

```bash
# yarn
$ yarn add @8x8/oxygen-label

# npm
$ npm install @8x8/oxygen-label
```

> **Registry prerequisite:** Add the 8x8 Artifactory registry to `.npmrc` or `.yarnrc.yml` and connect to 8x8 VPN before installing.

```
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

## Import

```tsx
import Label from '@8x8/oxygen-label';
import { ActionTarget } from '@8x8/oxygen-label';
```

## Props — `Label`

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `value` | `ReactNode` | No | — | Label text or content |
| `htmlFor` | `string` | No | — | Associates the label with a form element by its `id` |
| `isRequired` | `boolean` | No | `false` | Appends a required indicator to the label |
| `isDisabled` | `boolean` | No | `false` | Renders the label in a disabled state |
| `shouldWrapText` | `boolean` | No | — | Allows label text to wrap to multiple lines |
| `showTooltipOnOverflow` | `boolean` | No | — | Shows a tooltip when the label text overflows its container |
| `action` | `ActionProps['action']` | No | — | Callback for the optional inline action link |
| `actionLabel` | `string` | No | — | Visible text for the inline action link |
| `actionTarget` | `ActionTarget` | No | — | Target behaviour for the action link (`_blank`, `_self`, etc.) |
| `otherActionProps` | `Record<string, unknown>` | No | — | Additional props forwarded to the action element |
| `infoBoxText` | `ReactNode` | No | — | Content rendered inside the info box tooltip |
| `infoBoxShowOn` | `keyof typeof showOn` | No | — | Trigger for displaying the info box (`hover`, `click`, etc.) |
| `infoBoxButtonLabel` | `string` | No | — | Accessible label for the info box trigger button |
| `testId` | `string` | No | — | `data-testid` attribute for automated testing |

## Secondary export — `ActionTarget`

`ActionTarget` is a named export from `@8x8/oxygen-label`. It represents the target type for the action link. No props are documented in the MCP — use it as a type import when typing the `actionTarget` prop.

```tsx
import { ActionTarget } from '@8x8/oxygen-label';
```

_Source: Oxygen MCP · Extracted 2026-05-01_
