---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (https://oxygen.8x8.com/docs/components/button/usage, screenshot 2026-05-11) cross-referenced with extracted MCP/Figma artifacts — NOT from Figma Do/Don't card frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma ↳ Button examples page is created."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Button/props]]"
  - "[[Button/examples]]"
  - "[[Button/tokens]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/usage
  - stage/editorial
  - category/interaction
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/docs/components/button/usage, screenshot 2026-05-11) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Button-figma.md, Button-audit.md, published docs screenshot -->
<!-- DRAFTED: 2026-05-11 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 7 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Button examples" page is created -->

# Button — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Button-figma.md](./Button-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Button examples` Figma page with Do/Don't card frames exists, so `figma-extract-usage` cannot run. The guidance below is transcribed from the published Oxygen docs page for Button (`https://oxygen.8x8.com/docs/components/button/usage`, screenshot 2026-05-11) and cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), and [Button-figma.md](./Button-figma.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created.

Buttons let users initiate an action, submit a form, or trigger a state change. They are the most visible affordance for "this is something you can do" — visual weight, color, and placement work together to signal **how important** an action is relative to everything else on the surface.

---

## Anatomy

Element structure from the Label Button component set ([Button-figma.md:46](./Button-figma.md)) and the published docs page:

1. **Container** — the auto-laid-out frame holding label and icons. Carries the variant's background, border, and `6px` radius. See [Button-figma.md:175](./Button-figma.md).
2. **Leading icon** _(optional)_ — rendered via `iconLeft` ([props.md:75](./props.md)). Hidden by default; shown when an icon helps disambiguate the action (e.g. `<PlusIcon />` for "Add").
3. **Label** — the action text. Uses the `$bodyBold02` text style (16px, semi-bold, Inter). Treated as the accessible name of the button — see [accessibility.md:67](./accessibility.md).
4. **Trailing icon** _(optional)_ — rendered via `iconRight` ([props.md:76](./props.md)). Use for directional or disclosure affordances (e.g. arrow on a `DropdownButton`).
5. **Focus ring** — visible focus indicator, applied by Oxygen on keyboard focus. Required by WCAG 2.4.7; **never suppress with `outline: none`**. See [accessibility.md:97](./accessibility.md).

For circular control buttons, the container becomes a fixed-radius pill holding a single icon — see the Circular section in [examples.md:152](./examples.md).

---

## Overview

The button system spans seven visual variants and four sizes, plus boolean modifiers (`isDestructive`, `isCircular`, `isActive`, `isDisabled`) and the related components `ButtonGroup`, `DropdownButton`, and `IconButton`. Use the table below to pick the right combination; full prop signatures live in [props.md](./props.md).

### Type matrix

| Type | Oxygen API | Use for | Notes |
|------|-----------|---------|-------|
| Primary | `variant="primary"` (default) | The single most important action on a surface | One per surface — see Pair 1. |
| Secondary | `variant="secondary"` | Supporting actions next to a primary | Can repeat per surface. |
| Text | `variant="text"` | Low-emphasis inline actions, links inside dense UI | No visible container at rest — see Pair 2. |
| Destructive | `isDestructive` + any variant | Irreversible or data-loss actions | Pair with a confirmation step — see Pair 3. |
| Split | `ButtonGroup` of two buttons | A default action plus a related menu | Default action is most-used — see Pair 6. |
| Dropdown | `DropdownButton` | Action that opens a menu, no single default | Pair with `Popover`/`PopoverMenu` ([props.md:118](./props.md)). |
| Icon | `IconButton` or `Button` with `isCircular` | Compact, icon-only triggers | Always carry an accessible name — see Pair 4. |
| Control | `variant="tertiary"` / `tertiaryReversed` / `success` / `destructive` with `isCircular` | Call-control and toolbar affordances (mute, hang up, answer) | Live on dark/inverted surfaces — see [examples.md:152](./examples.md). |

> **Docs page note:** The published docs page also references "Soft", "Disclosure", "Optional", and "Indeterminate" treatments. These are **not** represented as separate variants in the current Oxygen API ([props.md:86](./props.md)) and appear to be composition patterns rather than first-class props. Tracked as a documentation gap — confirm with the Oxygen team before relying on them in code. <!-- TODO: confirm whether "Soft"/"Disclosure"/"Optional"/"Indeterminate" are intended as new variants, composed treatments, or rebranded existing variants -->

