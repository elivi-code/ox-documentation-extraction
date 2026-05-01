# Modal — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [Modal-figma.md](Modal-figma.md)

## ARIA role

The Modal renders a dialog element. The correct ARIA markup is:

```html
<div role="dialog" aria-modal="true" aria-labelledby="modal-title-id">
  <!-- modal content -->
</div>
```

Wire `aria-labelledby` to the title element via the `modalProps` and `titleProps` props:

```tsx
<Modal modalProps={{ 'aria-labelledby': 'my-modal-title' }} onClose={onClose}>
  <ModalHeader
    title="Settings"
    titleProps={{ id: 'my-modal-title' }}
    onClose={onClose}
  />
  ...
</Modal>
```

> **Note:** The Figma design annotations do not include explicit ARIA role documentation. The guidance above is based on the WCAG dialog pattern and the prop API returned by the Oxygen MCP.

---

## Focus management

### Focus trap

The Modal uses [focus-trap](https://github.com/focus-trap/focus-trap) internally, enabled by default (`shouldUseFocusTrap={true}`).

- Focus is contained within the modal while it is open
- Tab and Shift+Tab cycle through focusable elements inside the modal
- Focus does not escape to the page behind the overlay

**Do not disable** the focus trap (`shouldUseFocusTrap={false}`) unless you provide an equivalent mechanism. Disabling it breaks keyboard navigation for screen reader users.

### Initial focus

By default, focus moves to the first focusable element in the modal when it opens.

To customise initial focus:

```tsx
// ModalPortal: set initialFocus to a selector, element, or false
<ModalPortal initialFocus="#my-first-input" onClose={onClose}>...</ModalPortal>

// Focus the close button on open (via ModalHeader buttonCloseRef)
const closeRef = useRef(null);
<Modal onClose={onClose}>
  <ModalHeader
    title="..."
    onClose={onClose}
    buttonCloseRef={closeRef}
  />
  ...
</Modal>

// Prevent initial focus shift
<ModalPortal initialFocus={false} onClose={onClose}>...</ModalPortal>
```

### Return focus on close

Use `focusAfterCloseItemRef` to specify which element should receive focus when the modal closes:

```tsx
const triggerRef = useRef(null);

<>
  <Button ref={triggerRef} onClick={open}>Open</Button>
  {isOpen && (
    <Modal focusAfterCloseItemRef={triggerRef} onClose={close}>
      ...
    </Modal>
  )}
</>
```

This ensures keyboard and screen reader users are returned to a sensible position in the document.

---

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Move focus to the next focusable element inside the modal |
| `Shift + Tab` | Move focus to the previous focusable element inside the modal |
| `Escape` | Close the modal (when `shouldCloseOnEsc={true}`, the default) |
| `Enter` / `Space` | Activate the focused button (close, cancel, submit) |

---

## Close button

`ModalHeader` renders a close icon button when `onClose` is provided.

- The button's accessible name is set via `iconCloseTitle` (default: `'Close'`)
- Override to provide a more descriptive label if needed:

```tsx
<ModalHeader
  title="Delete file"
  onClose={onClose}
  iconCloseTitle="Close delete file dialog"
/>
```

---

## Overlay

The modal overlay (backdrop) is not interactive by default — clicks on it do not close the modal (`shouldCloseOnOverlayClick={false}`). If you enable overlay click to close, ensure there is also a visible close mechanism (close button or Escape key) so keyboard-only users have an equivalent path.

---

## Screen reader guidance

- Announce the dialog to screen readers by using `role="dialog"` with `aria-modal="true"` and `aria-labelledby` pointing to the modal title
- The `modalProps` prop passes through to the dialog container element — use it to set `aria-labelledby` and `aria-describedby`
- Use `aria-describedby` to point to `ModalContent` if it contains instructions or descriptions the user needs on open
- Avoid nesting interactive landmarks inside the modal unless intentional

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.3.1 Info and Relationships | Dialog role and label relationships conveyed via ARIA | Meets via `role="dialog"` + `aria-labelledby` |
| 1.4.3 Contrast (Minimum) | Text against background ≥ 4.5:1 (normal text), ≥ 3:1 (large text) | Tokens use semantic color system; verify in implementation |
| 2.1.1 Keyboard | All functionality operable by keyboard | Meets via focus trap + Escape + Tab navigation |
| 2.1.2 No Keyboard Trap | Focus trap must be escapable | Meets — Escape key dismisses; focus returns to trigger on close |
| 2.4.3 Focus Order | Focus order inside modal must be logical | Meets via DOM order; verify with custom `initialFocus` overrides |
| 2.4.7 Focus Visible | Keyboard focus indicator must be visible | Depends on OX theme; verify focus ring in implementation |
| 4.1.2 Name, Role, Value | Interactive elements have accessible names | Close button uses `iconCloseTitle`; verify custom content |
| 4.1.3 Status Messages | Status changes announced without focus move | Not applicable to base Modal; consumer responsible for content updates |

_Source: Oxygen MCP (component API) · Figma MCP (design annotations) · Extracted 2026-05-01_
