---
component: AlertBanner
package: "@8x8/oxygen-alertBanner"
category: feedback_status
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[AlertBanner/props]]"
  - "[[AlertBanner/examples]]"
  - "[[AlertBanner/tokens]]"
  - "[[AlertBanner/accessibility]]"
  - "[[AlertBanner/alert-banner-audit]]"
tags:
  - oxygen
  - component/AlertBanner
  - role/figma
  - stage/blocked
  - category/feedback_status
---
<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 31568:56098 (canvas) / COMPONENT_SET: 13899:15489 -->
<!-- EXTRACTED: 2026-04-28 -->
<!-- COMPONENT: AlertBanner -->
<!-- COLOR STRATEGY: A — ≤3 state variants; one table per element, modes as rows -->

# AlertBanner — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md) ·
> [alert-banner-usage.md](./alert-banner-usage.md)

---

## Visual reference

Screenshot captured from Figma node `31568:56098`. The component sheet shows four
variants arranged in two rows: light-mode variants on a white background (top) and
dark-mode variants on a near-black background (bottom). Each row shows two breakpoint
layouts — an inline/single-row layout (desktop ≥ 576 px) and a stacked/two-row layout
(mobile < 576 px).

All visible variants use an **amber/warning yellow** background (`#F8AE1A`), a warning
circle icon on the left, a body-text message in the centre, and an optional **Secondary
button** on the right (inline) or below the text (stacked).

---

## Anatomy

Element structure extracted from the Figma layer tree (node `13899:15489`). Children of
individual variants were not returned by the API — structure below is inferred from the
reconstruction data combined with the screenshot and Oxygen prop names.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame (COMPONENT_SET) | Alert banner | Structural — top-level container | Dashed-border Figma component-set boundary; 4 variants inside |
| 2 | component | mode=light, breakpoint=> 576 | Structural — variant | Desktop light; HORIZONTAL layout; 1200 × 56 px |
| 3 | component | mode=dark, breakpoint=> 576 | Structural — variant | Desktop dark; HORIZONTAL layout; 1200 × 56 px |
| 4 | component | mode=light, breakpoint=< 576 | Structural — variant | Mobile light; VERTICAL layout; 576 × 104 px |
| 5 | component | mode=dark, breakpoint=< 576 | Structural — variant | Mobile dark; VERTICAL layout; 576 × 104 px |
| 6 | instance | Warning icon | Content element — fixed | Circle warning icon; accessible label exposed via `iconAriaLabel` prop |
| 7 | text / frame | Message (children) | Content element — React children slot | Body text; maps to `children` prop |
| 8 | instance | Action button | Optional slot | Secondary button; shown only when `actionText` is set; hidden (boolean toggle) |

> **Note:** Rows 6–8 are inferred from the screenshot and Oxygen props — the API did not
> return the inner layer children of each variant. See **Gaps & conflicts**.

### Sidebar annotation frame: _Information & support

A non-component documentation frame at `48956:2083` (x = −1284, off-canvas) contains:

- Header text "Alert banner" (Inter 600 / 28 px)
- Status badge ("Stable"), links to Storybook / documentation / support
- Footer: "Contact us if you need further support."

This frame is a Figma-side annotation only — not part of the rendered component.

---

## API — Component properties

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| mode | light, dark | light |
| breakpoint | > 576, < 576 | > 576 |

> These axes are design-time layout aids. In code the component responds to the container /
> viewport width automatically; there is no explicit `mode` or `breakpoint` prop exposed to
> consumers (see `props.md`).

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| Action button visible | false (hidden) | Shown when `actionText` prop is provided; inferred from screenshot — no explicit Figma boolean property name returned |

### Instance swap slots

<!-- NO INSTANCE SWAP SLOTS FOUND — figma_get_component_details unavailable (requires Desktop Bridge) -->

### Persistent states

<!-- NO PERSISTENT STATES FOUND — no disabled / selected / loading / error variants visible in the component set -->

### Token coverage

<!-- NO COVERAGE DATA RETURNED BY figma_get_component enrich -->
<!-- figma_get_variables call failed — REST API permissions insufficient; Desktop Bridge not available -->

- **Coverage:** unknown — Variables API was inaccessible; background fill `#F8AE1A` matches `alertYellow` dark-mode token value but cannot be confirmed as a token binding
- **Hardcoded values flagged:**
  - All 4 variants — `fills[0].color`: `#F8AE1A` — raw value in API response; possible alias to `alertYellow` (dark) or a component-specific token; confirm with design team
  - `_Information & support` frame fill: `#FEF0D1` — annotation-only frame, not a component concern

---

## Color & token bindings

Token values resolved via `figma_execute` + `getVariableByIdAsync` alias chain traversal on node `13899:15489` (UI-components → UI-Foundations library). All values confirmed from Figma.

<!-- COLOR STRATEGY A: one table per element, modes as rows -->

### Banner container background

| Semantic token | Primitive | Hex (Light) | Hex (Dark) | Notes |
|---------------|-----------|-------------|------------|-------|
| `warning/warning01` | `color/yellow/yellow06` | `#f8ae1a` | `#f8ae1a` | **Same in both modes** — the amber background is intentionally fixed; no mode switch |

