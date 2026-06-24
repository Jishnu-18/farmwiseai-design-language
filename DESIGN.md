# FarmwiseAI — Design Language (`DESIGN.md`)

**This file is canonical.** It is the single source of truth for how every FarmwiseAI product looks and feels — across React + Tailwind apps and vanilla HTML prototypes, and across every AI coding tool (Claude Code, Cursor, v0, etc.). The forked `farmwiseai-brand-guidelines` skill mirrors these exact values; if the two ever disagree, **this file wins** and the skill is regenerated from it.

The model is: **one constant structural system + a choice of five color themes.** Structure (shadows, radii, spacing, layout, components, motion, type base) is identical everywhere so all our products feel like one family. The color theme is chosen per project, so different products stay fresh and audience-appropriate without drifting apart.

---

## 0 · Instructions for AI agents (read first)

You are building a FarmwiseAI product. Follow these rules on every UI, build, or restyle task.

1. **Pick a theme first — always ask.** At the start of any new project/prototype, ask the user *which of the five themes* to use before building. Offer the audience hints below. If they have no preference, default to **Meridian**. Set it once on the root element: `<html data-theme="meridian">` (or the project's root container). Never mix two themes in one product.

   | Theme | Accent | Best for |
   |---|---|---|
   | `meridian` | Emerald-teal | Agri / field-data apps, technical dashboards (**default**) |
   | `harbor` | Deep navy | Government, enterprise, institutional products |
   | `terra-ink` | Terracotta | Editorial, content-forward, marketing-leaning surfaces |
   | `mulberry` | Wine/berry | Bold, consumer-facing, brand-standout products |
   | `graphite` | Mono ink | Data-heavy / map-heavy tools where imagery should carry the color |

2. **Reference semantic tokens only — never raw values.** Use the CSS variables (`var(--accent)`, `var(--text-primary)`, `var(--shadow-card)`, `var(--radius-card)`, `var(--space-4)`…) or their Tailwind aliases. **Never hardcode a hex color or a px radius/shadow/spacing in a component.** This is what lets one product swap themes by changing one attribute.

3. **If a value you need isn't defined here, propose adding it to `DESIGN.md`** (and therefore to the skill) — do not improvise a one-off hex/px. Tokens live in exactly two places (this file + the skill) and must never drift.

4. **Hard guardrails (anti-slop).** No second brand accent color. No purple/blue *gradients* (solid blues like Harbor are fine). No Inter/Roboto/Arial as a primary face. No grid of identical cards as a layout. No emoji (including as icons — use a real icon set). No pill-shaped chips for content (use rounded rectangles). No left/top accent strokes on cards. No thin colored outlines on info cards. No raising the drop shadow on hover.

5. **KPI cards get generated illustrations.** Whenever you build KPI / metric cards, also generate their object-driven SVG illustrations at dev time using the `svg-design` skill and the fixed prompt + recipe in §6 ("KPI / metric card illustrations"), coloured strictly from the 6 `--kpi-*` tokens. This is part of building the cards, not an optional extra.

6. **Verify before you call it done.** After any UI work, run the visual-feedback loop (see §10): screenshot the result with the Playwright screenshot-inspector skill, audit it against the relevant sections of this file (color, type, depth, motion, anti-slop, accessibility), fix what fails, and re-verify.

7. **Persist project-specific decisions.** Org-wide rules live here. Anything specific to *this* project (chosen theme, new component patterns, project tokens) is recorded by the Interface Design skill in `.interface-design/system.md` so it holds across sessions. This file = org rules; that file = this project's extensions.

---

## 1 · Visual theme

Modern, polished, intuitive — spacious and calm, with extensive white space. Aiming for Awwwards / Dribbble-top-shelf quality, never "generic AI dashboard." The signatures:

- **Floating cards.** Surfaces detach from the viewport — they're rounded, softly shadowed cards with a gap from the edges, not panels welded to the window. The sidebar floats; overlays float.
- **Soft depth.** macOS-level rounded corners and layered, multi-stop shadows. Glass (blur) is reserved for overlays on map imagery.
- **Quiet color, confident type.** One accent, generous neutrals, bold headings, and tabular numerics. Color earns attention because it's used sparingly.
- **Calm motion.** Subtle, responsive hover/press feedback; nothing bouncy or attention-seeking in day-to-day UI.

References we're aligned with: Linear, Framer, Spline (craft & polish); Felt, Milanote, Linear (functionality).

---

## 2 · The five themes (color)

Every theme is light-mode, and **every text/background pair is WCAG 2.1 AA verified** (≥4.5:1 for body text, ≥3:1 for large text & UI fills). Themes differ only in color and heading font; all structural tokens (§4–§10) are shared.

Selection mechanism: set `data-theme` on the root. The semantic color variables below are what every component consumes.

### Per-theme palettes

**Meridian** — emerald-teal · heading font: Bricolage Grotesque
| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--canvas` | `#F6F7F9` | | `--accent` | `#0B7256` |
| `--surface` | `#FFFFFF` | | `--accent-hover` | `#095C45` |
| `--surface-muted` | `#EEF0F3` | | `--accent-text` | `#0B7256` |
| `--text-primary` | `#14181F` | | `--accent-soft` | `#DEF0EA` |
| `--text-secondary` | `#4A5160` | | `--on-accent` | `#FFFFFF` |
| `--text-muted` | `#757D8C` | | `--success` / `--success-soft` | `#157F54` / `#E0F1E9` |
| `--border` | `#E4E7EC` | | `--warning` / `--warning-soft` | `#8A6100` / `#F4ECD5` |
| `--border-strong` | `#D2D7DE` | | `--error` / `--error-soft` | `#C0392B` / `#F8E4E1` |
| | | | `--info` / `--info-soft` | `#2C6FB0` / `#E2EDF8` |

**Harbor** — deep navy · heading font: Bricolage Grotesque
| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--canvas` | `#F4F6F8` | | `--accent` | `#15577D` |
| `--surface` | `#FFFFFF` | | `--accent-hover` | `#0F4262` |
| `--surface-muted` | `#EAEEF2` | | `--accent-text` | `#15577D` |
| `--text-primary` | `#131A21` | | `--accent-soft` | `#DDEAF2` |
| `--text-secondary` | `#485663` | | `--on-accent` | `#FFFFFF` |
| `--text-muted` | `#76828D` | | `--success` / `--success-soft` | `#157F54` / `#E0F1E9` |
| `--border` | `#E1E7EC` | | `--warning` / `--warning-soft` | `#8A5D0C` / `#F4ECD5` |
| `--border-strong` | `#CFD8E0` | | `--error` / `--error-soft` | `#C0392B` / `#F8E4E1` |
| | | | `--info` / `--info-soft` | `#2C6FB0` / `#E2EDF8` |

**Terra Ink** — terracotta · heading font: Fraunces
| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--canvas` | `#F7F4EE` | | `--accent` | `#B4502E` |
| `--surface` | `#FFFFFF` | | `--accent-hover` | `#97401F` |
| `--surface-muted` | `#EFEAE0` | | `--accent-text` | `#97401F` |
| `--text-primary` | `#1C1A17` | | `--accent-soft` | `#F3E2DA` |
| `--text-secondary` | `#5A5448` | | `--on-accent` | `#FFFFFF` |
| `--text-muted` | `#837C6E` | | `--success` / `--success-soft` | `#2E7D4F` / `#E4F1E9` |
| `--border` | `#E5DFD3` | | `--warning` / `--warning-soft` | `#8A5D0C` / `#F6ECD8` |
| `--border-strong` | `#D4CCBC` | | `--error` / `--error-soft` | `#C0392B` / `#F8E4E1` |
| | | | `--info` / `--info-soft` | `#2C6E8F` / `#E0EDF3` |

**Mulberry** — wine/berry · heading font: Fraunces
| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--canvas` | `#F7F4F5` | | `--accent` | `#9B2D55` |
| `--surface` | `#FFFFFF` | | `--accent-hover` | `#7E2244` |
| `--surface-muted` | `#EFEAEC` | | `--accent-text` | `#9B2D55` |
| `--text-primary` | `#1E1A1C` | | `--accent-soft` | `#F4E2E9` |
| `--text-secondary` | `#574E51` | | `--on-accent` | `#FFFFFF` |
| `--text-muted` | `#847B7E` | | `--success` / `--success-soft` | `#2E7D4F` / `#E4F1E9` |
| `--border` | `#E7E0E2` | | `--warning` / `--warning-soft` | `#8A5D0C` / `#F6ECD8` |
| `--border-strong` | `#D7CCCF` | | `--error` / `--error-soft` | `#C0392B` / `#F8E4E1` |
| | | | `--info` / `--info-soft` | `#2C6E8F` / `#E0EDF3` |

**Graphite** — mono ink · heading font: Bricolage Grotesque
| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--canvas` | `#F6F6F7` | | `--accent` | `#1F2329` |
| `--surface` | `#FFFFFF` | | `--accent-hover` | `#0E1115` |
| `--surface-muted` | `#EDEDEF` | | `--accent-text` | `#1F2329` |
| `--text-primary` | `#18181B` | | `--accent-soft` | `#E9EAEC` |
| `--text-secondary` | `#46474D` | | `--on-accent` | `#FFFFFF` |
| `--text-muted` | `#74757C` | | `--success` / `--success-soft` | `#157F54` / `#E0F1E9` |
| `--border` | `#E5E5E8` | | `--warning` / `--warning-soft` | `#8A5D0C` / `#F4ECD5` |
| `--border-strong` | `#D5D5D9` | | `--error` / `--error-soft` | `#C0392B` / `#F8E4E1` |
| | | | `--info` / `--info-soft` | `#2C6FB0` / `#E2EDF8` |

> **Amber/terracotta note:** in any theme whose accent is too light to be legible as text on white (e.g. Terra Ink), `--accent-text` is a darker shade of the same hue. Use `--accent` for fills (buttons, badges, bars) and `--accent-text` for links, icons, and accent-colored text. Never invent a separate hue for this.

---

## 3 · Color token contract (semantic usage)

Components must speak in these names, not in hexes:

| Token | Use for |
|---|---|
| `--canvas` | App background / page behind floating cards |
| `--surface` | Card, panel, popover, table, input backgrounds |
| `--surface-muted` | Inset areas, hover backgrounds, track fills, neutral chips |
| `--text-primary` | Headings and primary body text |
| `--text-secondary` | Supporting text, secondary labels |
| `--text-muted` | Captions, placeholders, column headers, hints (large/secondary only) |
| `--border` | Default 1px separators and outlines |
| `--border-strong` | Emphasis borders, hover/active dividers |
| `--accent` | Primary action fills, selected states, brand emphasis, data bars |
| `--accent-hover` | Hover state of accent fills |
| `--accent-text` | Accent-colored links, icons, and text on light surfaces |
| `--accent-soft` | Tinted accent backgrounds (active nav, selected chip, soft fills) |
| `--on-accent` | Text/icons placed on an `--accent` fill |
| `--success / -soft` | Positive status, "healthy", positive deltas |
| `--warning / -soft` | Caution status, "stress", attention needed |
| `--error / -soft` | Critical status, destructive, negative deltas |
| `--info / -soft` | Informational/neutral status, "resolved" |

Status colors are functional, not brand accents — using them does not violate the "one accent" rule.

---

## 4 · Typography

- **Body:** `Figtree` — `--font-body`. Weights 400 / 500 / 600.
- **Headings:** per theme — `--font-heading` is `Bricolage Grotesque` (Meridian, Harbor, Graphite) or `Fraunces` (Terra Ink, Mulberry). Weights 600–700.
- **Numbers / data:** `Geist`, bold, with `font-variant-numeric: tabular-nums` — `--font-numeric`. Use for metrics, table numeric cells, areas, percentages, currency, IDs.

Load (Google Fonts): `Figtree`, `Bricolage Grotesque`, `Fraunces`, `Geist`.

### Type scale (spacious; rem on a 16px base)

Eight size tokens total: one display, three headers, three body, one overline.

| Token | Size / line-height | Use |
|---|---|---|
| `--text-display` | 3rem / 1.1 | Hero / landing display |
| `--text-h1` | 2.25rem / 1.15 | Page title |
| `--text-h2` | 1.75rem / 1.2 | Section title |
| `--text-h3` | 1.375rem / 1.3 | Card / block title, sub-headings |
| `--text-body-lg` | 1.0625rem / 1.6 | Lead body, prominent values |
| `--text-body` | 0.9375rem / 1.6 | Default body, controls |
| `--text-sm` | 0.8125rem / 1.5 | Secondary text, table body, captions, chips |
| `--text-overline` | 0.6875rem / 1.4 | Uppercase labels, column headers (letter-spacing .06em) |

Headings use `letter-spacing: -0.02em`. The smallest token is `--text-sm` (13px) for normal text and `--text-overline` (11px) for uppercase labels — never set running text below 13px. Sentence case for UI labels.

---

## 5 · Spacing & layout

- **Spacing scale (4px base):** `--space-1` 4 · `-2` 8 · `-3` 12 · `-4` 16 · `-5` 20 · `-6` 24 · `-8` 32 · `-10` 40 · `-12` 48 · `-16` 64.
- **Edge gap (`--space-edge`, 12px):** floating panels (sidebar, overlays) sit 12–14px from the viewport/parent edges — never flush.
- **Floating-card paradigm:** primary navigation and overlays are detached rounded cards with `--shadow-card` / `--shadow-float`, not docked panels. The sidebar floats on the left with the edge gap.
- **Generous whitespace:** prefer `--space-6`/`--space-8` between sections; let layouts breathe.
- **Consistent gutters:** card grids (KPI rows, dashboard modules, chart rows) use a **uniform 1rem (`--space-4`, 16px)** gap — between cards *and* between rows. Don't mix gap sizes within one dashboard.
- **Contained width (don't span edge-to-edge):** the main content sits in a centered max-width container — `max-width: var(--content-max)` (1320px), `margin-inline: auto`. On wide monitors content caps and leaves balanced whitespace on both sides; as the viewport narrows the container shrinks fluidly to fill. Never let content stretch the full width of a wide screen. (In an app with a sidebar, cap and center the content region to the right of the sidebar.)
- **Layout, not card-soup:** do **not** default to a grid of identical equal cards. Build real hierarchy — a lead region + supporting modules, varied card sizes, asymmetry where it helps. Use `minmax(0, 1fr)` grids to avoid overflow.

---

## 6 · Component styling

All components consume the semantic tokens and shared structural tokens. Patterns below are constant across every theme.

**Buttons**
- Radius `--radius-button` (12px); padding ~`9px 16px`; `--font-body` 600.
- Primary: `--accent` bg, `--on-accent` text, resting `--shadow-sm`. Hover: `--accent-hover` (or `brightness(.94)`) — **color change only, no scale**. Active: `scale(.97) translateY(1px)` (the pressed feel). Shadow does **not** grow.
- Ghost/secondary: `--surface` bg, `--text-primary`, `--shadow-sm`. Hover: `--surface-muted` (color only). Active: pressed.

**Inputs / sliders**
- Radius `--radius-control` (10px); `--surface-muted` field bg; focus ring `--focus-ring`.
- Checkboxes, radios, range sliders: `accent-color: var(--accent)`.

**Search inputs — bounded width**
- A search field has `min-width: var(--search-min)` (240px) and `max-width: var(--search-max)` (420px). **Never let it flex to fill the whole container** (it looks unbalanced and un-modern). At default width the placeholder shows in full; it may truncate only if the viewport forces the field below its min. In a flex row, pair it with a flexible spacer so trailing actions sit at the far edge.

**Selects & dropdowns — ONE pattern, no exceptions**
- Every select, dropdown, and menu (filters, table column menus, form selects) uses the **same custom popover component** — see the reference implementation in the skill (`Select` / `MultiSelect` / `Popover`). The popover is a floating card (`--radius-overlay`, `--shadow-float`) with token-styled options.
- **Never use a bare native `<select>`** for filters, menus, or form fields — its option list is unstyled by the browser and breaks the design language. **Never mix native and custom controls** in the same screen (the most common consistency failure).
- A field-style select (in forms) uses the `--surface-muted` field trigger; a filter-style select uses the `--surface` + `--shadow-sm` button trigger that tints to `--accent-soft`/`--accent-text` when active/open.

**Chips / badges** (predefined-value fields like status, crop, tags)
- Rounded **rectangles**, `--radius-chip` (8px) — **never full pills for content**.
- Soft tinted fill + same-hue darker text: neutral → `--surface-muted`/`--text-secondary`; semantic → `--success-soft`/`--success` etc. No thin colored outline.

**Severity / enum-with-meaning fields**
- Render as **icon + color + label** together: a soft-tinted rounded square holding a themed icon, plus the text label, colored by semantic token. Mapping: critical → `--error` (alert), high → `--warning` (chevrons-up), medium → `--info` (equals), low → `--success` (chevron-down).

**Cards / panels**
- `--surface` bg, `--radius-card` (16px), `--shadow-card`. No left/top accent stroke; no thin colored outline. Floating panels use `--radius-panel` (20px) + `--shadow-float`.

**Sidebar (floating nav)**
- Floating card, edge gap `--space-edge`. Items: radius ~11px, `--text-secondary`. Hover: `--surface-muted` (color only, no scale). Active: `--accent-soft` bg + `--accent-text`, with an accent dot.

**Filter strip + dropdowns**
- Horizontal row of filter controls. Every filter-bar control — buttons, dropdown triggers, the search field, the date-range box — sits on `--surface` with `--shadow-card` (a proper, visible drop shadow so they read as floating chips above the table; not the faint `--shadow-sm`), radius 12. Open state tints to `--accent-soft`/`--accent-text` and rotates the chevron. Active selections show a count badge (`--accent` fill, Geist).
- Popover = floating card (`--radius-overlay` 16px, `--shadow-float`), entrance via the **gentle spring** (`pop-spring` keyframe, `--dur-pop` 480ms — a slow, soft overshoot, not a snap). Holds the appropriate input type per filter: **checkboxes**, **multi-select checkboxes** (optionally with search), **radio buttons**, **sliders**. Each popover offers Reset / Done.

**Charts (recharts)**
- Bars: with few categories, **widen the bars to minimize the gaps** — set `barCategoryGap="20%"` and **do not cap with a small `maxBarSize`** (a small cap reintroduces big gaps on wide charts). Target: each bar reads at least as wide as the gap beside it. Radius `[6,6,0,0]`, fill `--accent`.
- Axes/grid: ticks `--text-muted`, grid lines `--border` (horizontal only), no axis lines where avoidable. Series color `--accent`; multi-series/status use semantic tokens. Tooltip = `--surface` card, `--shadow-float`, `--radius-lg`.

**Data table** (Linear/Notion-grade — the standard pattern)
- `--surface` card. **Header row:** `--accent-soft` background (a very light shade of the accent), `--text-muted` overline-style labels, `--border` bottom divider. Body rows `--text-sm`, `--surface-muted` row hover.
- Required features: **sort** (click header, direction arrow; sort enums by rank not alphabetically), **group by** (collapsible group header rows; pagination off while grouped), **resizable columns** (drag header edge), **show/hide columns** and **add column** (Columns menu), **pagination** (page-size select + prev/next + "1–N of M").
- **Field-aware cells:** text; numeric → Geist tabular; predefined set → chip; status → semantic chip; severity → icon+color+label; ratio/score (e.g. NDVI) → mini progress bar (`--surface-muted` track, `--accent` fill) + Geist value.

**KPI / metric card illustrations (generated, object-driven)**
- **Layout:** KPI cards prefer a **single row of 4** when width allows, collapsing responsively to **2×2** at medium widths and a **single column** when narrow — `grid-cols-1 md:grid-cols-2 xl:grid-cols-4`, with the 1rem gutter. (If 4-up makes the cards too tight for the art, dropping to 2×2 is an acceptable fallback.)
- Every KPI / metric card gets a bespoke **SVG illustration** filling its **right ~55–58%**, bleeding to the bottom and right edges (`preserveAspectRatio="xMidYMax slice"`). Text (label / value / delta) stays on the left, above the art (`position:relative; z-index`).
- **Generate it at dev time with the `svg-design` skill** (invoke it), using this exact brief **every time**:
  > Modern enterprise SaaS dashboard KPI card illustration, premium 2.5D vector artwork, large cropped composition, illustration fills entire right half of card, touches bottom edge and right edge, only partial scene visible, object-driven (no human characters or faces), soft gradients, subtle grain texture, ambient occlusion shadows, layered depth, oversized foreground elements, floating UI widgets, abstract organic shapes, premium fintech aesthetic, Stripe + Linear + Ramp + Brex + Figma illustration style, highly polished product-design showcase, minimal color palette, clean white background, modern B2B software design language, editorial vector art, sophisticated lighting, dashboard-ready, dribbble quality, design-system friendly.
- **Object-driven only — never human characters or faces.** The motif is the metric's subject (e.g. parcels/boxes for shipments, a clock + check for on-time, a route map + pin for transit, an alert triangle for exceptions).
- **Recipe — every illustration has all of:** (1) 2–3 layered light **organic blobs** in the card's KPI colour (radial + linear gradients); (2) an **oversized foreground object**, rendered 2.5D with top/side faces for depth; (3) a **floating UI widget** (small rounded white card / pill / chip); (4) **ambient shadows** — `feDropShadow` on objects + a faint ground ellipse; (5) a subtle **grain** overlay (`feTurbulence` fractalNoise, ~5% alpha, full-bleed `<rect>`); (6) soft gradient shading throughout.
- **Colour: strictly from the 6 KPI tokens** — `--kpi-{blue|green|purple|amber|teal|rose}` (each with `-bg` / `-soft` / base / `-deep`; see §11). Pick **one** KPI colour per card — by the metric's meaning where it maps (positive→green, caution→amber, alert→rose, neutral→blue/purple/teal) or for variety otherwise. **Never use a hue outside these 6.** White widgets use `--surface`; SVG fills/stops reference the tokens via `var(--kpi-…)`.
- Authoring in inline SVG: scope all gradient/filter `id`s per card (collisions across inline SVGs render wrong); `role="img"` + `aria-label` describing the scene.

**Ambient page background (optional, user-selectable)**
- A subtle full-viewport background may sit behind all content (`position:fixed; inset:0; z-index:-1; pointer-events:none`), token-colored — most visible in the margins around the centered content and the gaps between floating cards. Two sanctioned options + off:
  - **Aurora dots** *(default)* — a faint dot grid (`--text-muted` ~20%) with diffuse `--kpi-blue / -purple / -teal` blobs slowly drifting, revealed only at the dot positions via a CSS dot-mask. Pure CSS.
  - **Interactive hex** — a **flat** hexagon grid (no skew or perspective) on canvas; faint `--text-muted` outlines (~0.075α); hexes light with a **very light** `--accent` wash by pointer proximity over a **wide** radius, and each hex holds a **persistent, decaying glow so the cursor leaves a soft fading trail** (pointer tracked via a `window` listener since the layer is non-interactive).
  - **Off.**
- **Expose as a user setting** in **Settings → Appearance**: a **Background** selector (Aurora dots / Interactive hex / Off, default **Aurora dots**) alongside a **Theme** selector (the five themes, applied by setting `data-theme` on the root). Persist both (e.g. localStorage).
- Always subtle: low opacity, slow motion, never competes with content; respect `prefers-reduced-motion`. Reference implementation (aurora CSS + hex canvas + the prefs / runtime theme-switch) is in the skill.

---

## 7 · Depth & elevation

Layered, soft, multi-stop shadows. **Shadows never grow on hover.**

| Token | Value | Use |
|---|---|---|
| `--shadow-sm` | `0 1px 2px rgba(0,0,0,.05), 0 1px 3px rgba(0,0,0,.04)` | Buttons, filter buttons, small controls |
| `--shadow-card` | `0 1px 2px rgba(0,0,0,.04), 0 6px 16px rgba(0,0,0,.07), 0 18px 40px rgba(0,0,0,.05)` | Cards, floating sidebar, table card |
| `--shadow-float` | `0 2px 6px rgba(0,0,0,.06), 0 14px 34px rgba(0,0,0,.16)` | Popovers, menus, floating overlays |
| `--shadow-overlay` | `0 8px 26px rgba(0,0,0,.16)` | Glass panel on map |
| `--focus-ring` | `0 0 0 3px color-mix(in srgb, var(--accent) 40%, transparent)` | Keyboard focus |

**Glass (map overlays only):** `--glass-bg` `color-mix(in srgb, var(--surface) 62%, transparent)`, `--glass-blur` `blur(14px) saturate(150%)`, `--glass-border` `1px solid rgba(255,255,255,.55)`, with `--shadow-overlay`. Do not use glass for ordinary cards.

---

## 8 · Motion

| Token | Value | When to use |
|---|---|---|
| `--ease-standard` | `cubic-bezier(.2,.7,.3,1)` | Default for everything — all hover/press, color and transform transitions. Use unless an entrance specifically calls for spring. |
| `--ease-spring` | `cubic-bezier(.34,1.56,.64,1)` | Overlay / popover / menu **entrances** only, used sparingly. Never on hover or press (it overshoots and feels "off"). |
| `--dur-fast` | `120ms` | The press transform (`scale(.96)`) and other micro-interactions that must feel instant. |
| `--dur` | `160ms` | Color / background / opacity / border changes — the default, and **all** hover feedback. |
| `--dur-slow` | `240ms` | Larger movements: panel slide, expand / collapse, group-row toggle. |
| `--dur-pop` | `480ms` | Dropdown / menu / popover **entrance** (gentle spring). Deliberately slow + soft. |

**Hover/press feel (the house style):**
- **Hover = colour/highlight change ONLY — never scale.** Scaling an element drags its label text and reads as a glitch; growing padding shifts neighbours. So hover only shifts `background`/`color`/`accent`. **Do not increase the drop shadow.**
- **Press (`:active`):** presses down — `scale(.96) translateY(1px)` — so clicks feel physical. (This brief scale on the text is fine; it reads as "pressed.")
- **Dropdown/menu/popover entrance:** the `pop-spring` keyframe over `--dur-pop` (480ms) — a gentle overshoot-and-settle, not a snap. (`--ease-spring` remains available for other one-off entrances; never use it on hover/press.)
- Respect `prefers-reduced-motion` (drop the press transform and the entrance animation).

---

## 9 · Do's & Don'ts (anti-slop)

**Do**
- Ask which theme before building; set `data-theme` once.
- Use semantic tokens for every color/radius/shadow/space.
- Float cards with the edge gap; layer soft shadows; reserve glass for map overlays.
- Build real hierarchy and whitespace; bold headings; tabular Geist numbers.
- Render predefined-value fields as rounded-rect chips; severity as icon+color+label.

**Don't**
- ❌ A second brand accent color.
- ❌ Purple/blue **gradients** (solid blues like Harbor are fine).
- ❌ Inter / Roboto / Arial as a primary face.
- ❌ A grid of identical equal cards as the layout.
- ❌ Emoji anywhere, including as icons.
- ❌ Pill-shaped chips for content (rounded rectangles only).
- ❌ Left/top accent strokes on cards.
- ❌ Thin colored outlines on info cards.
- ❌ Growing the drop shadow on hover.
- ❌ Hardcoded hex/px in components.
- ❌ A bare native `<select>` for filters, menus, or form fields — use the shared dropdown component.
- ❌ Mixing native and custom form controls in the same screen (e.g. one custom popover next to three native selects).
- ❌ Content that spans edge-to-edge on a wide monitor — use the centered `--content-max` container.
- ❌ Scaling anything on hover — hover changes colour/highlight only; the scale belongs to the pressed/active state.
- ❌ A search input that flexes to full container width — bound it with `--search-min` / `--search-max`.
- ❌ Default browser scrollbars — use the thin, subtle, track-less accent-tinted scrollbar.
- ❌ Bar charts with a small `maxBarSize` that leaves big gaps between few bars — widen bars via `barCategoryGap`.
- ❌ Human characters or faces in KPI illustrations — object-driven only.
- ❌ KPI illustration colours outside the 6 `--kpi-*` tokens.

> **KPI palette exception:** the 6-colour KPI illustration palette is the *one* sanctioned multi-hue set. It applies **only** inside KPI-card illustrations and the ambient page background (their blobs / hexes) — never to UI chrome, buttons, links, charts, or general accent. The single-accent rule governs everything else.

---

## 10 · Accessibility & verification

- **Contrast:** every theme's text/background pairs meet **WCAG 2.1 AA** (body ≥4.5:1, large text & UI fills ≥3:1) — verified by computed contrast for all five themes. Keep new combinations to the same bar; if a value can't be a text color (e.g. amber/terracotta), use `--accent-text`.
- **Focus:** visible `--focus-ring` on all interactive elements; never remove focus styles.
- **Targets & semantics:** ≥40px touch targets where practical; real `<button>`/`<a>`/labelled inputs; icons that carry meaning get an accessible name.
- **Motion:** honor `prefers-reduced-motion` (drop scale/translate, keep instant state changes).

**Visual-feedback loop (run after any UI work, before "done"):**
1. Screenshot the running UI with the Playwright **screenshot-inspector** skill.
2. Audit the screenshot against §2 (theme/color), §4 (type), §6 (components), §7 (depth), §8 (motion/hover), §9 (anti-slop), §10 (a11y).
3. **Consistency checklist (the things that slip):** every dropdown/select/menu uses the one shared component — zero native `<select>` elements, and one dropdown looks identical to the next; content sits inside the centered `--content-max` container (not edge-to-edge); search inputs are width-bounded (not full-width); scrollbars are the thin custom ones (no default browser bars); hover changes colour only (nothing scales on hover); dropdowns open with the gentle 480ms spring; bars are wide with small gaps; chips are rounded rects, not pills; shadows don't grow on hover.
4. Fix every failure, then re-screenshot and re-verify.
5. Record any project-specific decisions in `.interface-design/system.md` (project extensions), keeping this file as the org-wide source of truth.

> Reference component implementations (Select, MultiSelect, Popover, Chip, Modal, Table) live in the `farmwiseai-brand-guidelines` skill — copy those rather than improvising each control, which is how inconsistencies (mixed native/custom dropdowns) creep in.

---

## 11 · Full CSS variables (authoritative copy-paste)

```css
/* ---- Shared structural tokens (identical for every theme) ---- */
:root {
  /* type */
  --font-body: 'Figtree', system-ui, sans-serif;
  --font-numeric: 'Geist', ui-monospace, monospace;
  /* --font-heading is set per theme below */

  --text-display: 3rem;      --lh-display: 1.1;
  --text-h1: 2.25rem;        --lh-h1: 1.15;
  --text-h2: 1.75rem;        --lh-h2: 1.2;
  --text-h3: 1.375rem;       --lh-h3: 1.3;
  --text-body-lg: 1.0625rem; --lh-body-lg: 1.6;
  --text-body: 0.9375rem;    --lh-body: 1.6;
  --text-sm: 0.8125rem;      --lh-sm: 1.5;
  --text-overline: 0.6875rem;--lh-overline: 1.4;

  /* spacing & layout */
  --space-1: 4px;  --space-2: 8px;  --space-3: 12px; --space-4: 16px;
  --space-5: 20px; --space-6: 24px; --space-8: 32px; --space-10: 40px;
  --space-12: 48px; --space-16: 64px; --space-edge: 12px;
  --content-max: 1320px; /* centered max-width for main content — never span edge-to-edge */
  --search-min: 240px; --search-max: 420px; /* search inputs are width-bounded, never full-width */

  /* radii */
  --radius-chip: 8px;    --radius-control: 10px; --radius-button: 12px;
  --radius-card: 16px;   --radius-overlay: 16px; --radius-panel: 20px;
  --radius-pill: 9999px; /* avatars/dots ONLY — never content chips */

  /* elevation */
  --shadow-sm: 0 1px 2px rgba(0,0,0,.05), 0 1px 3px rgba(0,0,0,.04);
  --shadow-card: 0 1px 2px rgba(0,0,0,.04), 0 6px 16px rgba(0,0,0,.07), 0 18px 40px rgba(0,0,0,.05);
  --shadow-float: 0 2px 6px rgba(0,0,0,.06), 0 14px 34px rgba(0,0,0,.16);
  --shadow-overlay: 0 8px 26px rgba(0,0,0,.16);
  --focus-ring: 0 0 0 3px color-mix(in srgb, var(--accent) 40%, transparent);

  /* glass (map overlays only) */
  --glass-bg: color-mix(in srgb, var(--surface) 62%, transparent);
  --glass-blur: blur(14px) saturate(150%);
  --glass-border: 1px solid rgba(255,255,255,.55);

  /* motion */
  --ease-standard: cubic-bezier(.2,.7,.3,1);
  --ease-spring: cubic-bezier(.34,1.56,.64,1);
  --dur-fast: 120ms; --dur: 160ms; --dur-slow: 240ms; --dur-pop: 480ms;

  /* KPI illustration palette — 6 fixed hues, theme-independent, ILLUSTRATION-ONLY
     (the one sanctioned multi-hue exception; decorative, not bound by text-contrast AA).
     Each: -bg (blob/background tint) · -soft (mid blob) · base (object) · -deep (object side / shadow). */
  --kpi-blue-bg:#EEF3FF;   --kpi-blue-soft:#C2D2FF;   --kpi-blue:#5470F0;   --kpi-blue-deep:#3B53C9;
  --kpi-green-bg:#ECFAF1;  --kpi-green-soft:#BFE9CE;  --kpi-green:#2FA45F;  --kpi-green-deep:#1F7D47;
  --kpi-purple-bg:#F3EFFF; --kpi-purple-soft:#D6CBFB; --kpi-purple:#7A5AF0; --kpi-purple-deep:#5B3FD6;
  --kpi-amber-bg:#FFF6E6;  --kpi-amber-soft:#FAD79A;  --kpi-amber:#F2A516;  --kpi-amber-deep:#C9790A;
  --kpi-teal-bg:#E6F7F6;   --kpi-teal-soft:#B6E6E2;   --kpi-teal:#14A89B;   --kpi-teal-deep:#0C7D73;
  --kpi-rose-bg:#FDEEF1;   --kpi-rose-soft:#F8C8D3;   --kpi-rose:#E85C7F;   --kpi-rose-deep:#C23A5E;
}

/* ---- Theme: Meridian (default) ---- */
[data-theme="meridian"] {
  --font-heading: 'Bricolage Grotesque', system-ui, sans-serif;
  --canvas:#F6F7F9; --surface:#FFFFFF; --surface-muted:#EEF0F3;
  --text-primary:#14181F; --text-secondary:#4A5160; --text-muted:#757D8C;
  --border:#E4E7EC; --border-strong:#D2D7DE;
  --accent:#0B7256; --accent-hover:#095C45; --accent-text:#0B7256; --accent-soft:#DEF0EA; --on-accent:#FFFFFF;
  --success:#157F54; --success-soft:#E0F1E9; --warning:#8A6100; --warning-soft:#F4ECD5;
  --error:#C0392B; --error-soft:#F8E4E1; --info:#2C6FB0; --info-soft:#E2EDF8;
}

/* ---- Theme: Harbor ---- */
[data-theme="harbor"] {
  --font-heading: 'Bricolage Grotesque', system-ui, sans-serif;
  --canvas:#F4F6F8; --surface:#FFFFFF; --surface-muted:#EAEEF2;
  --text-primary:#131A21; --text-secondary:#485663; --text-muted:#76828D;
  --border:#E1E7EC; --border-strong:#CFD8E0;
  --accent:#15577D; --accent-hover:#0F4262; --accent-text:#15577D; --accent-soft:#DDEAF2; --on-accent:#FFFFFF;
  --success:#157F54; --success-soft:#E0F1E9; --warning:#8A5D0C; --warning-soft:#F4ECD5;
  --error:#C0392B; --error-soft:#F8E4E1; --info:#2C6FB0; --info-soft:#E2EDF8;
}

/* ---- Theme: Terra Ink ---- */
[data-theme="terra-ink"] {
  --font-heading: 'Fraunces', Georgia, serif;
  --canvas:#F7F4EE; --surface:#FFFFFF; --surface-muted:#EFEAE0;
  --text-primary:#1C1A17; --text-secondary:#5A5448; --text-muted:#837C6E;
  --border:#E5DFD3; --border-strong:#D4CCBC;
  --accent:#B4502E; --accent-hover:#97401F; --accent-text:#97401F; --accent-soft:#F3E2DA; --on-accent:#FFFFFF;
  --success:#2E7D4F; --success-soft:#E4F1E9; --warning:#8A5D0C; --warning-soft:#F6ECD8;
  --error:#C0392B; --error-soft:#F8E4E1; --info:#2C6E8F; --info-soft:#E0EDF3;
}

/* ---- Theme: Mulberry ---- */
[data-theme="mulberry"] {
  --font-heading: 'Fraunces', Georgia, serif;
  --canvas:#F7F4F5; --surface:#FFFFFF; --surface-muted:#EFEAEC;
  --text-primary:#1E1A1C; --text-secondary:#574E51; --text-muted:#847B7E;
  --border:#E7E0E2; --border-strong:#D7CCCF;
  --accent:#9B2D55; --accent-hover:#7E2244; --accent-text:#9B2D55; --accent-soft:#F4E2E9; --on-accent:#FFFFFF;
  --success:#2E7D4F; --success-soft:#E4F1E9; --warning:#8A5D0C; --warning-soft:#F6ECD8;
  --error:#C0392B; --error-soft:#F8E4E1; --info:#2C6E8F; --info-soft:#E0EDF3;
}

/* ---- Theme: Graphite ---- */
[data-theme="graphite"] {
  --font-heading: 'Bricolage Grotesque', system-ui, sans-serif;
  --canvas:#F6F6F7; --surface:#FFFFFF; --surface-muted:#EDEDEF;
  --text-primary:#18181B; --text-secondary:#46474D; --text-muted:#74757C;
  --border:#E5E5E8; --border-strong:#D5D5D9;
  --accent:#1F2329; --accent-hover:#0E1115; --accent-text:#1F2329; --accent-soft:#E9EAEC; --on-accent:#FFFFFF;
  --success:#157F54; --success-soft:#E0F1E9; --warning:#8A5D0C; --warning-soft:#F4ECD5;
  --error:#C0392B; --error-soft:#F8E4E1; --info:#2C6FB0; --info-soft:#E2EDF8;
}

/* ---- Global base: scrollbar + interaction + popover entrance ---- */

/* Thin, subtle scrollbars — no track, no buttons, rounded ends, light accent tint */
* { scrollbar-width: thin; scrollbar-color: color-mix(in srgb, var(--accent) 35%, transparent) transparent; }
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: color-mix(in srgb, var(--accent) 35%, transparent); border-radius: 9999px; }
::-webkit-scrollbar-thumb:hover { background: color-mix(in srgb, var(--accent) 55%, transparent); }
::-webkit-scrollbar-button { display: none; width: 0; height: 0; }
::-webkit-scrollbar-corner { background: transparent; }

/* Interaction: hover = colour only (no scale); press = pressed feel. Apply .press to interactive elements. */
.press {
  transition: background-color var(--dur) var(--ease-standard), color var(--dur) var(--ease-standard),
    border-color var(--dur) var(--ease-standard), filter var(--dur) var(--ease-standard),
    transform var(--dur-fast) var(--ease-standard);
}
.press:active { transform: scale(.97) translateY(1px); }

/* Dropdown / menu / popover entrance — gentle spring (overshoot then settle). Apply .pop-enter to the panel. */
@keyframes pop-spring {
  0%   { opacity: 0; transform: translateY(-6px) scale(.96); }
  60%  { opacity: 1; transform: translateY(0) scale(1.012); }
  100% { opacity: 1; transform: translateY(0) scale(1); }
}
.pop-enter { transform-origin: top center; animation: pop-spring var(--dur-pop) var(--ease-standard) both; }

@media (prefers-reduced-motion: reduce) {
  .press:active { transform: none; }
  .pop-enter { animation: none; }
}
```

### Tailwind mapping (for React + Tailwind projects)

Map tokens in `tailwind.config.js` so utilities resolve to the CSS variables (theme swap stays a single `data-theme` change):

```js
// tailwind.config.js — theme.extend
colors: {
  canvas:'var(--canvas)', surface:'var(--surface)', 'surface-muted':'var(--surface-muted)',
  'text-primary':'var(--text-primary)', 'text-secondary':'var(--text-secondary)', 'text-muted':'var(--text-muted)',
  border:'var(--border)', 'border-strong':'var(--border-strong)',
  accent:'var(--accent)', 'accent-hover':'var(--accent-hover)', 'accent-text':'var(--accent-text)',
  'accent-soft':'var(--accent-soft)', 'on-accent':'var(--on-accent)',
  success:'var(--success)', 'success-soft':'var(--success-soft)',
  warning:'var(--warning)', 'warning-soft':'var(--warning-soft)',
  error:'var(--error)', 'error-soft':'var(--error-soft)',
  info:'var(--info)', 'info-soft':'var(--info-soft)',
},
fontFamily: { body:['Figtree'], heading:['var(--font-heading)'], numeric:['Geist'] },
borderRadius: { chip:'8px', control:'10px', button:'12px', card:'16px', overlay:'16px', panel:'20px' },
boxShadow: {
  sm:'var(--shadow-sm)', card:'var(--shadow-card)', float:'var(--shadow-float)', overlay:'var(--shadow-overlay)',
},
```

---

_Tokens are mirrored in the `farmwiseai-brand-guidelines` skill. On any change here, regenerate the skill's values from this file so the two never drift._
