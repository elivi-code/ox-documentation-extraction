# Toast — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

Token values resolved via Figma plugin API (`getVariableByIdAsync`) traversing the alias chain from the UI-components file (`5YihJ5WuDvnvrlrRMC4sBp`) into the linked UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`). All values are confirmed from Figma — not inferred.

---

## Container tokens

| Semantic token | Property | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|----------------|----------|-------------------|-------------|------------------|------------|
| `ui/ui07` | Background fill | `color/offWhite/offWhite02` | `#26252a` | `color/gray/gray10` | `#f1f1f1` |
| `ui/shadow01` | Drop shadow | *(direct value)* | `rgba(41,41,41,0.25)` | *(direct value)* | `rgba(20,20,20,1.0)` |
| `text/textColor09` | Title + description text | `color/pure/white` | `#ffffff` | `color/pure/black` | `#000000` |
| `icon/icon05` | Status icon fill | `color/pure/white` | `#ffffff` | `color/gray/gray02` | `#292929` |
| `actions/action10` | CTA action links | `color/blue/blue08` | `#99bbf3` | `color/blue/blue05` | `#0056e0` |

> The notification uses an **inverted background by design** — Light mode background is dark (`#26252a`), Dark mode background is light (`#f1f1f1`), so the toast always contrasts with the main app canvas.

---

## Left indicator bar — type-specific tokens

| `type` prop | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|-------------|---------------|-------------------|-------------|------------------|------------|
| `"success"` | `success/success02` | `color/green/green04` | `#189b55` | `color/green/green03` | `#12743f` |
| `"error"` | `error/error02` | `color/red/red07` | `#f24d5f` | `color/red/red05` | `#cb2233` |
| `"warning"` | `warning/warning01` | `color/yellow/yellow06` | `#f8ae1a` | `color/yellow/yellow03` | `#9f701c` |
| `"info"` | `info/info01` | `color/offWhite/offWhite09` | `#ebeae1` | `color/gray/gray05` | `#666666` |
| `"loading"` | `actions/action06` | `color/blue/blue07` | `#4687ed` | `color/blue/blue05` | `#0056e0` |

> Warning icon vector fill uses `warning/warning03` — in Light mode this resolves to the same `color/yellow/yellow06` primitive as `warning/warning01`.

---

## Typography tokens

| Style | Token prefix | Size | Weight | Line-height | Letter-spacing |
|-------|-------------|------|--------|-------------|----------------|
| Title | `typography/bodyBold01/` | `14px` | `600` | `20px` | `-0.06px` |
| Description | `typography/body01/` | `14px` | `400` | `20px` | `-0.06px` |
| CTA links | `typography/bodyBold01/` | `14px` | `600` | `20px` | `-0.06px` |
| Loading text | `typography/body01/` | `14px` | `400` | `20px` | `-0.06px` |

---

## Variants

| Variant | `type` prop value | Visual intent |
|---------|-------------------|---------------|
| Success | `"success"` | Positive feedback |
| Error | `"error"` | Failure / destructive state |
| Warning | `"warning"` | Cautionary state |
| Info | `"info"` | Neutral informational |
| Loading | `"loading"` | In-progress / spinner state |

## Sizes

| Size | `size` prop value |
|------|-------------------|
| Small | `"small"` |
| Medium | `"medium"` |
| Large | `"large"` |

---

> **Note:** OX MCP returned no token matches for the keyword `toast`. All token data above was extracted directly from Figma via plugin API alias chain traversal. Spacing and border-radius values (`320px` width, `4px` indicator, `6px` radius) appear hardcoded in Figma — no spacing/radius token bindings were found on those properties.

_Source: Figma plugin API (alias chain) · UI-Foundations library `iVY5nI8JAxM05Apnnvozzs` · Extracted 2026-05-05_
