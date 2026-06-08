---
component: Checkbox
package: "@8x8/oxygen-checkbox"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (https://oxygen.8x8.com/components/checkbox/usage, fetched 2026-05-12 via Claude_in_Chrome MCP) cross-referenced with extracted MCP/Figma artifacts. The published docs page contains Anatomy, Overview, Variants, Behaviour (Usage / States / Nesting), Best Practices (When to use), and Related sections — but NO Do/Don't card frames and NO accessibility section. Do/Don't pairs below are derived from the docs page intent + props.md, examples.md, tokens.md, accessibility.md, and checkbox-figma.md. Re-run /doc-audit Checkbox after creation; replace pairs with figma-extract-usage output if a Figma ↳ Checkbox examples page is ever populated with Do/Don't cards."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/examples]]"
  - "[[Checkbox/tokens]]"
  - "[[Checkbox/accessibility]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-audit]]"
tags:
  - oxygen
  - component/Checkbox
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/checkbox/usage, fetched 2026-05-12 via Claude_in_Chrome MCP) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, checkbox-figma.md, checkbox-pui.md, checkbox-audit.md, published docs page -->
<!-- DRAFTED: 2026-05-12 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 7 (derived from docs page Best Practices + Nesting section + extracted artifacts) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ Checkbox examples" page is created with Do/Don't card frames -->

# Checkbox — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [checkbox-figma.md](./checkbox-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ Checkbox examples` Figma page with Do/Don't card frames exists, so `figma-extract-usage` cannot run. The body below transcribes the published Oxygen docs page for Checkbox (`https://oxygen.8x8.com/components/checkbox/usage`, fetched 2026-05-12) verbatim where the page asserts something, and derives Do/Don't pairs from the page's Best Practices + Nesting intent cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), and [checkbox-figma.md](./checkbox-figma.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

> ⚠️ **Beta API.** The Checkbox Figma info card carries a **Beta** badge ([checkbox-figma.md:200](./checkbox-figma.md)). Expect API churn — `CheckboxGroup` in particular only exposes `isHorizontal` in [props.md:78](./props.md), while the Figma component set exposes `header`, `footer`, and `isError` slots ([checkbox-figma.md:111](./checkbox-figma.md)) that may correspond to props not yet returned by the Oxygen MCP. Tracked as GAP-008 / GAP-009 in [checkbox-audit.md](./checkbox-audit.md).

Checkboxes are input controls that let a user **select one or more options** from a list. Each checkbox is independent — selecting one does not unselect another — unless the checkbox is nested under a parent checkbox, in which case the parent reflects the aggregate state of its children. They are the canonical multi-select affordance in 8x8 product surfaces: form filters, permission lists, terms-and-conditions acknowledgements, and "select all" patterns in tables and lists.

---

## Anatomy

The published docs page numbers four parts on the anatomy illustration; in the API and Figma sources these compose as follows:

1. **Group label** *(optional)* — the `<legend>` (or equivalent) of a `CheckboxGroup`. Provides the accessible name for the set of related options. See [accessibility.md:84](./accessibility.md) and [checkbox-figma.md:71](./checkbox-figma.md) (`header` slot on Checkbox Group, default `true`).
2. **Selected checkbox** — the 20 × 20 px square filled with `ui/ui22` and a white check glyph. See [checkbox-figma.md:141](./checkbox-figma.md).
3. **Unselected checkbox** — the 20 × 20 px square with a 2 px `ui/ui21` border on transparent background. See [checkbox-figma.md:140](./checkbox-figma.md).
4. **Label** — the action text rendered with `text/textColor01`, positioned **to the right of the input** with vertical stacking for legibility. Maps to the `label` prop ([props.md:57](./props.md)).

Two further optional parts are exposed by the API but not numbered in the docs page anatomy:

5. **Info icon button + tooltip** *(optional)* — rendered when `infoBoxText` is set. The icon is a separate keyboard focus stop with its accessible name supplied by `infoBoxButtonLabel` ([props.md:60](./props.md), [accessibility.md:41](./accessibility.md)).
6. **Focus ring** — a 2 px `interactive/focus01` outline on keyboard focus ([checkbox-figma.md:143](./checkbox-figma.md)). Required by WCAG 2.4.7 — **never suppress with `outline: none`**.

> **Group spacing (verbatim from the docs page):** "Always maintain a padding of `$spacing04` between the title and label and `$spacing03` between labels."

The horizontal gap between input and label is visible in the layout but the exact px value is not currently captured — tracked as `SOURCE_GAP` GAP-004 in [checkbox-audit.md](./checkbox-audit.md).

