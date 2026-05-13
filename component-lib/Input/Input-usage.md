---
component: Input
package: "@8x8/oxygen-input"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (https://oxygen.8x8.com/components/textinput/usage, fetched 2026-05-13 via Claude_in_Chrome MCP) cross-referenced with extracted MCP/Figma artifacts. The published docs page contains Anatomy, Overview, Behavior (States / Size / Placement), Best Practices (When to use / When not to use), and Related sections — but NO Do/Don't card frames. Do/Don't pairs below are derived from the docs page intent + props.md, examples.md, tokens.md, accessibility.md, and Input-figma.md. Re-run /doc-audit Input after creation; replace pairs with figma-extract-usage output if a Figma '↳ Input examples' page is ever populated with Do/Don't cards."
source_type: editorial
audit_verdict: null
scope: "Text input only — Text area and Search input variants are out of scope; see Gaps."
siblings:
  - "[[Input/props]]"
  - "[[Input/examples]]"
  - "[[Input/tokens]]"
  - "[[Input/accessibility]]"
  - "[[Input/Input-figma]]"
  - "[[Input/Input-pui]]"
  - "[[Input/Input-audit]]"
tags:
  - oxygen
  - component/Input
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/textinput/usage, fetched 2026-05-13 via Claude_in_Chrome MCP) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Input-figma.md, Input-pui.md, Input-audit.md, published docs page -->
<!-- DRAFTED: 2026-05-13 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 8 (derived from docs page Best Practices + State / Size / Placement sections + extracted artifacts) -->
<!-- SCOPE: Text input only — Text area + Search input out of scope (see Gaps) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Input examples" page is created with Do/Don't card frames -->

# Input — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Input-figma.md](./Input-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Input examples` Figma page with Do/Don't card frames exists, so `figma-extract-usage` cannot run. The body below transcribes the published Oxygen docs page for Text input (`https://oxygen.8x8.com/components/textinput/usage`, fetched 2026-05-13) verbatim where the page asserts something, and derives Do/Don't pairs from the page's Behavior + Best Practices intent cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), and [Input-figma.md](./Input-figma.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

> ⚠ **Scope.** This document covers **Text input only** (Figma component set `22155:36793`). The Input canvas in Figma also ships **Text area** (`21562:34985`) and **Search input** (`25655:40530`) component sets, but the published docs URL is component-specific to Text input and Text area lives in its own [TextArea](../TextArea/) folder. Search input affordances (`iconLeft=SearchIcon`, `type='search'`) are mentioned in passing only where the Text input API overlaps. The Search-specific `isReadOnly` ambiguity is tracked as **CONFLICT-001** in [Input-audit.md](./Input-audit.md) and is out of scope here.

> ⚠ **Six props lack OX descriptions.** [props.md:72-86](./props.md) lists `size`, `suffix`, `focus`, `fixed`, `autoSuffixWidth`, and `autoPrefixWidth` with no description returned by the Oxygen MCP (tracked as **GAP-002** in [Input-audit.md](./Input-audit.md)). The semantics used in the pairs below are inferred from the prop names and the Figma variant axes — treat them as best-effort until OX source confirms.

The Text input component lets users enter and edit text on a single line. It is the canonical free-text affordance in 8x8 product surfaces — search bars, form fields for names and emails, numeric quantity inputs, and any context where the value can't be enumerated up-front as a finite set of options. It has a fixed height, fits neatly into form grids, and pairs naturally with a visible label and helper text for accessibility.

---

## Anatomy

The published docs page numbers five parts on the anatomy illustration; in the API and Figma sources these compose as follows:

