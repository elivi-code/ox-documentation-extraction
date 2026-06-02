---
parent: "[[Calendar]]"
section: anatomy
---

## Anatomy

> Visual reference: see the `figma` URL on the [[Calendar]] hub. Two published layouts — a range calendar (788 × 596) and a single calendar (312 × 348), both light mode.

### Range calendar (`mode=light, type=range` — node 80239:8864, 788×596)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Info | structural | Top bar containing optional predefined ranges panel + optional date/time inputs |
| 2 | frame | _Predefined ranges panel | optional slot | Boolean `predefinedRanges`; 148 px wide; right-border divider |
| 3 | instance | _Predefined ranges item × N | content | Repeated list items (Today, Last hour, Yesterday, Last 7 days, This month, Last month, Last 3 months, This year, Last year, Custom) |
| 4 | frame | _Range type | optional slot | Boolean `time`; Intraday toggle + From/To date inputs + Start/End time inputs |
| 5 | frame | Calendars | structural | Horizontal flex, `gap-[32px]`, `px-[24px]`; contains Left calendar + Right calendar |
| 6 | frame | Left calendar | structural | `w-[280px]`, `gap-[12px]` (header to body) |
| 7 | frame | Header (left) | content | Month title text (e.g. "September 2023"), centered, `px-[40px]` |
| 8 | frame | Body (left) | structural | Day grid rows |
| 9 | frame | Right calendar | structural | Mirror of Left calendar |
| 10 | frame | Navigation | structural | `←` icon button + month dropdown + year dropdown + `→` icon button; centered above both months |
| 11 | frame | Action bar | structural | Reset + Cancel + Apply buttons; top border divider |

### Single calendar (`mode=light, type=single` — node 80303:251931, 312×348)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Navigation | structural | `←` arrow + Month dropdown + Year dropdown + `→` arrow |
| 2 | frame | Header | content | Month name text, centered |
| 3 | frame | Body | structural | Weekday row + day grid rows |
| 4 | instance | Day Number (×~35) | content | Each day cell, `size-[40px]` |

### Sub-component: _Day Number (atoms — node frame 80239:9317)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Background Range | optional slot | Shows in-range fill when `range=true`; uses `--ui/ui01` background |
| 2 | frame | Focus ring | optional slot | `border-2 rounded-[1000px]` with `--interactive/focus01`; inner white inset shadow |
| 3 | text | Day number | content | Day digit; `body01` typography |

**Day types exposed in variant set:** `Default`, `Disabled`, `Empty`, `Dimmed`, `Current day`
**Boolean axes:** `Selected` (Yes/No), `Hover` (Yes/No)
**Mode:** Light, Dark

### Sub-component: _Predefined ranges item (atoms — node frame 80239:9446)

States: `Rest`, `Hover`, `Selected`, `Focus`, `Hover and Select - Focus`
Input variant: `Yes` (with text input for custom range), `No` (label only)
Mode: Light, Dark

### Sub-component: _Range type (atoms — node frame 80398:28952)

| Variant | Description |
|---------|-------------|
| `size=large, state=IntradayOn` | Full-width row with Intraday toggle ON + date/time inputs |
| `size=large, state=IntradayOff` | Toggle OFF; time inputs hidden |
| `size=large, state=noIntraday` | No intraday toggle; only date range inputs |
| `size=small, state=IntradayOn/Off/noIntraday` | Stacked/compact layout for narrower breakpoints |

---

## Variants

### Variant axes

Confirmed from `componentPropertyDefinitions` on COMPONENT_SET node `80239:8863`:

| Property | Figma key | Type | Values | Default |
|----------|-----------|------|--------|---------|
| `mode` | `mode` | VARIANT | `light` | `light` |
| `type` | `type` | VARIANT | `range`, `single` | `range` |

> Note: only `light` mode exists in this component set — no dark variant published here.

### Boolean toggles

| Property | Figma key | Default | Notes |
|----------|-----------|---------|-------|
| `time` | `time#29876:2` | `true` | Shows/hides the intraday range toggle and time inputs |
| `predefinedRanges` | `predefinedRanges#80303:0` | `true` | Shows/hides the left predefined ranges panel |
| `90 days` | `90 days#85539:0` | `false` | Enables 90-day range limit mode (disabled dates outside window + tooltip). No dedicated API prop — implemented via `disabledDates` + `disabledDateTooltip` (see [[Calendar.usage]] Pair 3). |

---

## States

### Persistent states

| State | Applied to | Notes |
|-------|-----------|-------|
| Selected | Day cell | `aria-selected`; filled blue circle (`--actions/action01`) |
| Disabled | Day cell | Greyed out; `aria-disabled`; tooltip available via `disabledDateTooltip` |
| Current day | Day cell | Dot indicator below day number |
| Dimmed | Day cell | Passive day from adjacent month |

### Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| hover (day) | pointer over valid day | background changes to `--ui/ui02` |
| focus (day) | keyboard Tab / arrow keys | `border-2` ring in `--interactive/focus01` with white inset shadow |
| selected (day) | click or Enter | filled circle in `--actions/action01`; text becomes white (`--ui/ui06`) |
| range preview | pointer hover in range mode | in-range days show `--ui/ui01` background |
| hover (predefined item) | pointer over | item background → `--ui/ui02` |
| selected (predefined item) | click | item background → `--ui/ui05` |
| focus (predefined item) | keyboard | item background → `--ui/ui05` |

---

## Structure & spacing

### Container

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Width | — | 788px | range mode |
| Width | — | 312px | single mode |
| Height | — | 596px | range mode |
| Height | — | 348px | single mode |
| Border radius | — | 6px | all |
| Border | `--ui/ui01` | 1px solid | all |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Predefined ranges panel width | — | 148px | optional; right-border divider |
| Predefined ranges panel padding-y | — | 16px | top/bottom |
| Predefined ranges item padding | — | 10px top/bottom, 16px left/right | |
| Calendars section padding-x | — | 24px | horizontal outer padding |
| Gap between calendar months | — | 32px | horizontal |
| Month column width | — | 280px | each calendar pane |
| Month header–to–body gap | — | 12px | |
| Month header padding-x | — | 40px | left/right (leaves room for nav arrows) |
| Day cell size | — | 40px × 40px | square |
| Navigation button padding | — | 6px | all sides |
| Action bar button padding | — | 10px top/bottom, 16px left/right | |

### Density / size variants (breakpoints)

| Breakpoint | Width | Predefined ranges | Layout |
|------------|-------|------------------|--------|
| 992–769px | ~495px | optional | dual month |
| 768–541px | ~495px | optional | dual month, compact |
| 768–541px (no ranges) | ~328px | no | dual month |
| 540–320px | ~312px | optional | single month, stacked |
| 540–320px (no ranges) | ~312px | no | single month |

---

## Design decisions & annotations

<!-- STUB:GAP-008 source="Designer should add annotation nodes to the Calendar Figma page explaining design decisions (e.g. why 280px column width, why 40px day cell, why 148px panel)." -->

No Figma design-intent annotations were captured — layer names and generated code only, no verbatim designer notes. Several structural values (788/312 px container, 148 px panel, 280 px month column, 40 px day cell, 6 px radius, 32 px gap, 40 px header padding) are currently hardcoded with no token binding (see [[Calendar.tokens]]).
