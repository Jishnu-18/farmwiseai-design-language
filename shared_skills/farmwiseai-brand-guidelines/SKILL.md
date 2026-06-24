---
name: farmwiseai-brand-guidelines
description: FarmwiseAI's official UI design language — five selectable color themes, typography, spacing, depth, motion, components, accessibility, and anti-slop rules. Use on ANY task that builds, designs, restyles, reviews, prototypes, or audits a user interface, web page, app, dashboard, screen, component, table, form, or visual layout for FarmwiseAI (React + Tailwind or vanilla HTML). At the start of UI work, ask the user which of the five themes to apply. Triggers on these phrases — UI, frontend, design, build a page/app/screen/component, dashboard, restyle, theme, brand, layout, prototype.
license: Internal — FarmwiseAI. Skill structure adapted from Anthropic's brand-guidelines skill.
---

# FarmwiseAI Brand & UI Guidelines

## Canonical source

The repository's root `DESIGN.md` is the **single source of truth**. The token values in this skill are an exact mirror of it. If the two ever disagree, `DESIGN.md` wins and this skill is regenerated from it. Tokens live in exactly these two places and must never drift.

The model is **one constant structural system + a choice of five color themes**. Structure (shadows, radii, spacing, layout, components, motion, type base) is identical across every FarmwiseAI product so they feel like one family; the color theme is chosen per project for freshness and audience fit.

**Keywords**: FarmwiseAI brand, UI design language, design system, theme, brand colors, typography, components, dashboard, maps, anti-slop, visual design.

---

## Rule 1 — Pick a theme first (always ask)

At the start of any new project/prototype, **ask the user which of the five themes to use** before building. Offer the audience hints. If they have no preference, default to **Meridian**. Set it once on the root element: `<html data-theme="meridian">` (or the project root container). Never mix two themes in one product.

| Theme | Accent | Best for |
|---|---|---|
| `meridian` | Emerald-teal `#0B7256` | Agri / field-data apps, technical dashboards (**default**) |
| `harbor` | Deep navy `#15577D` | Government, enterprise, institutional products |
| `terra-ink` | Terracotta `#B4502E` | Editorial, content-forward, marketing-leaning surfaces |
| `mulberry` | Wine/berry `#9B2D55` | Bold, consumer-facing, brand-standout products |
| `graphite` | Mono ink `#1F2329` | Data-heavy / map-heavy tools where imagery carries the color |

## Rule 2 — Semantic tokens only

Use the CSS variables (or their Tailwind aliases) for every color, radius, shadow, and spacing value. **Never hardcode a hex color or a px radius/shadow/spacing in a component.** This is what lets a product swap themes by changing one `data-theme` attribute. If a value you need isn't defined, propose adding it to `DESIGN.md` (and this skill) — do not improvise.

---

## Typography

- **Body:** `Figtree` (`--font-body`), weights 400/500/600.
- **Headings:** per theme (`--font-heading`) — `Bricolage Grotesque` for Meridian, Harbor, Graphite; `Fraunces` for Terra Ink, Mulberry. Weights 600–700, `letter-spacing: -0.02em`.
- **Numbers/data:** `Geist` (`--font-numeric`), bold, `font-variant-numeric: tabular-nums` — metrics, table numerics, areas, %, currency, IDs.

Eight size tokens only — 1 display, 3 headers, 3 body, 1 overline:

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

Never set running text below 13px. Sentence case for UI labels.

## Spacing & layout

- Scale (4px base): `--space-1..16` (4/8/12/16/20/24/32/40/48/64). Edge gap `--space-edge` 12px.
- **Floating-card paradigm:** nav and overlays are detached, rounded, softly shadowed cards sitting 12–14px from edges — never docked flush. The sidebar floats.
- **Contained width:** main content sits in a centered max-width container — `max-width: var(--content-max)` (1320px), `margin-inline: auto`. Caps on wide monitors with balanced whitespace both sides; shrinks fluidly when narrow. **Never span content edge-to-edge.** With a sidebar, cap and center the content region to the right of it.
- **Consistent gutters:** card grids (KPI rows, dashboard modules, chart rows) use a uniform **1rem (`--space-4`, 16px)** gap between cards *and* rows. Don't mix gap sizes within one dashboard.
- Generous whitespace; **no grid of identical equal cards** — build real hierarchy and varied sizes. Use `minmax(0,1fr)` grids.

