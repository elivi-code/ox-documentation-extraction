---
component: TextArea
package: "@8x8/oxygen-textarea"
category: form_inputs
role: usage_draft
role_description: "Editorial Do/Don't draft — scaffolding for the Figma examples page; NOT the canonical textarea-usage.md"
pipeline_stage: editorial_draft
pipeline_note: "Owned by usage-advisor. The canonical textarea-usage.md must be produced by figma-extract-usage after a designer fills the Figma ↳ TextArea examples page. Treat this file as candidate framings, not approved guidance."
source_type: editorial_draft
audit_verdict: null
siblings:
  - "[[TextArea/props]]"
  - "[[TextArea/examples]]"
  - "[[TextArea/tokens]]"
  - "[[TextArea/accessibility]]"
  - "[[TextArea/textarea-figma]]"
  - "[[TextArea/textarea-pui]]"
  - "[[TextArea/textarea-audit]]"
  - "[[TextField/TextField-usage]]"
tags:
  - oxygen
  - component/TextArea
  - role/usage_draft
  - stage/editorial_draft
  - category/form_inputs
---
<!-- SKILL: usage-advisor -->
<!-- COMPONENT: TextArea -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, textarea-figma.md, textarea-pui.md, textarea-audit.md, TextField/TextField-usage.md (precedent) -->
<!-- STATUS: DRAFT — not the canonical textarea-usage.md -->
<!-- PAIRS: 8 -->

# TextArea — Usage Guidelines (Draft)

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [textarea-figma.md](./textarea-figma.md) · [textarea-pui.md](./textarea-pui.md) · [textarea-audit.md](./textarea-audit.md) · [TextField-usage.md](../TextField/TextField-usage.md) (precedent)

> **Draft only — scaffolding for the Figma `↳ TextArea examples` page.**
> The canonical `textarea-usage.md` is produced by `figma-extract-usage` after a designer fills the Figma examples page with annotated component instances. The pairs below are grounded in `props.md`, `examples.md`, `accessibility.md`, and `textarea-figma.md`, with internal precedent drawn verbatim from [TextField-usage.md](../TextField/TextField-usage.md) where the editorial decision is identical. Treat as candidate framings to review, edit, or reject — not approved guidance.

`Textarea` is the canonical **multi-line free-form input** in Oxygen — paragraphs, comments, notes, messages, descriptions, code snippets. Like `TextField`, the component itself renders only the input box: the **label, hint, and error text are the consumer's responsibility** ([props.md:117](./props.md) — "error message display is handled at the form-field wrapper level, not inside this component"; [accessibility.md:55](./accessibility.md)).

---

## Grounding summary

- **Files used:** [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), [textarea-figma.md](./textarea-figma.md), [textarea-pui.md](./textarea-pui.md), [textarea-audit.md](./textarea-audit.md)
- **Files missing:** `textarea-usage.md` (this draft replaces it provisionally until Figma examples page exists)
- **Internal precedent:** [TextField-usage.md](../TextField/TextField-usage.md) — 6 pairs; 4 of them apply nearly verbatim to TextArea (label/placeholder, description, readonly vs disabled, error state)

---

## When to use

- The user must enter **multi-line free-form content** — paragraphs, comments, notes, descriptions, messages, code snippets ([accessibility.md:32](./accessibility.md) `aria-multiline="true"`; [props.md:83](./props.md) `rows` default `3`).
- The value is **unpredictable in length and structure** and benefits from line breaks, soft-wrapping, and visible whitespace ([examples.md](./examples.md) controlled patterns).
- The field is part of a form pattern that already mixes `TextField`, `Select`, `Checkbox`, etc., and one input requires more vertical space than a single line.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Single-line input — name, email, code, search | [TextField](../TextField/) — fixed-height, single-line, ships with built-in prefix/suffix/icon affordances |
| One option from a known list | [Dropdown](../Dropdown/), [Radio](../Radio/), or [Checkbox](../Checkbox/) — same precedent as [TextField-usage.md Pair 1](../TextField/TextField-usage.md) |
| Rich-text / formatted content (bold, links, mentions) | A dedicated rich-text editor — Oxygen does not ship one |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma ↳ TextArea examples page exists yet -->

