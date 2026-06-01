---
parent: "[[AlertBanner]]"
component: AlertBanner
section: props
role: spoke-props
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/props
  - stage/rewritten
---

# AlertBanner — Props

## Installation

```bash
# yarn
yarn add @8x8/oxygen-alert-banner

# npm
npm install @8x8/oxygen-alert-banner
```

> **Registry prerequisite:** Connect to the 8x8 VPN and configure the Artifactory registry before installing.

## Import

```tsx
import { AlertBanner } from '@8x8/oxygen-alert-banner';
```

## Props

| Prop | Type | Required | Default | Description | Accepts |
|------|------|----------|---------|-------------|---------|
| `children` | `ReactNode` | **Yes** | — | The message content rendered inside the banner | — |
| `actionText` | `string` | No | — | Label for the optional action button; when provided, the button is shown | — |
| `actionCallback` | `() => void` | No | — | Click handler for the action button | — |
| `iconAriaLabel` | `string` | No | — | Accessible label for the warning icon | — |
| `testId` | `string` | No | — | `data-testid` attribute for automated testing | — |

<!-- STUB:GAP-004 source="Escalate to Oxygen team to add official descriptions for actionText and actionCallback in the registry, or confirm the editorial descriptions are authoritative" -->

## Prop notes

**`children`** — Required. Accepts any React content but is typically a plain text string or a fragment with inline elements. Avoid complex interactive content inside the banner message.

**`actionText` / `actionCallback`** — These two props work together. Setting `actionText` without `actionCallback` renders the button label but it will not respond to clicks. The Figma design shows this as a Secondary button on the right (desktop) or below the text (mobile).

**`iconAriaLabel`** — The alert banner always renders a warning icon. If the icon conveys information not already expressed in `children`, set this label so screen-reader users receive the context. If the surrounding text already fully describes the alert, an empty string or omitting the prop may be appropriate.

## No variant / severity prop

The current Oxygen API does not expose a `type`, `variant`, or `severity` prop. The component renders with a single fixed amber/warning style. If your use case requires info, success, or error variants, raise a request with the design system team.

## Layout behaviour

The Figma design exposes two variant axes — `mode` (light | dark) and `breakpoint` (> 576 | < 576) — but neither is exposed as a consumer prop. Layout adapts automatically based on the container/viewport width; mode handling is not yet confirmed against the implementation.

<!-- CONFLICT:CONFLICT-001 finding="Figma component set exposes mode (light|dark) and breakpoint (>576|<576) variant axes. The Oxygen MCP returns 5 props; neither axis corresponds to a prop. Unconfirmed whether the component handles mode/breakpoint automatically (CSS media queries / theming context) or requires explicit parent-level wiring." HUMAN DECISION REQUIRED -->

<!-- STUB:GAP-003 source="After CONFLICT-001 resolved, add authoritative Layout behaviour note confirming mode and breakpoint are internal concerns" -->
