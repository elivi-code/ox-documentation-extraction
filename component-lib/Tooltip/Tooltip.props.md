---
parent: "[[Tooltip]]"
section: props
---

## Props

### Tooltip

**Package:** `@8x8/oxygen-tooltip`

```bash
yarn add @8x8/oxygen-tooltip
npm install @8x8/oxygen-tooltip
```

```tsx
import Tooltip from '@8x8/oxygen-tooltip';
```

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `title` | `ReactNode` | **Yes** | — | Content displayed inside the tooltip |
| `children` | `ReactNode` | No | — | The trigger element the tooltip is anchored to |
| `orientation` | `Orientation` | No | `'top'` | Placement of the tooltip relative to its trigger |
| `delay` | `number` | No | `300 (inferred)` | Show delay in milliseconds |
| `offset` | `OffsetOptions` | No | — | Fine-grained positioning offset from the anchor |
| `showOn` | `'hover' \| 'click'` | No | `'hover' (inferred)` | Trigger type |
| `disableInteractive` | `boolean` | No | `false (inferred)` | When true, tooltip dismisses immediately on cursor leave |
| `disableDescribedBy` | `boolean` | No | `false (inferred)` | When true, suppresses `aria-describedby` on the trigger |
| `enableArrow` | `boolean` | No | `false (inferred)` | Renders a directional arrow on the tooltip container |
| `triggerRef` | `HTMLElement` | No | — | External DOM element to use as trigger instead of `children` |
| `customCloseHandlers` | `Handler[]` | No | — | Additional event handlers that dismiss the tooltip |
| `renderContainer` | `HTMLElement` | No | — | DOM node to portal the tooltip into |
| `renderContainerId` | `string` | No | — | ID of the DOM node to portal the tooltip into |
| `includeWrapper` | `boolean` | No | — | Wraps `children` in `<span>` to enable tooltip anchoring on non-forwardRef elements |
| `modifiers` | `{ offset?: { offset?: number \| string } }` | No | — | Low-level Popper modifier overrides |

<!-- STUB:GAP-003 source="Verify delay (300), showOn ('hover'), disableInteractive (false), disableDescribedBy (false), enableArrow (false) defaults in Storybook argsConfig or @8x8/oxygen-tooltip source; remove (inferred) once confirmed" -->
<!-- SKIP:GAP-004 manual="modifiers TypeScript signature is truncated in MCP output — full type unknown. Look up in @8x8/oxygen-tooltip TypeScript source." -->

### Orientation values

```
'top' | 'right' | 'bottom' | 'left'
'top-start' | 'top-end'
'bottom-start' | 'bottom-end'
'left-start' | 'left-end'
'right-start' | 'right-end'
```

### StaticTooltip

A companion component for always-visible tooltip state (not interaction-triggered). Useful for documentation, demos, and design alignment.

**Package:** `@8x8/oxygen-static-tooltip`

```bash
yarn add @8x8/oxygen-static-tooltip
npm install @8x8/oxygen-static-tooltip
```

```tsx
import StaticTooltip from '@8x8/oxygen-static-tooltip';
```

<!-- STUB:GAP-009 source="Extract StaticTooltip props from @8x8/oxygen-static-tooltip TypeScript source or Storybook; add full props table here. Only `children` is confirmed from examples." -->

---

## Code examples

> **Note:** All examples below are inferred from props, usage docs, and component behaviour. No Storybook-sourced snippets are available.
<!-- SKIP:GAP-005 manual="All examples are inferred — no Storybook-sourced snippets. Extract from https://oxygen.8x8.dev/packages/release/latest/?path=/story/components-tooltip--tooltip-documentation and replace." -->
<!-- STUB:GAP-006 source="Add Light vs Dark mode side-by-side example once GAP-005 (Storybook) is resolved." -->
<!-- STUB:GAP-007 source="Add customCloseHandlers and modifiers usage examples once GAP-004 (full modifiers type) is resolved." -->

### Basic usage

```tsx
<Tooltip title="More information about this item">
  <button>Hover me</button>
</Tooltip>
```

### Orientation variants

```tsx
<Tooltip title="Top tooltip" orientation="top">
  <button>Top</button>
</Tooltip>

<Tooltip title="Bottom tooltip" orientation="bottom">
  <button>Bottom</button>
</Tooltip>

<Tooltip title="Left tooltip" orientation="left">
  <button>Left</button>
</Tooltip>

<Tooltip title="Right tooltip" orientation="right">
  <button>Right</button>
</Tooltip>
```

#### Fine-grained placement

```tsx
<Tooltip title="Top-start aligned" orientation="top-start">
  <button>Top start</button>
</Tooltip>

<Tooltip title="Bottom-end aligned" orientation="bottom-end">
  <button>Bottom end</button>
</Tooltip>
```

### With arrow

```tsx
<Tooltip title="With directional arrow" enableArrow>
  <button>Hover</button>
</Tooltip>
```

### Click trigger

```tsx
<Tooltip title="Shown on click" showOn="click">
  <button>Click me</button>
</Tooltip>
```

### Custom delay

```tsx
<Tooltip title="Appears after 500ms" delay={500}>
  <button>Slow tooltip</button>
</Tooltip>
```

### Non-interactive tooltip (dismisses instantly on leave)

```tsx
<Tooltip title="Disappears immediately" disableInteractive>
  <button>Hover</button>
</Tooltip>
```

### External trigger via triggerRef

```tsx
const triggerRef = useRef<HTMLElement>(null);

<span ref={triggerRef}>External trigger</span>
<Tooltip title="Anchored to external ref" triggerRef={triggerRef.current} />
```

### Wrapping non-forwardRef elements

```tsx
<Tooltip title="Wrapped component" includeWrapper>
  <MyCustomComponent />
</Tooltip>
```

### Portal to custom container

```tsx
<Tooltip title="Portalled tooltip" renderContainerId="tooltip-root">
  <button>Hover</button>
</Tooltip>
```

### ReactNode title (rich content)

```tsx
<Tooltip title={<span><strong>Bold label:</strong> extra detail</span>}>
  <button>Rich tooltip</button>
</Tooltip>
```

> **Content rule:** Tooltip content should be plain text in the vast majority of cases. Interactive elements (links, buttons) inside tooltips are not accessible for some users. Max 140 characters (English). The ReactNode form shown above is technically valid but contradicts the plain-text content rule — prefer string `title` for all production usage.

### StaticTooltip (always visible)

```tsx
import StaticTooltip from '@8x8/oxygen-static-tooltip';

<StaticTooltip>Tooltip always visible</StaticTooltip>
```
