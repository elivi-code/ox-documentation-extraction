---
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[SkeletonCircle/props]]"
  - "[[SkeletonCircle/tokens]]"
  - "[[SkeletonCircle/accessibility]]"
  - "[[SkeletonCircle/SkeletonCircle-figma]]"
  - "[[SkeletonCircle/SkeletonCircle-audit]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/examples
  - stage/blocked
  - category/feedback_status
---
# SkeletonCircle — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [SkeletonCircle-figma.md](SkeletonCircle-figma.md)

---

> **DATA GAP:** The Oxygen MCP returned 0 clean examples for the `skeletons` package. Examples below are derived from usage documentation and Figma design context. No additional Storybook stories were found.

---

## Basic usage

```tsx
import { SkeletonCircle } from '@8x8/oxygen-skeletons';

// Replace a medium avatar while loading
<SkeletonCircle size="40px - medium" />
```

---

## Avatar placeholder

```tsx
import { SkeletonCircle } from '@8x8/oxygen-skeletons';

// Large avatar (e.g. profile header)
<SkeletonCircle size="80px - xlarge" />

// Standard contact list avatar
<SkeletonCircle size="48px - large" />

// Compact list avatar
<SkeletonCircle size="40px - medium" />
```

---

## Icon placeholder

```tsx
import { SkeletonCircle } from '@8x8/oxygen-skeletons';

// Small icon slot
<SkeletonCircle size="24px - xsmall" />

// Tiny indicator icon
<SkeletonCircle size="16px - xsmall" />
```

---

## Combined with SkeletonBlock (contact row)

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

// Skeleton for a contact row: avatar + name + status
<div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
  <SkeletonCircle size="40px - medium" />
  <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
    <SkeletonBlock size="20px - body01" />
    <SkeletonBlock size="16px - label01" />
  </div>
</div>
```

---

_Source: Oxygen MCP · Figma design context · Extracted 2026-05-05_
