---
component: AlertBanner
package: "@8x8/oxygen-alertBanner"
category: feedback_status
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[AlertBanner/props]]"
  - "[[AlertBanner/tokens]]"
  - "[[AlertBanner/accessibility]]"
  - "[[AlertBanner/alert-banner-figma]]"
  - "[[AlertBanner/alert-banner-audit]]"
tags:
  - oxygen
  - component/AlertBanner
  - role/examples
  - stage/blocked
  - category/feedback_status
---
# AlertBanner — Examples

> **See also:** [alert-banner-figma.md](./alert-banner-figma.md) · [props.md](./props.md) ·
> [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) ·
> [alert-banner-usage.md](./alert-banner-usage.md)

---

## Basic usage

Minimal alert with a message only:

```tsx
import { AlertBanner } from '@8x8/oxygen-alert-banner';

<AlertBanner>
  Something went wrong. Please try again or contact your administrator.
</AlertBanner>
```

---

## With action button

When the user can take a corrective action, pair the message with `actionText` and
`actionCallback`:

```tsx
<AlertBanner
  actionText="Retry"
  actionCallback={() => retryOperation()}
>
  Your session has expired.
</AlertBanner>
```

---

## With accessible icon label

When the warning icon adds context not covered by the message text, supply
`iconAriaLabel`:

```tsx
<AlertBanner
  iconAriaLabel="Warning"
  actionText="View details"
  actionCallback={() => openDetails()}
>
  Scheduled maintenance begins in 30 minutes.
</AlertBanner>
```

---

## With test ID

```tsx
<AlertBanner testId="maintenance-banner">
  The system will be unavailable between 02:00 and 04:00 UTC.
</AlertBanner>
```

---

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

---

## Layout behaviour (from Figma)

The component adapts its internal layout based on viewport / container width:

| Breakpoint | Layout | Banner height |
|------------|--------|--------------|
| ≥ 576 px | Horizontal — icon · message · button in a single row | 56 px |
| < 576 px | Vertical — icon + message stacked above button | 104 px |

This is handled automatically by the component; no prop is needed.

---

## Storybook documentation story

The only example in the MCP registry is a Storybook documentation wrapper — not a
standalone usage snippet. The clean examples above are derived from the Figma design
and prop definitions.

```tsx
// From AlertBanner.documentation.stories.tsx
export const AlertBannerDocs: StoryFn<AlertBannerProps> = args => {
  const argsWithDefaults = { ...args };
  return (
    <>
      <Doc markdown>{README}</Doc>
      <Doc markdown>{exampleAlertBanner}</Doc>
      <ComponentSection block>
        <AlertBanner {...argsWithDefaults} />
      </ComponentSection>
      <Doc markdown>{CHANGELOG}</Doc>
    </>
  );
};
```

---

_Source: Oxygen MCP · Figma design · Extracted 2026-04-28_
