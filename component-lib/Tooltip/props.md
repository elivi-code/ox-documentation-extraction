---
component: Tooltip
package: "@8x8/oxygen-tooltip"
category: overlays_contextual
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Tooltip/examples]]"
  - "[[Tooltip/tokens]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-usage]]"
  - "[[Tooltip/Tooltip-pui]]"
  - "[[Tooltip/Tooltip-audit]]"
tags:
  - oxygen
  - component/Tooltip
  - role/props
  - stage/blocked
  - category/overlays_contextual
---
# Tooltip — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
yarn add @8x8/oxygen-tooltip

# npm
npm install @8x8/oxygen-tooltip
```

> **Registry prerequisite:** Add to `.npmrc`:
> `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/`
> Or `.yarnrc.yml` — see `get-project-setup` for full instructions. 8x8 VPN required.

## Import

```tsx
import Tooltip from '@8x8/oxygen-tooltip';
```

## Tooltip Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `title` | `ReactNode` | **Yes** | — | Content displayed inside the tooltip |
| `children` | `ReactNode` | No | — | The trigger element that the tooltip is anchored to |
| `orientation` | `Orientation` | No | `'top'` | Placement of the tooltip relative to its trigger. See Orientation values below. |
| `delay` | `number` | No | `300` | Show delay in milliseconds |
| `offset` | `OffsetOptions` | No | — | Fine-grained positioning offset from the anchor |
| `showOn` | `'hover' \| 'click'` | No | `'hover'` | Trigger type |
| `disableInteractive` | `boolean` | No | `false` | When true, the tooltip dismisses immediately when the cursor leaves the trigger (not interactive) |
| `disableDescribedBy` | `boolean` | No | `false` | When true, suppresses the `aria-describedby` binding on the trigger |
| `enableArrow` | `boolean` | No | `false` | Renders a directional arrow on the tooltip container |
| `triggerRef` | `HTMLElement` | No | — | External DOM element to use as the trigger instead of `children` |
| `customCloseHandlers` | `Handler[]` | No | — | Additional event handlers that dismiss the tooltip |
| `renderContainer` | `HTMLElement` | No | — | DOM node to portal the tooltip into |
| `renderContainerId` | `string` | No | — | ID of the DOM node to portal the tooltip into (alternative to `renderContainer`) |
| `includeWrapper` | `boolean` | No | — | Wraps `children` in a `<span>` to enable tooltip anchoring on non-forwardRef elements |
| `modifiers` | `{ offset?: { offset?: number \| string } }` | No | — | Low-level Popper modifier overrides |

### Orientation values

```
'top' | 'right' | 'bottom' | 'left'
'top-start' | 'top-end'
'bottom-start' | 'bottom-end'
'left-start' | 'left-end'
'right-start' | 'right-end'
```

## StaticTooltip

A companion component for rendering a tooltip in its always-visible state (not triggered by interaction). Useful for documentation, demos, and design alignment.

**Package:** `@8x8/oxygen-static-tooltip`

```bash
yarn add @8x8/oxygen-static-tooltip
npm install @8x8/oxygen-static-tooltip
```

```tsx
import StaticTooltip from '@8x8/oxygen-static-tooltip';
```

> **Note:** StaticTooltip props are not exposed via the Oxygen MCP. Only `children` is confirmed from examples. Refer to Figma or Storybook for full API.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
