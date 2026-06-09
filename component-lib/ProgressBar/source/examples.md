---
component: ProgressBar
package: "@8x8/oxygen-loaders"
category: feedback_status
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[ProgressBar/props]]"
  - "[[ProgressBar/tokens]]"
  - "[[ProgressBar/accessibility]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-usage]]"
  - "[[ProgressBar/ProgressBar-audit]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/examples
  - stage/spec_ready
  - category/feedback_status
---
# ProgressBar — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [ProgressBar-usage.md](ProgressBar-usage.md) · [ProgressBar-figma.md](ProgressBar-figma.md)

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

const step = 5;
const [progress, setProgress] = useState(0);

useEffect(() => {
  const interval = setInterval(() => {
    setProgress(prev => Math.min(prev + step, 100));
  }, 1000);
  return () => clearInterval(interval);
}, [step]);

<ProgressBar value={progress} text="Loading..." />
```

## Text swap (controlled)

Manage the `text` prop in tandem with `value` to confirm state changes to all users:

```tsx
import React from 'react';
import { ProgressBar } from '@8x8/oxygen-loaders';

function UploadProgress({ uploadPercent }: { uploadPercent: number }) {
  const label = uploadPercent >= 100 ? 'Complete' : 'Uploading...';
  return (
    <ProgressBar
      value={uploadPercent}
      text={label}
      fullWidth
      aria-label={label}
    />
  );
}
```

_Source: Oxygen MCP · Extracted 2026-05-05_
