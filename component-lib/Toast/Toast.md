---
component: Toast
status: partial
version: ""
category: feedback_status
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=26764:41883"
package: "@8x8/oxygen-toast"
companion_package: "@8x8/oxygen-toaster"
variants:
  - success
  - error
  - warning
  - info
  - loading
sizes:
  - small
  - medium
  - large
props:
  - title: ReactNode
  - description: ReactNode
  - children: ReactNode
  - actions: Array<ActionType>
  - type: ToastType
  - size: ToastSize
  - hideCloseControl: boolean
  - onCloseControlClick: "() => void"
  - isToast: boolean
  - iconTitle: string
  - closeButtonLabel: string
subcomponents: []
related:
  - "[[AlertBanner]]"
  - "[[Modal]]"
  - "[[Spinner]]"
  - "[[ProgressBar]]"
  - "[[Tag]]"
patterns:
  - "[[action-confirmation]]"
  - "[[background-job-feedback]]"
tokens:
  - "[[token.ui.ui07]]"
  - "[[token.ui.shadow01]]"
  - "[[token.text.textColor09]]"
  - "[[token.icon.icon05]]"
  - "[[token.actions.action10]]"
  - "[[token.success.success02]]"
  - "[[token.error.error02]]"
  - "[[token.warning.warning01]]"
  - "[[token.info.info01]]"
  - "[[token.actions.action06]]"
  - "[[token.typography.bodyBold01]]"
  - "[[token.typography.body01]]"
spokes:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.usage]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.platform]]"
  - "[[Toast.composition]]"
role: hub
pipeline_stage: spec_ready
audit_verdict: partial
audit_date: "2026-05-15"
tags:
  - oxygen
  - component/Toast
  - role/hub
  - stage/spec_ready
  - category/feedback_status
---

## Overview

Toast is a transient, floating notification surface from `@8x8/oxygen-toast` that announces the outcome of an action or a system event without interrupting the user's flow. It renders with an intentionally inverted dark background (even in Light mode) for contrast against the app canvas, and carries five semantic `type` values — success, error, warning, info, loading — each mapped to a coloured left indicator bar. The companion package `@8x8/oxygen-toaster` provides a portal-based `Toaster` manager and a `notify()` imperative API for dispatching toasts from anywhere in the app without prop drilling.

## Spokes

- [[Toast.props]] — 11 Toast props including title, description, type, size, hideCloseControl; ActionType shape (`label`, `onClick`); InlineNotification props absent from MCP (GAP-004 open)
- [[Toast.anatomy]] — 10 anatomy elements across 3 Style variants (Full / Group collapsed / Group expanded) × 5 Types × 2 Modes; InlineNotification 3 elements across 5 types × 2 modes; transient states not modelled in Figma
- [[Toast.tokens]] — 12 confirmed tokens covering container background (inverted), shadow, text, icon, action links, type-specific indicator bars (5 types), and typography; 3 InlineNotification semantic token names unresolved pending Desktop Bridge (GAP-010 open); all spacing values hardcoded (GAP-008 open)
- [[Toast.usage]] — 7 Do/Don't pairs covering role urgency (alert vs status), auto-dismiss discipline, close control pairing, accessible label requirements, surface selection (Toast vs AlertBanner vs Modal vs InlineNotification), loading toast scope, and copy quality; editorial guidance (no Figma examples page exists)
- [[Toast.accessibility]] — keyboard (Tab, Enter/Space, Escape), ARIA (role="status" / role="alert" split by type), WCAG 2.1 AA checklist; all content inferred — no MCP or Figma source data (GAP-002 open)
- [[Toast.platform]] — no PUI requirements; all 5 candidate hooks/events/MFEs reviewed and rejected
- [[Toast.composition]] — used inside ToastStack (manual stacking) and Toaster (portal-managed queue); InlineNotification is the inline sibling; related to AlertBanner, Modal, Spinner, ProgressBar, Tag
