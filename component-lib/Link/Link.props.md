---
component: Link
parent: "[[Link]]"
section: props
pipeline_stage: draft
siblings:
  - "[[Link.anatomy]]"
  - "[[Link.tokens]]"
  - "[[Link.usage]]"
  - "[[Link.accessibility]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-props
---

## Props

| Name | Type | Default | Required | Description | Accepts |
|------|------|---------|----------|-------------|---------|
| `children` | `ReactNode` | — | No | Link label content | — |
| `href` | `string` | — | No | URL the link navigates to — passed to the underlying `<a>` element | — |
| `icon` | `ReactNode` | — | No | ReactNode displayed alongside the link label; typically an external-link or directional icon. | [[Icon]] |
| `isChat` | `boolean` | `false` | No | Applies chat-surface color tokens (`$action05`/`$action07` depending on surface) | — |
| `standalone` | `false` | `false` | No | Constrains to inline variant — see CONFLICT below | — |
| `size` | `never` | — | No | Not applicable to the inline variant — see CONFLICT below | — |
| `testId` | `string` | — | No | `data-testid` attribute for automated testing | — |

> `Link` forwards a ref to `<HTMLAnchorElement>` and accepts all standard HTML anchor attributes (`href`, `target`, `rel`, `aria-label`, etc.) via prop spread.

<!-- STUB:GAP-003 source="Storybook/MCP exports inline-only shape (standalone: false, size: never). Figma documents a Standalone variant with size: Small | Large not currently reflected in the React API. Confirm with @8x8/oxygen-link source whether a StandaloneLinkProps shape exists as a separate export or is planned." -->

<!-- STUB:GAP-004 source="Check @8x8/oxygen-link source for isInverted prop. If it exists, add to this table. If CSS-only, document as theming consideration in tokens spoke." -->

## Variants

| Variant | Description |
|---------|-------------|
| Inline | Default. Inherits surrounding typography size and style. No explicit `size` control. |
| Standalone | Separated from body content. Uses `$body02` typography. Available in Small and Large. |

## States

| State | Description |
|-------|-------------|
| Rest | Default appearance |
| Hover | Visual feedback on hover |
| Active | Press/click state |
| Focus | Keyboard focus ring |
| Visited | Distinct visited color (`$textColor08`) |

## Installation

```bash
yarn add @8x8/oxygen-link
# or
npm install @8x8/oxygen-link
```

> Registry prerequisite: add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc`. VPN connection to 8x8 required.

## Import

```tsx
import { Link } from '@8x8/oxygen-link';
```
