---
component: Select
package: "@8x8/oxygen-select"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from https://oxygen.8x8.com/components/dropdown/usage (fetched 2026-05-14 via Claude_in_Chrome MCP) cross-referenced with the extracted MCP artifacts (props.md, examples.md, tokens.md, accessibility.md, select-pui.md). No Figma '↳ Select examples' page exists — figma-extract-usage cannot run. Select-figma.md is also absent and two CONFLICTs remain open in Select-audit.md (isAsync type, ref vs forwardedRef) — pairs intentionally avoid asserting around those gaps. Re-run /doc-audit Select after creation; replace pairs with figma-extract-usage output if Figma Do/Don't cards are ever added."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Select/props]]"
  - "[[Select/examples]]"
  - "[[Select/tokens]]"
  - "[[Select/accessibility]]"
  - "[[Select/select-pui]]"
tags:
  - oxygen
  - component/Select
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/dropdown/usage, fetched 2026-05-14 via Claude_in_Chrome MCP) + extracted MCP artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: partial — props.md, examples.md, tokens.md, accessibility.md, select-pui.md, published docs page, Select-audit.md. No Select-figma.md. -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 8 (derived from docs page Best Practices + Behavior + Placement + State sections cross-validated against extracted artifacts) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Select examples" page is created with Do/Don't card frames -->

# Select — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [select-pui.md](./select-pui.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Select examples` Figma page with Do/Don't card frames exists, so `figma-extract-usage` cannot run. The body below transcribes the published Oxygen docs page for Select / Dropdown (`https://oxygen.8x8.com/components/dropdown/usage`, fetched 2026-05-14) verbatim where the page asserts something, and derives Do/Don't pairs from the page's Best Practices + Behavior + Placement + State sections cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), and [accessibility.md](./accessibility.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

> ⚠️ **No Figma-extracted spec yet.** [component-lib/Select/](./) has no `Select-figma.md` — the Desktop Bridge was offline during the original extract session (see `Select-audit.md` `GAP-001`). The state and token tables below lean on [tokens.md](./tokens.md) and [accessibility.md](./accessibility.md) only — per-state colour bindings are flagged `UNKNOWN — pending Select-figma.md` until `figma-extract Select` runs against node `2105:2` in file `5YihJ5WuDvnvrlrRMC4sBp`.

> ⚠️ **Two open CONFLICTs in `Select-audit.md`.** (1) `isAsync` is typed `boolean` in one MCP endpoint and `IsAsync` in another (`GAP-002`). (2) The MCP Storybook example uses `<Select ref={...} />` while [props.md:75](./props.md) documents `forwardedRef` (`GAP-003`). The Do / Don't pairs below intentionally avoid `ref` examples and avoid type annotations on `isAsync`. The `SelectOption` shape is also undefined in source (`GAP-004`), so options are shown inline (`{ value, label }`) without type annotations.

---

