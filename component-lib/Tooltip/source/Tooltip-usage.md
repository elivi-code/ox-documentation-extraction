---
component: Tooltip
package: "@8x8/oxygen-tooltip"
category: overlays_contextual
role: usage
role_description: "Usage guidelines — text from Figma examples page + Do/Don't pairs derived from the published Oxygen docs (/components/tooltip/usage)"
pipeline_stage: extracted
pipeline_note: "GAP-001 reconciled to 140 chars (published docs canonical); GAP-002 reconciled to orientation default 'top'. Awaiting re-audit."
source_type: mixed
audit_verdict: null
siblings:
  - "[[Tooltip/props]]"
  - "[[Tooltip/examples]]"
  - "[[Tooltip/tokens]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-pui]]"
  - "[[Tooltip/Tooltip-audit]]"
tags:
  - oxygen
  - component/Tooltip
  - role/usage
  - stage/extracted
  - category/overlays_contextual
---
<!-- SOURCE: Figma examples page (text sections) + published Oxygen docs https://oxygen.8x8.com/components/tooltip/usage (Do/Don't pairs) -->
<!-- PAGE: ↳ Tooltip examples (Figma) + /components/tooltip/usage (Oxygen docs) -->
<!-- SECTION: Tooltip, Tooltip and Popover working together, Tooltip vs. Popover vs. Modal, Do / Don't -->
<!-- EXTRACTED: 2026-05-15 -->
<!-- COMPONENT: Tooltip -->
<!-- PAIRS: 5 -->
<!-- NOTE: No ✅ Do / ❌ Don't card frames exist on the Figma examples page. Do/Don't pairs below were authored from the published Oxygen docs (OX MCP + live page) and grounded in props.md / accessibility.md / Tooltip-figma.md. -->

# Tooltip — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md) ·
> [Tooltip-figma.md](./Tooltip-figma.md)

The text sections below (Overview, When to use, When not to use, Best practices, Size, and the comparison tables) were extracted from the Figma `↳ Tooltip examples` page. The Do / Don't pairs were authored from the published Oxygen usage docs at https://oxygen.8x8.com/components/tooltip/usage because the Figma page contains no `✅ Do —` / `❌ Don't —` card frames.

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

> Pairs below are authored from the published Oxygen docs at <https://oxygen.8x8.com/components/tooltip/usage> and grounded in [props.md](./props.md), [accessibility.md](./accessibility.md), and [Tooltip-figma.md](./Tooltip-figma.md). No `✅ Do —` / `❌ Don't —` card frames exist on the Figma examples page (see [Gaps](#gaps)).

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

