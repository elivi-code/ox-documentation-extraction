---
component: AlertBanner
package: "@8x8/oxygen-alert-banner"
status: draft
category: feedback_status
role: hub
pipeline_stage: rewritten
audit_verdict: NO
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=13899-15489"
variants:
  - mode=light, breakpoint=> 576
  - mode=dark, breakpoint=> 576
  - mode=light, breakpoint=< 576
  - mode=dark, breakpoint=< 576
props:
  - children: ReactNode
  - actionText: string
  - actionCallback: function
  - iconAriaLabel: string
  - testId: string
subcomponents:
  - "[[Icon]]"
  - "[[Button]]"
related:
  - "[[Toast]]"
  - "[[Modal]]"
  - "[[Dialog]]"
patterns:
  - "[[AppShell]]"
tokens:
  - "[[token.warning.warning01]]"
  - "[[token.text.textColor07]]"
  - "[[token.icon.icon08]]"
  - "[[token.actions.action02]]"
  - "[[token.text.textColor09]]"
  - "[[token.typography.body01]]"
  - "[[token.typography.labelBold01]]"
spokes:
  - "[[AlertBanner.props]]"
  - "[[AlertBanner.anatomy]]"
  - "[[AlertBanner.tokens]]"
  - "[[AlertBanner.usage]]"
  - "[[AlertBanner.accessibility]]"
  - "[[AlertBanner.platform]]"
  - "[[AlertBanner.composition]]"
tags:
  - oxygen
  - component
  - feedback_status
  - role/hub
  - stage/rewritten
---

# AlertBanner

## Overview

AlertBanner is a persistent, page-scoped warning strip. It uses a single fixed amber style to signal that a system-level condition requires the user's attention. The banner stays visible until the underlying condition is resolved — it is not dismissable.

> **Status: draft.** 2 unresolved CONFLICTs (mode/breakpoint handling, banner token identity) and 9 active SOURCE_GAPs remain. See spoke markers for details.

## Spokes

- [[AlertBanner.props]] — 5 props: `children`, `actionText`, `actionCallback`, `iconAriaLabel`, `testId`
- [[AlertBanner.anatomy]] — 8 elements across 4 variants (mode × breakpoint), no interaction states
- [[AlertBanner.tokens]] — 7 confirmed tokens covering background, text, icon, action label, dismiss icon, and typography
- [[AlertBanner.usage]] — 4 Do/Don't pairs covering urgency match, severity, action labelling, message copy
- [[AlertBanner.accessibility]] — ARIA role candidates, keyboard, focus, contrast pairs (ratios unverified)
- [[AlertBanner.platform]] — no PUI extract on file; likely no PUI surface
- [[AlertBanner.composition]] — contains [[Icon]] and optional [[Button]] (Secondary); commonly placed in app shell