Select is the canonical single- or multi-select control for picking from a list of options that's too long to display inline. In 8x8 product surfaces it's the default for >5 options, for searchable / async lists, and any time the user needs a chip-style multi-select inside a form. It is built on top of [react-select](https://react-select.com/) — most react-select props pass through ([props.md:65](./props.md)).

---

## Anatomy

The published docs page numbers four parts on the anatomy illustration ([oxygen.8x8.com/components/dropdown/usage](https://oxygen.8x8.com/components/dropdown/usage)):

1. **Label** — the visible heading rendered above the field. Maps to `labelValue` ([props.md:92](./props.md)). Programmatically associates with the control via `htmlFor` / `aria-labelledby` ([accessibility.md:40](./accessibility.md)).
2. **Select field** — the trigger row (input + dropdown chevron + optional clear `×`). The input renders a placeholder via `placeholder` ([props.md:100](./props.md)) when no value is selected, an optional `iconLeft` ([props.md:82](./props.md)), and the `ClearIndicator` when `isClearable` is `true` (default) ([props.md:86](./props.md)).
3. **Helper text** *(optional)* — copy rendered below the field. The Oxygen API does not expose a `helperText` prop directly; consuming surfaces render their own helper or error element beneath the Select (see the error guidance in Pair 6 and [accessibility.md:79](./accessibility.md)).
4. **Popover** — the floating menu containing the option list. Opens on click / Enter / Arrow Down. Each option carries `role="option"` and the selected option(s) `aria-selected="true"` ([accessibility.md:33](./accessibility.md)).

Two further optional parts are exposed by the API but not numbered in the docs page anatomy:

5. **Info icon button + tooltip** *(optional)* — rendered when `infoBoxText` is set, with the accessible name provided by `infoBoxButtonLabel` ([props.md:83](./props.md), [accessibility.md:41](./accessibility.md)).
6. **Required indicator** *(optional)* — the `*` shown when `isRequired={true}`; the control also receives `aria-required` ([props.md:91](./props.md), [accessibility.md:38](./accessibility.md)).
7. **Action element** *(optional)* — text + onClick rendered alongside the label via `action` / `actionLabel` ([props.md:72](./props.md)).

The exact horizontal gap between the label and the field, and the popover ↔ trigger offset, are not currently captured — to be confirmed in `Select-figma.md`.

---

## Overview / variants

A single Oxygen package, `@8x8/oxygen-select`, exports the main component and a set of customisable sub-components ([props.md:107](./props.md)):

| Export | Use for |
|--------|---------|
| `Select` (default) | The main control. |
| `VirtualMenuList` | Virtualised menu list — pass via `components={{ MenuList: VirtualMenuList }}` for ~1000+ options ([examples.md:112](./examples.md)). |
| `ClearIndicator`, `DropdownIndicator`, `SingleValue`, `MultiValue`, `ValueContainer` | Targeted sub-component overrides via the `components` prop ([props.md:74](./props.md)). |

The API supports several distinct usage modes, configured via boolean props rather than separate components:

| Mode | Toggle | Key props | Notes |
|------|--------|-----------|-------|
| **Single-select** | *(default)* | `options`, `value`, `onChange` | One value at a time. |
| **Multi-select** | `isMulti` | `isMulti`, `hasCheckbox`, `multipleSelectMaxRows`, `hasShortMultiDisplay`, `hideSelectedOptions` ([props.md:76,80,81,90,95](./props.md)) | Chips displayed in the field; `hasCheckbox` adds tick boxes inside the menu. |
| **Async** | `isAsync` | `isAsync`, `loadOptions`, `loadingMessage`, `isLoading` ([props.md:85,89,93,94](./props.md)) | `loadOptions(inputValue, callback)` replaces `options`. **See CONFLICT note above — do not type-annotate `isAsync` until `GAP-002` resolves.** |
| **Creatable** | `isCreatable` | `isCreatable` ([props.md:87](./props.md)) | User can type and create options not in the list. |
| **Icons in options** | `hasIcons` | `hasIcons`, `iconLeft` ([props.md:78,82](./props.md)) | Use only when the icon adds meaning. |
| **Virtual menu** | *(via `components`)* | `components={{ MenuList: VirtualMenuList }}` ([examples.md:117](./examples.md)) | Required for ≥1000 options to avoid scroll jank. |

**Source:** [props.md:64](./props.md) · [examples.md:42–157](./examples.md) · docs page Overview.

---

## Behaviour

### Interaction *(verbatim from the docs page)*

> "When a user clicks on the select, a list of options is displayed from the select. When he/she selects one of the options, the select label changes to reflect user selections and the list of options closes."

### States *(docs page + extracted artifacts)*

The docs page names four primary states: **Rest, Hover, Focused, Disabled**. [accessibility.md:78](./accessibility.md) and [props.md:125](./props.md) add **Open**, **Selected**, **Error**, and **Read-only** as separately rendered variants:

| # | State | Trigger | Visual change | Token |
|---|-------|---------|---------------|-------|
| 1 | Rest | Default | Standard border, no menu | `UNKNOWN — pending Select-figma.md` |
| 2 | Hover | Pointer over the field | Border emphasis | `UNKNOWN — pending Select-figma.md` |
| 3 | Focus | Keyboard `Tab` lands on the field | Visible focus ring (WCAG 2.4.7) | `UNKNOWN — pending Select-figma.md` |
| 4 | Open | Click / Enter / Arrow Down | Popover visible; `aria-expanded="true"` | `UNKNOWN — pending Select-figma.md` |
| 5 | Selected | One or more options chosen | Value text (single) or chips (multi) replace placeholder; selected option(s) carry `aria-selected="true"` ([accessibility.md:36](./accessibility.md)) | Selected-option row background: `ui01` ([tokens.md:33](./tokens.md)) |
| 6 | Disabled | `isDisabled={true}` | Reduced opacity, no interaction; `aria-disabled="true"` ([accessibility.md:37](./accessibility.md)) | `UNKNOWN — pending Select-figma.md` |
| 7 | Read-only | Figma variant (no direct boolean prop documented) | Muted appearance, non-editable | `UNKNOWN — pending Select-figma.md` |
| 8 | Error | `hasError={true}` | Red border + sibling error message; `aria-invalid="true"` ([accessibility.md:39](./accessibility.md)) | `UNKNOWN — pending Select-figma.md` |
| 9 | Loading | `isLoading={true}` or async fetch in flight | Spinner + `loadingMessage`; `aria-busy="true"` ([accessibility.md:42](./accessibility.md)) | `UNKNOWN — pending Select-figma.md` |

> ⚠️ **Per-state colour tokens not yet documented.** Only `ui01` (selected option row background) was returned by the MCP token search ([tokens.md:33](./tokens.md)). The other state tokens — border rest / hover / focus, focus ring, error red, disabled opacity, popover shadow — are defined inside the package's styled-components and not exposed as standalone theme tokens ([tokens.md:35](./tokens.md), audit `GAP-011` / `WARN-002`). Don't hand-assert token names here. <!-- TODO: replace `UNKNOWN` cells with confirmed token bindings once figma-extract Select runs. -->

### Keyboard *(verbatim from [accessibility.md:47–57](./accessibility.md))*

| Key | Behaviour |
|-----|-----------|
| `Tab` | Move focus to the Select |
| `Shift + Tab` | Move focus away from the Select |
| `Enter` / `Space` | Open dropdown (when closed); select focused option (when open) |
| `↓` Arrow Down | Open dropdown (when closed); move focus to next option (when open) |
| `↑` Arrow Up | Move focus to previous option (when open) |
| `Escape` | Close dropdown without selecting |
| `Home` / `End` | Jump to first / last option in the list |
| Printable characters | Jump to option starting with typed character(s) |
| `Backspace` / `Delete` | Remove last selected chip (when `isMulti`) |

> All keyboard guidance is inferred from react-select's documented behaviour ([accessibility.md:27](./accessibility.md), audit `GAP-013`). Confirm against rendered DOM before publishing externally.

**Source:** Published docs — Behavior / State sections · [accessibility.md:47](./accessibility.md) · [tokens.md:47](./tokens.md).

> **Heads up — copy issue on the docs page.** The published page has a second "Behavior" section that begins *"When the coachmark is triggered…"* — this paragraph references Coachmark, not Select, and is almost certainly a copy-paste error on the docs site. It is **not** transcribed here. New gap surfaced by this draft (see Gaps table): report upstream so the docs page is corrected.

---

## Placement & overflow

### Placement *(verbatim from the docs page)*

> "Usually a select is used in a form element. By default, the width of the select is set to fixed. Alternatively, the width of the select is fluid as its parent container size."

### Inside a modal *(from [examples.md:74–110](./examples.md))*

When the Select sits inside a `Modal`, the menu will be clipped or hidden behind the modal mask unless it's portal'd out. Capture the modal root via a callback ref and pass it to `menuPortalTarget`, and prefer `menuPlacement="auto"` so the menu opens upward when there isn't room below ([examples.md:47–53](./examples.md)). Both `menuPortalTarget` and `menuPlacement` are react-select pass-throughs and are currently undocumented in [props.md](./props.md) (audit `GAP-005` / `GAP-006`) — they will land in `props.md` during doc-rewrite.

---

## Sizes & spacing

[tokens.md:39–43](./tokens.md) captures the three size variants:

| `size` prop | Figma label | Input height |
|-------------|-------------|--------------|
| `'small'` | Small | 76 px |
| `'default'` | Medium | 84 px |
| `'large'` | Large | 92 px |

> ⚠️ **Naming mismatch.** The code value `'default'` maps to the Figma label "Medium" — engineers and designers should expect this disconnect when cross-referencing tickets (audit `GAP-012`). [props.md:102](./props.md) explicitly notes this.

The internal field padding, label-to-field gap, and menu-to-trigger offset are not yet documented and will be confirmed in `Select-figma.md`.

---

## Best Practices

### When to use *(verbatim from the docs page)*

> "Use select when there are more than five options. Otherwise, use a radio button for a single selection or a checkbox for multiple selections."

> "Use a select when you want to create a list of options for the user to choose."

Practically, reach for Select when **any** of these is true:

- The option list has **more than five** items (the docs-page threshold).
- The full list won't fit comfortably inline as Radio Buttons or Checkboxes.
- Options need to be **searched, filtered, or fetched** rather than scanned.
- The user might want to pick **many** items at once and see them as chips (`isMulti`).

### When not to use *(combines docs page + editorial)*

The docs page states only one rule: *"Do not use a select when your list of options is less than five."* Cross-referencing patterns elsewhere in Oxygen:

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Fewer than five options, single-select | The full list comparison is part of the decision. *(verbatim from the docs page)* | `Radio` / `RadioGroup` — see [../Radio/Radio-usage.md](../Radio/Radio-usage.md) Pair 4. |
| Fewer than five options, multi-select | Same reasoning — every option should be visible at once. | `Checkbox` / `CheckboxGroup` — see [../Checkbox/Checkbox-usage.md](../Checkbox/Checkbox-usage.md). |
| Two-option binary toggle that takes effect immediately | A Select reads as "pick a value" not "flip this setting". | `ToggleButton`. |
| Free-form input with autocomplete suggestions | The user is typing, not choosing from a closed list. | An Autocomplete pattern (or `Select` with `isCreatable` if the closed list is the source of truth and free-form is an exception). |

**Source:** Published docs — Best Practices / Related sections · [examples.md:165](./examples.md) (verbatim "Usage guidance") · cross-validated against [../Radio/Radio-usage.md](../Radio/Radio-usage.md) Pair 4 and [../Checkbox/Checkbox-usage.md](../Checkbox/Checkbox-usage.md).

---

## Do / Don't

> These pairs are derived editorially from the docs page's Best Practices, Behavior, State, and Placement sections combined with the extracted API and accessibility data. No Figma ✅ Do / ❌ Don't card frames exist for Select at the time of writing. Treat as provisional until a designer reviews them or a Figma examples page is created. Pairs intentionally avoid `ref` examples (`GAP-003`), token names (`GAP-011`), and `SelectOption` type annotations (`GAP-004`).

### Pair 1 — Reach for Select when the option list is too long for Radio / Checkbox

#### ✅ Do — Use Select for >5 options or a searchable list

The docs page draws an explicit line: more than five options → Select. Below that line, Radio (single) or Checkbox (multi) wins because users compare alternatives side-by-side.

```tsx
import Select from '@8x8/oxygen-select';

const countries = [
  { value: 'AF', label: 'Afghanistan' },
  { value: 'AL', label: 'Albania' },
  /* …200 more rows… */
  { value: 'ZW', label: 'Zimbabwe' },
];

<Select
  labelValue="Country"
  options={countries}
  placeholder="Select a country"
/>
```

#### ❌ Don't — Use Select for a 2 or 3 option choice

A Select hides options behind an extra click and replaces a one-glance comparison with an open / scan / close cycle. Use Radio for binary or near-binary picks; the docs page is explicit: *"Otherwise, use a radio button for a single selection or a checkbox for multiple selections."*

```tsx
{/* Wrong — three options that should be Radios */}
<Select
  labelValue="Billing cadence"
  options={[
    { value: 'monthly', label: 'Monthly' },
    { value: 'annual',  label: 'Annual' },
    { value: 'custom',  label: 'Custom' },
  ]}
/>
```

**Source:** Published docs — Best Practices (verbatim) · [examples.md:167](./examples.md) · inverse-rule cross-check in [../Radio/Radio-usage.md](../Radio/Radio-usage.md) Pair 4.

---

### Pair 2 — Use `isMulti` (with `hasCheckbox` when helpful) for genuine multi-select

#### ✅ Do — Render a single multi-select Select when one decision yields several values

`isMulti` produces a chip-style display ([props.md:90](./props.md)) and emits an array onChange. `hasCheckbox` adds tick boxes in the menu so users can see what's already selected; `multipleSelectMaxRows` caps the chip stack height before scrolling.

```tsx
const [tags, setTags] = useState<{ value: string; label: string }[]>([]);

<Select
  labelValue="Tags"
  isMulti
  hasCheckbox
  multipleSelectMaxRows={2}
  options={tagOptions}
  value={tags}
  onChange={(next) => setTags(next as { value: string; label: string }[])}
/>
```

#### ❌ Don't — Stack several single-select Selects to fake multi-select

Stacking single Selects breaks the mental model (one decision, many values), forces redundant clicks, leaves no obvious "remove" affordance per choice, and produces no canonical array shape for the form. If the user is picking *several* items for *one* slot, use `isMulti`.

```tsx
{/* Wrong — three single Selects for one logical field */}
<Select labelValue="Tag 1" options={tagOptions} />
<Select labelValue="Tag 2" options={tagOptions} />
<Select labelValue="Tag 3" options={tagOptions} />
```

**Source:** [props.md:76,90,95](./props.md) · [examples.md:42](./examples.md) (multi-select example with checkboxes).

---

### Pair 3 — Use `isAsync` + `loadOptions` for remote or very large data

#### ✅ Do — Stream options from the server when the full list is huge or external

When the option set lives in a backend (a user directory, a knowledge-base index, country lookup, etc.), `isAsync` swaps the static `options` array for a `loadOptions(inputValue, callback)` function ([props.md:85,94](./props.md)). The Select shows `loadingMessage` ([props.md:93](./props.md)) and sets `aria-busy="true"` ([accessibility.md:42](./accessibility.md)) while results are in flight.

```tsx
const loadUsers = (inputValue, callback) => {
  fetch(`/api/users?q=${encodeURIComponent(inputValue)}`)
    .then((r) => r.json())
    .then((rows) => callback(rows.map((u) => ({ value: u.id, label: u.name }))));
};

<Select
  labelValue="Assignee"
  isAsync
  loadOptions={loadUsers}
  loadingMessage="Loading users…"
  placeholder="Search by name"
/>
```

#### ❌ Don't — Pre-load 10 000 rows into `options`

Pre-loading a huge static list ships unnecessary bytes, makes the menu jank on open, and makes "filter" feel slow. If the dataset really does need to ship client-side (no network access, offline mode), use the **virtual menu** instead — wrap `VirtualMenuList` via `components={{ MenuList: VirtualMenuList }}` so only the visible rows render ([examples.md:112–134](./examples.md)).

```tsx
{/* Wrong — 10 000 options eagerly serialised into the bundle */}
import Select from '@8x8/oxygen-select';

let i = 0;
const options10k = Array.from({ length: 10000 }, () => {
  i += 1;
  return { value: i, label: `Option ${i}` };
});

<Select options={options10k} />
```

> The `isAsync` prop is type-conflicted in source (`boolean` vs `IsAsync` — audit `GAP-002`). The example above passes the boolean shorthand `isAsync` (truthy) only; do not annotate the prop type until the conflict is resolved.

**Source:** [props.md:85,93,94](./props.md) · [examples.md:112–157](./examples.md) (VirtualMenuList) · [accessibility.md:42](./accessibility.md).

---

### Pair 4 — Always pair Select-in-Modal with `menuPortalTarget` + `menuPlacement="auto"`

#### ✅ Do — Portal the menu out of the modal stacking context

Without a portal, the popover is clipped by the modal's `overflow` rules or pushed below the modal's z-index, and the menu effectively disappears. Capture the modal root via a callback ref and feed it to `menuPortalTarget`, and use `menuPlacement="auto"` so the menu flips to open upwards when the trigger is near the viewport bottom ([examples.md:47–110](./examples.md)).

```tsx
import Select from '@8x8/oxygen-select';
import Modal, { ModalHeader, ModalContent, ModalFooter } from '@8x8/oxygen-modal';

const [portalTarget, setPortalTarget] = useState<HTMLElement | null>(null);

<Modal portalRef={(el) => setPortalTarget(el)}>
  <ModalHeader title="Pick an option" />
  <ModalContent>
    <Select
      labelValue="Option"
      options={options}
      menuPortalTarget={portalTarget}
      menuPlacement="auto"
    />
  </ModalContent>
  <ModalFooter>{/* … */}</ModalFooter>
</Modal>
```

#### ❌ Don't — Drop a vanilla Select into a Modal

The menu will clip, overflow, or hide behind the modal mask; users see a Select that "doesn't open." This is the single most reported regression on Select-in-Modal surfaces.

```tsx
{/* Wrong — menu clips inside ModalContent's overflow */}
<Modal>
  <ModalContent>
    <Select labelValue="Option" options={options} />
  </ModalContent>
</Modal>
```

**Source:** [examples.md:74–110](./examples.md) (SelectModal example) · audit `GAP-005` / `GAP-006` (both pass-through props pending in [props.md](./props.md)). The Modal `portalRef` shape should be validated against the current `@8x8/oxygen-modal` release (audit `WARN-001`).

---

### Pair 5 — Give every Select a meaningful `labelValue` (and use `infoBoxText` only for context)

#### ✅ Do — Visible label via `labelValue`; reserve the info button for extra detail

`labelValue` renders the visible label that `htmlFor` / `aria-labelledby` ties to the control ([accessibility.md:40,72](./accessibility.md)). Use `infoBoxText` for the "why" — a tooltip the user can opt into. The info button is a **separate focus stop** and **must** carry an accessible name via `infoBoxButtonLabel` or it will be announced as unlabelled ([accessibility.md:64](./accessibility.md), [props.md:84](./props.md)).

```tsx
<Select
  labelValue="Compliance region"
  infoBoxText="Region determines which data-residency policy applies to the workspace."
  infoBoxButtonLabel="More info about compliance region"
  options={regionOptions}
/>
```

#### ❌ Don't — Rely on the `placeholder` to label the field

`placeholder` disappears the moment a value is chosen — there is then no visible label at all, and assistive tech announces the control without a name ([accessibility.md:72](./accessibility.md)). Likewise, dropping `labelValue` and showing the label as plain prose elsewhere breaks the `htmlFor` association.

```tsx
{/* Wrong — no labelValue; the placeholder is doing label duty */}
<Select
  placeholder="Compliance region"
  options={regionOptions}
/>
```

**Source:** [props.md:83–84,92,100](./props.md) · [accessibility.md:40,64,72](./accessibility.md). Mirrors [../Radio/Radio-usage.md](../Radio/Radio-usage.md) Pair 5.

---

### Pair 6 — Pair `hasError` with a visible message — not red border alone

#### ✅ Do — Render `hasError={true}` *and* a sibling error element

`hasError` flips the visual error state and sets `aria-invalid="true"` on the control ([props.md:77](./props.md), [accessibility.md:39](./accessibility.md)), but the error **message** is not part of the Select — consuming surfaces must render it themselves below the field. WCAG 3.3.1 requires the error to be programmatically determinable, so wire the message in with `aria-describedby` ([accessibility.md:79](./accessibility.md)) where possible.

```tsx
const errorId = 'region-error';

<>
  <Select
    labelValue="Compliance region"
    options={regionOptions}
    hasError={!region}
    inputProps={{ 'aria-describedby': errorId }}
  />
  {!region && (
    <p id={errorId} role="alert" className="error-text">
      Pick a region before continuing.
    </p>
  )}
</>
```

#### ❌ Don't — Set `hasError` and call it done

A red border alone fails colour-only communication checks and leaves screen-reader users with no idea **what** is wrong. Users who don't perceive the colour will repeatedly retry the same submission.

```tsx
{/* Wrong — visual error state with no message */}
<Select labelValue="Compliance region" options={regionOptions} hasError />
```

**Source:** [props.md:77](./props.md) · [accessibility.md:39,63,79](./accessibility.md) (WCAG 3.3.1 row) · audit `GAP-007` (no error example exists in `examples.md` yet — doc-rewrite will add one).

---

### Pair 7 — Be deliberate about `isClearable` on required fields

#### ✅ Do — Set `isClearable={false}` (or guard the clear) when the field is required

`isClearable` defaults to `true` ([props.md:86](./props.md)), so by default the field renders a clear `×` that drops the value back to nothing. On a required field that's a footgun — users can clear, blur, and submit an empty value that's still flagged as "required" with a visible chosen state moment-before. Either set `isClearable={false}` or pair clearing with explicit error handling.

```tsx
<Select
  labelValue="Plan"
  isRequired
  isClearable={false}
  options={planOptions}
  value={plan}
  onChange={setPlan}
/>
```

#### ❌ Don't — Leave `isClearable` at default on a required Select with no clear-handler

The default-true clear button silently invalidates the value with no user-visible feedback unless the form surrounds it with validation. The control still says "required" (`*` + `aria-required`) but the clear behaviour contradicts that affordance.

```tsx
{/* Wrong — required + clearable, no clear handler, no error state on empty */}
<Select
  labelValue="Plan"
  isRequired
  options={planOptions}
  value={plan}
  onChange={setPlan}
/>
```

**Source:** [props.md:86,91](./props.md) · [accessibility.md:38](./accessibility.md) (`aria-required` set when `isRequired`).

---

### Pair 8 — Keep `placeholder` short, action-shaped, and distinct from the label

#### ✅ Do — Use `placeholder` as a one-line hint about *what* to pick

The placeholder disappears the moment the user selects a value, so any information it carries is lost. Keep it to a short verb-phrase that previews the kind of choice — "Select a region", "Choose a billing cadence" — and rely on `labelValue` for the persistent label and `infoBoxText` for context.

```tsx
<Select
  labelValue="Region"
  placeholder="Select a region"
  options={regionOptions}
/>
```

#### ❌ Don't — Stuff explanation into `placeholder` or duplicate the label

A long `placeholder` overflows the field, wraps awkwardly, and vanishes on select. Repeating the label inside the placeholder doubles the visual weight and adds nothing for screen-reader users (the label is already announced).

```tsx
{/* Wrong — placeholder is doing the job of infoBoxText / labelValue */}
<Select
  labelValue="Region"
  placeholder="Region — the data-residency region for this workspace, which determines compliance, latency, and which storage tier the workspace will be billed against"
  options={regionOptions}
/>
```

**Source:** [props.md:92,100](./props.md) · Docs-page Anatomy (Label and Select field are separate parts) · mirrors the equivalent pair in [../Radio/Radio-usage.md](../Radio/Radio-usage.md) Pair 5.

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- The trigger renders `role="combobox"` with `aria-haspopup="listbox"` and `aria-expanded` toggling on open ([accessibility.md:33](./accessibility.md)).
- The popover renders `role="listbox"`; each item renders `role="option"`; selected option(s) carry `aria-selected="true"` ([accessibility.md:34–36](./accessibility.md)).
- `labelValue` produces a visible `<label>` programmatically associated with the control — **always provide it** ([accessibility.md:40,61](./accessibility.md)).
- `isRequired={true}` sets `aria-required="true"` in addition to the visible `*` ([accessibility.md:38](./accessibility.md)).
- `hasError={true}` sets `aria-invalid="true"` — pair with a visible error message for WCAG 3.3.1 ([accessibility.md:39,63,79](./accessibility.md)).
- `isDisabled={true}` sets `aria-disabled="true"` and removes the control from the focus order ([accessibility.md:37](./accessibility.md)).
- `isLoading={true}` / async fetch sets `aria-busy="true"` and announces `loadingMessage` ([accessibility.md:42,65](./accessibility.md)).
- The info button (`infoBoxText`) is a **separate focus stop** — its accessible name comes from `infoBoxButtonLabel` ([accessibility.md:41,64](./accessibility.md)).
- The focus ring is visible on the trigger; never suppress with `outline: none` (WCAG 2.4.7, [accessibility.md:78](./accessibility.md)).

> ⚠️ **All accessibility guidance here is inferred from react-select + the WAI-ARIA combobox pattern.** Audit `GAP-013` flags that the rendered DOM has not yet been confirmed. Don't ship external-facing material based on this section alone without spot-checking.

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists these neighbours under **Related → Components**:

- **Button** — for action triggers (a Select is a value-picker, not an action).
- **Checkbox** — for non-exclusive (multi-select) options when the full list is short. See Pair 1 inverse.
- **Radio button** — for single-select when the full list is short and visible. See [../Radio/Radio-usage.md](../Radio/Radio-usage.md).

Editorial additions, based on the inverse rules in the table above:

- **ToggleButton** — for instant-effect on/off settings.
- **Autocomplete / combobox with free-form input** — when the user types rather than picks. Use `isCreatable` here only if the closed list is the source of truth and free-form is an exception.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ Select examples` Figma page with Do/Don't card frames exists. Pairs above are editorially derived from the docs page intent + extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| `Select-figma.md` not extracted | SOURCE_GAP | `figma-extract Select` has not been run (Desktop Bridge was offline — audit `GAP-001`). Per-state token bindings (rest, hover, focus ring, error, disabled, popover shadow), variant axes, and the leading-visuals frame (icon/status/avatar) are not yet documented. Treat the state table above as visual-only until tokens are confirmed. |
| `isAsync` type CONFLICT | CONFLICT | OX MCP returns `boolean` from one endpoint and `IsAsync` from another for the same prop (audit `GAP-002`). Pair 3 intentionally avoids type annotations on `isAsync`. Resolve by inspecting `@8x8/oxygen-select` TypeScript exports. |
| `ref` vs `forwardedRef` CONFLICT | CONFLICT | [props.md:75](./props.md) documents `forwardedRef`, [examples.md:70](./examples.md) uses standard `ref=` (audit `GAP-003`). No Do/Don't pair touches `ref` until resolved. |
| `SelectOption` type undefined | DOC_GAP | The `options` prop is typed `SelectOption[]` but the interface is never defined in source (audit `GAP-004`). Examples here use inline `{ value, label }` without type annotations. |
| Theme tokens unresolved | DOC_GAP | [tokens.md:33](./tokens.md) returned only `ui01`; rest / hover / focus / error / disabled / popover-shadow tokens are not exposed (audit `GAP-011` / `WARN-002`). The State × Token cells above use `UNKNOWN — pending Select-figma.md` placeholders. |
| Accessibility inferred only | SOURCE_GAP | All ARIA / keyboard guidance is inferred from react-select; not yet confirmed from rendered DOM (audit `GAP-013`). Spot-check before publishing externally. |
| Docs-page "coachmark" paragraph | DOC_GAP | The published docs page contains a stray Coachmark paragraph inside the second Behavior section. Not transcribed above; report upstream so the page is corrected. |
| `menuPortalTarget` / `menuPlacement` props undocumented | DOC_GAP | Both used in [examples.md](./examples.md) but missing from [props.md](./props.md) (audit `GAP-005`, `GAP-006`). Pair 4 names them; doc-rewrite will add them to the props table. |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/dropdown/usage`, fetched 2026-05-14 via Claude_in_Chrome MCP) · Cross-referenced with Oxygen MCP extraction (`@8x8/oxygen-select`) and the existing audit (`Select-audit.md`) · Editorial draft_