**Source:** Published docs — Overview section · [props.md:86](./props.md) · [Button-figma.md:68](./Button-figma.md).

---

## Behaviour

### States

Buttons expose five interaction states, all visible in the Figma Label Button variant axis ([Button-figma.md:209](./Button-figma.md)):

| # | State | Trigger | Visual change | Token (Primary) |
|---|-------|---------|---------------|-----------------|
| 1 | Rest | Default | Base variant background and text | `action01` / `textColor09` |
| 2 | Hover | Pointer over | Background shifts to the variant's hover token | `hover15` / `textColor09` |
| 3 | Active | Pointer pressed / Space / Enter | Background shifts to the variant's active token | `active14` / `textColor09` |
| 4 | Focus | Keyboard tab | Focus ring visible; no background-token change | (focus ring layer) |
| 5 | Disabled | `isDisabled={true}` | Background → `disabled01`, text/icon → `disabled04`. Still focusable. | `disabled01` / `disabled04` |

Full token map for every variant lives in [tokens.md:96](./tokens.md) (Token-to-Variant Quick Reference). Disabled tokens (`disabled01`, `disabled04`) are newly identified in Figma and not yet in `tokens.md` — tracked as new data in [Button-figma.md:267](./Button-figma.md) (N-001).

> ⚠️ **Two token conflicts apply to this section** — flagged in [Button-audit.md](./Button-audit.md):
> - **GAP-001 (CONFLICT, blocker):** Secondary rest background — Figma annotates `$action01` (blue), `tokens.md` specifies `action02` (near-black). Designer confirmation required.
> - **GAP-002 (CONFLICT, blocker):** Text Primary / Text Danger active background — Figma annotates `$active17`, which `tokens.md` defines as an inverted-only token. Reconciliation required.
>
> Until resolved, treat the Behaviour table above as authoritative for **Primary only**. Do not hand-write Secondary or Text active styling against either source.

**Source:** Published docs — Behaviour section · [tokens.md](./tokens.md) · [Button-figma.md:209](./Button-figma.md) · [Button-audit.md](./Button-audit.md) GAP-001, GAP-002.

---

## Sizes

Four sizes are documented in [props.md:98](./props.md): `small`, `medium` (default), `large`, `big`. The published docs page emphasises:

- **`large` is the recommended size for touch targets** ([props.md:74](./props.md)) — meets WCAG 2.5.5 / AAA 2.5.5 minimums for fingertip activation.
- **`medium` is the default for desktop, mouse-driven UI.**
- **`small` is for compact layouts** where vertical density matters (toolbars, dense forms).
- **Only the `large` (`48px`) container dimensions are confirmed from Figma** ([Button-figma.md:201](./Button-figma.md)). Medium and Small dimensions are tracked as `SOURCE_GAP` (I-001) — do not hand-assert specific pixel values.

Do not mix sizes within a single action row — see Pair 5.

**Source:** Published docs — Sizes section · [props.md:98](./props.md) · [Button-figma.md:175](./Button-figma.md).

---

## Placement & alignment

Within a dialog, form, or action row, Oxygen recommends:

- **Primary action sits on the right** in horizontal action rows (Western reading order; right-most position is the resting place for the eye).
- **Secondary and tertiary actions sit to the left of the primary**, separated by `ButtonGroup` spacing ([examples.md:213](./examples.md)).
- **Destructive actions** are usually placed **left-most**, away from the resting primary affordance, to reduce accidental activation.
- Use `<ButtonGroup align="right" />` for dialogs and `<ButtonGroup align="left" />` for inline forms — both are illustrated in [examples.md:225](./examples.md).

> The "right-aligned primary in dialogs" convention is widespread but not literally annotated on the Oxygen docs page screenshot at high resolution; it is consistent with `ButtonGroup`'s exposed `align` values and the docs page's Alignment section. <!-- TODO: confirm exact wording from the published docs Alignment section -->

**Source:** Published docs — Placement / Alignment sections · [props.md:109](./props.md) · [examples.md:213](./examples.md).

---

## Best Practices

### When to use