---

## Overview

A single Oxygen package, `@8x8/oxygen-checkbox`, exports two components ([props.md:84](./props.md)):

| Component | Use for | Key props |
|-----------|---------|-----------|
| `Checkbox` | A single binary option, or a single row inside a group | `label`, `isChecked`, `isIndeterminate`, `isDisabled`, `infoBoxText`, `onChange` |
| `CheckboxGroup` | Two or more related options laid out together | `isHorizontal` (the only documented prop) — see GAP-008 below |

### Variants (verbatim from the docs page)

- **Single checkbox** — used for a binary option, e.g. terms and conditions at the end of a form.
- **Multiple checkboxes** — used when the user can choose between various options. The set may have a group label, and the options can be nested.

### Nesting (verbatim from the docs page)

> "Checkboxes can have a parent-and-child relationship with other checkboxes.
>
> - When the parent checkbox is unselected all the child checkboxes are unselected.
> - When a parent checkbox is selected all the child checkboxes are selected.
>
> If some checkboxes are checked, the parent checkbox will be in an intermediate state. If an intermediate state is unselected then it will uncheck the parent and all the nested items."

The intermediate state is exposed via the `isIndeterminate` prop ([props.md:64](./props.md)). It maps to `aria-checked="mixed"` and requires the consumer to **also** set the DOM `indeterminate` property — see [accessibility.md:63](./accessibility.md).

**Source:** Published docs — Overview / Variants / Nesting sections · [props.md:51](./props.md) · [examples.md:77](./examples.md).

---

## Behaviour

### States

The Figma Checkbox Input component set ([checkbox-figma.md:78](./checkbox-figma.md)) defines six variant axes — `Mode` (Light/Dark), `State` (Rest/Hover), `isChecked`, `isIndeterminate`, `isDisabled`, `isFocused`. The published docs page names three: **Rest**, **Focus**, **Disabled**. Combined, the full visible state matrix is:

| # | State | Trigger | Visual change | Token |
|---|-------|---------|---------------|-------|
| 1 | Unchecked / Rest | Default | 2 px border, transparent fill | `ui/ui21` |
| 2 | Hover | Pointer over | Border / fill brightens (transient — no API prop) | (variant only) |
| 3 | Focus | Keyboard `Tab` | 2 px outline ring | `interactive/focus01` |
| 4 | Checked | `isChecked={true}` | Filled square, white check glyph | `ui/ui22` |
| 5 | Indeterminate | `isIndeterminate={true}` | Filled square, white dash glyph | `ui/ui22` |
| 6 | Disabled | `isDisabled={true}` | Muted fill, no hover/focus | `interactive/disabled02` |
| 7 | Error *(group)* | `CheckboxGroup` `isError` variant in Figma | Red border + error message | `error/error01` |

> ⚠️ **Token reconciliation pending.** [tokens.md](./tokens.md) still contains speculative `blue05`/`blue06` language ([tokens.md:55](./tokens.md)). The authoritative bindings — `ui/ui21`, `ui/ui22`, `interactive/disabled02`, `interactive/focus01`, `text/textColor01`, `error/error01` — were resolved via `figma_execute` alias-chain traversal on 2026-05-05 and live in [checkbox-figma.md:136](./checkbox-figma.md). This is tracked as `DOC_GAP` GAP-002 in [checkbox-audit.md](./checkbox-audit.md); treat the table above as authoritative until `tokens.md` is updated.

> ⚠️ **`isError` is in Figma but not in `props.md`.** [checkbox-figma.md:114](./checkbox-figma.md) shows an `isError` variant on `CheckboxGroup`; [props.md:72](./props.md) lists only `isHorizontal`. Tracked as `SOURCE_GAP` GAP-008. Don't hand-write `<CheckboxGroup isError />` against the current API surface until the prop is confirmed in package source.

### Keyboard

| Key | Behaviour |
|-----|-----------|
| `Tab` / `Shift + Tab` | Move focus to / away from the checkbox |
| `Space` | Toggle checked / unchecked |
| `Enter` | **No action** — per the WAI-ARIA Checkbox pattern, Enter does not activate ([accessibility.md:53](./accessibility.md)) |

The info icon button (`infoBoxText`) is a **separate focus stop** with its own keyboard tab order — sighted, keyboard, and screen-reader users all reach it independently of the checkbox itself ([accessibility.md:41](./accessibility.md)).

