---
parent: "[[TextArea]]"
section: composition
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/composition
---

## Subcomponents

`Textarea` renders a single native `<textarea>` element. It has no Oxygen subcomponents.

The Figma layer tree includes `_base_form_label` and `_base_form_hint` instances, but these are Figma-side design abstractions — they do not correspond to exported Oxygen components.

---

## Required consumer composition

`Textarea` renders only the input box. The following elements are required or strongly recommended in any production usage, rendered externally by the consumer:

| Element | How to link | WCAG requirement |
|---------|-------------|-----------------|
| `<label>` | `htmlFor` matching `id`, or `aria-labelledby` | 1.3.1, 3.3.2 (consumer responsibility) |
| Hint text | `aria-describedby` pointing to the hint element's `id` | Advisory |
| Error message | `aria-describedby` + `role="alert"` | 3.3.1 (consumer responsibility) |
| Required indicator | `required` or `aria-required="true"` on the textarea | Advisory |

```tsx
{/* Minimal accessible composition */}
<label htmlFor="message">Your message</label>
<Textarea
  id="message"
  aria-describedby="message-hint"
  rows={4}
  onChange={(e) => setValue(e.target.value)}
/>
<span id="message-hint">Max 500 characters.</span>
```

---

## Related components

| Component | Relationship |
|-----------|-------------|
| [[TextField]] | Single-line equivalent — use when input fits on one line |
| [[Checkbox]], [[Radio]], [[Dropdown]] | Co-occur in form patterns alongside Textarea |

---

## Form patterns

Textarea is an ingredient of generic form patterns. No named Oxygen patterns explicitly include Textarea at this time.

---

_Source: textarea-figma.md (anatomy) · accessibility.md · props.md · Extracted 2026-04-29_