## Components (constant across themes)

- **Buttons** — radius `--radius-button` (12px). Primary: `--accent` bg / `--on-accent` text / `--shadow-sm`. Ghost: `--surface` / `--text-primary`. Hover = colour only (no scale); active = `scale(.97) translateY(1px)`.
- **Inputs/sliders/checkboxes/radios** — radius `--radius-control` (10px), `--surface-muted` field, `accent-color: var(--accent)`, focus `--focus-ring`.
- **Search inputs — bounded width:** `min-width: var(--search-min)` (240px), `max-width: var(--search-max)` (420px). **Never flex to full container width.** Placeholder shows fully at default; truncates only if forced below min. Pair with a flexible spacer to push trailing actions to the edge.
- **Selects & dropdowns — ONE pattern:** every select/dropdown/menu (filters, column menus, form selects) uses the **same custom popover component** (see Reference components: `Select`/`MultiSelect`/`Popover`). **Never a bare native `<select>`** (its option list is unstyled and breaks the system); **never mix native and custom controls** in one screen. Field-style trigger = `--surface-muted`; filter-style trigger = `--surface` + `--shadow-sm`, tinting to `--accent-soft`/`--accent-text` when active.
- **Chips/badges** — rounded **rectangles** `--radius-chip` (8px), **never pills for content**. Soft tinted fill + same-hue darker text; semantic chips use `--success-soft`/`--success` etc. No thin colored outline.
- **Severity / enum-with-meaning** — icon + color + label: tinted rounded square + themed icon + label. critical→`--error` (alert), high→`--warning` (chevrons-up), medium→`--info` (equals), low→`--success` (chevron-down).
- **Cards/panels** — `--surface`, `--radius-card` (16px), `--shadow-card`. No left/top accent stroke, no thin colored outline. Floating panels: `--radius-panel` (20px) + `--shadow-float`.
- **Sidebar** — floating card, edge gap. Hover = `--surface-muted` (color only). Active item: `--accent-soft` bg + `--accent-text` + accent dot.
- **Filter strip + dropdowns** — every filter-bar control (buttons, dropdown triggers, search field, date-range box) sits on `--surface` with **`--shadow-card`** (a proper visible drop shadow — floating chips, not the faint `--shadow-sm`), radius 12; open tints to `--accent-soft`/`--accent-text`; active count badge. Popover = floating card (`--radius-overlay`, `--shadow-float`), **gentle-spring entrance** (`pop-spring`, `--dur-pop` 480ms); holds checkboxes / multi-select (optionally searchable) / radios / sliders.
- **Charts (recharts)** — bars: widen to minimize gaps with few categories — `barCategoryGap="20%"`, **no small `maxBarSize` cap** (a small cap reintroduces big gaps on wide charts); bar should read at least as wide as the gap. Radius `[6,6,0,0]`, fill `--accent`. Axes ticks `--text-muted`, grid `--border` (horizontal only); tooltip = `--surface` card + `--shadow-float`.
- **Data table (Linear/Notion-grade, the standard)** — header row on a `--accent-soft` background (a very light shade of the accent) with `--text-muted` overline labels + `--border` divider; sort (rank-aware for enums), group-by (collapsible groups; pagination off while grouped), resizable columns, show/hide + add columns, pagination (page-size + prev/next + "1–N of M"). Field-aware cells: text; numeric→Geist tabular; enum→chip; status→semantic chip; severity→icon+color+label; ratio/score (NDVI)→mini progress bar (`--surface-muted` track, `--accent` fill) + Geist value.
- **KPI / metric card illustrations (generated, object-driven)** — **layout:** prefer a single row of 4, collapsing to 2×2 then single column (`grid-cols-1 md:grid-cols-2 xl:grid-cols-4`, 1rem gutter); 2×2 is an acceptable fallback if 4-up is too tight for the art. Every KPI card gets a bespoke SVG filling its **right ~55–58%**, bleeding to bottom + right edges (`preserveAspectRatio="xMidYMax slice"`); text stays left, above the art. **Generate it at dev time with the `svg-design` skill** using the fixed prompt below. **Object-driven only — no human characters or faces.** Recipe: (1) 2–3 layered light **blobs** in the card's KPI colour; (2) an **oversized 2.5D object** for the metric (boxes, clock+check, route map+pin, alert triangle…) with top/side faces; (3) a **floating UI widget** (rounded white card / pill / chip); (4) **ambient shadows** (`feDropShadow` + ground ellipse); (5) subtle **grain** (`feTurbulence` fractalNoise ~5% alpha, full-bleed rect); (6) soft gradient shading. **Colour strictly from the 6 `--kpi-*` tokens** (one per card, by meaning or for variety; white widgets use `--surface`); never a hue outside them. Scope every gradient/filter `id` per card; add `role="img"` + `aria-label`. See Reference components for the prompt + a worked template.
- **Ambient page background (optional, user-selectable)** — a subtle full-viewport layer behind all content (`fixed; inset:0; z-index:-1; pointer-events:none`), token-colored, most visible in the margins/gaps. Two sanctioned options + off: **Aurora dots** *(default)* — faint dot grid + diffuse `--kpi-blue/-purple/-teal` blobs slowly drifting, revealed via a CSS dot-mask (pure CSS); **Interactive hex** — a flat hex grid on canvas (no skew/perspective), faint `--text-muted` outlines, hexes lit by a **very light** `--accent` wash on pointer proximity (wide radius) with a **persistent decaying glow → soft trail** (pointer via `window` listener); **Off**. Expose both a **Background** selector (default Aurora dots) and a **Theme** selector (the 5 themes via `data-theme`) in **Settings → Appearance**; persist both. Always subtle, slow, `prefers-reduced-motion`-aware. Code in Reference components.

