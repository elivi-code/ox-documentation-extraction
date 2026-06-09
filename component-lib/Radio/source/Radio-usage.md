---
component: Radio
package: "@8x8/oxygen-radio"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from https://oxygen.8x8.com/components/radiobutton/usage (fetched 2026-05-14 via Claude_in_Chrome MCP) cross-referenced with extracted MCP artifacts (props.md, examples.md, tokens.md, accessibility.md). No Figma '↳ Radio examples' page exists — figma-extract-usage cannot run. Re-run /doc-audit Radio after creation; replace pairs with figma-extract-usage output if Figma Do/Don't cards are ever added."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Radio/props]]"
  - "[[Radio/examples]]"
  - "[[Radio/tokens]]"
  - "[[Radio/accessibility]]"
tags:
  - oxygen
  - component/Radio
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/radiobutton/usage, fetched 2026-05-14 via Claude_in_Chrome MCP) + extracted MCP artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: partial — props.md, examples.md, tokens.md, accessibility.md, published docs page. No Radio-figma.md and no doc-audit yet. -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 6 (derived from docs page Best Practices + Variants + Behavior + Overflow sections cross-validated against extracted artifacts) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Radio examples" page is created with Do/Don't card frames -->

# Radio — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Radio examples` Figma page with Do/Don't card frames exists, so `figma-extract-usage` cannot run. The body below transcribes the published Oxygen docs page for Radio Button (`https://oxygen.8x8.com/components/radiobutton/usage`, fetched 2026-05-14) verbatim where the page asserts something, and derives Do/Don't pairs from the page's Best Practices + Behavior + Overflow content cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), and [accessibility.md](./accessibility.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

> ⚠️ **No Figma-extracted spec yet.** [component-lib/Radio/](./) has no `Radio-figma.md`. The state/token table below leans on [tokens.md](./tokens.md) and [accessibility.md](./accessibility.md) only — colour and per-state bindings are flagged as gaps until `figma-extract Radio` is run.

Radio Buttons are input controls that let a user **select exactly one option** from a related group. Selecting a new option automatically deselects the previously selected one. They are the canonical single-select affordance in 8x8 product surfaces: form choices, plan pickers, side-panel filters, modal confirmations, and any setting where the choices are mutually exclusive and the full list is short enough to display at once.

---

## Anatomy