---

### Pair 1 — Use Textarea for multi-line free-form input; reach for TextField when one line is enough

#### ✅ Do — Use Textarea when the user is writing more than a line

> Comments, descriptions, notes, addresses spanning multiple lines, support messages, code paste-ins — anything where the user may need to insert line breaks or where the expected response runs past a single sentence belongs in Textarea. The default `rows={3}` is a strong hint to the user that a paragraph is welcome ([props.md:83](./props.md)).

```tsx
import { Textarea } from '@8x8/oxygen-textarea';

<label htmlFor="feedback">What could we improve?</label>
<Textarea
  id="feedback"
  rows={4}
  placeholder="Tell us what didn't work…"
  onChange={(e) => setFeedback(e.target.value)}
/>
```

**Grounded in:** [accessibility.md:32](./accessibility.md) — implicit `aria-multiline="true"`; [props.md:83](./props.md) — `rows` default `3`; [examples.md](./examples.md) — controlled and basic patterns.

#### ❌ Don't — Use Textarea for a value that fits on one line

> A 3-row box signals "write me a paragraph." Asking for an email, a ZIP code, or a referral code inside a Textarea wastes vertical space and confuses users about how much text you expect.

```tsx
// ❌ One-line value inside a 3-row Textarea
<Textarea id="email" placeholder="you@company.com" />

// ✅ Use TextField for single-line values
// <TextField label="Email" placeholder="you@company.com" />
```

**Grounded in:** [TextField-usage.md Pair 1](../TextField/TextField-usage.md) — free-form vs choice; extended here to single-line vs multi-line.

---

### Pair 2 — Always pair Textarea with a real `<label>`; never use `placeholder` as a label

#### ✅ Do — Provide a programmatic label every time

> Textarea does not render its own label — the consumer wires one up via `htmlFor` + `id`, `aria-label`, or `aria-labelledby` ([accessibility.md:42–53](./accessibility.md)). A persistent visible label is a WCAG 2.1 AA requirement (1.3.1, 3.3.2) and stays visible after the user starts typing. Use `placeholder` only for **example formatting** — the shape of the value — never to communicate what the field is for.

```tsx
<label htmlFor="bio">Bio</label>
<Textarea
  id="bio"
  placeholder="A short intro you'd put on a conference badge…"
  rows={3}
  onChange={(e) => setBio(e.target.value)}
/>
```

**Grounded in:** [accessibility.md:42–55, 145](./accessibility.md) — "The Oxygen `Textarea` component does not render its own `<label>` element — labelling is the consumer's responsibility"; WCAG 3.3.2 marked as **consumer responsibility**.

#### ❌ Don't — Rely on placeholder text as the field's label

> Placeholder disappears the moment the user starts typing, fails contrast in many themes, and is announced inconsistently by screen readers. A placeholder-only Textarea is invisible to anyone who tabs back to review the form.

```tsx
// ❌ Placeholder-as-label — fails WCAG 1.3.1 and 3.3.2
<Textarea placeholder="Bio" />

// ✅ Real label + placeholder as example
<label htmlFor="bio">Bio</label>
<Textarea id="bio" placeholder="A short intro…" />
```

**Grounded in:** [accessibility.md:42–55, 145](./accessibility.md); [TextField-usage.md Pair 2](../TextField/TextField-usage.md) — mirrored verbatim.

---

### Pair 3 — Put hints and constraints in a description below the field, not in placeholder

#### ✅ Do — Render hint text as a sibling node and link it via `aria-describedby`

> Textarea has no built-in `description` prop — the consumer renders a hint element below the input and links it via `aria-describedby` ([accessibility.md:60–73](./accessibility.md)). Helper text rendered below the field stays visible as the user types, is announced when the field receives focus, and is the right place for "Max 500 characters", "Markdown supported", "Include steps to reproduce".

```tsx
<label htmlFor="repro">Steps to reproduce</label>
<Textarea
  id="repro"
  aria-describedby="repro-hint"
  rows={5}
  maxLength={2000}
/>
<span id="repro-hint">List the exact steps so we can recreate the issue.</span>
```

