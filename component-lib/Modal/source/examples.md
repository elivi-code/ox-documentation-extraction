---
component: Modal
package: "@8x8/oxygen-modal"
category: layout_overlay
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Modal/props]]"
  - "[[Modal/tokens]]"
  - "[[Modal/accessibility]]"
  - "[[Modal/Modal-figma]]"
  - "[[Modal/Modal-pui]]"
  - "[[Modal/Modal-audit]]"
tags:
  - oxygen
  - component/Modal
  - role/examples
  - stage/spec_ready
  - category/layout_overlay
---
# Modal — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [Modal-figma.md](Modal-figma.md)

## Basic usage

The standard pattern: a trigger button conditionally renders the modal, with `ModalHeader`, `ModalContent`, and `ModalFooter` as children.

```tsx
import {
  Modal,
  ModalHeader,
  ModalContent,
  ModalFooter,
} from '@8x8/oxygen-modal';
import { Button, buttonVariant } from '@8x8/oxygen-button';
import { useState } from 'react';

function Example() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <>
      <Button onClick={() => setIsOpen(true)}>Open modal</Button>
      {isOpen && (
        <Modal onClose={() => setIsOpen(false)}>
          <ModalHeader
            title="Modal title"
            onClose={() => setIsOpen(false)}
          />
          <ModalContent>
            Press Escape to close the modal, or click on the Close icon in the
            title if available.
          </ModalContent>
          <ModalFooter>
            <Button
              onClick={() => setIsOpen(false)}
              variant={buttonVariant.secondary}
            >
              Cancel
            </Button>
            <Button>Submit</Button>
          </ModalFooter>
        </Modal>
      )}
    </>
  );
}
```

> **Prefer conditional rendering** over the `isVisible` prop for showing and hiding modals.

---

## With useModalState hook (Storybook pattern)

The `useModalState` hook manages open/close state and wires up props for `Modal`, `ModalHeader`, and `ModalFooter`:

```tsx
import {
  Modal,
  ModalHeader,
  ModalContent,
  ModalFooter,
  useModalState,
} from '@8x8/oxygen-modal';
import { Button, buttonVariant } from '@8x8/oxygen-button';

function Example(args) {
  const {
    isOpen,
    onClose,
    onOpen,
    modalProps,
    modalHeaderProps,
    modalFooterProps,
  } = useModalState(args);

  return (
    <>
      <Button onClick={onOpen}>Open modal</Button>
      {isOpen && (
        <Modal {...modalProps} onClose={onClose}>
          <ModalHeader {...modalHeaderProps} />
          <ModalContent>
            Press Escape to close the modal, or click on the Close icon in the
            title if available.
          </ModalContent>
          <ModalFooter {...modalFooterProps}>
            <Button onClick={onClose} variant={buttonVariant.secondary}>
              Cancel
            </Button>
            <Button>Submit</Button>
          </ModalFooter>
        </Modal>
      )}
    </>
  );
}
```

---

## Sizes

```tsx
// Small
<Modal size="small" onClose={onClose}>...</Modal>

// Medium (default)
<Modal size="medium" onClose={onClose}>...</Modal>

// Big
<Modal size="big" onClose={onClose}>...</Modal>

// Custom dimensions
<Modal width="800px" height="600px" onClose={onClose}>...</Modal>
```

---

## Close behaviour variants

```tsx
// Default: closes only on Escape key
<Modal onClose={onClose}>...</Modal>

// Also closes on overlay click
<Modal shouldCloseOnOverlayClick onClose={onClose}>...</Modal>

// Disable Escape key close
<Modal shouldCloseOnEsc={false} onClose={onClose}>...</Modal>

// Allow clicks to pass through focus trap without closing
<Modal allowOutsideClick onClose={onClose}>...</Modal>

// Conditional outside click pass-through
<Modal
  allowOutsideClick={(e) => e.target.closest('.my-exception')}
  onClose={onClose}
>
  ...
</Modal>
```

---

## Custom portal target