> The AlertBanner background does not invert between Light and Dark mode. The `warning/warning01` token resolves to the same `color/yellow/yellow06` primitive in both modes. This was confirmed via alias chain traversal — the previous "mismatch" note was incorrect.

### Text and icon tokens

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Title / message text | `text/textColor07` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray02` | `#292929` |
| Warning icon fill | `icon/icon08` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray02` | `#292929` |
| Action button (secondary) | `actions/action02` | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray08` | `#c2c2c2` |
| Close / dismiss icon | `text/textColor09` | `color/pure/white` | `#ffffff` | `color/pure/black` | `#000000` |

> Dark text and icon on the fixed amber background ensures contrast in both modes. The close icon (`textColor09`) flips white↔black to accommodate mode-specific usage contexts.

### Typography tokens

| Element | Token family | Size | Weight | Line-height | Letter-spacing |
|---------|-------------|------|--------|-------------|----------------|
| Message body | `typography/body01/` | `14px` | `400` | `20px` | `-0.06px` |
| Action label | `typography/labelBold01/` | `12px` | `600` | `16px` | `0px` |

---

## Structure & spacing

### Container

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Width | — | 1200 px | breakpoint > 576 (desktop) |
| Height | — | 56 px | breakpoint > 576 (desktop) |
| Width | — | 576 px | breakpoint < 576 (mobile) |
| Height | — | 104 px | breakpoint < 576 (mobile) |
| Padding left | — | 16 px | all variants |
| Padding right | — | 16 px | all variants |
| Padding top | — | 12 px | all variants |
| Padding bottom | — | 12 px | all variants |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Gap (between elements) | — | 16 px | breakpoint > 576 — HORIZONTAL layout |
| Gap (between elements) | — | 8 px | breakpoint < 576 — VERTICAL layout |

### Auto-layout

- Direction: **HORIZONTAL** for breakpoint > 576; **VERTICAL** for breakpoint < 576
- Sizing: `layoutSizingHorizontal = FIXED` / `layoutSizingVertical = HUG` for desktop variant; `counterAxisSizingMode = FIXED` for mobile variant
- Alignment: <!-- NOT RETURNED — children not resolved in API response -->

### Density / size variants

The component has no explicit density or size variants. The two breakpoint values produce
size differences:

| Variant | Width | Height | Layout direction |
|---------|-------|--------|-----------------|
| breakpoint > 576 | 1200 px | 56 px | HORIZONTAL |
| breakpoint < 576 | 576 px | 104 px | VERTICAL |

---

## Interaction states

<!-- NO INTERACTION STATES FOUND IN FIGMA RESPONSE -->

The component set contains only `mode` and `breakpoint` variant axes. No hover, focus,
pressed, or loading states were found in the Figma layer tree. The action button
(Secondary button) likely inherits its own interaction states from the Button component.

---

## Design decisions & annotations

<!-- NO ANNOTATIONS FOUND IN FIGMA RESPONSE — the Figma Desktop Bridge plugin is required
     for annotation data; get_design_context returned a selection-required error -->

The only design-intent text found in the page is in the off-canvas documentation card
(`_Information & support`):

> **Alert banner:** "Contact us if you need further support."

This is a documentation/support link, not a design annotation.

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA — no annotations returned -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA -->

See [accessibility.md](./accessibility.md) for full accessibility documentation derived
from the Oxygen MCP and component nature.

> The `iconAriaLabel` prop in the Oxygen API implies the icon is exposed to assistive
> technology with a configurable label — design intent for this prop was not annotated
> in the Figma file.

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Incomplete data | Inner layer children of all 4 variants not returned by Figma REST API — anatomy rows 6–8 are inferred, not confirmed |
| Incomplete data | `figma_get_component_details` unavailable (requires Figma Desktop Bridge running locally) |
| ~~Incomplete data~~ | ~~`figma_get_variables` unavailable~~ — **Resolved 2026-05-05**: all tokens extracted via `figma_execute` alias chain traversal; `warning/warning01` confirmed as background token (same `#f8ae1a` in both modes) |
| Incomplete data | `get_design_context` unavailable (requires active layer selection in Figma Desktop) — spacing tokens, auto-layout alignment, and annotations not extractable |
| ~~Missing token~~ | ~~Banner background fill `#F8AE1A` hardcoded~~ — **Resolved 2026-05-05**: confirmed as `warning/warning01` → `color/yellow/yellow06`; intentionally mode-invariant (same yellow in Light and Dark) |
| Missing token | All padding and gap values (16 px, 12 px, 8 px) are raw px — no token bindings confirmed |
| Missing annotation | No design-intent annotations extracted — the "why" for colour choice, breakpoint values, and gap differences is undocumented in Figma |
| Conflict | Figma variant axes `mode` (light/dark) and `breakpoint` (> 576 / < 576) have no corresponding props in the Oxygen API — confirm whether these are handled automatically by the component or require parent-level wiring |
| Missing annotation | `iconAriaLabel` prop exists in the Oxygen API but no ARIA/a11y annotations were found in the Figma file |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-28_