## Depth & elevation (shadows never grow on hover)

`--shadow-sm` (controls) · `--shadow-card` (cards, sidebar, table) · `--shadow-float` (popovers, menus) · `--shadow-overlay` (glass) · `--focus-ring` (keyboard focus). **Glass** (`--glass-bg` / `--glass-blur` / `--glass-border` + `--shadow-overlay`) is reserved for overlays on map imagery — never ordinary cards.

## Motion — hover/press feel

- **Hover = colour/highlight change ONLY — never scale.** Scaling drags the label text (reads as a glitch) and growing padding shifts neighbours. Hover shifts `background`/`color`/`accent` only; **never grow the drop shadow.**
- **Press (`:active`):** presses down — `scale(.97) translateY(1px)` — so clicks feel physical.
- **Dropdown/menu/popover entrance:** the `pop-spring` keyframe over `--dur-pop` (480ms) — a gentle, slow overshoot-and-settle, not a snap.
- Durations: `--dur-fast` 120ms (the press transform), `--dur` 160ms (color/bg + all hover), `--dur-slow` 240ms (expand/collapse), `--dur-pop` 480ms (popover entrance). Honor `prefers-reduced-motion`.

---

## Anti-slop guardrails (hard bans)

- ❌ A second brand accent color.
- ❌ Purple/blue **gradients** (solid blues like Harbor are fine).
- ❌ Inter / Roboto / Arial as a primary face.
- ❌ A grid of identical equal cards as the layout.
- ❌ Emoji anywhere, including as icons (use a real icon set).
- ❌ Pill-shaped chips for content (rounded rectangles only).
- ❌ Left/top accent strokes on cards.
- ❌ Thin colored outlines on info cards.
- ❌ Growing the drop shadow on hover.
- ❌ Hardcoded hex/px in components.
- ❌ A bare native `<select>` for filters, menus, or form fields — use the shared dropdown component.
- ❌ Mixing native and custom form controls in one screen (e.g. a custom popover beside native selects).
- ❌ Content spanning edge-to-edge on wide screens — use the centered `--content-max` container.
- ❌ Scaling anything on hover — hover changes colour/highlight only; the scale belongs to the pressed state.
- ❌ A search input that flexes to full container width — bound it with `--search-min` / `--search-max`.
- ❌ Default browser scrollbars — use the thin, subtle, track-less accent-tinted scrollbar.
- ❌ Bar charts with a small `maxBarSize` leaving big gaps between few bars — widen via `barCategoryGap`.
- ❌ Human characters or faces in KPI illustrations — object-driven only.
- ❌ KPI illustration colours outside the 6 `--kpi-*` tokens.