**Source:** Published docs — Behaviour / States section · [checkbox-figma.md:78](./checkbox-figma.md) · [accessibility.md:46](./accessibility.md).

---

## Sizes & dimensions

Only one Checkbox size is documented in Oxygen ([checkbox-figma.md:166](./checkbox-figma.md)):

- **Input control:** 20 × 20 px square.
- **Full row (input + label):** 128 × 20 px in the Figma master, but the label takes its natural intrinsic width at runtime.
- **Group items:** 320 × 168 px per Figma variant ([checkbox-figma.md:186](./checkbox-figma.md)).

### Spacing (verbatim from the docs page)

- `$spacing04` between the group title and the first checkbox label.
- `$spacing03` between successive checkbox labels in a vertical stack.

> The exact horizontal gap between the **input square** and **its own label** is not currently measured — `get_design_context` was unavailable at extraction time. Tracked as `SOURCE_GAP` GAP-004 in [checkbox-audit.md](./checkbox-audit.md). Don't hand-assert a pixel value here.

**Source:** Published docs — Anatomy section · [checkbox-figma.md:163](./checkbox-figma.md) · [examples.md:128](./examples.md).

---

## Best Practices

### When to use *(verbatim from the docs page)*

- Single or multiple checkboxes can be used in forms for selection from a list of options on a single page, modal, or panel.
- A single checkbox can be used in terms and conditions to indicate whether you agree or disagree.

### When not to use *(editorial — not on the docs page)*

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The user can pick **only one** option from a set | Checkbox affords independent multi-select; a mutually-exclusive control needs a different role / different aria semantics. | Radio. (The docs page lists Radio buttons under Related — see below.) |
| The control toggles a setting that takes effect **immediately** (e.g. "Enable notifications" with no Save button) | Checkboxes are typically committed by a form submit; instant-effect toggles read more naturally as switches. | `ToggleButton`. (The docs page lists Toggle under Related.) |
| There are **many** options and vertical space is constrained | A long list of checkboxes overflows surfaces and slows scanning. | A multi-select `Select` / dropdown with checkbox rows. |
| You need a **purely visual** indicator (read-only state) | A checkbox advertises interactivity; assistive tech announces it as a control. | Plain text, `Tag`, or an icon. |

**Source:** Published docs — Best Practices section · [props.md:51](./props.md) · [accessibility.md:35](./accessibility.md) (native `<input type="checkbox">` role).

---

## Do / Don't

> These pairs are derived editorially from the docs page's Variants, Nesting, and Best Practices sections combined with the extracted API and accessibility data. No Figma ✅ Do / ❌ Don't card frames exist for Checkbox at the time of writing (the `↳ Checkbox examples` page is absent — GAP-001 in [checkbox-audit.md](./checkbox-audit.md)).

### Pair 1 — Reach for Checkbox when the user can select more than one

#### ✅ Do — Use Checkbox for independent, multi-select options

Each checkbox is independent. Use the control when picking option A does not preclude picking option B.

```tsx
import { Checkbox, CheckboxGroup } from '@8x8/oxygen-checkbox';

<CheckboxGroup>
  <Checkbox id="email"   name="channels" label="Email"   value="email"   isChecked={email}   onChange={(e) => setEmail(e.target.checked)} />
  <Checkbox id="sms"     name="channels" label="SMS"     value="sms"     isChecked={sms}     onChange={(e) => setSms(e.target.checked)} />
  <Checkbox id="push"    name="channels" label="Push"    value="push"    isChecked={push}    onChange={(e) => setPush(e.target.checked)} />
</CheckboxGroup>
```

#### ❌ Don't — Use Checkbox when only one selection is allowed

If picking option A must clear option B, a checkbox lies about the affordance: keyboard and screen-reader users hear "checkbox, not checked" rather than "radio button, not selected", and the group's `aria-checked` semantics misrepresent the constraint.

```tsx
{/* Wrong — these are mutually exclusive; use Radio */}
<CheckboxGroup>
  <Checkbox label="Annual billing"  isChecked={plan === 'annual'}  onChange={() => setPlan('annual')} />
  <Checkbox label="Monthly billing" isChecked={plan === 'monthly'} onChange={() => setPlan('monthly')} />
</CheckboxGroup>
```

**Source:** Published docs — Overview section (independence of selection) · [accessibility.md:35](./accessibility.md) (native `checkbox` role) · Related → Radio buttons.

---

### Pair 2 — Use a single Checkbox for binary commitments, not for instant-effect toggles

#### ✅ Do — Use a single Checkbox for terms-and-conditions or other form-committed binary choices

