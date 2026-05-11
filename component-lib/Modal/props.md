---
component: Modal
package: "@8x8/oxygen-modal"
category: layout_overlay
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - pui
  - audit
siblings:
  - "[[Modal/examples]]"
  - "[[Modal/tokens]]"
  - "[[Modal/accessibility]]"
  - "[[Modal/Modal-figma]]"
  - "[[Modal/Modal-pui]]"
  - "[[Modal/Modal-audit]]"
tags:
  - oxygen
  - component/Modal
  - role/props
  - stage/spec_ready
  - category/layout_overlay
---
# Modal — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [Modal-figma.md](Modal-figma.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-modal

# npm
$ npm install @8x8/oxygen-modal
```

**Registry configuration required** — add to project root before installing:

```ini
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

---

## Package components

The `@8x8/oxygen-modal` package exports five components:

| Component | Default export | Description |
|-----------|---------------|-------------|
| `Modal` | ✓ | Main modal — renders children into a portal on `document.body` |
| `ModalPortal` | — | Headless portal variant; consumer manages portal target |
| `ModalHeader` | — | Header section with title, optional close button |
| `ModalFooter` | — | Footer section for action buttons |
| `ModalContent` | — | Scrollable content area |

---

## Modal props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | ✓ | Rendered content of the modal |
| `targetNode` | `Element \| React.ReactElement` | `window.document.body` | — | DOM node where the modal portal renders |
| `isVisible` | `boolean` | `true` | — | Visibility flag. Prefer conditional rendering over this prop |
| `hasShadow` | `boolean` | `true` | — | Whether the modal has a box-shadow |
| `shouldCloseOnEsc` | `boolean` | `true` | — | Whether `onClose` fires on Escape key press |
| `shouldCloseOnOverlayClick` | `boolean` | `false` | — | Whether `onClose` fires on overlay click |
| `allowOutsideClick` | `boolean \| ((e: MouseEvent) => boolean)` | — | — | If `true` or returns `true`, clicks outside the focus trap deactivate it and pass through to the clicked element |
| `size` | `'small' \| 'medium' \| 'big'` | `'medium'` | — | Preset size of the modal |
| `width` | `string` | — | — | Custom CSS width (overrides `size`) |
| `height` | `string` | — | — | Custom CSS height |
| `onClose` | `() => void` | — | — | Close callback; triggered by `shouldCloseOnEsc` or `shouldCloseOnOverlayClick` |
| `shouldUseFocusTrap` | `boolean` | `true` | — | Enables or disables the focus trap |
| `portalRef` | `React.RefObject<HTMLDivElement> \| ((instance: HTMLDivElement \| null) => void)` | — | — | Ref for a sibling node of the portal container; needed when Select or Popover renders inside the modal |
| `testId` | `string` | `'MODAL'` | — | `data-testid` DOM attribute |
| `theme` | `object` | _(from OX theme provider)_ | — | Theme object; provided automatically via `@8x8/oxygen-config` and `@8x8/oxygen-constants` |

---

## ModalPortal props

`ModalPortal` is the headless variant — it does not create its own portal target. It shares most props with `Modal`.

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | ✓ | Rendered content |
| `isVisible` | `boolean` | `true` | — | Visibility flag |
| `hasShadow` | `boolean` | `true` | — | Box-shadow toggle |
| `shouldCloseOnEsc` | `boolean` | `true` | — | Escape key close |
| `shouldCloseOnOverlayClick` | `boolean` | `false` | — | Overlay click close |
| `size` | `'small' \| 'medium' \| 'big'` | `'medium'` | — | Preset size |
| `width` | `string` | — | — | Custom CSS width |
| `height` | `string` | — | — | Custom CSS height |
| `onClose` | `() => void` | — | — | Close callback |
| `shouldUseFocusTrap` | `boolean` | `true` | — | Focus trap toggle |
| `initialFocus` | `HTMLElement \| SVGElement \| string \| false \| (() => HTMLElement \| SVGElement \| string \| false)` | — | — | Element to receive initial focus; set to `false` to prevent initial focus shift |
| `testId` | `string` | `'MODAL'` | — | `data-testid` DOM attribute |
| `theme` | `object` | _(from OX theme provider)_ | — | Theme object |

---

## ModalHeader props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | — | Optional content rendered below the `title` |
| `title` | `string` | `''` | — | Title string |
| `alignTitle` | `'left' \| 'right' \| 'center'` | `'left'` | — | Title alignment |
| `hasBorderBottom` | `boolean` | `false` | — | Whether the header shows a bottom border |
| `iconCloseTitle` | `string` | `'Close'` | — | `title` attribute on the close icon button (for accessibility) |
| `onClose` | `() => void` | — | — | Close icon click callback; close icon is only rendered when this is a function |
| `buttonCloseRef` | `React.Ref<HTMLButtonElement>` | — | — | Ref for the close button; useful for setting initial focus |
| `titleProps` | `object` | — | — | Additional props for the title element (e.g. manually set `id` for `aria-labelledby`) |
| `testId` | `string` | `'MODAL_HEADER'` | — | `data-testid` DOM attribute |
| `theme` | `object` | _(from OX theme provider)_ | — | Theme object |

---

## ModalFooter props

No documented props beyond standard HTML attributes. Renders children in a footer container.

---

## ModalContent props

No documented props beyond standard HTML attributes. Renders children in a scrollable content area.

---

## Additional props (from get-component-props)

These props are present in the TypeScript types but not in the main documentation:

| Prop | Type | Description |
|------|------|-------------|
| `disableAutoFocus` | `boolean` | Disables automatic focus management |
| `initialFocus` | `FocusTrap.Props['focusTrapOptions']['initialFocus']` | Available on `Modal` (in addition to `ModalPortal`) |
| `focusAfterCloseItemRef` | `React.RefObject<HTMLElement>` | Ref for the element that should receive focus after the modal closes |
| `modalProps` | `{ 'aria-labelledby'?: string }` | Pass-through ARIA props for the modal dialog element |

_Source: Oxygen MCP · Extracted 2026-05-01_