> **KPI palette exception:** the 6-colour KPI illustration palette is the *one* sanctioned multi-hue set — used **only** inside KPI-card illustrations and the ambient page background (blobs / hexes), never for UI chrome, buttons, links, charts, or general accent. The single-accent rule governs everything else.

---

## Voice & tone (UI copy and product writing)

FarmwiseAI sounds **confident, clear, grounded, and precise** — like an expert colleague, not a marketer. We earn trust with specifics, not adjectives.

- **Clear over clever.** Plain language; short sentences; say the thing.
- **Grounded & specific.** Prefer concrete numbers and outcomes ("12,480 parcels mapped") over vague claims ("powerful insights").
- **Active & direct.** "Run a survey," not "Surveys can be run."
- **Calm & respectful.** No hype, no pressure, no fake urgency. Confident, not loud.
- **Sentence case** for buttons, labels, headings, and menus. No ALL CAPS except the overline label style.
- **Honest empty/error states.** Explain what happened and the next step; never blame the user.

### Banned phrases / words

Never use: "revolutionary", "revolutionize", "game-changer / game-changing", "supercharge", "unleash", "unlock the power of", "harness the power of", "cutting-edge", "next-generation / next-gen", "seamless / seamlessly", "robust", "synergy", "best-in-class", "world-class", "leverage" (as a verb), "delve", "elevate your …", "in today's fast-paced world", "the future of …". No emoji in copy. No exclamation-mark spam (at most one, and rarely).

---

## Accessibility & verification

- **Contrast:** all five themes are WCAG 2.1 AA verified (body ≥4.5:1; large text & UI fills ≥3:1). Hold new combinations to the same bar; if a hue can't be a text color (amber/terracotta), use `--accent-text`.
- **Focus:** visible `--focus-ring` on every interactive element; never remove focus styles.
- **Semantics & targets:** real `<button>`/`<a>`/labelled inputs; ≥40px touch targets where practical; meaningful icons get accessible names.

**Visual-feedback loop — run after any UI work, before calling it done:**
1. Screenshot the running UI with the **playwright-screenshot-inspector** skill.
2. Audit the screenshot against this skill / `DESIGN.md`: theme & color, typography, components, depth, motion & hover, anti-slop, accessibility.
3. **Consistency checklist (the things that slip):** every dropdown/select/menu uses the one shared component — **zero native `<select>` elements**, and one dropdown looks identical to the next; content sits in the centered `--content-max` container (not edge-to-edge); search inputs are width-bounded (not full-width); scrollbars are the thin custom ones (no default browser bars); hover changes colour only (nothing scales on hover); dropdowns open with the gentle 480ms spring; bars are wide with small gaps; chips are rounded rects not pills; shadows don't grow on hover; KPI cards carry object-driven illustrations coloured only from the `--kpi-*` palette (no characters/faces, no off-palette hues).
4. Fix every failure, then re-screenshot and re-verify.
5. Record project-specific decisions (chosen theme, new patterns, project tokens) via the **interface-design** skill in `.interface-design/system.md`. Org-wide rules live here / in `DESIGN.md`; that file holds this project's extensions across sessions.

---

## Reference components (React + Tailwind)

Copy these canonical implementations instead of improvising each control — improvising is how inconsistencies (a polished custom dropdown next to raw native `<select>`s) creep in. They assume the Tailwind token aliases from `DESIGN.md` (`bg-surface`, `text-accent-text`, `rounded-overlay`, `shadow-float`, etc.) and a `.press` utility for the hover/press feel.