1. **Label** — the visible text above the field that names what the user is being asked for. Rendered with `typography/body01` in `text/textColor01`. Lives in the `_base_form_label` slot in Figma ([Input-figma.md:77](./Input-figma.md)) and is the value of the `<label htmlFor={id}>` associated with the underlying `<input>` ([accessibility.md:64](./accessibility.md)).
2. **Required symbol** — the visible `*` that signals a required field. Rendered with `typography/bodyBold01` in `error/error01`. The visual `*` is decorative (`aria-hidden="true"`); use `isRequired` ([props.md:81](./props.md)) and `aria-required="true"` on the underlying input for the semantic signal ([accessibility.md:120](./accessibility.md)).
3. **Help icon** — an optional `IconButton` in the label row that opens a tooltip with longer explanatory copy. A separate keyboard focus stop with its own accessible name. Sits inside the `_base_form_label` slot ([Input-figma.md:80](./Input-figma.md)).
4. **Field / Placeholder** *(placeholder optional, and discouraged)* — the `Input Text` container (`bg=ui05`, `px=16`, `py=12`, `border-radius=6`). Placeholder text uses `typography/body02` in `text/textColor02` and is conditional on the `hasPlaceholder` Figma boolean. **Verbatim from the docs page:** "Avoid using placeholders whenever possible as they are not accessible, never use them to communicate important information."
5. **Helper text** *(optional)* — the `_base_form_hint` slot below the field, used for guidance, formatting hints, or — when `hasError` is true — the error message. Rendered with `typography/label01` in `text/textColor02` (or `error/error01` in the error state).

A sixth part is exposed by the variant matrix but not numbered in the docs page anatomy:

6. **Focus ring** — a blue border (`interactive/focus01`, `#0056E0` Light / `#D7E3F9` Dark) that appears on the field when it receives keyboard focus, and persists through the Error+Focus state. Required by WCAG 2.4.7 — **never suppress with `outline: none`** ([accessibility.md:190](./accessibility.md)).

> **Placement (verbatim from the docs page):** "Make sure the input width is proportional to the content that the user has to insert and align to grid columns. The component should also be vertically aligned to other contents of the page."

**Source:** Published docs — Anatomy section · [Input-figma.md:61](./Input-figma.md) · [props.md:70](./props.md). Hardcoded inner-field spacings (16 px h-pad, 12 px v-pad, 6 px border-radius, 4 px label-to-field gap) are flagged as missing spacing tokens — tracked under the Gaps table.

---

## Overview

> **Verbatim from the docs page:** "Inputs are ideal for scenarios where users need to provide short to moderate amounts of text in a single line. They have a fixed height and can be used in forms, search interfaces, and any other context requiring user input."

A single Oxygen package, `@8x8/oxygen-input`, exports one component ([props.md:62](./props.md)):

| Component | Use for | Key props |
|-----------|---------|-----------|
| `Input` | A single-line free-text field — name, email, search query, numeric quantity, etc. | `size`, `isRequired`, `isDisabled`, `isReadOnly`, `hasError`, `iconLeft`, `iconRight`, `suffix`, `fullWidth`, `inputProps` (for `type`, `placeholder`, `aria-*`, `id`, `name`, `value`, `onChange`) |

`Input` renders the raw field only — wrap with `TextField` ([props.md:122](./props.md)) for a complete form row with label, required indicator, help icon, and error message slot.

**Source:** Published docs — Overview section · [props.md:62](./props.md) · [examples.md:31](./examples.md).

---

## Behaviour

### States

The Text input Figma component set ([Input-figma.md:129](./Input-figma.md)) defines six variant axes — `Mode` (Light/Dark), `Size` (Small/Medium/Large), `State` (Rest/Focus/Disabled), `Error` (False/True), `Read Only` (False/True), and `Filled` (False/True). The published docs page names five: **Rest**, **Focus**, **Disabled**, **Read only**, **Error**. Combined, the full visible state matrix is:

