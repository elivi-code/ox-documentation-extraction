---
parent: "[[Accordion]]"
section: tokens
---

<!-- STUB:GAP-003 source="Re-run get-theme-tokens with broader search terms (e.g. 'ui06', 'textcolor', 'interactive') to confirm canonical names. Token names below use Figma CSS variable syntax and may differ from @8x8/oxygen-tokens registry paths." -->
> **Caveat:** Oxygen MCP returned 0 tokens for the `accordion` package. All data below is from Figma design inspection. Cross-reference against `@8x8/oxygen-tokens` before use in implementation.

## Color tokens

### Header background

| State | Token | Light | Dark |
|---|---|---|---|
| Rest / Focus | `--ui/ui06` | `#ffffff` | `#171719` |
| Hover | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Disabled | `--ui/ui06` | `#ffffff` | `#171719` |

### Title text

| State | Token | Light | Dark |
|---|---|---|---|
| Rest / Hover / Focus | `--text/textcolor01` | `#26252a` | `#ffffff` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` | `#858585` |

### Secondary text

| State | Token | Light | Dark |
|---|---|---|---|
| Rest / Hover / Focus | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` | `#858585` |

### Focus ring

| State | Token | Light | Dark |
|---|---|---|---|
| Focus | `--interactive/focus01` | `#0056e0` | `#d7e3f9` |

### Divider

| Element | Token | Light | Dark |
|---|---|---|---|
| Bottom separator | `--ui/ui01` | `#ebeae1` | `#666666` |

### AI Badge (`AIBadge?=true`)

| Element | Token | Light | Dark |
|---|---|---|---|
| Badge background | `--ui/ui23` | `#e7e3ff` | `#3c2f8e` |
| Badge text | `--text/textcolor10` | `#4a3da4` | `#e7e3ff` |

<!-- SKIP:GAP-008 type=DOC_GAP manual — Scrollbar thumb in dark mode uses hardcoded #858585. No token binding detected. Design must confirm intentional or should be token-bound. -->

---

## Typography tokens

| Element | Token | Size | Weight | Line height | Letter spacing |
|---|---|---|---|---|---|
| Title | `--typography/bodyBold01` | `14px` | `600` | `20px` | `-0.06px` |
| Secondary text | `--typography/label01` | `12px` | `400` | `16px` | `0px` |
| AI badge text | `--typography/label01` | `12px` | `400` | `16px` | `0px` |

| Token | Resolved |
|---|---|
| `--typography/bodyBold01/font-family` | `Inter:Semi_Bold` |
| `--typography/font-family/sans` | `Inter:Regular` |

---

## Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE -->

---

## Token coverage

<!-- STUB:GAP-015 source="Run figma_get_component with enrich=true via Desktop Bridge to obtain authoritative token coverage %. Update this section." -->
> Manual assessment: all color and typography values are tokenised. Exception: `Scrollbar_Mac OS` thumb in dark mode uses `#858585` (see GAP-008). Placeholder `Slot` component uses `--ui/ui23` and `--ui/ui22` for its dashed border (system tokens, not hardcoded).