**Dropdowns — the single pattern (`Select`, `MultiSelect`, `Popover`).** All three share one `usePopover` hook (outside-click close) and one trigger/panel style. Use `Select` for single-choice (filters and form fields), `MultiSelect` for multi-choice, `Popover` for custom menu content (e.g. a column show/hide menu).

```tsx
import { useEffect, useRef, useState, type ReactNode } from 'react'

function usePopover() {
  const [open, setOpen] = useState(false)
  const ref = useRef<HTMLDivElement>(null)
  useEffect(() => {
    if (!open) return
    const onDown = (e: MouseEvent) => { if (ref.current && !ref.current.contains(e.target as Node)) setOpen(false) }
    document.addEventListener('mousedown', onDown)
    return () => document.removeEventListener('mousedown', onDown)
  }, [open])
  return { open, setOpen, ref }
}

const filterTrigger = (active: boolean) =>
  `press flex items-center gap-2 rounded-button px-3 py-2 text-sm font-medium shadow-sm ${
    active ? 'bg-accent-soft text-accent-text' : 'bg-surface text-text-primary hover:bg-surface-muted'}`
const fieldTrigger = 'press flex w-full items-center gap-2 rounded-control bg-surface-muted px-3 py-2 text-sm text-text-primary'
const PANEL = 'absolute z-50 mt-2 max-h-72 overflow-auto rounded-overlay bg-surface p-1.5 shadow-float'
const OPTION = 'flex w-full cursor-pointer items-center gap-2.5 rounded-control px-2 py-1.5 text-left text-sm hover:bg-surface-muted'

export interface Option { value: string; label: string }

export function Select({ value, options, onChange, variant = 'filter', active = false }: {
  value: string; options: Option[]; onChange: (v: string) => void; variant?: 'filter' | 'field'; active?: boolean
}) {
  const { open, setOpen, ref } = usePopover()
  const current = options.find((o) => o.value === value)
  return (
    <div ref={ref} className={`relative ${variant === 'field' ? 'w-full' : ''}`}>
      <button type="button" onClick={() => setOpen((o) => !o)} className={variant === 'field' ? fieldTrigger : filterTrigger(active || open)}>
        <span className={variant === 'field' ? 'flex-1 truncate text-left' : ''}>{current?.label}</span>
        <span aria-hidden className={`ml-auto transition-transform ${open ? 'rotate-180' : ''}`}>▾</span>
      </button>
      {open && (
        <div className={`${PANEL} left-0 ${variant === 'field' ? 'w-full' : 'w-48'}`}>
          {options.map((o) => (
            <button key={o.value} type="button" onClick={() => { onChange(o.value); setOpen(false) }}
              className={`${OPTION} ${o.value === value ? 'font-semibold text-accent-text' : 'text-text-primary'}`}>{o.label}</button>
          ))}
        </div>
      )}
    </div>
  )
}

export function MultiSelect({ label, values, options, onToggle }: {
  label: string; values: Set<string>; options: string[]; onToggle: (v: string) => void
}) {
  const { open, setOpen, ref } = usePopover()
  return (
    <div ref={ref} className="relative">
      <button type="button" onClick={() => setOpen((o) => !o)} className={filterTrigger(values.size > 0 || open)}>
        <span>{label}</span>
        {values.size ? <span className="rounded-md bg-accent px-1.5 font-numeric text-xs font-bold text-on-accent">{values.size}</span> : null}
      </button>
      {open && (
        <div className={`${PANEL} left-0 w-52`}>
          {options.map((o) => (
            <label key={o} className={OPTION}>
              <input type="checkbox" className="h-4 w-4 accent-accent" checked={values.has(o)} onChange={() => onToggle(o)} />
              <span>{o}</span>
            </label>
          ))}
        </div>
      )}
    </div>
  )
}

export function Popover({ label, count, children }: { label: ReactNode; count?: number; children: ReactNode }) {
  const { open, setOpen, ref } = usePopover()
  return (
    <div ref={ref} className="relative">
      <button type="button" onClick={() => setOpen((o) => !o)} className={filterTrigger(open || (count || 0) > 0)}>{label}</button>
      {open && <div className={`${PANEL} right-0 w-56`}>{children}</div>}
    </div>
  )
}
```

