---
parent: "[[Tooltip]]"
section: usage
---

## Usage guidelines

The text sections below (Overview, When to use, When not to use, Best practices, Size, and the comparison tables) were extracted from the Figma `↳ Tooltip examples` page. The Do / Don't pairs were authored from the published Oxygen usage docs at <https://oxygen.8x8.com/components/tooltip/usage> because the Figma page contains no `✅ Do —` / `❌ Don't —` card frames.

<!-- STUB:GAP-017 source="The Figma ↳ Tooltip examples page contains no ✅ Do / ❌ Don't card frames. Pairs below are derived from published Oxygen docs (mitigated 2026-05-15). Replace with figma-extract-usage output if designers add card frames." -->
<!-- STUB:GAP-018 source="Image block screenshots from the Figma examples page not captured — Desktop Bridge was not connected during extraction. Re-run figma-extract-usage with Desktop Bridge active." -->

---

## Overview

The Tooltip component displays contextual information when users hover over or focus on an element. Tooltips are designed to provide brief, supplementary information that helps users understand the purpose or function of UI elements.

Tooltips should only be used for short descriptions. Keep tooltip content concise and limited to a single sentence or brief phrase. If you need to provide longer explanations, consider using a popover, modal, or dedicated help section instead.

---

## When to use

- Explaining the purpose of an icon-only button
- Providing additional context for truncated text
- Clarifying abbreviations or technical terms
- Describing disabled elements
- Adding extra context to an element that needs more explanation (e.g. table headers)

## When not to use

- Displaying long paragraphs or detailed instructions
- Presenting complex information that requires user interaction
- Conveying critical information that the user must read — use helper text instead
- Hosting links, buttons, or other interactive elements — these are inaccessible to some users

---

## Best practices

**Keep it short:** Limit tooltip text to a maximum of **140 characters** in English. Users should be able to read and understand the content in 2–3 seconds.

**Be descriptive:** While brief, tooltips should still provide meaningful information. Avoid redundant text that simply repeats the label.

**Use plain language:** Write in clear, simple terms that all users can understand.

**Avoid essential information:** Never put critical information solely in a tooltip — they can be missed and may not be accessible to all users.

**Trust the defaults:** The component opens after a **300 ms** hover delay and dismisses immediately when the cursor leaves. Default orientation is `top`. Change these only when the UI demands it.

---

## Do / Don't

> Pairs below are authored from the published Oxygen docs at <https://oxygen.8x8.com/components/tooltip/usage> and grounded in [[Tooltip.props]], [[Tooltip.accessibility]], and [[Tooltip.anatomy]]. No `✅ Do —` / `❌ Don't —` card frames exist on the Figma examples page.

### Pair 1 — Keep tooltip content to 140 characters of plain text

#### ✅ Do — One short, descriptive sentence per tooltip

The published docs cap tooltip length at **140 characters in English** and require plain text. The container's max-width is **320px**, which is sized for short hints — not paragraphs.

```tsx
<Tooltip title="Move this file to Trash. You can restore it within 30 days.">
  <IconButton icon={<TrashIcon />} aria-label="Delete file" />
</Tooltip>
```

#### ❌ Don't — Stretch a tooltip into multi-line or multi-paragraph help

A tooltip that needs scrolling, line breaks, or punctuation-heavy phrasing belongs in a Popover or in helper text under the input. Tooltips can be missed, so anything that has to be read should not live here.

```tsx
{/* Wrong — paragraph-length content that needs a Popover or helper text */}
<Tooltip title="Deleting a file removes it from this workspace and from any shared links. Restoration is possible within 30 days from the Trash view, after which the file is permanently purged. Administrators can override this period in workspace settings.">
  <IconButton icon={<TrashIcon />} aria-label="Delete file" />
</Tooltip>
```

---

### Pair 2 — Use Tooltip for supplementary context, never for critical information

#### ✅ Do — Reach for Tooltip when the information is *nice to have*

Tooltips earn their place when the rest of the UI already conveys the action and the tooltip just clarifies *why* or *what for* — an icon button's intent, an abbreviation, the meaning of a column header.

```tsx
{/* Right — clarifies the icon's purpose without being load-bearing */}
<Tooltip title="Send invite to selected teammates">
  <IconButton icon={<MailIcon />} aria-label="Send invite" />
</Tooltip>

{/* Right — explains a technical term in a table header */}
<Tooltip title="Average API response time in the last 24 hours">
  <span>Latency (avg 24h)</span>
</Tooltip>
```

#### ❌ Don't — Hide load-bearing information in a Tooltip

If the user *must* read it to complete the task, the tooltip is the wrong home. Required-field rules, validation errors, fees, dates, and legal disclosures belong in always-visible helper text or in a Popover the user must dismiss.

```tsx
{/* Wrong — payment fee is required for the decision; users on touch devices can't hover */}
<Tooltip title="A 2.9% processing fee applies to all card payments.">
  <Button>Pay with card</Button>
</Tooltip>
```

---

### Pair 3 — Tooltip content is text, not interactive

#### ✅ Do — Plain text only inside `title`

The published docs are explicit: **"Do not put links or other interactive elements in tooltips."** Tooltips dismiss on blur and may not be reachable by all input modes.

