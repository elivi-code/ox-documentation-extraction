<!-- SOURCE: Figma — ↳ Popover examples -->
<!-- PAGE: ↳ Popover examples (node 49969:10533) -->
<!-- SECTION: Section / Usage Guidelines (frame 88806:12708) -->
<!-- EXTRACTED: 2026-05-08 -->
<!-- COMPONENT: PopoverMenu -->
<!-- PAIRS: 0 — no Do/Don't card frames found; textual guidelines captured instead -->

# PopoverMenu — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [PopoverMenu-figma.md](./PopoverMenu-figma.md)

Usage guidelines extracted from the `↳ Popover examples` Figma page.
The page contains textual prose guidelines rather than Do/Don't card frames.
Do/Don't cards have not been authored yet — see [Gaps](#gaps).

---

## Overview

Popovers are ideal for displaying supplementary information that is too complex or lengthy for a tooltip but doesn't require a full modal dialog. They provide contextual information without navigating away from the current page.

---

## When to Use

- Displaying detailed explanations or help content (2–3 paragraphs)
- Showing forms or interactive controls in context
- Presenting formatted content with headings, lists, or links
- Providing additional options or actions related to an element
- Displaying previews of content (e.g. user profiles, image previews)

---

## When Not to Use

- **Brief, single-sentence descriptions** — use a Tooltip instead
- **Critical actions requiring user attention** — use a Modal instead
- **Complex workflows spanning multiple steps** — use dedicated pages or modals
- **Mobile-first interfaces where screen space is limited**

---

## Key Characteristics

- **Interactive** — Popovers can contain buttons, links, form inputs, and other interactive elements that users can engage with.
- **Persistent** — Unlike tooltips, popovers remain visible until the user dismisses them by clicking outside, pressing Escape, or clicking a close button.
- **Rich content** — Popovers support formatted text, images, icons, and structured layouts.
- **Contextual** — Popovers are positioned relative to their trigger element.

---

## Best Practices

- **Keep content focused** — While popovers can contain more information than tooltips, they should still be concise and relevant. Aim for 2–4 short paragraphs maximum.
- **Make dismissal obvious** — Include a clear close button (×) and ensure users can dismiss by clicking outside or pressing the Escape key.
- **Use appropriate triggers** — Click is the standard trigger for popovers. Avoid hover triggers as they can be accidentally activated and are inaccessible on touch devices.
- **Limit concurrent popovers** — Only show one popover at a time to maintain focus and clarity.

---

## Gaps

| Item | Description |
|------|-------------|
| No Do/Don't cards | The `↳ Popover examples` page contains prose guidelines only — no `✅ Do —` or `❌ Don't —` card frames have been authored in Figma |
| Desktop Bridge not connected | `figma-console:figma_get_selection` returned a WebSocket error; full interactive page scan was blocked. Prose content extracted via `Figma:get_metadata` fallback |

---

_Source: Figma examples page · Extracted 2026-05-08_