Single-checkbox-as-binary works when the state is committed by a form submit (or an explicit Save action). The user can review the value before applying it.

```tsx
<Checkbox
  id="terms"
  name="terms"
  label="I agree to the terms and conditions"
  value="terms"
  isChecked={agreed}
  onChange={(e) => setAgreed(e.target.checked)}
/>
<Button type="submit" isDisabled={!agreed}>Sign up</Button>
```

#### ❌ Don't — Use a Checkbox for a setting that takes effect immediately

A checkbox doesn't visually signal "I am a switch you flip and the system reacts now". Use `ToggleButton` for instant-effect settings; reserve Checkbox for form fields whose value is part of a pending submission.

```tsx
{/* Wrong — this toggles a notification setting instantly; use ToggleButton */}
<Checkbox label="Send me product updates" isChecked={isSubscribed} onChange={(e) => updateSubscription(e.target.checked)} />
```

**Source:** Published docs — Variants → Single checkbox (terms-and-conditions example) · Related → Toggle.

---

### Pair 3 — Pair `isIndeterminate` with a real "select all" parent

#### ✅ Do — Use `isIndeterminate` only on a parent that has at least one selected child

The indeterminate visual (a dash, not a tick) tells the user "some — but not all — of my children are selected". Setting it without children, or without a parent/child relationship, lies about the state. The Oxygen docs page describes this pattern in full under **Nesting**.

```tsx
const childIds = ['a', 'b', 'c'];
const someSelected = childIds.some(id => selected.includes(id));
const allSelected  = childIds.every(id => selected.includes(id));

<Checkbox
  id="select-all"
  name="selectAll"
  label="Select all items"
  value="all"
  isChecked={allSelected}
  isIndeterminate={someSelected && !allSelected}
  onChange={handleSelectAll}
/>
{childIds.map(id => (
  <Checkbox
    key={id}
    id={id}
    label={`Item ${id}`}
    value={id}
    isChecked={selected.includes(id)}
    onChange={(e) => toggleChild(id, e.target.checked)}
  />
))}
```

#### ❌ Don't — Set `isIndeterminate` to convey "loading", "partial validation", or "unknown"

Indeterminate is for an aggregate of children, not a generic third state. Screen readers announce `aria-checked="mixed"` — anything other than a real parent/child group will be confusing to assistive-tech users.

```tsx
{/* Wrong — this checkbox has no children; "mixed" misrepresents the state */}
<Checkbox label="Saving…" isIndeterminate />
```

**Source:** Published docs — Nesting section · [accessibility.md:63](./accessibility.md) (`aria-checked="mixed"` + DOM `indeterminate` property required) · [examples.md:77](./examples.md).

---

### Pair 4 — Always ship a Checkbox with an accessible name

#### ✅ Do — Pass a `label` (or a visually-equivalent labelled node)

The `label` prop is wired to `<label htmlFor={id}>`, so it is **the** accessible name for the input ([accessibility.md:72](./accessibility.md)). Keep it concise and action-oriented — what does selecting this option do or commit?

```tsx
<Checkbox
  id="receive-updates"
  name="receiveUpdates"
  label="Receive monthly product updates"
  value="updates"
  isChecked={updates}
  onChange={(e) => setUpdates(e.target.checked)}
/>
```

#### ❌ Don't — Ship a Checkbox with no `label` and rely on adjacent body copy

Screen readers will announce the input as "checkbox, not checked" with no further context. Visual users get the same loss when label text is reflowed or hidden by a CSS rule.

```tsx
{/* Wrong — no accessible name */}
<p>I agree to the terms and conditions</p>
<Checkbox id="terms" />
```

**Source:** Published docs — Anatomy (Label is part 4) · [accessibility.md:39](./accessibility.md) (`htmlFor` ↔ `id` association) · [accessibility.md:97](./accessibility.md) (WCAG 1.3.1).

---

### Pair 5 — Group related options in a `CheckboxGroup`

#### ✅ Do — Wrap related Checkboxes in a `CheckboxGroup` with a group label

`CheckboxGroup` provides the visual and structural grouping. Pair it with a heading (the `header` slot in Figma — see [checkbox-figma.md:71](./checkbox-figma.md)) so screen-reader users hear the group context before each option.

