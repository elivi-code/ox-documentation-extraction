# SkeletonBlock — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [SkeletonBlock-figma.md](SkeletonBlock-figma.md)

---

> **DATA GAP:** The Oxygen MCP returned 0 clean examples for the `skeletons` package. The example below is derived from the Storybook documentation story and usage documentation. No additional Storybook stories were found.

---

## Basic usage

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

// Block skeleton — replaces a body01 text line
<SkeletonBlock size="20px - body01" />

// Circle skeleton — replaces an avatar
<SkeletonCircle size="medium" />
```

---

## Text content placeholder

Replace a paragraph of text while it loads. Use `spacing03` (8px) between lines.

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

// Simulating a heading + two body lines
<div style={{ display: 'flex', flexDirection: 'column', gap: '8px' }}>
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

---

## Image placeholder

Replace an image or card thumbnail while content loads.

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

<SkeletonBlock size="custom - image" />
```

---

## Card skeleton (combined)

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

// Skeleton for a card with an avatar, title, and body text
<div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
  <SkeletonCircle size="medium" />
  <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
    <SkeletonBlock size="22px - body02" />
    <SkeletonBlock size="16px - label01" />
  </div>
</div>
```

---

## Storybook documentation story (from MCP)

```tsx
// Skeletons.documentation.stories.tsx
export const SkeletonDocumentation = ({
  customSize,
  ...initialArgs
}: typeof argsConfig & { customSize?: string }) => {
  const args = {
    ...initialArgs,
    ...(customSize && { size: customSize }),
  };

  return (
    <>
      <Doc markdown>{README}</Doc>
      <Doc markdown>{example}</Doc>
      <Doc>
        <h2><code>SkeletonBlock</code></h2>
      </Doc>
      <ComponentSection block>
        <SkeletonBlock {...args} />
      </ComponentSection>
      <Doc>
        <h2><code>SkeletonCircle</code></h2>
      </Doc>
      <ComponentSection>
        <SkeletonCircle {...args} />
      </ComponentSection>
      <Doc markdown>{CHANGELOG}</Doc>
    </>
  );
};

SkeletonDocumentation.storyName = 'Documentation';
SkeletonDocumentation.args = argsConfig;
SkeletonDocumentation.argTypes = argTypesConfig;
```

---

_Source: Oxygen MCP · Extracted 2026-05-05_
