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

5. **Verify before you call it done.** After any UI work, run the visual-feedback loop (see §10): screenshot the result with the Playwright screenshot-inspector skill, audit it against the relevant sections of this file (color, type, depth, motion, anti-slop, accessibility), fix what fails, and re-verify.

6. **Persist project-specific decisions.** Org-wide rules live here. Anything specific to *this* project (chosen theme, new component patterns, project tokens) is recorded by the Interface Design skill in `.interface-design/system.md` so it holds across sessions. This file = org rules; that file = this project's extensions.

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
- **Layout, not card-soup:** do **not** default to a grid of identical equal cards. Build real hierarchy — a lead region + supporting modules, varied card sizes, asymmetry where it helps. Use `minmax(0, 1fr)` grids to avoid overflow.

---

## 6 · Component styling

All components consume the semantic tokens and shared structural tokens. Patterns below are constant across every theme.

**Buttons**
- Radius `--radius-button` (12px); padding ~`9px 16px`; `--font-body` 600.
- Primary: `--accent` bg, `--on-accent` text, resting `--shadow-sm`. Hover: `--accent-hover` (or `brightness(.94)`) + `scale(1.02)`. Active: `scale(.97) translateY(1px)`. Shadow does **not** grow.
- Ghost/secondary: `--surface` bg, `--text-primary`, `--shadow-sm`. Hover: `--surface-muted` + `scale(1.02)`.

**Inputs / selects / sliders**
- Radius `--radius-control` (10px); `--surface-muted` field bg; focus ring `--focus-ring`.
- Checkboxes, radios, range sliders: `accent-color: var(--accent)`.

**Chips / badges** (predefined-value fields like status, crop, tags)
- Rounded **rectangles**, `--radius-chip` (8px) — **never full pills for content**.
- Soft tinted fill + same-hue darker text: neutral → `--surface-muted`/`--text-secondary`; semantic → `--success-soft`/`--success` etc. No thin colored outline.

**Severity / enum-with-meaning fields**
- Render as **icon + color + label** together: a soft-tinted rounded square holding a themed icon, plus the text label, colored by semantic token. Mapping: critical → `--error` (alert), high → `--warning` (chevrons-up), medium → `--info` (equals), low → `--success` (chevron-down).

**Cards / panels**
- `--surface` bg, `--radius-card` (16px), `--shadow-card`. No left/top accent stroke; no thin colored outline. Floating panels use `--radius-panel` (20px) + `--shadow-float`.

**Sidebar (floating nav)**
- Floating card, edge gap `--space-edge`. Items: radius ~11px, `--text-secondary`. Hover: `--surface-muted` + `scale(1.02)`. Active: `--accent-soft` bg + `--accent-text`, with an accent dot.

**Filter strip + dropdowns**
- Horizontal row of filter buttons (`--surface`, `--shadow-sm`, radius 12). Open state tints to `--accent-soft`/`--accent-text` and rotates the chevron. Active selections show a count badge (`--accent` fill, Geist).
- Popover = floating card (`--radius-overlay` 16px, `--shadow-float`), entrance via `--ease-spring`. Holds the appropriate input type per filter: **checkboxes**, **multi-select checkboxes** (optionally with search), **radio buttons**, **sliders**. Each popover offers Reset / Done.

**Data table** (Linear/Notion-grade — the standard pattern)
- `--surface` card, header row in `--text-muted` overline style on a `--border` divider; body rows `--text-sm`, `--surface-muted` row hover.
- Required features: **sort** (click header, direction arrow; sort enums by rank not alphabetically), **group by** (collapsible group header rows; pagination off while grouped), **resizable columns** (drag header edge), **show/hide columns** and **add column** (Columns menu), **pagination** (page-size select + prev/next + "1–N of M").
- **Field-aware cells:** text; numeric → Geist tabular; predefined set → chip; status → semantic chip; severity → icon+color+label; ratio/score (e.g. NDVI) → mini progress bar (`--surface-muted` track, `--accent` fill) + Geist value.

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
| `--dur-fast` | `120ms` | Transform changes: hover `scale(1.02)`, press `scale(.96)`, and other micro-interactions that must feel instant. |
| `--dur` | `160ms` | Color / background / opacity / border changes; the default for most state transitions. |
| `--dur-slow` | `240ms` | Larger movements: overlay enter/exit, panel slide, expand / collapse, group-row toggle. |

**Hover/press feel (the house style):**
- **Hover:** color shift (background/accent) + a very slight `scale(1.02)`. **Do not increase the drop shadow.**
- **Press (`:active`):** presses down — `scale(.96) translateY(1px)` — so clicks feel physical.
- Transition `transform` with `--ease-standard` at `--dur-fast`; transition color/background at `--dur`.
- Reserve `--ease-spring` for popover/overlay entrances. Respect `prefers-reduced-motion`.

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

---

## 10 · Accessibility & verification

- **Contrast:** every theme's text/background pairs meet **WCAG 2.1 AA** (body ≥4.5:1, large text & UI fills ≥3:1) — verified by computed contrast for all five themes. Keep new combinations to the same bar; if a value can't be a text color (e.g. amber/terracotta), use `--accent-text`.
- **Focus:** visible `--focus-ring` on all interactive elements; never remove focus styles.
- **Targets & semantics:** ≥40px touch targets where practical; real `<button>`/`<a>`/labelled inputs; icons that carry meaning get an accessible name.
- **Motion:** honor `prefers-reduced-motion` (drop scale/translate, keep instant state changes).

**Visual-feedback loop (run after any UI work, before "done"):**
1. Screenshot the running UI with the Playwright **screenshot-inspector** skill.
2. Audit the screenshot against §2 (theme/color), §4 (type), §6 (components), §7 (depth), §8 (motion/hover), §9 (anti-slop), §10 (a11y).
3. Fix every failure, then re-screenshot and re-verify.
4. Record any project-specific decisions in `.interface-design/system.md` (project extensions), keeping this file as the org-wide source of truth.

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

  /* spacing */
  --space-1: 4px;  --space-2: 8px;  --space-3: 12px; --space-4: 16px;
  --space-5: 20px; --space-6: 24px; --space-8: 32px; --space-10: 40px;
  --space-12: 48px; --space-16: 64px; --space-edge: 12px;

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
  --dur-fast: 120ms; --dur: 160ms; --dur-slow: 240ms;
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
