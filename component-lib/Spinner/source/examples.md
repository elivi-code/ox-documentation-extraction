---
component: Spinner
package: "@8x8/oxygen-loaders"
category: feedback_status
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Spinner/props]]"
  - "[[Spinner/tokens]]"
  - "[[Spinner/accessibility]]"
  - "[[Spinner/Spinner-figma]]"
  - "[[Spinner/Spinner-audit]]"
tags:
  - oxygen
  - component/Spinner
  - role/examples
  - stage/blocked
  - category/feedback_status
---
# Spinner — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [Spinner-figma.md](Spinner-figma.md) · [Spinner-usage.md](Spinner-usage.md)

## Basic usage

```tsx
import { Spinner } from '@8x8/oxygen-loaders';

<Spinner aria-label="Loading" />
```

## Sizes

### Small — inline/compact contexts

```tsx
<Spinner size="small" aria-label="Loading" />
```

Use for loading small parts of the UI — cards, dropdown menus, overflow menus.

### Default — general purpose

```tsx
<Spinner size="default" aria-label="Loading" />
```

The standard choice for loading a whole page or large section.

### Large (`large2x`) — prominent display

```tsx
<Spinner size="large2x" aria-label="Loading" />
```

## With supporting text

```tsx
<Spinner size="small" text="Example text" />
```

Always include supporting text where space permits. The `text` prop replaces the need for an explicit `aria-label` when the spinner has a visible label — see [accessibility.md](accessibility.md) for details.

_Source: Oxygen MCP · Extracted 2026-05-05_