```tsx
<CheckboxGroup>
  {/* Group label is provided by the consuming surface — e.g. a heading immediately above
       the group — or by the CheckboxGroup `header` slot once exposed in the API. */}
  <Checkbox id="email" name="channels" label="Email" value="email" isChecked={email} onChange={(e) => setEmail(e.target.checked)} />
  <Checkbox id="sms"   name="channels" label="SMS"   value="sms"   isChecked={sms}   onChange={(e) => setSms(e.target.checked)} />
  <Checkbox id="push"  name="channels" label="Push"  value="push"  isChecked={push}  onChange={(e) => setPush(e.target.checked)} />
</CheckboxGroup>
```

#### ❌ Don't — Free-float related Checkboxes without a group container

Without a group container, AT users get no signal that the items belong together. Visually, the `$spacing03` rhythm between labels also breaks down.

```tsx
{/* Wrong — related options scattered, no group container */}
<Checkbox label="Email" />
<p>Some unrelated paragraph.</p>
<Checkbox label="SMS" />
<Checkbox label="Push" />
```

> Whether Oxygen's `CheckboxGroup` emits a `<fieldset>` / `<legend>` automatically is **unverified** — tracked as `DOC_GAP` GAP-011 in [checkbox-audit.md](./checkbox-audit.md). If it does not, add your own `<fieldset>` / `<legend>` wrapper or supply the group name via `aria-labelledby` on the container. <!-- TODO: verify rendered DOM emits fieldset/legend; remove this caveat once confirmed -->

**Source:** Published docs — Variants → Multiple checkboxes · [accessibility.md:84](./accessibility.md) (`<fieldset>` + `<legend>` pattern) · [checkbox-figma.md:71](./checkbox-figma.md) (`header` slot).

---

### Pair 6 — Don't disable a Checkbox to hide a validation error

#### ✅ Do — Keep the Checkbox enabled and surface the error inline

A disabled checkbox removes the affordance without explaining why. Keep it enabled, let the user click, and show inline error text (and the `error/error01` border on its `CheckboxGroup` parent, once `isError` is in the API — see GAP-008) when validation fails.

```tsx
<CheckboxGroup>
  <Checkbox id="terms" name="terms" label="I agree to the terms and conditions" value="terms" isChecked={agreed} onChange={(e) => setAgreed(e.target.checked)} />
</CheckboxGroup>
{!agreed && submitted ? (
  <p id="terms-error" role="alert">You must accept the terms before continuing.</p>
) : null}
<Button type="submit" aria-describedby="terms-error">Sign up</Button>
```

#### ❌ Don't — Disable the submit until every box is ticked, with no explanation

The button greys out, the user can't tell which box is missing, and screen-reader users hear nothing about the unmet requirement. `isDisabled` keeps the button focusable but mute.

```tsx
{/* Wrong — disabled until valid, no inline error */}
<Button type="submit" isDisabled={!agreed}>Sign up</Button>
```

**Source:** Published docs — Best Practices section · [accessibility.md:64](./accessibility.md) (`isDisabled` ↔ `aria-disabled`) · matches the Button-usage Pair 7 pattern in [../Button/Button-usage.md](../Button/Button-usage.md).

---

### Pair 7 — Use `infoBoxText` for explanatory tooltips; keep the label tight

#### ✅ Do — Put short, action-shaped text in `label`; put context in `infoBoxText`

The label is the option name; the info button — a separate focus stop — is for the "why" or "how does this affect me?" tooltip. The accessible name of the info button comes from `infoBoxButtonLabel`.

```tsx
<Checkbox
  id="route-to-overflow"
  name="routeToOverflow"
  label="Route to overflow agent group"
  value="routeToOverflow"
  isChecked={routeToOverflow}
  infoBoxText="When all primary agents are busy, calls are routed to the overflow group after the configured wait time."
  infoBoxButtonLabel="More information about routing to the overflow agent group"
  onChange={(e) => setRouteToOverflow(e.target.checked)}
/>
```

#### ❌ Don't — Pack the explanation into the `label`

Long labels wrap, defeat scanning, and overflow the `showLabelTooltipOnOverflow` tooltip (which is meant for graceful truncation of the option name, not for hosting essay-length help copy — see [props.md:65](./props.md)).

```tsx
{/* Wrong — the label is doing the job of infoBoxText */}
<Checkbox
  label="Route to overflow agent group — when all primary agents are busy, calls are routed to the overflow group after the configured wait time."
  isChecked={routeToOverflow}
  onChange={(e) => setRouteToOverflow(e.target.checked)}
/>
```