**Chip** (rounded rect, never a pill; soft fill + same-hue text):

```tsx
type Tone = 'info' | 'success' | 'warning' | 'error' | 'neutral' | 'accent'
const tones: Record<Tone, string> = {
  info: 'bg-info-soft text-info', success: 'bg-success-soft text-success',
  warning: 'bg-warning-soft text-warning', error: 'bg-error-soft text-error',
  accent: 'bg-accent-soft text-accent-text', neutral: 'bg-surface-muted text-text-secondary',
}
export const Chip = ({ tone, children }: { tone: Tone; children: ReactNode }) =>
  <span className={`inline-block rounded-chip px-2.5 py-1 text-xs font-semibold ${tones[tone]}`}>{children}</span>
```

**Modal** (centered floating panel, dimmed backdrop, never `position: fixed` content collapse):

```tsx
export function Modal({ title, onClose, children }: { title: string; onClose: () => void; children: ReactNode }) {
  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center p-4">
      <div className="absolute inset-0 bg-black/35" onClick={onClose} />
      <div className="relative z-10 w-full max-w-lg rounded-panel bg-surface p-6 shadow-float">
        <div className="mb-4 flex items-center justify-between">
          <h2 className="text-xl font-bold text-text-primary">{title}</h2>
          <button onClick={onClose} aria-label="Close" className="press grid h-9 w-9 place-items-center rounded-control text-text-secondary hover:bg-surface-muted">✕</button>
        </div>
        {children}
      </div>
    </div>
  )
}
```

**Data table** — build one `columns` config (`{ key, label, numeric? }`), derive a visible/ordered subset, and render with: sortable `<th>` buttons (rank-aware for enums), `--surface-muted` row hover, `--text-overline` header style, a `Popover` "Columns" menu for show/hide + reorder, and a pager (`Showing X–Y of Z` + prev/next). Field-aware cells: text; numeric → `font-numeric`; enum → `Chip`; severity → icon+color+label; ratio → mini bar (`--surface-muted` track, `--accent` fill). All filter controls above the table are `Select`/`MultiSelect` from above — never native selects.

**KPI card illustration** — generate one per KPI card at dev time. Invoke the `svg-design` skill with this exact brief **every time**:

> Modern enterprise SaaS dashboard KPI card illustration, premium 2.5D vector artwork, large cropped composition, illustration fills entire right half of card, touches bottom edge and right edge, only partial scene visible, object-driven (no human characters or faces), soft gradients, subtle grain texture, ambient occlusion shadows, layered depth, oversized foreground elements, floating UI widgets, abstract organic shapes, premium fintech aesthetic, Stripe + Linear + Ramp + Brex + Figma illustration style, highly polished product-design showcase, minimal color palette, clean white background, modern B2B software design language, editorial vector art, sophisticated lighting, dashboard-ready, dribbble quality, design-system friendly.

Card shell: `position:relative; overflow:hidden`, text in a `z-index:2` block on the left; the SVG in an absolutely-positioned right panel (`top/right/bottom:0; width:58%`) with `preserveAspectRatio="xMidYMax slice"`. Worked template (blue "shipments" card — swap the `kpi-blue` tokens for another KPI hue and the motif for the metric):

