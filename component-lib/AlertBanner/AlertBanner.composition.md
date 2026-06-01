---
parent: "[[AlertBanner]]"
component: AlertBanner
section: composition
role: spoke-composition
pipeline_stage: rewritten
audit_verdict: NO
tags:
  - oxygen
  - component/AlertBanner
  - role/spoke/composition
  - stage/rewritten
---

# AlertBanner — Composition

AlertBanner is a leaf component in most page layouts. It contains a warning [[Icon]] and an optional Secondary [[Button]], and is itself typically placed at the top of a page region or app shell.

## Basic usage

Minimal alert with a message only:

```tsx
import { AlertBanner } from '@8x8/oxygen-alert-banner';

<AlertBanner>
  Something went wrong. Please try again or contact your administrator.
</AlertBanner>
```

## With action button

When the user can take a corrective action, pair the message with `actionText` and `actionCallback`:

```tsx
<AlertBanner
  actionText="Retry"
  actionCallback={() => retryOperation()}
>
  Your session has expired.
</AlertBanner>
```

## With accessible icon label

When the warning icon adds context not covered by the message text, supply `iconAriaLabel`:

```tsx
<AlertBanner
  iconAriaLabel="Warning"
  actionText="View details"
  actionCallback={() => openDetails()}
>
  Scheduled maintenance begins in 30 minutes.
</AlertBanner>
```

## With test ID

```tsx
<AlertBanner testId="maintenance-banner">
  The system will be unavailable between 02:00 and 04:00 UTC.
</AlertBanner>
```

## Full example

```tsx
<AlertBanner
  iconAriaLabel="Warning"
  actionText="Contact support"
  actionCallback={() => openSupportModal()}
  testId="alert-banner-main"
>
  Hello. Uh oh! Something very specific went wrong. Please contact your supervisor or admin.
</AlertBanner>
```

## Layout behaviour

The component adapts its internal layout based on viewport / container width:

| Breakpoint | Layout | Banner height |
|------------|--------|--------------|
| ≥ 576 px | Horizontal — icon · message · button in a single row | 56 px |
| < 576 px | Vertical — icon + message stacked above button | 104 px |

Handled automatically by the component; no prop is needed. See [[AlertBanner.anatomy]] for the underlying variant axes.

## Containment

| Contains | Role |
|----------|------|
| [[Icon]] | Fixed warning icon |
| [[Button]] (Secondary) | Optional action — rendered when `actionText` is provided |

## Common patterns

- App shell — placed at the top of a page region to communicate a persistent system-level warning (session expiry, connectivity loss, scheduled maintenance).
- Workflow guard — paired with a corrective action button (retry, reconnect, contact support).

<!-- STUB:GAP-011 source="Request official usage examples from the Oxygen team or validate the editorial examples above against the real component in a test environment. All snippets currently derived from Figma design + prop definitions, not MCP-sourced." -->

<!-- STUB:GAP-012 source="Add edge-case examples once validated: actionText with missing actionCallback, very long message text causing line-wrap, ReactNode children (non-string). Skill rule: do not invent — confirm behaviour in a test environment first." -->
