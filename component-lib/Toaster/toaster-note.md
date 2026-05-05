# Toaster — Extraction Note

> **No separate Figma extraction required.** Toaster shares Toast's visual design.
> See [component-lib/Toast/](../Toast/) for all Figma specs, tokens, and visual documentation.

---

## What Toaster is

`@8x8/oxygen-toaster` is an **imperative notification system** — infrastructure, not a visual component.
It has zero props. Consumers never render it with visual configuration; instead they:

1. Place `<Toaster />` once at the app root (acts as a portal/queue manager)
2. Call `notify()` imperatively from anywhere in the app to trigger a notification

The notifications it renders are visually identical to `Toast` from `@8x8/oxygen-toast`.

---

## Key API surface

### `notify(options)` — imperative trigger

| Option | Type | Notes |
|--------|------|-------|
| `content` | `ReactNode` | Notification body text |
| `iconTitle` | `string` | Accessible label for the status icon |
| `onClose` | `() => void` | Called when notification is dismissed |

### `DURATION` — timing constants

Exported constant from `@8x8/oxygen-toaster`. Provides preset duration values for auto-dismiss timing.

### Placement rules (from OX usage docs)

- Always appears in the **top corner of the UI, below the top bar**
- Incoming notifications always stack at the **top** of the list
- Multiple notifications of the same type form a stack — expandable or clearable in one click

---

## Minimal usage example

```jsx
import { Toaster, notify } from '@8x8/oxygen-toaster';

// Place once at app root
<Toaster />

// Call from anywhere
notify({
  content: 'File saved successfully',
  iconTitle: 'Success',
  onClose: () => console.log('dismissed'),
});
```

---

## Pipeline decisions

| Step | Decision |
|------|----------|
| `oxygen-mcp-extract` | Skip — props: [] (empty); API is imperative, not prop-based |
| `figma-extract` | **Skip — no separate Figma design**; visual design is in Toast |
| `figma-extract-usage` | Skip — usage guidelines are in Toast |
| `pui-mcp-extract` | Worth checking — Toaster is app-level and may integrate with PUI notification events |
| `doc-audit` | N/A — no source files to audit |
| `doc-rewrite` | Covered by Toast spec; Toaster gets a reference note only |

_Confirmed via OX MCP · 2026-05-05_