**Source:** [oxygen.8x8.com/components/tooltip/usage — Behavior](https://oxygen.8x8.com/components/tooltip/usage) · [Tooltip-figma.md](./Tooltip-figma.md) (max-width 320px).

---

### Pair 2 — Use Tooltip for supplementary context, never for critical information

#### ✅ Do — Reach for Tooltip when the information is *nice to have*

Tooltips earn their place when the rest of the UI already conveys the action and the tooltip just clarifies *why* or *what for* — an icon button's intent, an abbreviation, the meaning of a column header. Per the docs, use them "when more information is useful in helping a user make decisions **but is not critical**."

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

**Source:** [oxygen.8x8.com/components/tooltip/usage — When to use / When not to use](https://oxygen.8x8.com/components/tooltip/usage) · [accessibility.md](./accessibility.md) (touch / no-hover users).

---

### Pair 3 — Tooltip content is text, not interactive

#### ✅ Do — Plain text only inside `title`

The published docs are explicit: **"Do not put links or other interactive elements in tooltips."** Tooltips dismiss on blur and may not be reachable by all input modes; any element inside them that needs to be clicked, tabbed to, or focused will be unreachable for some users.

```tsx
<Tooltip title="This dashboard refreshes every 5 minutes.">
  <InfoIcon />
</Tooltip>
```

#### ❌ Don't — Embed links, buttons, or rich interactive content

Putting a "Learn more" link or a "Confirm" button inside `title` creates content that keyboard, screen-reader, and touch users cannot reliably reach. If the content needs interaction, use a Popover instead — Popovers are designed for interactive, persistent content.

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

{/* Wrong — button inside tooltip; this needs a Popover */}
<Tooltip
  title={
    <>
      Delete this record? <Button onClick={onConfirm}>Yes</Button>
    </>
  }
>
  <IconButton icon={<TrashIcon />} aria-label="Delete" />
</Tooltip>
```

**Source:** [oxygen.8x8.com/components/tooltip/usage — Behavior, When not to use](https://oxygen.8x8.com/components/tooltip/usage) · [accessibility.md](./accessibility.md) (keyboard / SR reachability).

---

### Pair 4 — Pair Tooltip with `aria-label` on icon-only buttons — don't rely on Tooltip alone

#### ✅ Do — Give the trigger its own accessible name

Tooltip exposes its content via `aria-describedby` by default ([props.md](./props.md): `disableDescribedBy=false`), which **describes** the trigger but does not **name** it. An icon-only button still needs its own `aria-label` (or visible text) so assistive tech can announce *what the control is*, independently of the supplementary tooltip text.

```tsx
{/* Right — button has an accessible name; tooltip adds a description */}
<Tooltip title="Archive this conversation. You can restore it from the Archived view.">
  <IconButton icon={<ArchiveIcon />} aria-label="Archive conversation" />
</Tooltip>
```

#### ❌ Don't — Use Tooltip as a substitute for an accessible name

A bare icon button with only a tooltip leaves screen-reader users with nothing announced when the button receives focus until the describedby fires (and not at all on some configurations). It also breaks for keyboard-only users who pass quickly through the focus order.

```tsx
{/* Wrong — icon button has no aria-label; the tooltip is the only naming source */}
<Tooltip title="Archive conversation">
  <IconButton icon={<ArchiveIcon />} />
</Tooltip>

{/* Also wrong — disabling describedby and relying on the visual tooltip only */}
<Tooltip title="Archive conversation" disableDescribedBy>
  <IconButton icon={<ArchiveIcon />} />
</Tooltip>
```

**Source:** [props.md](./props.md) (`disableDescribedBy`, default `false`) · [accessibility.md](./accessibility.md) (icon-button labelling) · [oxygen.8x8.com/components/tooltip/usage — When to use](https://oxygen.8x8.com/components/tooltip/usage) ("describe an icon button").

---

### Pair 5 — Let the defaults work; pick an alternative when Tooltip is the wrong shape

#### ✅ Do — Ship with `orientation="top"`, `delay=300`, `showOn="hover"`, and reach for an alternative when content doesn't fit

The defaults are tuned: **top** placement, **300 ms** show delay, dismiss-on-blur, hover trigger. Override only when the viewport edge clips the default placement (flip to `bottom` / `left` / `right`) or when an embedded touch UI needs a click trigger. When the content is **critical**, **interactive**, or **rich**, pick the right alternative instead:

| Content shape | Component |
|---------------|-----------|
| Short, supplementary hint | **Tooltip** |
| Required-field rules, validation, always-visible guidance | **Helper text** below the field |
| Rich text, links, or buttons the user can interact with | **Popover** |
| Decisions or workflows that must block the page | **Modal** |

```tsx
{/* Right — defaults, override placement only when the trigger sits near the viewport top */}
<Tooltip title="Filter results by recent activity" orientation="bottom">
  <IconButton icon={<FilterIcon />} aria-label="Filter" />
</Tooltip>
```

#### ❌ Don't — Tune the defaults to mask a content-shape problem, or pick Tooltip when another component fits

A 0 ms delay flickers; a multi-second delay frustrates. Forcing `showOn="click"` to keep a tooltip persistent suggests the content actually belongs in a Popover. Stretching `orientation` and `offset` to fit a paragraph means the content is too long.

```tsx
{/* Wrong — 0 ms delay produces flicker on quick mouse movement */}
<Tooltip title="Send" delay={0}>
  <IconButton icon={<SendIcon />} aria-label="Send message" />
</Tooltip>

{/* Wrong — using click + interactive content; this is a Popover */}
<Tooltip
  showOn="click"
  title={
    <>
      <p>Filter results by activity, status, or owner.</p>
      <Button>Reset filters</Button>
    </>
  }
>
  <Button>Filter</Button>
</Tooltip>
```

**Source:** [props.md](./props.md) (`orientation` default `'top'`, `delay` default `300`, `showOn` default `'hover'`) · [oxygen.8x8.com/components/tooltip/usage — Behavior, Alternatives](https://oxygen.8x8.com/components/tooltip/usage) · `## Tooltip vs. Popover vs. Modal` table below.

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

The examples page also illustrates:
- **Hover state:** cursor is a Pointer arrow — tooltip appears
- **Focus state:** keyboard focus on trigger — tooltip appears (same content, no cursor)

---

## Tooltip vs. Popover vs. Modal

Comparison table extracted from the Figma examples page; character limit aligned with the published Oxygen docs (140 characters).

| Criteria | Tooltip | Popover | Modal |
|----------|---------|---------|-------|
| Content length | 140 characters | 2–4 paragraphs | Unlimited content |
| Interactivity | Non-interactive (read-only) | Interactive (buttons, forms, links) | Fully interactive workflows |
| Trigger method | Hover or focus | Click or tap | Click, action, or system event |
| Dismissal | Automatic (mouse out/blur) | Manual (click trigger again, click outside, close button, action completion, Esc) | Manual (click scrim, close button, action completion, Esc) |
| User attention | Passive, subtle | Moderate, contextual | High, demands focus |
| Blocks workflow | No | Partially (overlay, but page visible) | Yes (blocks entire page) |
| Position | Anchored to trigger element | Anchored to trigger element | Center of screen |
| Purpose | Quick hints and labels | Contextual details and options | Critical tasks and decisions |

---

## Alternatives

From the published docs:

- **Helper text** — text placed beneath an input field that provides important or critical information needed to complete the action. Always visible. Use this for required-field rules and other vital information; links are permitted.
- **Contextual information** — copy that lives in the surrounding UI (panel intros, section descriptions) and guides the user without requiring a hover or focus.

---

## Gaps

| Item | Description |
|------|-------------|
| Do/Don't pairs are derived, not Figma-sourced | The Figma `↳ Tooltip examples` page has no `✅ Do —` / `❌ Don't —` card frames. Pair content above was authored from the published Oxygen docs (OX MCP + live page) and grounded in `props.md` / `accessibility.md` / `Tooltip-figma.md`. Replace with `figma-extract-usage` output if designers add card frames in the future. ([Tooltip-audit.md](./Tooltip-audit.md) GAP-017) |
| Image block screenshots | Not captured — Desktop Bridge was not connected during the original Figma extract. ([Tooltip-audit.md](./Tooltip-audit.md) GAP-018) |
| Character limit reconciled | Was previously documented as 136 in Tooltip-usage.md (Figma) vs 140 in OX MCP. Now aligned to **140** per the canonical published docs ([Tooltip-audit.md](./Tooltip-audit.md) GAP-001 — resolved). |

---

_Source: Figma examples page (text sections, 2026-05-05) + Oxygen published docs `/components/tooltip/usage` (Do/Don't pairs, 2026-05-15)_
