---
parent: "[[Label]]"
section: props
---

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

## Props

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `value` | `ReactNode` | — | No | Label text or content | — |
| `htmlFor` | `string` | — | No | Associates the label with a form element by its `id` | — |
| `isRequired` | `boolean` | `false` | No | Appends a required indicator (`*`) to the label | — |
| `isDisabled` | `boolean` | `false` | No | Renders the label in a disabled state | — |
| `shouldWrapText` | `boolean` | — | No | Allows label text to wrap to multiple lines | — |
| `showTooltipOnOverflow` | `boolean` | — | No | Shows a tooltip when the label text overflows its container | — |
| `action` | `ActionProps['action']` | — | No | Callback for the optional inline action link | — |
| `actionLabel` | `string` | — | No | Visible text for the inline action link | — |
| `actionTarget` | `ActionTarget` | — | No | Target behaviour for the action link (`_blank`, `_self`, etc.) | — |
| `otherActionProps` | `Record<string, unknown>` | — | No | Additional props forwarded to the action element | — |
| `infoBoxText` | `ReactNode` | — | No | Content rendered inside the info box tooltip | — |
| `infoBoxShowOn` | `keyof typeof showOn` | — | No | Trigger for displaying the info box (`hover`, `click`, etc.) | — |
| `infoBoxButtonLabel` | `string` | — | No | Accessible label for the info box trigger button | — |
| `testId` | `string` | — | No | `data-testid` attribute for automated testing | — |

<!-- STUB:GAP-001 source="Look up the showOn enum in @8x8/oxygen-label source and document accepted string values (e.g. hover, click) for infoBoxShowOn" -->
<!-- STUB:GAP-002 source="Expand the action type signature — ActionProps['action'] is an internal type; document the function signature (e.g. () => void or (event: MouseEvent) => void)" -->

## Secondary export — `ActionTarget`

`ActionTarget` is a named export from `@8x8/oxygen-label`. Use it as a type import when typing the `actionTarget` prop.

```tsx
import { ActionTarget } from '@8x8/oxygen-label';
```

_Source: Oxygen MCP · Extracted 2026-05-01_
