---
parent: "[[Modal]]"
section: composition
component: Modal
role: spoke
pipeline_stage: published
audit_verdict: partial
siblings:
  - "[[Modal]]"
  - "[[Modal.props]]"
  - "[[Modal.anatomy]]"
  - "[[Modal.tokens]]"
  - "[[Modal.usage]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.platform]]"
tags:
  - oxygen
  - component/Modal
  - role/spoke
  - stage/published
---

## Package components

The `@8x8/oxygen-modal` package exports five components that compose together:

| Component | Default export | Composition role |
|-----------|---------------|-----------------|
| `Modal` | ✓ | Root — creates portal on `document.body`, owns focus trap |
| `ModalPortal` | — | Headless root — no auto-portal; consumer supplies DOM target |
| `ModalHeader` | — | Structural child — title + optional close icon button |
| `ModalContent` | — | Structural child — scrollable body area |
| `ModalFooter` | — | Structural child — action button row with optional divider |

---

## Containment structure

`Modal` (or `ModalPortal`) is the root. `ModalHeader`, `ModalContent`, and `ModalFooter` are structural children passed via `children`:

```tsx
<Modal onClose={onClose}>
  <ModalHeader title="Dialog title" onClose={onClose} />
  <ModalContent>Body content</ModalContent>
  <ModalFooter>
    <Button>Action</Button>
  </ModalFooter>
</Modal>
```

None of the three structural children are required by the component API — `children` is unrestricted — but all three are expected in production usage.

---

## Figma sub-components (Atoms)

The Figma design exposes two reusable atoms used inside both component sets:

| Sub-component | Node ID | Used in |
|--------------|---------|---------|
| `_footer` | `29083:47566` | Custom Modal, Dialog Modal |
| `_header` | `43118:1490` | Custom Modal, Dialog Modal |

The `_header` atom contains:
- `Title` frame (text + optional `Icon Button` for close)
- `Icon Button` instance — the rendered close icon; maps to `ModalHeader`'s `onClose` / `iconCloseTitle` props

The `_footer` atom variants (`stacked?`, `divider`, `textButton`, `secondaryButton`) map to the button hierarchy described in [[Modal.usage]].

---

## Used with

- **[[Button]]** — always rendered inside `ModalFooter` for primary, secondary, and destructive actions
- **[[Icon]]** — the close icon inside `_header` is an Icon Button instance
- **[[Select]], [[Popover]]** — when rendered inside `ModalContent`, the `portalRef` prop must be wired to avoid z-index conflicts

---

## ModalPortal for cross-MFE use

Use `ModalPortal` instead of `Modal` when:
- The portal container must be a specific DOM node (not `document.body`)
- The modal is rendered across MFE boundaries where shell ownership of the portal target matters
- You need `initialFocus` without the auto-portal behaviour

```tsx
import { ModalPortal, ModalHeader, ModalContent, ModalFooter } from '@8x8/oxygen-modal';

<ModalPortal onClose={onClose} initialFocus={false}>
  <ModalHeader title="Dialog" onClose={onClose} />
  <ModalContent>Content goes here</ModalContent>
  <ModalFooter>
    <Button onClick={onClose}>Confirm</Button>
  </ModalFooter>
</ModalPortal>
```

---

## Design documentation links

- Oxygen usage: https://oxygen.8x8.com/patterns/modal/usage
- Icon Button: https://zeroheight.com/714056d2f/p/75909b-icons/b/1725fe
- Button: https://oxygen.8x8.com/docs/components/button/usage

_Source: Figma MCP (claude.ai) + Oxygen MCP · Extracted 2026-05-01_