```xml
<svg viewBox="0 0 400 260" preserveAspectRatio="xMidYMax slice" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Stacked parcels with a tracking widget">
  <defs>
    <radialGradient id="k1bgA" cx="64%" cy="40%" r="76%"><stop offset="0%" stop-color="var(--kpi-blue-bg)"/><stop offset="100%" stop-color="#fff"/></radialGradient>
    <linearGradient id="k1bgB" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="var(--kpi-blue-soft)"/><stop offset="100%" stop-color="var(--kpi-blue-soft)"/></linearGradient>
    <linearGradient id="k1obj" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="var(--kpi-blue)"/><stop offset="100%" stop-color="var(--kpi-blue-deep)"/></linearGradient>
    <filter id="k1soft" x="-40%" y="-40%" width="180%" height="180%"><feDropShadow dx="0" dy="7" stdDeviation="9" flood-color="var(--kpi-blue-deep)" flood-opacity="0.18"/></filter>
    <filter id="k1grain"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" stitchTiles="stitch"/><feColorMatrix type="saturate" values="0"/><feComponentTransfer><feFuncA type="linear" slope="0.05"/></feComponentTransfer></filter>
  </defs>
  <path d="M70,150 C40,95 95,40 165,52 C230,63 250,18 305,40 C375,67 405,150 372,210 C342,262 250,266 165,256 C92,247 100,205 70,150 Z" fill="url(#k1bgA)"/>
  <path d="M150,118 C140,74 205,54 252,72 C300,90 346,82 360,132 C374,180 328,212 268,212 C202,212 160,168 150,118 Z" fill="url(#k1bgB)" opacity="0.8"/>
  <!-- floating UI widget -->
  <g filter="url(#k1soft)"><rect x="226" y="34" width="150" height="58" rx="13" fill="#fff"/>
    <circle cx="246" cy="63" r="5" fill="var(--kpi-blue)"/><path d="M251,63 h70" stroke="var(--kpi-blue-soft)" stroke-width="3" stroke-dasharray="2 7" stroke-linecap="round"/>
    <rect x="240" y="76" width="64" height="6" rx="3" fill="var(--kpi-blue-soft)" opacity="0.6"/></g>
  <ellipse cx="214" cy="250" rx="156" ry="16" fill="var(--kpi-blue-deep)" opacity="0.10"/>
  <!-- oversized 2.5D object (parcel) -->
  <g filter="url(#k1soft)">
    <path d="M214,158 l64,-19 l64,19 l0,88 l-128,0 Z" fill="url(#k1obj)"/>
    <path d="M214,158 l64,-19 l64,19 l-64,19 Z" fill="var(--kpi-blue)" opacity="0.7"/>
    <path d="M278,177 l64,-19 l0,88 l-64,0 Z" fill="var(--kpi-blue-deep)"/>
    <rect x="262" y="196" width="30" height="10" rx="2" fill="var(--kpi-blue-soft)" opacity="0.9"/>
  </g>
  <rect x="0" y="0" width="400" height="260" filter="url(#k1grain)" opacity="0.6"/>
</svg>
```

**Ambient page background** — a `<PageBackground>` reads the chosen mode from prefs and renders one fixed layer. Aurora is pure CSS; Interactive hex is a canvas. Selector + theme switch live in Settings.

```css
/* aurora + hex layer base */
.fwbg { position: fixed; inset: 0; z-index: -1; pointer-events: none; overflow: hidden; }
.fwbg-canvas { position: absolute; inset: 0; width: 100%; height: 100%; }
.fwbg-dots { position: absolute; inset: 0;
  background-image: radial-gradient(circle 1.4px, color-mix(in srgb, var(--text-muted) 20%, transparent) 99%, transparent);
  background-size: 24px 24px; }
.fwbg-mask { position: absolute; inset: 0;
  -webkit-mask: radial-gradient(circle 1.7px, #000 99%, transparent) 0 0 / 24px 24px;
          mask: radial-gradient(circle 1.7px, #000 99%, transparent) 0 0 / 24px 24px; }
.fwbg-aurora > i { position: absolute; inset: -30%; display: block; opacity: .5;
  background:
    radial-gradient(38vw 38vw at 22% 30%, color-mix(in srgb, var(--kpi-blue) 70%, transparent), transparent 60%),
    radial-gradient(42vw 42vw at 78% 26%, color-mix(in srgb, var(--kpi-purple) 65%, transparent), transparent 60%),
    radial-gradient(40vw 40vw at 60% 82%, color-mix(in srgb, var(--kpi-teal) 65%, transparent), transparent 60%);
  animation: fwDrift 34s ease-in-out infinite alternate; }
@keyframes fwDrift { 0% { transform: translate3d(-3%,-2%,0) scale(1); } 100% { transform: translate3d(3%,3%,0) scale(1.1); } }
@media (prefers-reduced-motion: reduce) { .fwbg-aurora > i { animation: none; } }
```