```tsx
const targetRef = useRef(document.getElementById('modal-root'));

<Modal targetNode={targetRef.current} onClose={onClose}>
  ...
</Modal>
```

---

## ModalPortal (headless variant)

Use `ModalPortal` when you need to manage the portal container yourself — e.g. for cross-MFE rendering scenarios.

```tsx
import { ModalPortal, ModalHeader, ModalContent, ModalFooter } from '@8x8/oxygen-modal';

<ModalPortal
  onClose={onClose}
  initialFocus={false}
>
  <ModalHeader title="Dialog" onClose={onClose} />
  <ModalContent>Content goes here</ModalContent>
  <ModalFooter>
    <Button onClick={onClose}>Confirm</Button>
  </ModalFooter>
</ModalPortal>
```

---

## ModalHeader variants

```tsx
// With close button
<ModalHeader title="Title" onClose={onClose} />

// Centered title, with border
<ModalHeader
  title="Centered"
  alignTitle="center"
  hasBorderBottom
  onClose={onClose}
/>

// Custom close button ref (for initial focus)
const closeRef = useRef(null);
<Modal
  shouldUseFocusTrap
  portalRef={closeRef}
  onClose={onClose}
>
  <ModalHeader
    title="Focus example"
    onClose={onClose}
    buttonCloseRef={closeRef}
    iconCloseTitle="Dismiss dialog"
  />
  ...
</Modal>

// titleProps for aria-labelledby + aria-describedby wiring
<Modal
  modalProps={{
    'aria-labelledby': 'my-modal-title',
    'aria-describedby': 'my-modal-desc',
  }}
  onClose={onClose}
>
  <ModalHeader
    title="Accessible Modal"
    titleProps={{ id: 'my-modal-title' }}
    onClose={onClose}
  />
  <ModalContent id="my-modal-desc">
    Review the following items before confirming.
  </ModalContent>
  ...
</Modal>
```

---

## Disable focus trap

```tsx
<Modal shouldUseFocusTrap={false} onClose={onClose}>
  ...
</Modal>
```

> Only disable the focus trap when you are providing an equivalent focus management mechanism. Removing it breaks keyboard accessibility for modal dialogs.

---

## Confirmation dialog

Use the Dialog Modal variant for destructive confirmations. Set initial focus on the safe action (Cancel) and wire `focusAfterCloseItemRef` to return focus to the trigger on close.

```tsx
import {
  Modal,
  ModalHeader,
  ModalContent,
  ModalFooter,
} from '@8x8/oxygen-modal';
import { Button, buttonVariant } from '@8x8/oxygen-button';
import { useRef, useState } from 'react';

function ConfirmDeleteDialog() {
  const [isOpen, setIsOpen] = useState(false);
  const triggerRef = useRef(null);
  const cancelRef = useRef(null);

  return (
    <>
      <Button ref={triggerRef} onClick={() => setIsOpen(true)}>
        Delete item
      </Button>
      {isOpen && (
        <Modal
          size="small"
          focusAfterCloseItemRef={triggerRef}
          initialFocus={() => cancelRef.current}
          onClose={() => setIsOpen(false)}
          modalProps={{ 'aria-labelledby': 'confirm-title' }}
        >
          <ModalHeader
            title="Delete item?"
            titleProps={{ id: 'confirm-title' }}
          />
          <ModalContent>
            This action cannot be undone.
          </ModalContent>
          <ModalFooter>
            <Button
              ref={cancelRef}
              variant={buttonVariant.secondary}
              onClick={() => setIsOpen(false)}
            >
              Cancel
            </Button>
            <Button
              isDestructive
              onClick={() => {
                /* delete action */
                setIsOpen(false);
              }}
            >
              Delete
            </Button>
          </ModalFooter>
        </Modal>
      )}
    </>
  );
}
```

> **Focus on Cancel:** `initialFocus` defaults to the Cancel button to protect against accidental destructive actions. The destructive verb ("Delete") labels the action — never "OK" or "Yes".

_Source: Oxygen MCP · Extracted 2026-05-01_