**Grounded in:** [accessibility.md:60–73, 153](./accessibility.md); [textarea-figma.md](./textarea-figma.md) "Show Hint" anatomy element; [TextField-usage.md Pair 3](../TextField/TextField-usage.md) — adapted to Textarea's wrapper pattern.

#### ❌ Don't — Pack constraints into the placeholder

> Once the user types one character, the placeholder is gone — along with the constraint. If the rule matters enough to state, it matters enough to stay visible.

```tsx
// ❌ Rule vanishes on first keystroke
<Textarea placeholder="Max 2000 characters. Markdown supported." />
```

**Grounded in:** [accessibility.md:60–73](./accessibility.md); [TextField-usage.md Pair 3](../TextField/TextField-usage.md).

---

### Pair 4 — Use `isReadOnly` to display a value the user can read and copy; use `isDisabled` only when the field is genuinely unavailable

#### ✅ Do — Reach for `isReadOnly` when the user needs to see and copy the value but not change it

> Read-only textareas stay in the tab order, are announced as "read only" by screen readers, and let users select and copy the value — ideal for generated reports, saved notes, system-supplied content ([accessibility.md:109–113](./accessibility.md); [examples.md](./examples.md) Read-only pattern). Disabled textareas are skipped by keyboard navigation entirely.

```tsx
<label htmlFor="report">Generated summary</label>
<Textarea id="report" value={summary} isReadOnly rows={6} />
```

**Grounded in:** [props.md:90](./props.md) `isReadOnly`; [accessibility.md:109–113](./accessibility.md) — "Read-only textareas remain in the tab order and are announced as 'read only' by screen readers"; [TextField-usage.md Pair 4](../TextField/TextField-usage.md) — mirrored verbatim.

#### ❌ Don't — Disable a Textarea just to display a value

> A disabled textarea is silent to assistive tech and skipped by keyboard navigation. If a user can read the value with their eyes but a screen reader user can't reach it, the form is broken.

```tsx
// ❌ User can't tab to it or copy the value with a screen reader
<Textarea value={summary} isDisabled />

// ✅ Read-only keeps the field in the tab order
<Textarea value={summary} isReadOnly />
```

Reserve `isDisabled` for textareas that are temporarily unavailable because a prerequisite isn't met — and in that case, explain *why* in nearby helper text.

**Grounded in:** [accessibility.md:101–105](./accessibility.md); [TextField-usage.md Pair 4](../TextField/TextField-usage.md).

---

### Pair 5 — Show errors with `hasError` + an accessible error message; never colour alone

#### ✅ Do — Combine `hasError` with a descriptive error message linked via `aria-describedby`

> `hasError` only applies the red 2px border ([props.md:91, 117](./props.md)). The error **text** must be rendered as a sibling element, linked via `aria-describedby`, and given `role="alert"` so screen readers announce it on appearance ([accessibility.md:60–73, 117–121](./accessibility.md)). WCAG 3.3.1 requires errors to be described in text — colour alone fails.

```tsx
<label htmlFor="message">Message</label>
<Textarea
  id="message"
  aria-describedby={hasError ? 'message-error' : undefined}
  hasError={hasError}
  rows={4}
  value={value}
  onChange={(e) => setValue(e.target.value)}
/>
{hasError && (
  <span id="message-error" role="alert">
    Message must be at least 20 characters.
  </span>
)}
```

**Grounded in:** [props.md:91, 117](./props.md); [accessibility.md:60–73, 117–121, 144](./accessibility.md) — WCAG 3.3.1 marked as **consumer responsibility**; [textarea-figma.md](./textarea-figma.md) error anatomy; [TextField-usage.md Pair 5](../TextField/TextField-usage.md) — mirrored with Textarea's wrapper pattern.

#### ❌ Don't — Set `hasError` without rendering an accessible message

> A red border with no text fails WCAG 1.4.1 (use of colour) and 3.3.1 (error identification). Users with low vision, colour-blindness, or in high-glare environments may not perceive the border, and even those who see it won't know **what** is wrong or **how to fix it**.