```tsx
// Aurora = <div className="fwbg"><div className="fwbg-dots"/><div className="fwbg-mask fwbg-aurora"><i/></div></div>
// Interactive hex (flat grid, pointer-proximity glow with a persistent decaying trail):
function HexCanvas() {
  const ref = useRef<HTMLCanvasElement>(null)
  useEffect(() => {
    const cv = ref.current!, ctx = cv.getContext('2d')!
    const cs = getComputedStyle(document.documentElement)
    const accent = cs.getPropertyValue('--accent').trim(), neutral = cs.getPropertyValue('--text-muted').trim()
    const rgba = (hex: string, a: number) => { const n = parseInt(hex.replace('#',''),16); return `rgba(${(n>>16)&255},${(n>>8)&255},${n&255},${a})` }
    const dpr = Math.min(devicePixelRatio||1,2), size=24, sq3=Math.sqrt(3), colStep=1.5*size, rowStep=sq3*size
    let w=0,h=0,raf=0,mx=-9999,my=-9999,dmx=-9999,dmy=-9999, hex:{x:number;y:number}[]=[], hi=new Float32Array(0)
    const setup = () => { w=cv.clientWidth; h=cv.clientHeight; cv.width=w*dpr|0; cv.height=h*dpr|0; ctx.setTransform(dpr,0,0,dpr,0,0)
      hex=[]; for(let c=-1;c*colStep<w+size;c++){const cx=c*colStep,off=c%2?rowStep/2:0; for(let r=-1;r*rowStep+off<h+size;r++)hex.push({x:cx,y:r*rowStep+off})} hi=new Float32Array(hex.length) }
    const draw = () => { dmx<-9000?(dmx=mx,dmy=my):(dmx+=(mx-dmx)*0.2,dmy+=(my-dmy)*0.2); ctx.clearRect(0,0,w,h)
      const R=220, live=dmx>-9000, stroke=rgba(neutral,0.075); ctx.lineWidth=1
      for(let i=0;i<hex.length;i++){ const p=hex[i]; let v=hi[i]*0.95
        if(live){const b=Math.max(0,1-Math.hypot(p.x-dmx,p.y-dmy)/R); if(b>v)v=b} hi[i]=v
        ctx.beginPath(); for(let k=0;k<6;k++){const a=Math.PI/3*k,px=p.x+size*Math.cos(a),py=p.y+size*Math.sin(a); k?ctx.lineTo(px,py):ctx.moveTo(px,py)} ctx.closePath()
        if(v>0.003){ctx.fillStyle=rgba(accent,v*0.11); ctx.fill()} ctx.strokeStyle=stroke; ctx.stroke() } }
    const loop = () => { draw(); raf=requestAnimationFrame(loop) }
    setup(); matchMedia('(prefers-reduced-motion: reduce)').matches ? draw() : raf=requestAnimationFrame(loop)
    const onMove=(e:MouseEvent)=>{mx=e.clientX;my=e.clientY}, onLeave=()=>{mx=-9999;my=-9999}, onResize=()=>setup()
    addEventListener('mousemove',onMove); addEventListener('resize',onResize); document.addEventListener('mouseleave',onLeave)
    return ()=>{cancelAnimationFrame(raf);removeEventListener('mousemove',onMove);removeEventListener('resize',onResize);document.removeEventListener('mouseleave',onLeave)}
  }, [])  // remount on theme change (key={theme}) so it re-reads --accent
  return <canvas ref={ref} className="fwbg-canvas" />
}
```

Theme + background are app-level prefs (persisted; theme applied via `document.documentElement.setAttribute('data-theme', theme)` on change), surfaced as two `Select`s in Settings → Appearance.

---

## Full CSS variables (must stay identical to `DESIGN.md` §11)

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

---

_Adapted from Anthropic's `brand-guidelines` skill structure; all Anthropic values (Dark/Light/Orange/Blue/Green colors; Poppins/Lora fonts) replaced with FarmwiseAI's. Regenerate this skill's token values from `DESIGN.md` on every change._
