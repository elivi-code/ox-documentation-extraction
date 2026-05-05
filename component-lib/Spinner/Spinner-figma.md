<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 1561:11079 -->
<!-- EXTRACTED: 2026-05-05 -->
<!-- COMPONENT: Spinner -->
<!-- COLOR STRATEGY: A -->

# Spinner — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

![Spinner](./figma-screenshot-Spinner.png)

---

## Anatomy

The Figma page for Spinner contains two component sets: **Spinner** (animated loading state) and **Spinner complete** (terminal states: complete and error). Both are documented below.

### Component set: Spinner (node `2063:0`)

Six variant combinations arranged in the component set frame (470×542px):

| # | Type | Name / Variant key | Dimensions | Notes |
|---|------|--------------------|------------|-------|
| 1 | symbol | `mode=light, size=default, isInverted=no` | 100×108px | Primary default variant |
| 2 | symbol | `mode=light, size=default, isInverted=yes` | 100×108px | Inverted (light mode, dark background) |
| 3 | symbol | `mode=dark, size=default, isInverted=no` | 100×108px | Dark mode default |
| 4 | symbol | `mode=light, size=small, isInverted=no` | 87×52px | Compact inline variant |
| 5 | symbol | `mode=light, size=small, isInverted=yes` | 87×52px | Inverted small |
| 6 | symbol | `mode=dark, size=small, isInverted=no` | 87×52px | Dark mode small |

> **Note:** The `dark + isInverted=yes` combination is absent from the component set — only 6 of 8 possible permutations are defined.

### Component set: Spinner complete (node `28591:41808`)

Terminal state variants. Frame dimensions: 404×122px. Each variant is ~186×44px.

| # | Type | Name / Variant key | Dimensions | Notes |
|---|------|--------------------|------------|-------|
| 1 | symbol | `mode=light, state=complete` | 186×44px | Loading completed successfully |
| 2 | symbol | `mode=dark, state=complete` | 186×44px | Dark mode complete |
| 3 | symbol | `mode=light, state=error` | 186×44px | Loading failed |
| 4 | symbol | `mode=dark, state=error` | 186×44px | Dark mode error |

---

## API — Component properties

### Variant axes

#### Spinner (animated)

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| `mode` | `light`, `dark` | `light` | Theme mode |
| `size` | `default`, `small` | `default` | Maps to `size` prop in Oxygen (`"default"`, `"small"`) |
| `isInverted` | `no`, `yes` | `no` | Inverted colour variant for use on dark/coloured backgrounds |

#### Spinner complete (terminal states)

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| `mode` | `light`, `dark` | `light` | Theme mode |
| `state` | `complete`, `error` | — | Terminal outcome state |

### Boolean toggles

<!-- NO BOOLEAN TOGGLES FOUND — Desktop Bridge offline, inner layer properties unavailable -->

### Instance swap slots

<!-- NO INSTANCE SWAP SLOTS FOUND — Desktop Bridge offline, inner layer properties unavailable -->

### Persistent states

| State | Property name | Notes |
|-------|--------------|-------|
| Inverted | `isInverted` | Controls colour rendering on dark/coloured surfaces |
| Complete | `state=complete` | Terminal — loading finished; use Spinner complete component set |
| Error | `state=error` | Terminal — loading failed; use Spinner complete component set |

### Token coverage

<!-- NO COVERAGE DATA RETURNED — Variables API unavailable (Enterprise plan required); Desktop Bridge not connected -->

---

## Color & token bindings

<!-- NO TOKEN BINDINGS FOUND IN FIGMA RESPONSE -->

The Variables API returned a permissions error (Enterprise plan required), and the figma-console Desktop Bridge was not running. Token bindings for the Spinner stroke, track, and text colours could not be extracted.

**Known gap:** Token names for spinner colours should be resolved from the UI-Foundations token library (file key `iVY5nI8JAxM05Apnnvozzs`) using `getVariableByIdAsync` on the spinner node properties.

### Text styles

<!-- NO STYLE DATA RETURNED — Styles API returned 0 styles for this file -->

### Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE -->

---

## Structure & spacing

### Component set: Spinner

| Variant | Width | Height | Notes |
|---------|-------|--------|-------|
| `size=default` | 100px | 108px | Height includes supporting text area |
| `size=small` | 87px | 52px | Compact; includes supporting text area |

### Component set: Spinner complete

| Variant | Width | Height | Notes |
|---------|-------|--------|-------|
| `state=complete` / `state=error` | ~186px | 44px | Fixed terminal state card |

### Internal spacing

<!-- NO STRUCTURE DATA FOUND — get_design_context unavailable (requires selection in Figma Desktop) -->

Inner padding, gap between spinner icon and supporting text, and icon dimensions could not be extracted. These would require `get_design_context` on an individual variant node while selected in Figma Desktop.

### Auto-layout

- Direction: <!-- NOT FOUND — get_design_context unavailable -->
- Alignment: <!-- NOT FOUND -->

---

## Interaction states

The Spinner is a non-interactive, passive component. No hover, focus, or pressed states are present in the Figma component set. The only state transitions are:

| State | Trigger | Visual change |
|-------|---------|---------------|
| Animating | Mount / `hasAnimation=true` | Continuous rotation of the spinner arc |
| Static | `hasAnimation=false` | Spinner arc frozen; no rotation |
| Complete | Loading finishes | Transition to "Spinner complete" with `state=complete` |
| Error | Loading fails | Transition to "Spinner complete" with `state=error` |

---

## Design decisions & annotations

> **isInverted variant:** A dedicated inverted colour variant is provided for placement on dark or brand-coloured backgrounds, rather than relying on CSS inversion filters. The `dark + isInverted=yes` combination is intentionally absent (redundant — dark mode already handles that context).

> **Spinner complete as separate component set:** Terminal states (complete, error) live in a separate component set ("Spinner complete") rather than as variants of the Spinner. This signals that the consuming code should swap the component rather than changing a variant prop when loading ends.

> **Supporting text:** Oxygen usage docs state supporting text should always be present where space permits and must never be removed for stylistic reasons. The 108px height of the default variant (vs ~56px for the spinner arc alone) accommodates the text label below the arc.

<!-- NO FURTHER ANNOTATIONS FOUND IN FIGMA RESPONSE -->

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA -->

For full accessibility documentation see [accessibility.md](./accessibility.md).

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| Missing token | All colour/stroke token bindings absent — Variables API requires Enterprise plan; Desktop Bridge was offline |
| Missing token | Text style bindings for supporting text label not extracted |
| Missing annotation | No ARIA role annotated in Figma |
| Missing annotation | No keyboard interaction notes in Figma |
| Incomplete data | `get_design_context` unavailable — inner padding, gap, icon size, and auto-layout direction not extracted |
| Incomplete data | `figma_get_component_details` unavailable (Desktop Bridge offline) — component key not recorded |
| Conflict | `isInverted` Figma prop has no direct equivalent in the Oxygen `Spinner` React props — consuming teams need to apply theme/surface context manually |
| Incomplete variant coverage | `dark + isInverted=yes` combination missing from Figma component set — intentional or oversight TBC |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-05_
