---
name: farmwiseai-brand-guidelines
description: FarmwiseAI's official UI design language — five selectable color themes, typography, spacing, depth, motion, components, accessibility, and anti-slop rules. Use on ANY task that builds, designs, restyles, reviews, prototypes, or audits a user interface, web page, app, dashboard, screen, component, table, form, or visual layout for FarmwiseAI (React + Tailwind or vanilla HTML). At the start of UI work, ask the user which of the five themes to apply. Triggers on: UI, frontend, design, build a page/app/screen/component, dashboard, restyle, theme, brand, layout, prototype.
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
- Generous whitespace; **no grid of identical equal cards** — build real hierarchy and varied sizes. Use `minmax(0,1fr)` grids.

## Components (constant across themes)

- **Buttons** — radius `--radius-button` (12px). Primary: `--accent` bg / `--on-accent` text / `--shadow-sm`. Ghost: `--surface` / `--text-primary`.
- **Inputs/sliders/checkboxes/radios** — radius `--radius-control` (10px), `--surface-muted` field, `accent-color: var(--accent)`, focus `--focus-ring`.
- **Chips/badges** — rounded **rectangles** `--radius-chip` (8px), **never pills for content**. Soft tinted fill + same-hue darker text; semantic chips use `--success-soft`/`--success` etc. No thin colored outline.
- **Severity / enum-with-meaning** — icon + color + label: tinted rounded square + themed icon + label. critical→`--error` (alert), high→`--warning` (chevrons-up), medium→`--info` (equals), low→`--success` (chevron-down).
- **Cards/panels** — `--surface`, `--radius-card` (16px), `--shadow-card`. No left/top accent stroke, no thin colored outline. Floating panels: `--radius-panel` (20px) + `--shadow-float`.
- **Sidebar** — floating card, edge gap. Active item: `--accent-soft` bg + `--accent-text` + accent dot.
- **Filter strip + dropdowns** — horizontal filter buttons; open tints to `--accent-soft`/`--accent-text`; active count badge. Popover = floating card (`--radius-overlay`, `--shadow-float`), spring entrance; holds checkboxes / multi-select (optionally searchable) / radios / sliders.
- **Data table (Linear/Notion-grade, the standard)** — sort (rank-aware for enums), group-by (collapsible groups; pagination off while grouped), resizable columns, show/hide + add columns, pagination (page-size + prev/next + "1–N of M"). Field-aware cells: text; numeric→Geist tabular; enum→chip; status→semantic chip; severity→icon+color+label; ratio/score (NDVI)→mini progress bar (`--surface-muted` track, `--accent` fill) + Geist value.

## Depth & elevation (shadows never grow on hover)

`--shadow-sm` (controls) · `--shadow-card` (cards, sidebar, table) · `--shadow-float` (popovers, menus) · `--shadow-overlay` (glass) · `--focus-ring` (keyboard focus). **Glass** (`--glass-bg` / `--glass-blur` / `--glass-border` + `--shadow-overlay`) is reserved for overlays on map imagery — never ordinary cards.

## Motion — hover/press feel

- **Hover:** color shift + slight `scale(1.02)`. **Do not increase the drop shadow.**
- **Press (`:active`):** presses down — `scale(.96) translateY(1px)`.
- `--ease-standard` is the default (hover/press, color & transform). `--ease-spring` is for overlay/popover **entrances only**, never hover/press. Durations: `--dur-fast` 120ms (transforms), `--dur` 160ms (color/bg), `--dur-slow` 240ms (overlay/expand/collapse). Honor `prefers-reduced-motion`.

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
3. Fix every failure, then re-screenshot and re-verify.
4. Record project-specific decisions (chosen theme, new patterns, project tokens) via the **interface-design** skill in `.interface-design/system.md`. Org-wide rules live here / in `DESIGN.md`; that file holds this project's extensions across sessions.

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

---

_Adapted from Anthropic's `brand-guidelines` skill structure; all Anthropic values (Dark/Light/Orange/Blue/Green colors; Poppins/Lora fonts) replaced with FarmwiseAI's. Regenerate this skill's token values from `DESIGN.md` on every change._