**Source:** [props.md:60](./props.md) (`infoBoxText` + `infoBoxButtonLabel`) · [accessibility.md:41](./accessibility.md) (info button is a separate focus stop with its own accessible name) · [examples.md:62](./examples.md).

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- Renders a native `<input type="checkbox">` — implicit ARIA role `checkbox`, no `role` override needed ([accessibility.md:35](./accessibility.md)).
- Label is associated via `htmlFor` ↔ `id`; the `label` prop is the accessible name ([accessibility.md:39](./accessibility.md)).
- `Tab` / `Shift+Tab` move focus; `Space` toggles. **Enter does not activate** — WAI-ARIA Checkbox Pattern ([accessibility.md:46](./accessibility.md)).
- `aria-checked` mapping: unchecked → `false`, checked → `true`, indeterminate → `mixed`. Setting `isIndeterminate` also requires setting the DOM `indeterminate` property ([accessibility.md:63](./accessibility.md)).
- `isDisabled` sets `disabled` + `aria-disabled="true"` and removes the input from the focus order ([accessibility.md:64](./accessibility.md)).
- For groups, wrap in `<fieldset>` / `<legend>` (or supply `aria-labelledby`) — whether Oxygen's `CheckboxGroup` does this automatically is unverified (GAP-011).
- Never suppress the focus ring (`outline: none`) — required by WCAG 2.4.7 ([accessibility.md:104](./accessibility.md)).
- The info button (`infoBoxText`) is a separate focusable element with its own accessible name from `infoBoxButtonLabel` ([accessibility.md:41](./accessibility.md)).

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists these neighbours under **Related → Components**:

- **Radio buttons** — for mutually-exclusive selection (one of N). See Pair 1.
- **Toggle** (`ToggleButton`) — for instant-effect on/off settings. See Pair 2.

And under **Related → Patterns**:

- **Forms** — Checkbox is most often used inside the broader Forms pattern (label + control + error + help text).

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP (GAP-001) | No `↳ Checkbox examples` Figma page with Do/Don't card frames exists. Pairs above are editorially derived from the docs page intent + extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| `tokens.md` still speculative | DOC_GAP (GAP-002) | [tokens.md:55](./tokens.md) still references `blue05`/`blue06` as the likely accent. The confirmed bindings live in [checkbox-figma.md:136](./checkbox-figma.md). `tokens.md` should be updated by `doc-rewrite`. |
| `text/textColor01` / `error/error01` confirmation | SOURCE_GAP (GAP-003) | Resolved from shared-token pattern, not directly bound on the Checkbox component set. Verify in the Oxygen theme layer. |
| Input ↔ label horizontal gap | SOURCE_GAP (GAP-004) | Exact px value not measured — `get_design_context` unavailable at extraction. Re-run with Figma Desktop Bridge on node `51776:5081`. |
| Figma component description | SOURCE_GAP (GAP-005) | Component descriptions absent (known Figma API bug without Desktop Bridge). |
| Clean Storybook code examples | SOURCE_GAP (GAP-006) | Oxygen MCP returned 0 clean snippets ([examples.md:28](./examples.md)). Examples above are derived from prop definitions. |
| `CheckboxGroup` full prop list | SOURCE_GAP (GAP-008, heuristic) | [props.md:78](./props.md) lists only `isHorizontal`. Figma shows `header` / `footer` / `isError` slots ([checkbox-figma.md:111](./checkbox-figma.md)). Verify against `CheckboxGroup` package source. |
| Beta stability notice | DOC_GAP (GAP-009) | Beta badge present in Figma; not in [props.md](./props.md). Surfaced in the banner above. |
| `CheckboxGroup` error a11y pattern | DOC_GAP (GAP-010) | No documented `aria-describedby` / `aria-live` pattern for `CheckboxGroup` errors. Pair 6 sketches one but the canonical Oxygen recommendation is not yet captured. |
| `<fieldset>` / `<legend>` auto-wrapping | DOC_GAP (GAP-011, heuristic) | [accessibility.md:86](./accessibility.md) recommends `<fieldset>` / `<legend>` but notes the wrapping is "should be handled" by `CheckboxGroup` — unverified. |
| "When not to use" prose | DOC_GAP | Published docs page does not include this section; the table above is editorial. <!-- TODO: confirm the four "When not to use" rows with the Oxygen team and either promote to docs or trim. --> |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/checkbox/usage`, fetched 2026-05-12 via Claude_in_Chrome MCP) · Cross-referenced with Oxygen MCP and Figma extraction (`@8x8/oxygen-checkbox`, Figma file `5YihJ5WuDvnvrlrRMC4sBp`, node `51776:5078`) · Editorial draft_
