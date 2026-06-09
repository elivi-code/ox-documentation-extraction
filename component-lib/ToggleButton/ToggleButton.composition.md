---
parent: "[[ToggleButton]]"
section: composition
pipeline_stage: draft
tags:
  - oxygen
  - component/ToggleButton
  - role/spoke
  - section/composition
---

## Subcomponents

| Subcomponent | Relationship | Notes |
|---|---|---|
| `ToggleButtonGroup` | exported wrapper | Stacks or aligns multiple `ToggleButton` instances; provides vertical (default) or horizontal layout via `isHorizontal` |
| Toggle Input | internal fixed sub-component | The 40×24px pill switch rendered inside every `Toggle`; not individually importable (Figma design concept, rendered internally when `label=null`) |

## Related components

| Component | Relationship | Notes |
|---|---|---|
| [[IconButton]] | peer — placed adjacent | Per Figma, an Icon Button may be placed to the **right** of a Toggle with a 4px gap (`$spacing02`). The two elements are separate focus stops. |
| [[Tooltip]] | peer — triggered by info icon | Rendered inside `ToggleButton` when `infoBoxText` is set; the info icon opens the Tooltip on click. |
| [[Radio]] | alternative | Use Radio for single-select from a list of mutually-exclusive options; do not use Toggle for list selection. |
| [[Checkbox]] | alternative | Use Checkbox inside a form with a Save button; use Toggle for immediate-effect binary settings. |

## Composition patterns

### ToggleButton inside ToggleButtonGroup

```tsx
import ToggleButton, { ToggleButtonGroup } from '@8x8/oxygen-toggle-button';

<ToggleButtonGroup>
  <ToggleButton label="Option A" name="group" value="a" isChecked={a} onChange={handleA} />
  <ToggleButton label="Option B" name="group" value="b" isChecked={b} onChange={handleB} />
  <ToggleButton label="Option C" name="group" value="c" isChecked={c} onChange={handleC} />
</ToggleButtonGroup>
```

Gap between stacked Toggle items: 8px (`$spacing03`).

### ToggleButton + IconButton (adjacent pair)

```tsx
{/* Icon Button sits to the RIGHT of Toggle; gap = 4px ($spacing02) */}
<div style={{ display: 'flex', alignItems: 'center', gap: '4px' }}>
  <ToggleButton label="Setting" name="setting" value="on" isChecked={isChecked} onChange={handleChange} />
  <IconButton aria-label="Learn more about this setting" icon={<InfoIcon />} size="iconSizeM" />
</div>
```

Both elements are separate focus stops (each has its own focus ring).

### ToggleButtonGroup with composed error state

`ToggleButtonGroup` does not expose an `isError` prop. Compose a validation message as a sibling element below the group using the `--error/error01` token.

```tsx
<>
  <ToggleButtonGroup>
    <ToggleButton label="Marketing" name="prefs" value="marketing" isChecked={a} onChange={fa} />
    <ToggleButton label="Product"   name="prefs" value="product"   isChecked={b} onChange={fb} />
  </ToggleButtonGroup>
  {error && <p role="alert" style={{ color: 'var(--error-error01)', marginTop: 8 }}>{error}</p>}
</>
```

See [[ToggleButton.usage]] Pair 5 and [[ToggleButton.anatomy]] for the Figma `isError` CONFLICT detail.

### Toggle Group with Slot (Figma)

In Figma, the Toggle Group contains a Slot component — a placeholder instance that designers swap with actual multi-toggle content via the instance swapper. In code this maps to passing `ToggleButton` children directly to `ToggleButtonGroup`.

_Source: Figma MCP · Oxygen MCP · Extracted 2026-04-29_
