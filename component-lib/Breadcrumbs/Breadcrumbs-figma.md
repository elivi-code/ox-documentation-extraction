<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 21927:40413 -->
<!-- EXTRACTED: 2026-04-30 -->
<!-- COMPONENT: Breadcrumbs -->
<!-- COLOR STRATEGY: B (4 interaction states × 2 modes = 8 combinations per element) -->

# Breadcrumbs — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Visual reference

<!-- SCREENSHOT: Captured via MCP but returned as embedded image only — no downloadable URL.
     Export manually from Figma node 21927:40413 and save as figma-screenshot-Breadcrumbs.png -->

The component set displays 6 variants arranged in rows:
- Row 1 (light, no collapse): `Home / Page link / Page link / … / Current page`
- Row 2 (light, collapsed, menu closed): `Home / … / Page link / … / Current page`
- Row 3 (light, collapsed, menu open): same as row 2 with an open dropdown below `…`
- Rows 4–6 repeat the same three states in dark mode.

---

## Anatomy

Element structure extracted from the Figma layer tree (node `21927:40413`).

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Page (× N) | Structural group | Repeating group: one `_Text link breadcrumb` + one separator text. N items shown depending on collapse state. |
| 2 | sub-component | `_Text link breadcrumb` | Fixed sub-component | Clickable link item; states: rest / hover / active / focus × light / dark (atom at node `20648:30062`). |
| 3 | text | `/` (separator) | Content / decorative | Bound to `--text/textcolor01`. Rendered as plain `<p>`. |
| 4 | frame | Menu | Structural group (optional) | Present only when `collapse?=yes`. Contains `_Text link elipsis` + trailing separator. |
| 5 | sub-component | `_Text link elipsis` | Fixed sub-component (conditional) | Ellipsis indicator; states: rest / hover / active / focus × light / dark (atom at node `22076:37746`). When `↪ menu?=yes` renders as a `<button>` that opens the overflow menu. |
| 6 | frame | Overflow Menu | Optional slot | Absolutely positioned dropdown; visible when `↪ menu?=yes`. Contains a `Slot` placeholder for custom content. Width: 160 px, radius: 6 px. |
| 7 | frame | Curent page | Content element | Non-link current-page label (note: typo "Curent" in Figma layer name). Text bound to `--text/textcolor01`. Controlled by text property `curent page#20679:3`. |

### Sub-component: `_Text link breadcrumb` (node `20648:30062`)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | text | Link label | Content element | Body01 typography; `--actions/action08` for link colour. |
| — | — | States | — | rest / hover / active / focus; light mode and dark mode rows. |

### Sub-component: `_Text link elipsis` (node `22076:37746`)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | text / button | `...` label | Content element | Renders as `<p>` when `↪ menu?=no`; as `<button>` when `↪ menu?=yes`. `--actions/action08` (rest) / `--interactive/active07` (pressed/menu open). |
| 2 | frame | Overflow Menu | Optional slot (hidden) | Present only in `state=active`/`↪ menu?=yes` variants. |

---

## API — Component properties

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `collapse?` | `no`, `yes` | `no` |
| `↪ menu?` | `no`, `yes` | `no` |

**Variant key map (6 components):**

| mode | collapse? | ↪ menu? | Node ID |
|------|-----------|---------|---------|
| light | no | no | `21927:40414` |
| dark | no | no | `22088:43533` |
| light | yes | no | `21984:40606` |
| dark | yes | no | `22088:43560` |
| light | yes | yes | `21984:42427` |
| dark | yes | yes | `22088:43590` |

> **Note:** `collapse?=no, ↪ menu?=yes` is not a valid combination — the menu can only appear when collapsed.

### Boolean toggles

<!-- NO BOOLEAN TOGGLES FOUND — the collapse and menu states are modelled as VARIANT axes, not boolean properties. -->

### Instance swap slots

| Slot | Accepted types | Default |
|------|---------------|---------|
| Overflow Menu content | Any component (placeholder "Slot") | Placeholder frame — "swap me with your content" |

### Text properties

| Property | Default | Notes |
|----------|---------|-------|
| `curent page#20679:3` | `"Current page"` | Controls the label of the active (non-link) trail end. **Note: Figma property name has a typo — "curent" not "current".** |

### Persistent states

<!-- NO PERSISTENT STATES FOUND — disabled is not a variant in this component set. -->

### Token coverage

- **Coverage:** Not returned by `figma_get_component` enrichment (no formal metric available).
- **Hardcoded values flagged (in Overflow Menu — dark mode):**
  - `Overflow Menu (dark).background`: `#171719` — no token binding found
  - `Overflow Menu (dark).border-color`: `#666` — no token binding found
  - `Overflow Menu (dark).box-shadow`: `0px 1px 2px 1px #141414` — no token binding found
  - `Overflow Menu (light).box-shadow`: `0px 1px 2px 0px rgba(41,41,41,0.25)` — no token binding found
  - `Overflow Menu.border-radius`: `6px` — no token binding found
  - `Overflow Menu.width`: `160px` — no token binding found
  - `Overflow Menu.padding-y`: `9px` — no token binding found

---

## Color & token bindings

<!-- COLOR STRATEGY B: states as columns, elements as rows -->
<!-- Note: only rest-state token values were returned by design context; hover/active/focus states exist in the atom sub-components but their token bindings were not resolved by this extraction. -->

### Link text (`_Text link breadcrumb` / `_Text link elipsis` — rest state)

| Element | Token | Collection | Light | Dark |
|---------|-------|------------|-------|------|
| Link label | `--actions/action08` | actions | `#0056e0` | `#99bbf3` |
| Ellipsis button (rest) | `--actions/action08` | actions | `#0056e0` | `#99bbf3` |
| Ellipsis button (menu open / active) | `--interactive/active07` | interactive | `#0045b3` | `#0056e0` |