| # | State | Trigger | Visual | Token (Light / Dark) |
|---|-------|---------|--------|---------------------|
| 1 | Rest | Default | Solid field background, no border | `ui/ui05` `#F4F3EE` / `#2F2E32` |
| 2 | Hover | Pointer over field | Background shifts lighter | `hover/hover06` `#EBEAE1` / `#666666` |
| 3 | Focus | Keyboard `Tab` or pointer click into field | Blue focus ring/border on field | `interactive/focus01` `#0056E0` / `#D7E3F9` |
| 4 | Filled | User has typed a value | Placeholder replaced by entered text in `text/textColor01` | *(value via `inputProps.value`)* |
| 5 | Disabled | `isDisabled={true}` | Field visually greyed, no interaction, removed from focus order | `interactive/disabled01` `#C8C8BD` / `#C2C2C2` |
| 6 | Read only | `isReadOnly={true}` | Field shows value, no cursor / edit capability | (bg=`ui/ui05`; no edit affordance) |
| 7 | Error + Rest | `hasError={true}`, field not focused | Red border on field + error message row below | `error/error01` `#CB2233` / `#F24D5F` |
| 8 | Error + Focus | `hasError={true}`, field focused | Blue focus ring overrides red border; **error message stays visible** | `interactive/focus01` + `error/error01` (message) |

> **Key behaviour from Figma annotations ([Input-figma.md:286](./Input-figma.md)):** "When an error occurs in the input text field and a user tries to change the text, the border becomes highlighted in-focus state (blue) while the error message stays visible at the bottom." The error message only clears when the value becomes valid.

> ⚠ **Token reconciliation pending.** [tokens.md:50-53](./tokens.md) is missing the dark-mode value for `textColor02` and shows `*(dark value not captured)*` for `error01` Dark. The authoritative bindings — `ui/ui05`, `hover/hover06`, `interactive/disabled01`, `interactive/focus01`, `text/textColor01`, `text/textColor02`, `error/error01` — were resolved via `figma_execute` alias-chain traversal on 2026-05-05 and live in [Input-figma.md:194](./Input-figma.md). This is tracked as `SOURCE_GAP` GAP-010 / GAP-011 in [Input-audit.md](./Input-audit.md); treat the table above as authoritative until `tokens.md` is updated.

### Keyboard

| Key | Behaviour |
|-----|-----------|
| `Tab` / `Shift + Tab` | Move focus to / away from the input |
| Any printable key | Enters text into the field |
| `Backspace` / `Delete` | Remove characters |
| `Enter` | Submits the enclosing `<form>` if present — **no default activation on the Input itself** ([accessibility.md:51](./accessibility.md)) |
| `Escape` | No default behaviour — application-defined (e.g. clear and blur in a search bar) |

The optional help icon button is a **separate focus stop** with its own keyboard tab order — sighted, keyboard, and screen-reader users all reach it independently of the input itself.

**Source:** Published docs — Behavior / States section · [Input-figma.md:274](./Input-figma.md) · [accessibility.md:43](./accessibility.md).

---

## Sizes & dimensions

Three Text input sizes are documented ([Input-figma.md:230](./Input-figma.md)):

| OX value | Figma value | Total height | Notes |
|----------|-------------|--------------|-------|
| `size="small"` | Small | 76 px | Use in dense lists, table-row editors, compact filter rows |
| `size="medium"` | Medium | 84 px | Default for most form layouts |
| `size="large"` | Large | 92 px | Use as a hero / primary field in onboarding or empty states |

- **Width:** 320 px in Figma master; in code the field is responsive — set `fullWidth` for 100 % container width or let it adopt its intrinsic width.
- **Field padding:** 16 px horizontal, 12 px vertical *(hardcoded — no spacing token binding, see Gaps)*.
- **Border radius:** 6 px *(hardcoded)*.
- **Label-to-field gap:** 4 px *(hardcoded)*.

> **Placement (verbatim from the docs page):** "Make sure the input width is proportional to the content that the user has to insert and align to grid columns. The component should also be vertically aligned to other contents of the page."

**Source:** Published docs — Size / Placement sections · [Input-figma.md:227](./Input-figma.md) · [props.md:99](./props.md).