```tsx
// ❌ Red border with no text — fails WCAG 1.4.1 and 3.3.1
<Textarea id="message" hasError />

// ❌ Even worse: vague message that doesn't say what's wrong
<Textarea id="message" hasError aria-describedby="err" />
<span id="err" role="alert">Invalid.</span>

// ✅ Specific, actionable error text
<Textarea id="message" hasError aria-describedby="err" />
<span id="err" role="alert">
  Add at least one sentence describing the problem.
</span>
```

**Grounded in:** [accessibility.md:117–121, 139, 144](./accessibility.md); [TextField-usage.md Pair 5](../TextField/TextField-usage.md).

---

### Pair 6 — Size `rows` to the expected input length

#### ✅ Do — Pick `rows` based on how much text you actually expect

> A "Title" Textarea at `rows={3}` and a "Detailed description" Textarea at `rows={3}` give the user the same visual signal for two very different asks. Use `rows={2–3}` for short notes, `rows={4–6}` for paragraphs, `rows={8+}` for long-form content like bug reports or feedback essays ([props.md:83](./props.md) — default `3`; [examples.md](./examples.md) controlled patterns).

```tsx
{/* Short note */}
<label htmlFor="alias">Display name override</label>
<Textarea id="alias" rows={2} maxLength={80} />

{/* Long-form feedback */}
<label htmlFor="incident">Describe what happened</label>
<Textarea id="incident" rows={8} maxLength={5000} />
```

**Grounded in:** [props.md:83](./props.md) — `rows` (default `3`); [examples.md](./examples.md) controlled patterns; adapted from [TextField-usage.md Pair 6](../TextField/TextField-usage.md) — "Input width should be proportional to the content."

#### ❌ Don't — Leave every Textarea at the default `rows={3}` regardless of expected input

> A 3-row box for a one-sentence note wastes space; a 3-row box for a multi-paragraph bug report forces the user to scroll their own input as they write. Either way, you've signalled the wrong amount of effort.

```tsx
// ❌ Same height for inputs that expect very different amounts of text
<Textarea id="title" rows={3} />          {/* Title — too tall */}
<Textarea id="description" rows={3} />    {/* Description — too short */}
<Textarea id="reproSteps" rows={3} />     {/* Repro steps — too short */}
```

**Grounded in:** [props.md:83](./props.md); craft heuristic — no internal precedent for multi-line sizing.

---

### Pair 7 — Lock `resize` to `vertical` or `none` inside structured forms; avoid `horizontal` and `both`

#### ✅ Do — Keep the default `resize="vertical"`, or set `resize="none"` in tight layouts

> Vertical resize lets the user grow the field for long inputs without breaking the form's column width — the default for good reason ([props.md:87, 100–110](./props.md)). In dense dashboards, fixed-width modals, or grid-aligned forms where any height change would push surrounding content unpredictably, `resize="none"` and a generous `rows` value is the right call.

```tsx
{/* Default — vertical resize allowed */}
<Textarea id="bio" rows={4} maxLength={500} />

{/* Locked in a tight grid cell */}
<Textarea id="note" rows={3} resize="none" maxLength={280} />
```

**Grounded in:** [props.md:87, 100–110](./props.md) — `resize` enum, default `'vertical'`; [textarea-figma.md](./textarea-figma.md) resize-grip anatomy; craft heuristic — no internal precedent (TextField has no `resize` equivalent).

#### ❌ Don't — Allow horizontal or both-axis resize inside fixed-width form columns

> `resize="horizontal"` and `resize="both"` let the user widen the field beyond its column, breaking the form's grid alignment and on responsive layouts pushing other inputs offscreen. There is no Oxygen layout where horizontal resize improves the user's outcome.

```tsx
// ❌ Lets the user break the grid
<Textarea id="bio" resize="horizontal" />
<Textarea id="bio" resize="both" />

// ✅ Vertical (default) is safe inside columns
<Textarea id="bio" /> {/* resize defaults to 'vertical' */}
```

**Grounded in:** [props.md:87, 100–110](./props.md); craft heuristic — flag for designer review.

---

### Pair 8 — Show a live character counter when `maxLength` represents a hard limit users care about

