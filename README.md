# FarmwiseAI Design Language

One design language for every FarmwiseAI product, so prototypes from different teams and different AI tools (Claude Code, Cursor, v0, …) stop looking different.

The model is **one constant structural system + a choice of five color themes**. Structure — shadows, radii, spacing, layout, components, motion, and the type base — is identical everywhere, so all our products feel like one family. The color theme is chosen per project for freshness and audience fit.

## What's here

| Path | What it is |
|---|---|
| [`DESIGN.md`](DESIGN.md) | **Canonical source of truth.** All tokens, themes, components, anti-slop rules, and the agent-instructions block. Read this first. |
| [`shared_skills/farmwiseai-brand-guidelines/`](shared_skills/farmwiseai-brand-guidelines) | The brand skill that enforces `DESIGN.md` inside Claude. Auto-loads on UI work; its token values mirror `DESIGN.md` exactly. |
| [`_preview/`](_preview) | Standalone HTML previews — the five themes applied to a dashboard, and an interactive filters + data-table demo. Open in a browser. |

## The five themes

Pick one per project (set `data-theme` on the root). Defaults to `meridian`.

| Theme | Accent | Best for |
|---|---|---|
| `meridian` | Emerald-teal | Agri / field-data apps, technical dashboards (default) |
| `harbor` | Deep navy | Government, enterprise, institutional |
| `terra-ink` | Terracotta | Editorial, content-forward surfaces |
| `mulberry` | Wine/berry | Bold, consumer-facing products |
| `graphite` | Mono ink | Data / map-heavy tools |

## Using it

1. Install the brand skill so Claude (and other agents) follow the language:
   ```
   npx skills add <this-repo-url> --skill farmwiseai-brand-guidelines
   ```
2. Start any UI task. Claude asks which of the five themes to use, sets `data-theme`, and builds against the semantic tokens in `DESIGN.md`.
3. Reference semantic CSS variables only — never hardcode hex/px in components.
4. After UI work, run the visual-feedback loop (screenshot → audit against `DESIGN.md` → fix → re-verify). Project-specific decisions persist to `.interface-design/system.md`.

## Sync rule

Tokens live in exactly two places — `DESIGN.md` (canonical) and the `farmwiseai-brand-guidelines` skill — and must never drift. On any change, treat `DESIGN.md` as the source and regenerate the skill's values from it.
