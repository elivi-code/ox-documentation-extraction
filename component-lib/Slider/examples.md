# Slider — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [slider-pui.md](slider-pui.md)

## Basic — controlled single-thumb

```tsx
import { Slider } from '@8x8/oxygen-slider';
import { useState } from 'react';

function VolumeControl() {
  const [value, setValue] = useState(50);

  return (
    <Slider
      value={value}
      minValue={0}
      maxValue={100}
      step={1}
      ariaLabel="Ring volume"
      onChange={setValue}
    />
  );
}
```

## With drag callbacks

```tsx
<Slider
  value={value}
  onChange={setValue}
  onDragStart={() => console.log('drag started')}
  onDragEnd={() => console.log('drag ended')}
  ariaLabel="Ring volume"
/>
```

## Disabled state

```tsx
<Slider
  value={50}
  isDisabled
  ariaLabel="Ring volume"
/>
```

## Range (two-thumb) mode

```tsx
import { useState } from 'react';

function RangeSlider() {
  const [range, setRange] = useState<[number, number]>([20, 80]);

  return (
    <Slider
      isMultiple
      value={range}
      minValue={0}
      maxValue={100}
      step={5}
      onChange={setRange}
      ariaLabel="Volume range"
    />
  );
}
```

## Track-draggable range

```tsx
<Slider
  isMultiple
  isTrackDraggable
  value={[30, 70]}
  onChange={setRange}
  ariaLabel="Adjustable range"
/>
```

## Expanded hit areas (accessibility / touch)

```tsx
<Slider
  value={value}
  onChange={setValue}
  expandTrackAreaBy="8px"
  expandKnobAreaBy="8px"
  ariaLabel="Ring volume"
/>
```

## Storybook documentation story (internal reference)

```tsx
// Slider.documentation.stories.tsx
export const SliderDocumentation = (args: typeof argsConfig) => {
  const [value, setValue] = useState(args.value);

  useEffect(() => {
    setValue(args.value);
  }, [args.value]);

  return (
    <>
      <Doc markdown>{README}</Doc>
      <Doc markdown>{example}</Doc>
      <ComponentSection>
        <Slider
          {...args}
          value={value}
          onChange={newValue => {
            setValue(newValue);
            action('onChange')(newValue);
          }}
        />
      </ComponentSection>
      <Doc markdown>{CHANGELOG}</Doc>
    </>
  );
};
```

## Figma design reference — "Audio Volume" pattern

The Figma component ("Audio Volume", node `22902:37514`) demonstrates the canonical usage
of the Slider for audio/volume control, with:

- Optional label above ("Ring volume")
- `volume-off` icon on the left side
- Slider track in the centre
- `volume-up` icon on the right side
- States: Default, Hover, Active, Focus, Disabled
- Modes: Light and Dark

_Source: Oxygen MCP + Figma (UI-components · 5YihJ5WuDvnvrlrRMC4sBp) · Extracted 2026-04-29_