- Use `Button` for **actions** the user takes — submitting a form, opening a dialog, applying a setting, triggering a process.
- Use the **Primary** variant for the most important action on a surface, and only one.
- Use **Secondary** for supporting actions.
- Use **Text** for low-emphasis or inline actions.
- Use **`isDestructive`** for irreversible or data-loss actions, paired with a confirmation step.
- Use **`IconButton`** (with a `Tooltip`) for compact, icon-only triggers in dense toolbars.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Navigating to another page or external URL | A button implies an action; navigation should be discoverable as a link. Screen readers announce them differently (button vs link). | `TextLink` (or your routing equivalent). See [accessibility.md:111](./accessibility.md). |
| Inline within a paragraph of body text | Buttons break reading flow; their container weight overwhelms surrounding type. | `TextLink`. |
| To represent a non-interactive label or status | Buttons promise interaction; using them as decoration confuses AT users. | `Badge`, `Chip`, or plain text. |
| As the only validation feedback (disabling until valid) | Hides _why_ submission is unavailable from sighted and screen-reader users alike. | Keep the button enabled and show inline field errors — see Pair 7. |

**Source:** Published docs — Best Practices section · [accessibility.md:104](./accessibility.md).

---

## Do / Don't

### Pair 1 — One primary per surface

#### ✅ Do — Use a single Primary button for the most important action

Establish a clear focal point. Secondary and Text buttons handle everything else on the surface.

```tsx
<ButtonGroup align="right">
  <Button variant="text">Cancel</Button>
  <Button variant="secondary">Save as draft</Button>
  <Button variant="primary">Publish</Button>
</ButtonGroup>
```

#### ❌ Don't — Stack multiple Primary buttons next to each other

Two primary buttons compete for attention and erode the visual hierarchy. Keyboard and screen-reader users lose the cue about which action is "the" action.

```tsx
{/* Wrong — every action shouts */}
<ButtonGroup align="right">
  <Button variant="primary">Save as draft</Button>
  <Button variant="primary">Publish</Button>
</ButtonGroup>
```

**Source:** Published docs — Primary button section · [accessibility.md:110](./accessibility.md) (one primary per section).

---

### Pair 2 — Use Text buttons for low-emphasis actions

#### ✅ Do — Use `variant="text"` for inline, low-priority actions

Text buttons have no visible container at rest, so they sit unobtrusively next to body content or denser controls. Good for "Cancel", "Learn more", or inline-form actions.

```tsx
<ButtonGroup>
  <Button variant="text">Cancel</Button>
  <Button variant="primary">Confirm</Button>
</ButtonGroup>
```

#### ❌ Don't — Use Text buttons as the primary call-to-action

Stripping the container also strips the visual weight users rely on to find the main action. The lack of background means the affordance reads as a link, not a button.

```tsx
{/* Wrong — the publish action disappears */}
<ButtonGroup align="right">
  <Button variant="text">Publish</Button>
</ButtonGroup>
```

**Source:** Published docs — Text button section · [props.md:94](./props.md) · [tokens.md:105](./tokens.md) (no rest background for `text`).

---

### Pair 3 — Reserve destructive styling for irreversible actions

#### ✅ Do — Combine `isDestructive` with a confirmation step

Red is a strong signal. Earn it: use `isDestructive` only when the action is irreversible (deleting data, ending a call, leaving a workspace) and gate it with a confirmation dialog.

```tsx
<Button variant="primary" isDestructive onClick={openConfirmDialog}>
  Delete account
</Button>
```

#### ❌ Don't — Use `isDestructive` for routine actions or as emphasis

Reserving red for "real" destruction keeps the signal trustworthy. Don't reach for it because "this button felt important".

```tsx
{/* Wrong — sign out is not destructive */}
<Button variant="primary" isDestructive>Sign out</Button>
```

**Source:** Published docs — Destructive button section · [accessibility.md:108](./accessibility.md) (WCAG 3.2.2 — preface destructive actions with confirmation) · [examples.md:113](./examples.md).

---

### Pair 4 — Icon-only buttons must carry an accessible name

#### ✅ Do — Pair `IconButton` with a `Tooltip`, or pass `aria-label` to a circular `Button`