### Separator and current-page text

| Element | Token | Collection | Light | Dark |
|---------|-------|------------|-------|------|
| `/` separator | `--text/textcolor01` | text | `#26252a` | `white` |
| Current page label | `--text/textcolor01` | text | `#26252a` | `white` |

### Overflow Menu container

| Property | Token | Light | Dark |
|----------|-------|-------|------|
| Background | — (hardcoded) | `white` | `#171719` |
| Border | `--ui/ui01` (light); hardcoded (dark) | `#ebeae1` | `#666` |
| Box shadow | — (hardcoded) | `rgba(41,41,41,0.25)` | `#141414` |

### Text styles

| Element | Style name | Size | Weight | Line height | Letter spacing |
|---------|-----------|------|--------|-------------|----------------|
| All text (links, separator, current page) | `$body01` / `--typography/body01/*` | 14 px (`typography/body01/font-size`) | 400 (`typography/body01/font-weight`) | 20 px (`typography/body01/line-height`) | −0.06 px (`typography/body01/letter-spacing`) |

### Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE — shadow on overflow menu is hardcoded (see Token coverage above). -->

---

## Structure & spacing

### Container

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Height | — | 20 px (driven by `body01` line-height) | No explicit height constraint |
| Width | — | `fit-content` / `content-stretch` | Grows with trail length |
| Padding | — | None | No padding on the root container |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Gap (between Page groups) | — | 8 px (`gap-[8px]`) | Hardcoded |
| Gap (link ↔ separator within a Page group) | — | 8 px (`gap-[8px]`) | Hardcoded |
| Overflow Menu gap (item rows) | — | 4 px (`gap-[4px]`) | Hardcoded; applies when `↪ menu?=yes` |
| Overflow Menu width | — | 160 px | Hardcoded |
| Overflow Menu padding-y | — | 9 px | Hardcoded |
| Overflow Menu padding-x | — | 1 px | Hardcoded |
| Overflow Menu border-radius | — | 6 px | Hardcoded |
| Overflow Menu top offset | — | 24 px | Absolute position below ellipsis button |

### Auto-layout

- Direction: horizontal
- Alignment: `items-center` (vertically centred)
- Overflow: no wrap — trail never wraps to a second line (by design)

### Density / size variants

<!-- NO SIZE OR DENSITY VARIANTS — single size only. -->

---

## Interaction states

States visible in the Figma atom sub-components (`_Text link breadcrumb`, `_Text link elipsis`).

| State | Trigger | Visual change |
|-------|---------|---------------|
| rest | default | Link: `--actions/action08` |
| hover | pointer over | Distinct hover style present in atom (token binding not resolved by this extraction) |
| active | pointer down | Distinct active style present in atom (token binding not resolved by this extraction) |
| focus | keyboard Tab | Distinct focus ring present in atom (token binding not resolved by this extraction) |
| menu open | click on `…` button | Ellipsis colour switches from `--actions/action08` to `--interactive/active07`; Overflow Menu becomes visible |

---

## Design decisions & annotations

> **Component description (Figma):** `https://oxygen.8x8.com/components/breadcrumbs/usage`
> Breadcrumbs are a secondary navigational system. The trail starts at home/root and ends at the parent of the current page. The current page itself is never a link.

> **Collapsed variant description:** `"State"` — minimal annotation on variants `21984:40606`, `22088:43560`, `21984:42427`, `22088:43590`. No further design intent documented.

> **Overflow Menu slot:** The dropdown container uses a `Slot` placeholder annotated _"This is a placeholder, swap me with your content"_ — indicating this slot is intended for designer/consumer customisation, not prescriptive content.

> **"Curent page" typo:** The Figma text property and layer are named `curent page` (one `r`). This is a known Figma-side typo and should not be replicated in code prop names.

<!-- NO FURTHER ANNOTATIONS FOUND IN FIGMA RESPONSE — `annotations` array was empty. -->

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
| Missing token | `Overflow Menu (dark).background` is hardcoded `#171719` — no token binding |
| Missing token | `Overflow Menu (dark).border-color` is hardcoded `#666` — no token binding |
| Missing token | `Overflow Menu (dark).box-shadow` is hardcoded `0px 1px 2px 1px #141414` — no token binding |
| Missing token | `Overflow Menu (light).box-shadow` is hardcoded `rgba(41,41,41,0.25)` — no token binding |
| Missing token | `Overflow Menu.border-radius` is hardcoded `6px` — no token binding |
| Missing token | `Overflow Menu.width` is hardcoded `160px` — no token binding |
| Missing token | `Overflow Menu.padding-y` is hardcoded `9px` — no token binding |
| Missing token | Container and item gap `8px` is hardcoded — no spacing token binding |
| Incomplete data | Hover / active / focus token bindings for `_Text link breadcrumb` and `_Text link elipsis` were not resolved — the atoms exist in the file but their variable bindings were not returned (no local variables in this file; tokens come from a shared library) |
| Incomplete data | No local variables found in the file (`total_variables: 0`) — token names are inferred from CSS variable references in the design context code, not from the Variables API |
| Missing annotation | No accessibility annotations in Figma (ARIA role, focus order, keyboard behaviour all undocumented) |
| Design gap (typo) | Figma text property `curent page#20679:3` has a typo ("curent" not "current") — should be corrected in Figma |
| Incomplete data | `figma_get_component_details` returned "Component not found" — component key unavailable for cross-referencing |
| Missing file | Screenshot captured as embedded MCP image but not saved as `figma-screenshot-Breadcrumbs.png` — export manually from Figma node `21927:40413` |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-30_
