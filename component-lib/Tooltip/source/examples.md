---
component: Tooltip
package: "@8x8/oxygen-tooltip"
category: overlays_contextual
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Tooltip/props]]"
  - "[[Tooltip/tokens]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-usage]]"
  - "[[Tooltip/Tooltip-pui]]"
  - "[[Tooltip/Tooltip-audit]]"
tags:
  - oxygen
  - component/Tooltip
  - role/examples
  - stage/blocked
  - category/overlays_contextual
---
# Tooltip — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic usage

```tsx
import Tooltip from '@8x8/oxygen-tooltip';

<Tooltip title="More information about this item">
  <button>Hover me</button>
</Tooltip>
```

## Orientation variants

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

### Fine-grained placement

```tsx
<Tooltip title="Top-start aligned" orientation="top-start">
  <button>Top start</button>
</Tooltip>

<Tooltip title="Bottom-end aligned" orientation="bottom-end">
  <button>Bottom end</button>
</Tooltip>
```

## With arrow

```tsx
<Tooltip title="With directional arrow" enableArrow>
  <button>Hover</button>
</Tooltip>
```

## Click trigger

```tsx
<Tooltip title="Shown on click" showOn="click">
  <button>Click me</button>
</Tooltip>
```

## Custom delay

```tsx
<Tooltip title="Appears after 500ms" delay={500}>
  <button>Slow tooltip</button>
</Tooltip>
```

## Non-interactive tooltip (dismisses instantly on leave)

```tsx
<Tooltip title="Disappears immediately" disableInteractive>
  <button>Hover</button>
</Tooltip>
```

## External trigger via triggerRef

```tsx
const triggerRef = useRef<HTMLElement>(null);

<span ref={triggerRef}>External trigger</span>
<Tooltip title="Anchored to external ref" triggerRef={triggerRef.current} />
```

## Wrapping non-forwardRef elements

```tsx
<Tooltip title="Wrapped component" includeWrapper>
  <MyCustomComponent />
</Tooltip>
```

## Portal to custom container

```tsx
<Tooltip title="Portalled tooltip" renderContainerId="tooltip-root">
  <button>Hover</button>
</Tooltip>
```

## ReactNode title (rich content)

```tsx
<Tooltip title={<span><strong>Bold label:</strong> extra detail</span>}>
  <button>Rich tooltip</button>
</Tooltip>
```

> **Content rule:** Tooltip content should be plain text in the vast majority of cases. Interactive elements (links, buttons) inside tooltips are not accessible for some users. Max 140 characters (English).

## StaticTooltip (always visible)

```tsx
import StaticTooltip from '@8x8/oxygen-static-tooltip';

<StaticTooltip>Tooltip always visible</StaticTooltip>
```

---

> **Note:** The Oxygen MCP returned no clean code snippets for Tooltip. Examples above are inferred from props, usage docs, and component behaviour. Verify against Storybook before use in production.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