The published docs page numbers four parts on the anatomy illustration ([oxygen.8x8.com/components/radiobutton/usage](https://oxygen.8x8.com/components/radiobutton/usage)):

1. **Group label** *(optional)* — the accessible name of the `RadioGroup`. Provides the context that ties the options together. The group label should label the `radiogroup` via `aria-labelledby` / `aria-label` ([accessibility.md:30](./accessibility.md)).
2. **Unselected radio button** — the open circle drawn when `isChecked` is `false` ([props.md:70](./props.md)).
3. **Selected radio button** — the filled circle drawn when `isChecked` is `true` ([props.md:70](./props.md)).
4. **Label** — the option text rendered to the right of the input (in left-to-right languages). Maps to the `label` prop ([props.md:67](./props.md)).

Two further optional parts are exposed by the API but not numbered in the docs page anatomy:

5. **Info icon button + tooltip** *(optional)* — rendered when `infoBoxText` is set. A separate keyboard focus stop with its accessible name supplied by `infoBoxButtonLabel` ([props.md:73](./props.md), [accessibility.md:31](./accessibility.md)).
6. **Focus ring** — covers the **entire Radio row** (input + label area), not just the input circle ([accessibility.md:47](./accessibility.md)). Required by WCAG 2.4.7 — **never suppress with `outline: none`**.

> **Hit area (verbatim from `accessibility.md`):** "The focus ring encompasses the entire Radio Button row — from the Radio Button Input to the label. The whole row area is interactive, clickable, and responsive to hover actions." ([accessibility.md:47](./accessibility.md))

The exact horizontal gap between the input circle and its label is not currently captured — to be confirmed in `Radio-figma.md`.

---

## Overview

A single Oxygen package, `@8x8/oxygen-radio`, exports two components ([props.md:58](./props.md)):

| Component | Use for | Key props |
|-----------|---------|-----------|
| `Radio` | A single option inside a group | `label`, `value`, `name`, `isChecked`, `isDisabled`, `infoBoxText`, `infoBoxButtonLabel`, `onChange` |
| `RadioGroup` | The container that wraps two or more `Radio` children and manages selection state | `value`, `onChange`, `isHorizontal`, `name`, `children` |

`Radio` is **always used inside** `RadioGroup`. The group compares its `value` prop against each child's `value` to decide which option is checked ([props.md:100](./props.md), [examples.md:34](./examples.md)).

### Variants *(verbatim from the docs page)*

> "In this component you can find a vertical and an horizontal option that can be used accordingly."

The default is vertical; horizontal layout is opt-in via `RadioGroup`'s `isHorizontal` prop ([props.md:95](./props.md), [examples.md:51](./examples.md)).

**Source:** Published docs — Overview / Variants sections · [props.md:62](./props.md) · [examples.md:30](./examples.md).

---

## Behaviour

### States *(from docs page + extracted artifacts)*

The docs page names the visible states explicitly:

> "There are mainly two states: unselected and selected. … In addition to this, this component also has states for unselected disabled, selected disabled and focus."

Cross-referencing [tokens.md:49](./tokens.md), the full visible state matrix is:

| # | State | Trigger | Visual change |
|---|-------|---------|---------------|
| 1 | Unselected / Rest | Default | Open circle, 2 px border |
| 2 | Hover | Pointer over the row | Background / border emphasis (transient — no API prop) |
| 3 | Focus | Keyboard `Tab` lands on the row | Focus ring covers the **whole row** ([accessibility.md:47](./accessibility.md)) |
| 4 | Selected (checked) | `isChecked={true}` (or matched by `RadioGroup` `value`) | Filled inner dot inside the circle |
| 5 | Unselected disabled | `isDisabled={true}` on an unchecked Radio | Muted border, no interaction ([props.md:71](./props.md)) |
| 6 | Selected disabled | `isDisabled={true}` on a checked Radio | Muted filled circle, no interaction |

> ⚠️ **Per-state colour tokens not yet documented.** [tokens.md:25](./tokens.md) reports "No dedicated Radio-specific theme tokens were returned by the Oxygen MCP token search." The authoritative per-state bindings (rest border, selected fill, focus ring, disabled border / fill) should come from `Radio-figma.md` — which has not been extracted yet. Don't hand-assert token names here. <!-- TODO: replace this table with confirmed token bindings once figma-extract Radio runs. -->

### Keyboard *(verbatim from [accessibility.md:39](./accessibility.md))*

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus into the radio group (to the checked option, or first option if none selected) |
| `Arrow Up` / `Arrow Left` | Moves focus to **and selects** the previous radio in the group |
| `Arrow Down` / `Arrow Right` | Moves focus to **and selects** the next radio in the group |
| `Tab` (from last item) | Moves focus out of the radio group to the next focusable element |
| `Space` | Selects the focused radio button (if not already selected) |

Two important consequences of this pattern:

- **Arrow keys both move focus and change selection** — this is the WAI-ARIA Radio Group pattern. Don't try to decouple them.
- **The radio group is a single Tab stop.** Once focused, the user uses arrow keys to move between options, not `Tab`. Setting `tabindex` manually on each Radio breaks the pattern.

The info icon button (`infoBoxText`) is a **separate focus stop** with its own keyboard tab order — sighted, keyboard, and screen-reader users all reach it independently of the radio itself ([accessibility.md:55](./accessibility.md)).

**Source:** Published docs — Behavior / States section · [accessibility.md:39](./accessibility.md) · [tokens.md:49](./tokens.md).

---

## Placement & overflow

### Placement *(verbatim from the docs page)*

> "Radio button labels are positioned to the right of their inputs in languages that read left to right. In this component you can also find two diferent directions; horizontal and vertical. The use for each one should be determined by the space in the UI designated for this component."

### Overflow content *(verbatim from the docs page)*

> "Radio buttons should be short and concise, but in the cases that the space is limited the label should wrap and the radio button icon and label should aligned to the top."

Cross-validated against [accessibility.md:75](./accessibility.md): "When a label text wraps to a second line or more, the Radio Button Input alignment stays at the top of the label text (not centered)." See also the multiline example at [examples.md:185](./examples.md).

---

## Sizes & spacing

[tokens.md:31](./tokens.md) captures the only explicit dimension currently extracted:

- **Gap between Radio items in a `RadioGroup`:** `$spacing(2)` = **8 px** (confirmed via Figma node `50606:93474`).

> The exact horizontal gap between the **input circle** and **its own label** is not yet documented — `Radio-figma.md` has not been generated. Don't hand-assert a pixel value here.

**Source:** [tokens.md:31](./tokens.md) · [examples.md:58](./examples.md) (gap call-out under the horizontal-group example).

---

## Best Practices

### When to use *(verbatim from the docs page)*

> "You can use this component in forms, modals, side panels, full pages, etc."

Practically, reach for Radio Buttons when **all** of these are true:

- The user must pick **exactly one** option from a related set.
- The full list of options is short enough to show at once (typically ≤ 5 options).
- Seeing every option side-by-side helps the user choose — they're comparing alternatives, not searching.

### When not to use *(combines docs page + editorial)*

The docs page states only one rule: "If the user can select multiple options, use checkboxes instead." Cross-referencing the patterns observed elsewhere in the Oxygen system, the broader "when not to use" table is:

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The user can pick **more than one** option | Radio is single-select by definition. *(verbatim from the docs page)* | `Checkbox` / `CheckboxGroup`. |
| The control toggles a setting that takes effect **immediately** (e.g. "Notifications on/off") | A two-option Radio reads as "pick A or B" rather than "flip this setting now". | `ToggleButton`. |
| There are **many** options and vertical space is constrained | A long list of radios overflows the surface and slows scanning. | A single-select `Select` / dropdown. |
| You need a **purely visual** indicator (read-only state) | A radio advertises interactivity; assistive tech announces it as an input control. | Plain text, `Tag`, or an icon. |

**Source:** Published docs — Best Practices / Related sections · [accessibility.md:28](./accessibility.md) (native `radiogroup` / `radio` roles) · cross-validated against [../Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md) Pair 1 (inverse rule).

---

## Do / Don't

> These pairs are derived editorially from the docs page's Behavior / Variants / Overflow / Best Practices sections combined with the extracted API and accessibility data. No Figma ✅ Do / ❌ Don't card frames exist for Radio at the time of writing (the `↳ Radio examples` page is absent). Treat as provisional until a designer reviews them or a Figma examples page is created.

### Pair 1 — Reach for Radio when exactly one option must be selected

#### ✅ Do — Use Radio for mutually-exclusive single-select

Each `RadioGroup` enforces single-select by tracking one `value`. Use it when picking option A must clear option B.

```tsx
import { Radio, RadioGroup } from '@8x8/oxygen-radio';

const [plan, setPlan] = useState<'monthly' | 'annual'>('monthly');

<RadioGroup value={plan} onChange={(v: string) => setPlan(v as 'monthly' | 'annual')}>
  <Radio name="plan" label="Monthly billing" value="monthly" testId="radio-monthly" />
  <Radio name="plan" label="Annual billing"  value="annual"  testId="radio-annual" />
</RadioGroup>
```

#### ❌ Don't — Use Radio when more than one option can be selected

If the user can choose several options simultaneously, the affordance lies: arrow keys will silently switch the selection between unrelated items, and the `radiogroup` semantics misrepresent the constraint. Use `Checkbox` / `CheckboxGroup` instead — the docs page is explicit: *"If the user can select multiple options, use checkboxes instead."*

```tsx
{/* Wrong — these are independent choices; use Checkbox */}
<RadioGroup value={selectedChannel} onChange={setSelectedChannel}>
  <Radio name="channels" label="Email" value="email" />
  <Radio name="channels" label="SMS"   value="sms" />
  <Radio name="channels" label="Push"  value="push" />
</RadioGroup>
```

**Source:** Published docs — Best Practices → When not to use (verbatim) · [accessibility.md:28](./accessibility.md) · [props.md:88](./props.md) (`RadioGroup` `value` is singular).

---

### Pair 2 — Preselect a default option in every RadioGroup

#### ✅ Do — Ship a `RadioGroup` with one option already selected

The docs page states this directly:

> "It's important to know that for default view for a radio button group is to have one of them preselected."

Pick the safest or most common option as the default. The grounded note in [examples.md:44](./examples.md) reinforces this: *"Default layout is vertical. One option should always be preselected."*

```tsx
const [billing, setBilling] = useState('monthly'); // ← preselected

<RadioGroup value={billing} onChange={setBilling}>
  <Radio name="billing" label="Monthly" value="monthly" />
  <Radio name="billing" label="Annual"  value="annual" />
</RadioGroup>
```

#### ❌ Don't — Ship a `RadioGroup` with nothing selected

An unselected `RadioGroup` makes the keyboard pattern awkward (`Tab` lands on the first item, but no option is committed), forces the user into an extra step, and breaks the docs-page expectation. If you genuinely have no safe default, ask whether a different control — `Select` with a placeholder, or two independent `ToggleButton`s — is a better fit.

```tsx
{/* Wrong — no default; the group has no committed value when the user arrives */}
<RadioGroup value={undefined} onChange={setBilling}>
  <Radio name="billing" label="Monthly" value="monthly" />
  <Radio name="billing" label="Annual"  value="annual" />
</RadioGroup>
```

**Source:** Published docs — Behavior / States section (verbatim) · [examples.md:44](./examples.md).

---

### Pair 3 — Always wrap related Radios in a `RadioGroup` with a group label

#### ✅ Do — Use `RadioGroup` and give the group an accessible name

`RadioGroup` provides the `role="radiogroup"` container that ties options together for assistive tech ([accessibility.md:28](./accessibility.md)). Pair it with a visible heading immediately above the group (which screen readers reach via `aria-labelledby`), or — when no visible label is possible — set `aria-label` on the container.

```tsx
<>
  <h3 id="billing-cadence">Billing cadence</h3>
  <RadioGroup value={billing} onChange={setBilling} aria-labelledby="billing-cadence">
    <Radio name="billing" label="Monthly" value="monthly" testId="radio-monthly" />
    <Radio name="billing" label="Annual"  value="annual"  testId="radio-annual" />
  </RadioGroup>
</>
```

#### ❌ Don't — Free-float bare `Radio` components without a `RadioGroup` container

Without `RadioGroup`, the `radiogroup` role is absent: arrow keys won't roving-tabindex between options, the group has no shared `name`, and assistive tech announces each radio as an isolated control. Visually, the `$spacing(2)` rhythm between options ([tokens.md:31](./tokens.md)) also breaks down.

```tsx
{/* Wrong — no group container, no shared selection state, no group label */}
<Radio name="r1" label="Monthly" value="monthly" />
<p>Some unrelated paragraph.</p>
<Radio name="r2" label="Annual"  value="annual" />
```

**Source:** Published docs — Anatomy (Group label is part 1) · [accessibility.md:28](./accessibility.md) (`role="radiogroup"`) · [tokens.md:31](./tokens.md) (group gap).

---

### Pair 4 — Reserve Radio for short lists; reach for `Select` when the list grows

#### ✅ Do — Use Radio when the full set of options is visible at once

Radio shines when the user can scan all alternatives in one glance and the comparison itself is part of the decision (e.g. 2–5 plans, yes/no/maybe, billing cadence). The docs page's example surfaces — forms, modals, side panels — implicitly assume a short list.

```tsx
<RadioGroup value={plan} onChange={setPlan}>
  <Radio name="plan" label="Basic"      value="basic" />
  <Radio name="plan" label="Standard"   value="standard" />
  <Radio name="plan" label="Enterprise" value="enterprise" />
</RadioGroup>
```

#### ❌ Don't — Stack 10+ options as Radios

A long vertical Radio list overflows the surface, slows scanning, and makes arrow-key navigation tedious. If the option list is long, paginated, or commonly searched, use a single-select `Select` / dropdown — it collapses to one row of UI and supports type-to-search.

```tsx
{/* Wrong — country picker as a 200-row RadioGroup; use Select instead */}
<RadioGroup value={country} onChange={setCountry}>
  <Radio name="country" label="Afghanistan" value="AF" />
  <Radio name="country" label="Albania"     value="AL" />
  {/* … 200 more rows … */}
</RadioGroup>
```

**Source:** Published docs — Placement section (verbatim — "use … should be determined by the space in the UI") · cross-validated against [../Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md) "many options + space pressure" rule.

---

### Pair 5 — Put short text in `label`; put context in `infoBoxText`

#### ✅ Do — Keep `label` tight and action-shaped; use `infoBoxText` for the "why"

The label is the option name; the info button — a separate focus stop with its own accessible name from `infoBoxButtonLabel` — is for the explanation. This keeps the visible Radio rows scannable and lets users opt into more detail.

```tsx
<RadioGroup value={plan} onChange={setPlan}>
  <Radio
    name="plan"
    label="Standard plan"
    value="standard"
    testId="radio-standard"
  />
  <Radio
    name="plan"
    label="Enterprise plan"
    value="enterprise"
    testId="radio-enterprise"
    infoBoxText="Includes advanced features and dedicated support."
    infoBoxButtonLabel="More info about Enterprise plan"
  />
</RadioGroup>
```

#### ❌ Don't — Pack the explanation into `label`

Long labels wrap (the docs page's overflow rule kicks in and the radio top-aligns to the first line — see [accessibility.md:75](./accessibility.md)), defeat scanning, and force every user — sighted or not — to read the full sentence before they can compare options.

```tsx
{/* Wrong — the label is doing the job of infoBoxText */}
<Radio
  name="plan"
  label="Enterprise plan — includes advanced features and dedicated support, including a named CSM, SSO, audit logging, and 24/7 premium phone support."
  value="enterprise"
/>
```

**Source:** [props.md:73](./props.md) (`infoBoxText` + `infoBoxButtonLabel`) · [accessibility.md:55](./accessibility.md) (info button is a separate focus stop) · [examples.md:74](./examples.md). Mirrors [../Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md) Pair 7.

---

### Pair 6 — Use horizontal layout only when labels are short and the set is small

#### ✅ Do — Use `isHorizontal` for binary or near-binary choices with short labels

The horizontal variant works best for two- or three-option choices whose labels fit comfortably side-by-side (Yes/No, On/Off, Annual/Monthly). The `$spacing(2)` (8 px) gap between items ([tokens.md:31](./tokens.md)) is tight — anything longer than ~12 characters per label will feel cramped.

```tsx
<RadioGroup value={answer} onChange={setAnswer} isHorizontal>
  <Radio name="confirm" label="Yes" value="yes" testId="radio-yes" />
  <Radio name="confirm" label="No"  value="no"  testId="radio-no" />
</RadioGroup>
```

#### ❌ Don't — Force a long-label list into a horizontal row

Horizontal layout breaks down once labels wrap or the row count exceeds three: the input circle top-aligns to multi-line labels ([accessibility.md:75](./accessibility.md)), which looks intentional only when each label is a single line. Stick to the default vertical layout in those cases.

```tsx
{/* Wrong — long labels + horizontal layout = cramped, wrapped, hard to scan */}
<RadioGroup value={plan} onChange={setPlan} isHorizontal>
  <Radio name="plan" label="Basic — for individuals" value="basic" />
  <Radio name="plan" label="Standard — for small teams" value="standard" />
  <Radio name="plan" label="Enterprise — for organisations with advanced needs" value="enterprise" />
</RadioGroup>
```

**Source:** Published docs — Placement section ("use … should be determined by the space in the UI") · [props.md:95](./props.md) (`isHorizontal`) · [examples.md:51](./examples.md) ("Use horizontal layout when space is limited and options are short") · [tokens.md:31](./tokens.md) (`$spacing(2)` group gap).

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- `RadioGroup` renders a `role="radiogroup"` container that groups its options for assistive tech ([accessibility.md:28](./accessibility.md)).
- Each `Radio` is a native `<input type="radio">` with implicit ARIA role `radio` ([accessibility.md:29](./accessibility.md)).
- The group label is the accessible name of the `radiogroup` — supplied via `aria-labelledby` (heading nearby) or `aria-label` on the container ([accessibility.md:30](./accessibility.md)).
- `Tab` enters/exits the group; **arrow keys move focus and select within the group**. `Space` selects the focused option if it isn't already selected ([accessibility.md:39](./accessibility.md)).
- The focus ring covers the **entire row** (input + label), not just the input circle ([accessibility.md:47](./accessibility.md), [accessibility.md:62](./accessibility.md)) — never suppress with `outline: none` (WCAG 2.4.7).
- The info button (`infoBoxText`) is a **separate focus stop** with its own accessible name from `infoBoxButtonLabel` ([accessibility.md:55](./accessibility.md)).
- When a label wraps to multiple lines, the input circle top-aligns with the first line of text — don't override this ([accessibility.md:75](./accessibility.md)).
- `isDisabled={true}` sets `disabled` + `aria-disabled="true"` and removes the input from the focus order ([accessibility.md:33](./accessibility.md)).

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists these neighbours under **Related**:

- **Components → Checkbox** — for non-exclusive (multi-select) options. See Pair 1.
- **Patterns → Forms** — Radio groups are most often used inside the broader Forms pattern (group label + radios + hint + error).

Editorial additions, based on the inverse rules in the table above:

- **ToggleButton** — for instant-effect on/off settings.
- **Select** — for single-select when the option list is too long for inline Radios.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ Radio examples` Figma page with Do/Don't card frames exists. Pairs above are editorially derived from the docs page intent + extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| `Radio-figma.md` not extracted | SOURCE_GAP | `figma-extract Radio` has not been run. Per-state token bindings (rest border, selected fill, focus ring, disabled border / fill) and the input ↔ label horizontal gap are not yet documented. Treat the state table above as visual-only until tokens are confirmed. |
| Radio-specific theme tokens | DOC_GAP | [tokens.md:25](./tokens.md): "No dedicated Radio-specific theme tokens were returned by the Oxygen MCP token search." Awaiting `Radio-figma.md` extraction to resolve the per-state bindings via Figma variable lookups. |
| `RadioGroup` `<fieldset>` / `<legend>` emission | DOC_GAP | The current [accessibility.md](./accessibility.md) recommends `aria-labelledby` / `aria-label` on the `radiogroup`, but doesn't confirm whether Oxygen's `RadioGroup` emits a native `<fieldset>` / `<legend>` wrapper. If it does not, consuming surfaces should supply one. <!-- TODO: verify rendered DOM emits fieldset/legend; remove this caveat once confirmed. --> |
| `RadioGroup` error / hint pattern | DOC_GAP | The Slot-based form-field pattern in [examples.md:149](./examples.md) shows a Header / Slot / Footer / Error layout, but Oxygen has not documented the canonical `aria-describedby` / `aria-live` wiring for RadioGroup errors. Consuming surfaces should pattern-match against `CheckboxGroup` error guidance until this is captured. |
| "When not to use" prose | DOC_GAP | The published docs page covers only one "when not to use" rule (multi-select → Checkbox). The four-row table above is editorial. <!-- TODO: confirm the three additional "When not to use" rows with the Oxygen team and either promote to docs or trim. --> |
| Per-state colour token resolution | DOC_GAP | The state matrix above intentionally omits token names; the authoritative bindings should come from `Radio-figma.md` (Figma variable traversal), not from guesswork against the broader theme. |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/radiobutton/usage`, fetched 2026-05-14 via Claude_in_Chrome MCP) · Cross-referenced with Oxygen MCP extraction (`@8x8/oxygen-radio`) and the Figma node references already captured in [examples.md:197](./examples.md) and [accessibility.md:100](./accessibility.md) · Editorial draft_
