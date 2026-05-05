# SlideOut — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

> **SOURCE_GAP:** The Oxygen MCP returned 0 clean examples for SlideOut (`get-component-examples` with `cleanExamples: true`). The only available example is the raw Storybook documentation story, reproduced below with minimal cleanup. Clean usage examples are not available from the MCP source at this time.

## Basic toggle (from Storybook documentation story)

```tsx
import { useState } from 'react';
import { SlideOut } from '@8x8/oxygen-slide-out';
import { Button } from '@8x8/oxygen-button';

export function SlideOutExample() {
  const [isVisible, setIsVisible] = useState(false);
  const [currentWidth, setCurrentWidth] = useState<number | undefined>(undefined);

  const toggleIsVisible = () => setIsVisible(!isVisible);

  const handleResize = (newWidth: number) => {
    setCurrentWidth(newWidth);
  };

  return (
    <>
      <Button onClick={toggleIsVisible}>Toggle SlideOut</Button>
      <SlideOut isVisible={isVisible} onResize={handleResize}>
        <div>Content</div>
        <div>
          {currentWidth
            ? `Current width ${currentWidth}`
            : '<------ Drag left margin to resize'}
        </div>
      </SlideOut>
    </>
  );
}
```

### Key patterns shown
- `isVisible` is controlled externally via state — the component is **controlled**, not self-managing its open/close state.
- `onResize` receives the new pixel width as the argument and is used to track current dimensions.
- `children` are arbitrary React nodes rendered inside the panel.

_Source: Oxygen MCP · Extracted 2026-05-05_
