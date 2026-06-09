---
component: Modal
status: partial
category: layout_overlay
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=2625-167"
variants: [Custom Modal, Dialog Modal]
props:
  - children: ReactNode
  - targetNode: Element|ReactElement
  - isVisible: boolean
  - hasShadow: boolean
  - shouldCloseOnEsc: boolean
  - shouldCloseOnOverlayClick: boolean
  - allowOutsideClick: boolean|function
  - size: enum
  - width: string
  - height: string
  - onClose: function
  - shouldUseFocusTrap: boolean
  - initialFocus: function|element|string|false
  - portalRef: Ref
  - disableAutoFocus: boolean
  - focusAfterCloseItemRef: RefObject
  - modalProps: object
  - testId: string
  - theme: object
subcomponents: ["[[ModalHeader]]", "[[ModalContent]]", "[[ModalFooter]]", "[[ModalPortal]]"]
related: ["[[Button]]", "[[Icon]]"]
patterns: []
tokens:
  - "[[--ui/ui06]]"
  - "[[--ui/shadow01]]"
  - "[[--ui/ui01]]"
  - "[[--text/textcolor01]]"
  - "[[--text/textcolor02]]"
  - "[[--text/textcolor09]]"
  - "[[--actions/action02]]"
  - "[[--actions/action08]]"
  - "[[--actions/action09]]"
  - "[[typography/heading01]]"
  - "[[typography/body01]]"
  - "[[typography/bodyBold01]]"
  - "[[--ui/ui22]]"
  - "[[--ui/ui23]]"
spokes:
  - "[[Modal.props]]"
  - "[[Modal.anatomy]]"
  - "[[Modal.tokens]]"
  - "[[Modal.usage]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.platform]]"
  - "[[Modal.composition]]"
role: hub
pipeline_stage: published
audit_verdict: partial
tags:
  - oxygen
  - component/Modal
  - role/hub
  - stage/published
  - category/layout_overlay
---

## Overview

Modal renders child components into a `document.body` portal that traps focus until the dialog is dismissed. It ships with four structural sub-components — ModalHeader, ModalContent, ModalFooter, and a headless ModalPortal variant for cross-MFE rendering. Reserve Modal for tasks the user must complete before continuing; use Toast or AlertBanner for non-blocking notifications.

## Spokes

- [[Modal.props]] — 19 Modal props including children, size, shouldUseFocusTrap, initialFocus; 10 ModalHeader props; ModalFooter and ModalContent accept standard HTML attributes
- [[Modal.anatomy]] — 2 component sets (Custom Modal, Dialog Modal), 3 layers each (_header, content, _footer), 3 variant axes (mode, breakpoint, scrollbar/message)
- [[Modal.tokens]] — 14 tokens covering surface (background, shadow, border), typography (heading01, body01, bodyBold01), text color, and footer action buttons
- [[Modal.usage]] — 7 Do/Don't pairs covering modal intent, focus trap, overlay dismissal, destructive actions, footer limits, dismissibility, size selection
- [[Modal.accessibility]] — keyboard (Tab, Shift+Tab, Escape, Enter/Space), ARIA (role=dialog, aria-modal, aria-labelledby, aria-describedby), focus management (trap, initial focus, return focus)
- [[Modal.platform]] — no PUI requirements
- [[Modal.composition]] — 5 package components; Modal wraps ModalHeader, ModalContent, ModalFooter; ModalPortal for headless/cross-MFE use; used with Button for footer actions
