# ProgressBar — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic usage

```tsx
import { ProgressBar } from '@8x8/oxygen-loaders';

<ProgressBar value={50} aria-label="Loading 50%" />
```

## Sizes

```tsx
<ProgressBar value={30} size="small" aria-label="Loading 30%" />
<ProgressBar value={30} size="default" aria-label="Loading 30%" />
<ProgressBar value={30} size="large" aria-label="Loading 30%" />
```

## Full width

```tsx
<ProgressBar value={30} fullWidth aria-label="Loading 30%" />
```

## With text label

```tsx
<ProgressBar value={30} text="Loading data..." size="small" />
<ProgressBar value={30} text="Loading data..." size="default" />
<ProgressBar value={30} text="Loading data..." size="large" />
```

## Complete states

```tsx
<ProgressBar value={99} fullWidth text="Loading..." />
<ProgressBar value={100} fullWidth text="Complete" />
```

## Animated (controlled)

Using `useState` + `useEffect` to drive progress over time:

```tsx
import React, { useEffect, useState } from 'react';
import { ProgressBar } from '@8x8/oxygen-loaders';

const [progress, setProgress] = useState(0);

useEffect(() => {
  const interval = setInterval(() => {
    setProgress(prev => Math.min(prev + step, 100));
  }, 1000);
  return () => clearInterval(interval);
}, [step]);

<ProgressBar value={progress} text="Loading..." />
```

_Source: Oxygen MCP · Extracted 2026-05-05_