```tsx
<Tooltip title="This dashboard refreshes every 5 minutes.">
  <InfoIcon />
</Tooltip>
```

#### ❌ Don't — Embed links, buttons, or rich interactive content

Putting a "Learn more" link or a "Confirm" button inside `title` creates content that keyboard, screen-reader, and touch users cannot reliably reach. Use a Popover instead — Popovers are designed for interactive, persistent content.

```tsx
{/* Wrong — link inside tooltip can't be reached on touch and dismisses on blur */}
<Tooltip
  title={
    <>
      Refreshes every 5 minutes. <a href="/docs/refresh">Learn more</a>
    </>
  }
>
  <InfoIcon />
</Tooltip>
```

---

### Pair 4 — Pair Tooltip with `aria-label` on icon-only buttons — don't rely on Tooltip alone

#### ✅ Do — Give the trigger its own accessible name

Tooltip exposes its content via `aria-describedby` by default (`disableDescribedBy=false`), which **describes** the trigger but does not **name** it. An icon-only button still needs its own `aria-label`.

```tsx
{/* Right — button has an accessible name; tooltip adds a description */}
<Tooltip title="Archive this conversation. You can restore it from the Archived view.">
  <IconButton icon={<ArchiveIcon />} aria-label="Archive conversation" />
</Tooltip>
```

#### ❌ Don't — Use Tooltip as a substitute for an accessible name

A bare icon button with only a tooltip leaves screen-reader users with nothing announced when the button receives focus.

```tsx
{/* Wrong — icon button has no aria-label; the tooltip is the only naming source */}
<Tooltip title="Archive conversation">
  <IconButton icon={<ArchiveIcon />} />
</Tooltip>
```

---

### Pair 5 — Let the defaults work; pick an alternative when Tooltip is the wrong shape

#### ✅ Do — Ship with defaults and reach for an alternative when content doesn't fit

Default placement is `top`, delay is `300ms`, trigger is `hover`. Override only when the viewport edge clips the default placement, or when a touch UI needs a click trigger. When content is critical, interactive, or rich, pick the right alternative:

| Content shape | Component |
|---------------|-----------|
| Short, supplementary hint | **Tooltip** |
| Required-field rules, validation, always-visible guidance | **Helper text** |
| Rich text, links, or buttons the user can interact with | **Popover** |
| Decisions or workflows that must block the page | **Modal** |

```tsx
{/* Right — override placement only when trigger sits near the viewport top */}
<Tooltip title="Filter results by recent activity" orientation="bottom">
  <IconButton icon={<FilterIcon />} aria-label="Filter" />
</Tooltip>
```

#### ❌ Don't — Tune the defaults to mask a content-shape problem

A 0 ms delay flickers; forcing `showOn="click"` to keep a tooltip persistent means the content belongs in a Popover.

```tsx
{/* Wrong — 0 ms delay produces flicker on quick mouse movement */}
<Tooltip title="Send" delay={0}>
  <IconButton icon={<SendIcon />} aria-label="Send message" />
</Tooltip>
```

---

## Size

Min-width is 40px and max-width is 320px.

### Content length examples (from Figma)

| Label | Approx. width | Lines |
|-------|--------------|-------|
| Good — short and clear | ~91px | 1 |
| 50 characters | ~313px | 1 |
| 75 characters | 320px | 2 |
| 140 characters (maximum) | 320px | 3 |

---

## Tooltip and Popover working together

The Popover component displays rich, interactive content in a floating panel that appears when users click or interact with a trigger element. Unlike tooltips, popovers can contain longer text, formatted content, interactive elements, and remain visible until explicitly dismissed.

### Trigger state progression

| State | Component shown | Cursor |
|-------|----------------|--------|
| Trigger rest state | — | Default |
| Trigger on hover | Tooltip | Pointer (indicating actionable element) |
| Trigger on click | Popover | — |

### Hover vs focus trigger

- **Hover state:** cursor is a pointer arrow — tooltip appears
- **Focus state:** keyboard focus on trigger — tooltip appears (same content, no cursor)

---

## Tooltip vs. Popover vs. Modal

| Criteria | Tooltip | Popover | Modal |
|----------|---------|---------|-------|
| Content length | 140 characters | 2–4 paragraphs | Unlimited content |
| Interactivity | Non-interactive (read-only) | Interactive (buttons, forms, links) | Fully interactive workflows |
| Trigger method | Hover or focus | Click or tap | Click, action, or system event |
| Dismissal | Automatic (mouse out/blur) | Manual (click trigger again, click outside, close button, Esc) | Manual (click scrim, close button, action completion, Esc) |
| User attention | Passive, subtle | Moderate, contextual | High, demands focus |
| Blocks workflow | No | Partially (overlay, but page visible) | Yes (blocks entire page) |
| Position | Anchored to trigger element | Anchored to trigger element | Center of screen |
| Purpose | Quick hints and labels | Contextual details and options | Critical tasks and decisions |

---

## Alternatives

- **Helper text** — text placed beneath an input field that provides important or critical information needed to complete the action. Always visible. Use for required-field rules and vital information.
- **Contextual information** — copy that lives in the surrounding UI (panel intros, section descriptions) and guides the user without requiring a hover or focus.
