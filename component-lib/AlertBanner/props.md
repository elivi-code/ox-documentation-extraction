---
component: AlertBanner
package: "@8x8/oxygen-alertBanner"
category: feedback_status
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[AlertBanner/examples]]"
  - "[[AlertBanner/tokens]]"
  - "[[AlertBanner/accessibility]]"
  - "[[AlertBanner/alert-banner-figma]]"
  - "[[AlertBanner/alert-banner-audit]]"
tags:
  - oxygen
  - component/AlertBanner
  - role/props
  - stage/blocked
  - category/feedback_status
---
# AlertBanner — Props

> **See also:** [alert-banner-figma.md](./alert-banner-figma.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Installation

```bash
# yarn
yarn add @8x8/oxygen-alert-banner

# npm
npm install @8x8/oxygen-alert-banner
```

> **Registry prerequisite:** You must be connected to the 8x8 VPN and have the
> Artifactory registry configured before installing.
>
> **npm** — add to `.npmrc` in your project root:
> ```
> @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
> ```
>
> **yarn** — add to `.yarnrc.yml` in your project root:
> ```yaml
> npmScopes:
>   8x8:
>     npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
>
> nodeLinker: node-modules
> ```

---

## Import

```tsx
import { AlertBanner } from '@8x8/oxygen-alert-banner';
```

---

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | **Yes** | — | The message content rendered inside the banner |
| `actionText` | `string` | No | — | Label for the optional action button; when provided, the button is shown |
| `actionCallback` | `() => void` | No | — | Click handler for the action button |
| `iconAriaLabel` | `string` | No | — | Accessible label for the warning icon |
| `testId` | `string` | No | — | `data-testid` attribute for automated testing |

### Prop notes

**`children`** — Required. Accepts any React content but is typically a plain text string
or a fragment with inline elements. Avoid complex interactive content inside the banner
message.

**`actionText` / `actionCallback`** — These two props work together. Setting `actionText`
without `actionCallback` renders the button label but it will not respond to clicks.
The Figma design shows this as a "Secondary button" on the right (desktop) or below the
text (mobile).

**`iconAriaLabel`** — The alert banner always renders a warning icon. If the icon conveys
information not already expressed in `children`, set this label so screen-reader users
receive the context. If the surrounding text already fully describes the alert, an empty
string or omitting the prop may be appropriate (confirm with the a11y team).

---

## No variant / severity prop

The current Oxygen API does not expose a `type`, `variant`, or `severity` prop. The
component renders with a single fixed amber/warning style. If your use case requires
info, success, or error variants, raise a request with the design system team.

---

_Source: Oxygen MCP · Extracted 2026-04-28_