The tooltip's `title` becomes the accessible name. Screen-reader and switch-control users get the same affordance sighted users do from the glyph.

```tsx
import Tooltip from '@8x8/oxygen-tooltip';
import { IconButton } from '@8x8/oxygen-button';
import { AddReactionIcon } from '@8x8/oxygen-icon';

<Tooltip title="Add reaction">
  <IconButton>
    <AddReactionIcon />
  </IconButton>
</Tooltip>
```

#### ❌ Don't — Ship a bare icon button with no label

Without `aria-label` or a `Tooltip`, the button announces as "button" — there is no way for non-sighted users to know what it does, and the page fails WCAG 4.1.2.

```tsx
{/* Wrong — no accessible name */}
<IconButton>
  <AddReactionIcon />
</IconButton>
```

**Source:** Published docs — Icon button section · [accessibility.md:68](./accessibility.md) (IconButton + Tooltip pattern) · [accessibility.md:98](./accessibility.md) (WCAG 4.1.2 Name, Role, Value).

---

### Pair 5 — Keep one size per action row

#### ✅ Do — Match button sizes within a `ButtonGroup`

A row reads as a single decision. Matching sizes preserves baseline alignment and the visual rhythm of the row.

```tsx
<ButtonGroup spacing="small">
  <Button size="small" variant="text">Cancel</Button>
  <Button size="small" variant="secondary">Save as draft</Button>
  <Button size="small" variant="primary">Publish</Button>
</ButtonGroup>
```

#### ❌ Don't — Mix sizes within a single action row

Mixing sizes implies the actions are at different levels of importance _and_ from different layers of the UI. It breaks the row's alignment and reads as inconsistency, not hierarchy.

```tsx
{/* Wrong — mixed sizes in one row */}
<ButtonGroup>
  <Button size="small" variant="text">Cancel</Button>
  <Button size="large" variant="primary">Publish</Button>
</ButtonGroup>
```

**Source:** Published docs — Sizes section · [props.md:98](./props.md) · [examples.md:75](./examples.md).

---

### Pair 6 — Choose Split vs Dropdown by the user's intent

#### ✅ Do — Use a Split (`ButtonGroup` with two buttons) when one action is clearly the default

A split control surfaces the most-used action as a one-click affordance and tucks alternatives behind the menu. Use it when 80% of users want the same thing.

```tsx
<ButtonGroup>
  <Button variant="primary">Reply</Button>
  <DropdownButton variant="primary" aria-label="More reply options" />
</ButtonGroup>
```

#### ✅ Do — Use a `DropdownButton` alone when there is no single default

If the choices are equal-weight, surface them all behind a single menu — don't fake a default.

```tsx
<DropdownButton>Reply</DropdownButton>
```

#### ❌ Don't — Surface a "Reply" split when half your users want "Reply all"

A split button promises that the default is the right action _most of the time_. If that's not true, you've just hidden the action half your users wanted behind an extra click and an extra tab stop.

**Source:** Published docs — Split button / Dropdown button sections · [props.md:118](./props.md) · [examples.md:263](./examples.md).

---

### Pair 7 — Don't disable a button to hide a validation error

#### ✅ Do — Keep the button enabled and surface the error inline

A disabled button removes the affordance without explaining why. Keep the button enabled, let the user submit, and show inline field errors when validation fails — both sighted and assistive-tech users get the same feedback.

```tsx
<form onSubmit={handleSubmit}>
  <Input
    label="Email"
    error={emailError}
    aria-describedby="email-error"
  />
  <Button type="submit">Save</Button>
</form>
```

#### ❌ Don't — Disable the submit until every field is valid with no explanation

The button greys out, the user can't tell why, and screen-reader users hear nothing about the missing field. `isDisabled` keeps the button focusable but mute — it doesn't announce the reason.

```tsx
{/* Wrong — disabled until valid, no inline error */}
<Button type="submit" isDisabled={!isFormValid}>Save</Button>
```

> If you _must_ disable a button (e.g. while a long-running submit is in flight), pair it with a visible status message via `aria-describedby` so the disabled reason is announced. See [accessibility.md:109](./accessibility.md).

**Source:** Published docs — Best Practices section · [accessibility.md:44](./accessibility.md) (Disabled state) · [accessibility.md:109](./accessibility.md) ("prefer keeping buttons enabled and showing inline validation errors").

