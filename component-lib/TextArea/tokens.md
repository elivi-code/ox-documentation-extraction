# Textarea — Tokens

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [accessibility.md](./accessibility.md) · [textarea-figma.md](./textarea-figma.md) · [textarea-pui.md](./textarea-pui.md)

---

## Note on token extraction

The Oxygen MCP `get-theme-tokens` search for "textarea" returned 0 matches — no dedicated textarea tokens are registered in the MCP token registry. All tokens documented here were extracted directly from the Figma design via `get_design_context` on three state variants (Rest, Error/False, Focus, Disabled).

Figma variables API was not accessible (Enterprise plan required); aliases are recorded as CSS variable names as they appear in the compiled output.

---

## Color tokens

### Input container background

| State | CSS Variable | Resolved value (Light) |
|-------|-------------|------------------------|
| Rest | `--ui/ui05` | `#f4f3ee` |
| Focus | `--ui/ui05` | `#f4f3ee` |
| Error | `--ui/ui05` | `#f4f3ee` |
| Disabled | `--interactive/disabled01` | `#c8c8bd` |

### Input border

| State | CSS Variable | Resolved value (Light) | Width |
|-------|-------------|------------------------|-------|
| Rest | _(none — no border)_ | — | — |
| Focus | `--interactive/focus01` | `#0056e0` | 2px |
| Error | `--error/error01` | `#cb2233` | 2px |
| Disabled | _(none)_ | — | — |

### Text colors

| Element | State | CSS Variable | Resolved value (Light) |
|---------|-------|-------------|------------------------|
| Label | All | `--text/textcolor01` | `#26252a` |
| Required `*` marker | All | `--error/error01` | `#cb2233` |
| Placeholder text | Rest / Focus | `--text/textcolor02` | `#6c6862` |
| Input value text | Rest / Focus | _(inherits `textcolor02` when placeholder visible)_ | `#6c6862` |
| Input text | Disabled | `--interactive/disabled04` | `#8d8b7e` |
| Hint text | All | `--text/textcolor02` | `#6c6862` |
| Error message text | Error | `--error/error01` | `#cb2233` |
| Focus cursor indicator | Focus | `--text/textcolor01` | `#26252a` |

---

## Typography tokens

| Element | Token family | Weight | Size | Line height | Letter spacing |
|---------|-------------|--------|------|-------------|----------------|
| Label | `typography/body01` | 400 (Regular) | `typography/body01/font-size` (14px) | `typography/body01/line-height` (20px) | `typography/body01/letter-spacing` (−0.06px) |
| Required `*` | `typography/bodyBold01` | 600 (SemiBold) | `typography/bodyBold01/font-size` (14px) | `typography/bodyBold01/line-height` (20px) | `typography/bodyBold01/letter-spacing` (−0.06px) |
| Input / Placeholder | `typography/body02` | 400 (Regular) | 16px (hardcoded) | `typography/body02/line-height` (24px) | `typography/body02/letter-spacing` (0.0121px) |
| Hint text | `typography/label01` | 400 (Regular) | `typography/label01/font-size` (12px) | `typography/label01/line-height` (16px) | `typography/label01/letter-spacing` (0px) |
| Error text | `typography/label01` | 400 (Regular) | `typography/label01/font-size` (12px) | `typography/label01/line-height` (16px) | `typography/label01/letter-spacing` (0px) |

> **Hardcoded value flagged:** Input text font-size is set to `16px` directly in the design (not via a token variable). All other typography values reference tokens.

---

## Structural / spacing values

| Property | Value | Token |
|----------|-------|-------|
| Border radius | `6px` | Not tokenised — hardcoded |
| Padding horizontal | `16px` | Not tokenised — hardcoded |
| Padding vertical | `12px` | Not tokenised — hardcoded |
| Gap (label → input → hint) | `4px` | Not tokenised — hardcoded |
| Resize grip position (bottom-right) | `8px` from edges | Not tokenised — hardcoded |
| Focus ring width | `2px` | Not tokenised — hardcoded |
| Focus cursor bar width | `1px` | Not tokenised — hardcoded |

---

## Size variants (from Figma component set)

| Size | Component total height | Input content height |
|------|----------------------|----------------------|
| Large | ~156px | ~88px (112px box − 24px vertical padding) |
| Medium | ~124px | ~56px |
| Small | ~90px | ~22px |

> Heights are approximate — component total height includes label row (20px lh) + 4px gap + input box + 4px gap + hint row (16px lh).

---

## Dark mode

The component supports a `Mode=Dark` variant in Figma. Dark mode token aliases were not resolved (variables API not accessible). Dark mode behavior is controlled at the Oxygen theme provider level, not via a prop on this component.

---

_Source: Oxygen MCP + Figma MCP · Extracted 2026-04-29_