---

## Best Practices

### When to use *(verbatim from the docs page)*

> "The user needs to input information that cannot be predicted with predetermined options."

### When not to use *(verbatim from the docs page)*

> "If the user has to enter a specific option other than a free-form input. If that's the case, consider using a dropdown, radio button or checkbox instead."

To make the boundary concrete:

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The user picks **one** option from a small, known set | A Select / Radio carries the choice constraint in its semantics and prevents typos. | `Select` (for many options) or `Radio` (for ≤ 5 options). |
| The user picks **multiple** options from a known set | Independent multi-select needs the right ARIA role. | `Checkbox` group or multi-select `Select`. |
| The user enters **multi-line** prose (descriptions, notes, comments) | Text input has a fixed height; long content overflows horizontally and clips. | `TextArea` — see [../TextArea/](../TextArea/). |
| The user picks a date, time, or date range | Free-text dates are error-prone; pickers enforce a valid format. | `DateTimeSelector` / `DateTimeRangeSelector`. |
| The user picks a numeric value from a **bounded** range | A slider is faster than typing within a known min/max. | `Slider`. |

**Source:** Published docs — Best Practices section · [props.md:62](./props.md) · [accessibility.md:33](./accessibility.md).

---

## Do / Don't

> These pairs are derived editorially from the docs page's Anatomy + Behavior + Best Practices sections combined with the extracted API and accessibility data. No Figma ✅ Do / ❌ Don't card frames exist for Text input at the time of writing (the `↳ Input examples` page contains accessibility-pattern annotations only, not Do/Don't cards — tracked as **GAP-016** in [Input-audit.md](./Input-audit.md)).

### Pair 1 — Always pair the Input with a visible, persistent label

#### ✅ Do — Pair the Input with a real `<label>` (or `aria-labelledby`)

A visible, persistent label survives input focus, autofill, and assistive-tech navigation. The label is the input's accessible name and the answer to "what am I being asked?"

```tsx
import { Input } from '@8x8/oxygen-input';

<label htmlFor="email">Email address</label>
<Input
  inputProps={{
    id: 'email',
    name: 'email',
    type: 'email',
    'aria-describedby': 'email-hint',
  }}
  onChange={handleChange}
/>
<p id="email-hint">We'll use this to send your receipt.</p>
```

#### ❌ Don't — Use the `placeholder` as the only label

The placeholder disappears the instant the user starts typing, taking the only context with it. Screen readers do not announce it consistently, and visual users lose the label as soon as a value is entered or autofilled. **Verbatim from the docs page:** "Avoid using placeholders whenever possible as they are not accessible, never use them to communicate important information."

```tsx
{/* Wrong — placeholder is not a label */}
<Input
  inputProps={{ placeholder: 'Email address', type: 'email' }}
  onChange={handleChange}
/>
```

**Source:** Published docs — Anatomy (placeholder caveat) · [accessibility.md:79](./accessibility.md) (`hasPlaceholder=false` recommended for new designs) · [Input-figma.md:296](./Input-figma.md) (placeholder accessibility rationale).

---

### Pair 2 — Use helper text for guidance, error text for failures — never blur the two

#### ✅ Do — Put format hints and constraints in the helper slot; use the error slot only when validation fails

Helper text answers "how do I fill this in?". The error region answers "what went wrong?". Keeping them in separate slots — and toggling `hasError` only on failure — lets screen-reader users distinguish guidance from a correction prompt.

```tsx
<label htmlFor="phone">Phone number</label>
<Input
  hasError={isInvalid}
  inputProps={{
    id: 'phone',
    name: 'phone',
    type: 'tel',
    'aria-invalid': isInvalid ? 'true' : 'false',
    'aria-describedby': isInvalid ? 'phone-error' : 'phone-hint',
  }}
/>
{isInvalid
  ? <p id="phone-error" role="alert">Enter a valid 10-digit phone number.</p>
  : <p id="phone-hint">Format: 555-123-4567</p>}
```

#### ❌ Don't — Use the helper text to hold a permanent error-style warning

The helper region is the wrong channel for failure state — colour and role differ. Permanent warnings in the helper slot dull the user's attention to genuine errors and break the visual contract between `hasError` and the red border.

```tsx
{/* Wrong — error-style warning shoved into the helper slot */}
<label htmlFor="phone">Phone number</label>
<Input inputProps={{ id: 'phone', name: 'phone' }} />
<p id="phone-hint" style={{ color: 'red' }}>
  ⚠ Invalid number — please check.
</p>
```

**Source:** Published docs — Anatomy (Helper text) · [accessibility.md:88](./accessibility.md) (`aria-describedby` for helper text) · [examples.md:191](./examples.md) (real-time validation pattern).

---

### Pair 3 — Set `hasError` together with `aria-invalid` and an associated error region

#### ✅ Do — Bind the error message to the field via `aria-errormessage` (or `aria-describedby`) with `role="alert"`

`hasError` paints the red border, but the assistive-tech announcement comes from the associated error region. Without the association, sighted users see red and screen-reader users hear nothing.

```tsx
<label htmlFor="email">Email address</label>
<Input
  hasError
  inputProps={{
    id: 'email',
    name: 'email',
    type: 'email',
    'aria-invalid': 'true',
    'aria-describedby': 'email-error',
    'aria-errormessage': 'email-error',
  }}
/>
<p id="email-error" role="alert">
  Please enter a valid email address.
</p>
```

#### ❌ Don't — Communicate the failure with colour alone

A red border without an associated message fails WCAG 1.4.1 (Use of colour) and 4.1.3 (Status messages). Users with low vision, colour-blindness, or using a screen reader get no signal that anything is wrong.

```tsx
{/* Wrong — red border but no message, no aria-invalid */}
<Input hasError inputProps={{ id: 'email', type: 'email' }} />
```

**Source:** Published docs — Behavior / States (Error) · [accessibility.md:101](./accessibility.md) (`role="alert"` pattern) · [Input-figma.md:286](./Input-figma.md) (error persists through Error+Focus state).

---

### Pair 4 — Pick `size` to match surface density — don't mix sizes in a single form row

#### ✅ Do — Use one `size` per form row, picked to match the surrounding density

Sizes (`small` / `medium` / `large`) map to fixed Figma heights — 76 / 84 / 92 px ([Input-figma.md:230](./Input-figma.md)). Picking one and sticking to it within a form row keeps baselines aligned and the grid honest. The docs page's **Placement** rule — "vertically aligned to other contents of the page" — depends on consistent input heights.

```tsx
<div className="form-row">
  <Input size="medium" inputProps={{ id: 'first-name', placeholder: 'First name' }} />
  <Input size="medium" inputProps={{ id: 'last-name',  placeholder: 'Last name'  }} />
</div>
```

#### ❌ Don't — Mix sizes in the same row to make a field "stand out"

Mismatched heights misalign baselines, break the form grid, and read as a layout bug. Use a visual hierarchy mechanism (a section heading, helper text, or layout grouping) — not a different `size` — to draw attention.

```tsx
{/* Wrong — large + small in the same row */}
<div className="form-row">
  <Input size="large"  inputProps={{ id: 'first-name', placeholder: 'First name' }} />
  <Input size="small"  inputProps={{ id: 'last-name',  placeholder: 'Last name'  }} />
</div>
```

> **Note:** The `size` prop is one of the six undocumented props from [Input-figma.md:131](./Input-figma.md) / **GAP-002** — the `'small' | 'medium' | 'large'` mapping above is taken from [props.md:95](./props.md), which derives it from the Figma variant axis rather than an OX description.

**Source:** Published docs — Size / Placement sections · [Input-figma.md:227](./Input-figma.md) · [props.md:99](./props.md).

---

### Pair 5 — Use `iconLeft` / `iconRight` semantically — never decoratively

#### ✅ Do — Use a leading icon for a semantic affordance (search, currency, lock for read-only)

A leading or trailing icon should mean something — the `SearchIcon` says "this is a search bar"; a currency symbol says "this field expects money"; a clear `×` on the right says "tap to clear". Make the icon button focusable and labelled if it does anything on click.

```tsx
import { SearchIcon } from '@8x8/oxygen-icons';

<label htmlFor="filter">Filter contacts</label>
<Input
  iconLeft={SearchIcon}
  inputProps={{
    id: 'filter',
    type: 'search',
    'aria-label': 'Filter contacts',
  }}
  onChange={handleFilter}
/>
```

#### ❌ Don't — Add a decorative icon that has no functional or semantic meaning

Decorative icons inside the field add visual noise, eat horizontal space, and confuse assistive-tech users who hear an icon name with no associated action. If you must include a brand mark or illustration, place it outside the field — not inside the input row.

```tsx
{/* Wrong — purely decorative icon inside the field */}
<Input
  iconLeft={SparkleIcon}
  inputProps={{ id: 'name', placeholder: 'Your name' }}
/>
```

**Source:** Published docs — Behavior section · [props.md:74](./props.md) (`iconLeft` / `iconRight`) · [accessibility.md:185](./accessibility.md) (WCAG 1.1.1 non-text content).

---

### Pair 6 — Mark required fields with `isRequired` *and* a programmatic signal

#### ✅ Do — Set both `isRequired` and `aria-required="true"`; let the visual `*` stay decorative

`isRequired` paints the `*` indicator; `aria-required` is what assistive tech actually announces. Pairing them keeps the sighted and the non-sighted experience in sync. The visual asterisk should be `aria-hidden="true"` so it isn't read literally as "asterisk" — the component handles this internally (verify in your implementation).

```tsx
<label htmlFor="last-name">
  Last name
</label>
<Input
  isRequired
  inputProps={{
    id: 'last-name',
    name: 'lastName',
    'aria-required': 'true',
  }}
/>
```

#### ❌ Don't — Use only `aria-required` (no visual `*`) or only a visual `*` (no semantic)

A semantic-only signal leaves sighted scanners guessing which fields they must fill. A visual-only signal leaves screen-reader users with no announcement of the constraint. WCAG 1.3.1 expects both channels to agree.

```tsx
{/* Wrong — visual * but no programmatic required */}
<label htmlFor="last-name">Last name <span aria-hidden>*</span></label>
<Input inputProps={{ id: 'last-name' }} />
```

**Source:** Published docs — Anatomy (Required symbol = part 2) · [props.md:81](./props.md) (`isRequired`) · [accessibility.md:120](./accessibility.md) (visual `*` is decorative; use `aria-required`).

---

### Pair 7 — Don't conflate `isDisabled` and `isReadOnly`

#### ✅ Do — Use `isReadOnly` when the value matters but isn't editable now; use `isDisabled` when the field isn't applicable at all

A read-only field still participates in the form: its value is submitted, it's reachable by keyboard, and screen-readers announce it. A disabled field is removed from the focus order and excluded from form submission — the right control when the user has no business interacting with it in this context.

```tsx
{/* Display a stored email that the user can't edit here, but
    needs to see and which is part of the form payload */}
<label htmlFor="account-email">Account email</label>
<Input
  isReadOnly
  inputProps={{
    id: 'account-email',
    name: 'accountEmail',
    value: user.email,
    readOnly: true,
    'aria-readonly': 'true',
  }}
/>

{/* This field doesn't apply to the user's plan tier — disable it */}
<label htmlFor="custom-domain">Custom domain</label>
<Input
  isDisabled
  inputProps={{
    id: 'custom-domain',
    name: 'customDomain',
    disabled: true,
    placeholder: 'Available on Enterprise plans',
  }}
/>
```

#### ❌ Don't — Use `isDisabled` to display a non-editable value

A disabled field removes itself from the focus order and from the form payload — users can't copy the value with keyboard navigation and the server never receives it. Use `isReadOnly` whenever the value is real and meaningful but locked.

```tsx
{/* Wrong — disabled removes from focus order; value won't submit */}
<Input
  isDisabled
  inputProps={{ value: user.email, disabled: true }}
/>
```

**Source:** [props.md:79](./props.md) (`isDisabled` vs `isReadOnly`) · [accessibility.md:132](./accessibility.md) (`isReadOnly` ↔ `aria-readonly`) · [accessibility.md:145](./accessibility.md) (`isDisabled` ↔ `aria-disabled`).

> **Caveat:** The Search input Figma component set has no Read Only variant. Whether `isReadOnly` is supported on the Search input is unresolved — tracked as **CONFLICT-001** in [Input-audit.md](./Input-audit.md). The pair above applies to plain Text input. <!-- TODO: confirm Search input read-only support with designer; either add the variant or document the constraint. -->

---

### Pair 8 — Keep placeholder contrast within WCAG AA — or remove the placeholder altogether

#### ✅ Do — Use a real label + helper text instead of a low-contrast placeholder

The current Figma default — `text/textColor02` `#6C6862` on `ui/ui05` `#F4F3EE` — sits at an estimated ~3.8:1 contrast ratio, **below** the 4.5:1 WCAG 2.1 AA threshold for normal text ([accessibility.md:177](./accessibility.md), **WARN-004** in [Input-audit.md](./Input-audit.md)). The cleanest fix is to drop the placeholder entirely and rely on the visible label + helper text — which is also the docs page's stated guidance.

```tsx
<label htmlFor="city">City</label>
<Input
  inputProps={{
    id: 'city',
    name: 'city',
    'aria-describedby': 'city-hint',
  }}
/>
<p id="city-hint">As shown on your government ID.</p>
```

#### ❌ Don't — Ship the placeholder as the sole prompt and rely on it for legibility

Even when used as a supplemental hint (not as the label), the placeholder must clear 4.5:1 against the field background. The default token pairing currently does not — verify with a contrast checker and remediate the placeholder colour (or drop the placeholder) before shipping.

```tsx
{/* Wrong — placeholder is the only prompt and contrast likely fails AA */}
<Input
  inputProps={{
    id: 'city',
    placeholder: 'City as shown on your government ID',
  }}
/>
```

**Source:** [accessibility.md:177](./accessibility.md) (Color contrast table) · [Input-audit.md WARN-004](./Input-audit.md) · [Input-figma.md:202](./Input-figma.md) (`textColor02` / `ui05` token pairing) · [accessibility.md:79](./accessibility.md) (`hasPlaceholder=false` recommended).

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- Renders a native `<input type="text">` — implicit ARIA role `textbox`; no `role` override needed ([accessibility.md:35](./accessibility.md)). Use `type="search"` for search affordances → implicit `searchbox` role.
- Label is associated via `htmlFor` ↔ `id` or `aria-labelledby` ([accessibility.md:64](./accessibility.md)) — **never** rely on `placeholder` alone.
- `Tab` / `Shift+Tab` move focus; printable keys enter text; `Enter` submits the enclosing `<form>` if present ([accessibility.md:46](./accessibility.md)).
- `hasError` paints the border red — pair with `aria-invalid="true"`, `aria-describedby` (or `aria-errormessage`), and an error region with `role="alert"` ([accessibility.md:101](./accessibility.md)).
- `isRequired` paints the `*` — pair with `aria-required="true"` for the semantic signal ([accessibility.md:120](./accessibility.md)).
- `isReadOnly` keeps the value reachable; `isDisabled` removes the field from the focus order and from form submission ([accessibility.md:132](./accessibility.md)).
- Focus ring must clear 3:1 contrast (WCAG 1.4.11); placeholder text must clear 4.5:1 (WCAG 1.4.3) — **the default placeholder pairing is at risk**, see WARN-004 ([accessibility.md:170](./accessibility.md)).
- Never suppress the focus ring (`outline: none`) — required by WCAG 2.4.7.
- The optional help icon button is a separate focusable element with its own accessible name.

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists these neighbours under **Related → Components**:

- **Buttons** — most often submit the form the Input belongs to. Disable the Submit button when an `Input` is in an error state, or let the submit attempt surface the inline error.

And under **Related → Patterns**:

- **Forms** — the Input is the atom most form rows are built from (label + control + helper text + optional error region).

Additional 8x8 components that absorb work from a plain Text input:

- **TextArea** — single-line vs. multi-line. See [../TextArea/](../TextArea/).
- **Select** / **Radio** / **Checkbox** — when the value set is finite. See Pair 5 of [../Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md).
- **DateTimeSelector** / **DateTimeRangeSelector** — for any date or time value. See [../DateTimeSelector/DateTimeSelector-usage.md](../DateTimeSelector/DateTimeSelector-usage.md).
- **Slider** — for bounded numeric ranges.
- **TextField** — higher-level wrapper that composes Input + label + hint + error ([props.md:122](./props.md)).

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP (GAP-016) | No `↳ Input examples` Figma page with Do/Don't card frames exists. Pairs above are editorially derived from the docs page intent + extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| Search input `isReadOnly` discrepancy | CONFLICT-001 | OX API exposes `isReadOnly` globally but the Figma Search input set has no Read Only variant axis. Out of scope here; resolve with designer before doc-rewrite. |
| 6 props lack OX descriptions | SOURCE_GAP (GAP-002) | `size`, `suffix`, `focus`, `fixed`, `autoSuffixWidth`, `autoPrefixWidth` — semantics in pairs are inferred from prop names + Figma variant axes. |
| 0 clean Storybook examples | SOURCE_GAP (GAP-003) | OX MCP returned 0 snippets; pairs above use hand-derived TSX from the prop API. |
| Inner-field spacings hardcoded | SOURCE_GAP (multiple) | 16 px h-pad, 12 px v-pad, 6 px border-radius, 4 px label-to-field gap, 8 px search-icon gap — none bound to a spacing token. |
| `textColor02` / `error01` dark values | SOURCE_GAP (GAP-010 / GAP-011) | Some dark-mode tokens in [tokens.md](./tokens.md) still show `*(dark value not captured)*`. The state matrix above uses the values resolved on 2026-05-05 and now living in [Input-figma.md](./Input-figma.md). |
| Placeholder contrast likely fails AA | WARN-004 | `#6C6862` on `#F4F3EE` ≈ 3.8:1 vs. 4.5:1 AA threshold for normal text. Pair 8 frames the remediation; needs a measured contrast value + an updated token. |
| Focus ring contrast unverified | SOURCE_GAP (GAP-013) | WCAG 1.4.11 requires ≥ 3:1 for the focus ring. Verify `interactive/focus01` against the field background. |
| Text area + Search input out of scope | SOURCE_GAP (scope) | This document covers Text input only. TextArea has its own folder; Search input shares the API surface but the Figma Read Only / variant axes differ. Document Search in a separate usage doc when its API is clarified. |
| "When not to use" expanded table | DOC_GAP | The published docs page mentions only "use a dropdown, radio button or checkbox instead". The 5-row table in the Best Practices section above is editorial expansion. <!-- TODO: confirm the additional rows (TextArea, DateTimeSelector, Slider) with the Oxygen team and either promote to docs or trim. --> |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/textinput/usage`, fetched 2026-05-13 via Claude_in_Chrome MCP) · Cross-referenced with Oxygen MCP and Figma extraction (`@8x8/oxygen-input`, Figma file `5YihJ5WuDvnvrlrRMC4sBp`, Text input node `22155:36793`) · Editorial draft_