---

## Related components

The published docs page lists these neighbours in its "Related" section:

- **`ButtonGroup`** — horizontal arrangement of multiple buttons with shared spacing and alignment. See [props.md:109](./props.md), [examples.md:213](./examples.md).
- **`DropdownButton`** — button that opens a menu (typically `Popover` or `PopoverMenu`). See [props.md:118](./props.md), [examples.md:263](./examples.md).
- **`IconButton`** — compact icon-only trigger; always pair with `Tooltip`. See [props.md:133](./props.md), [examples.md:292](./examples.md).
- **`TextLink`** — for navigation rather than actions. See [accessibility.md:111](./accessibility.md) (Button vs. link).

<!-- TODO: confirm whether the published docs page lists any further Related entries (e.g. Tooltip, Popover, ConfirmDialog) -->

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- Renders a native `<button>` — implicit ARIA role `button`, no `role` override needed.
- `Tab` / `Shift+Tab` move focus; `Enter` and `Space` activate.
- `isDisabled` keeps the button **focusable** (does not leave the tab order) but suppresses form submission — see [accessibility.md:44](./accessibility.md).
- Icon-only buttons need an `aria-label` or a `Tooltip` (which provides the accessible name) — Pair 4.
- Never suppress the focus ring (`outline: none`) — required by WCAG 2.4.7.
- Destructive actions should be preceded by a confirmation pattern (WCAG 3.2.2).

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ Button examples` Figma page with Do/Don't card frames found. Pairs above are editorially transcribed from the published Oxygen docs page (`https://oxygen.8x8.com/docs/components/button/usage`, screenshot 2026-05-11) and cross-validated against MCP/Figma extraction. Re-run `figma-extract-usage` if such a page is created. |
| Secondary rest background token | CONFLICT (blocker) | GAP-001 in [Button-audit.md](./Button-audit.md). Figma annotates `$action01`; `tokens.md` specifies `action02`. Behaviour section above is authoritative for **Primary only** until resolved. |
| Text active background token | CONFLICT (blocker) | GAP-002 in [Button-audit.md](./Button-audit.md). Figma annotates `$active17`, which `tokens.md` defines as inverted-only. Do not hand-assert Text active styling against either source until resolved. |
| CSS variable / semantic token name divergence | CONFLICT | GAP-003 in [Button-audit.md](./Button-audit.md). `--actions/action09` (Figma CSS export) vs `action01` (Oxygen semantic) name the same color. Downstream tooling must pick a canonical name. |
| `Soft` / `Disclosure` / `Optional` / `Indeterminate` treatments | SOURCE_GAP | Referenced on the published docs page screenshot but absent from `props.md` ([props.md:86](./props.md)). Likely composition patterns rather than first-class variants — confirm with the Oxygen team. |
| Medium / Small dimensions | SOURCE_GAP | Only `large` (48px) container dimensions are confirmed in [Button-figma.md:201](./Button-figma.md). Medium and Small pixel values not asserted here. |
| Disabled tokens `disabled01` / `disabled04` | DOC_GAP | Identified in Figma but absent from `tokens.md` (tracked as N-001 in [Button-figma.md:267](./Button-figma.md)). Behaviour table above references them by name only. |
| `fullWidth` / `Fluid 100%` prop on Button | DOC_GAP | Figma exposes a `Fluid 100%` variant axis ([Button-figma.md:78](./Button-figma.md)); `props.md` documents `fullWidth` for `DropdownButton` only. May be a props gap. |
| Alignment section verbatim copy | DOC_GAP | The "primary right-aligned in dialogs" convention above is consistent with `ButtonGroup`'s `align` prop and the docs page's Alignment section, but the exact wording from the published docs was not captured in the screenshot at readable resolution. Confirm before promoting to a normative rule. |
| "Related" component list completeness | DOC_GAP | The four Related entries listed above are derived from `props.md` and `accessibility.md`. The full set on the published docs page (e.g. Tooltip, Popover, ConfirmDialog) is not yet confirmed against the live page. |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/docs/components/button/usage`, screenshot 2026-05-11) · Cross-referenced with Oxygen MCP and Figma extraction · Editorial draft_