#### ✅ Do — Surface a visible counter when the limit is a real constraint (SMS, tweets, bios, summary fields)

> When `maxLength` is set to a value the user is likely to bump up against — and where running out of room matters (a 160-character SMS, a 280-character bio, a 500-character incident summary) — render a live `N / maxLength` counter as a sibling element. Update it on `onChange` and tie it to the same `aria-describedby` as the hint so it's announced contextually ([props.md:86, 93](./props.md); [examples.md](./examples.md) char-limit example).

```tsx
const MAX = 280;
const [bio, setBio] = useState('');

<label htmlFor="bio">Bio</label>
<Textarea
  id="bio"
  aria-describedby="bio-hint bio-count"
  maxLength={MAX}
  value={bio}
  onChange={(e) => setBio(e.target.value)}
/>
<span id="bio-hint">A short intro for your profile.</span>
<span id="bio-count" aria-live="polite">{bio.length} / {MAX}</span>
```

**Grounded in:** [props.md:86](./props.md) `maxLength`; [examples.md](./examples.md) character-limit pattern; [TextField-usage.md GAP-USAGE-003](../TextField/TextField-usage.md) — surfaces this as an explicit open question; craft heuristic.

#### ❌ Don't — Set a long `maxLength` and rely on the browser's silent cut-off

> The browser will simply refuse keystrokes past `maxLength` with no feedback. Users assume their input is being captured, then discover later that the last paragraph of their bug report vanished. Either show a counter, raise the limit, or split the field.

```tsx
// ❌ Silent cap — user has no idea they're near the limit
<Textarea id="bio" maxLength={280} />

// ❌ Even worse: long limit with no counter on a field users may push
<Textarea id="incident" maxLength={5000} rows={8} />
```

**Grounded in:** [props.md:86](./props.md); [TextField-usage.md GAP-USAGE-003](../TextField/TextField-usage.md); craft heuristic.

---

## Axes presented but skipped

_None in this draft — all 8 candidate axes from the plan were drafted. Designer to mark which to keep, edit, or drop._

## Axes flagged as ungrounded (craft heuristics)

- **Pair 6 — `rows` sizing.** No internal precedent for multi-line input sizing. Adapted from TextField's "width proportional to content" rule.
- **Pair 7 — `resize` direction.** No precedent (TextField has no resize). Anchored to `resize` enum values in props.md; recommendation is craft judgment.
- **Pair 8 — Character counter.** Explicitly flagged as a gap in TextField-usage.md (GAP-USAGE-003). No internal ruling exists yet — this pair would set the precedent.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | All 8 pairs are draft scaffolding for the Figma examples page. Replace with `figma-extract-usage` output once a designer fills the `↳ TextArea examples` page. |
| GAP-USAGE-001 | Source gap | No Figma `↳ TextArea examples` page exists. Until one is created and populated with annotated component instances, `figma-extract-usage TextArea` cannot run. |
| GAP-USAGE-002 | Source gap | The Oxygen public docs site does not currently host a TextArea usage page (TextField has one at oxygen.8x8.com/components/textinput/usage; the equivalent for TextArea would help anchor pairs 1, 6, 7, 8). |
| GAP-USAGE-003 | Conflict | The blocked audit verdict (Figma `Size` / `Mode` / `Filled` axes that don't map to Oxygen API) means there is no agreed-upon "small / medium / large" Textarea recommendation. Pair 6 sidesteps this by anchoring to `rows` instead of `size`. Resolve before producing the canonical usage page. |
| GAP-USAGE-004 | Open question | No editorial guidance exists for `minLength` (which TextArea has but TextField lacks). When should designers require a minimum content length? Worth a future pair if the team has a stance. |
| GAP-USAGE-005 | Cross-ref | [TextField-usage.md "When not to use" row 4](../TextField/TextField-usage.md) states "Oxygen does not yet ship a dedicated Textarea component" — this is now stale. Update TextField-usage.md to point to Textarea when this draft is approved. |

---

_Source: editorial draft authored by `usage-advisor` from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, textarea-figma.md, textarea-pui.md, textarea-audit.md) and internal precedent in TextField-usage.md · No Figma examples page available · 2026-05-15_
