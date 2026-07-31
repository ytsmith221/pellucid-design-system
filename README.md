# Pellucid design system — lightweight reference

> **Pellucid** /pəˈluːsɪd/ — *translucently clear; easy to understand.*
> AI-native document remediation. Mission: eliminate the world's accessibility debt.

This is a **distilled, framework-free reference**, not a component library or a
rebuild of the original Claude Design export. It exists to be dropped into any
new web project (starting with `pellucid-os`) so a build has the right colors,
type, spacing, and voice from the first commit — copy `tokens.css` in, skim
this file, done.

Two files:

- **`tokens.css`** — every design token as a plain CSS custom property
  (`:root { --paper-50: ...; }`), plus a handful of semantic typography
  classes (`.h1`, `.body`, `.caption`, `.mono`, …). Zero dependencies, zero
  build step — link it and go.
- **`components.html`** — a single static page showing every token and a
  handful of common patterns (buttons, badges, forms, cards) rendered in
  plain HTML/CSS. Open it in a browser as a visual reference; copy markup
  out of it directly. No JS, no React, nothing to install.
- **`assets/`** — logo/mark SVGs (primary lockup, on-dark, app icon, a sample
  illustration).

Deliberately **not** included here (present in the original Claude Design
export if you ever need them, but not useful outside that tool): the
`_ds_manifest.json` preview-grid metadata, `_ds_bundle.js` runtime, the
`_adherence.oxlintrc.json` lint config, the tweaks-panel authoring component,
and the bundled/print HTML exports.

---

## Brand, in short

| | |
|---|---|
| **Audience** | Accessibility leads, compliance officers, doc-ops teams — enterprise, gov, edu, regulated industries. |
| **Personality** | Calm, exact, quietly confident. A specialist, not a salesperson. |
| **Anti-personality** | Hyped, breathless, "AI-magical," emoji-laden growth-marketing. |
| **Visual register** | Editorial. Warm paper. Generous whitespace. Serif display + geometric sans. Teal accent. |

## Voice & content — quick rules

- **Sentence case everywhere.** Only "Pellucid" is capitalized (never PELLUCID, never pellucid).
- **Plain language, precise terms** — "tag tree," "reading order," "alt text," "PDF/UA." Don't soften real vocabulary.
- **Short sentences, one idea each. Active voice.** "Pellucid tagged 412 figures," not "412 figures were tagged."
- **Concrete numbers over superlatives.** "97% of headings detected automatically" beats "industry-leading."
- **"You" for the reader, "we" for Pellucid.** Avoid "users." Address the team: "your team can review…"
- **No emoji, anywhere.** No unicode decoration (✨ ▶ ◆) as ornament. Em dashes (—) are fine for asides.
- Errors are specific and calm: *"We couldn't read page 14. The page is image-only and OCR returned no text."* Not *"Oops! Something went wrong 😬"*

## Color

Warm paper + deep ink, with a single chromatic anchor — **Lucid Teal**
(`--teal-500`, `#2E7567`). Status colors are muted/earthy, never
traffic-light bright: **Amber** (warning), **Rust** (error), **Sage**
(success). Full ramps and semantic aliases (`--bg-page`, `--fg-default`,
`--border-default`, `--brand`, `--warning`, `--error`, `--success`, …) are in
`tokens.css` — always reach for a token/alias, never a raw hex.

- Default page background: `--paper-50` (`#FAF8F3`), not pure white.
- Pure white (`--canvas`) is reserved for "canvas" surfaces — content being
  worked on, not app chrome.
- `--ink-900` (`#14181C`) is a near-black with a slight blue cast, warmer than `#000`.

## Typography

| Role | Family | Use |
|---|---|---|
| Display serif | **Newsreader** | Hero text, big numbers, quotes — italic for moments of voice. |
| Body sans | **Manrope** | Everything else. |
| Mono | **JetBrains Mono** | Code, file paths, tag names, percentages. |

All three load from Google Fonts (see the `<link>` tags at the top of
`components.html`) — no local font files. Semantic classes (`.h1`–`.h4`,
`.body`, `.body-small`, `.caption`, `.micro`, `.eyebrow`, `.mono`,
`.display-xl/l/m`, `.serif-italic`) are defined in `tokens.css`; use them
directly on any element rather than hand-rolling `font-size`/`font-family`.

## Spacing, radii, shadows

- **Spacing:** 4px base scale — `4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 96, 128`
  as `--space-1` … `--space-32`. Generous; never cramped.
- **Radii:** `--radius-sm` 6px (inputs, chips) · `--radius-md` 10px (buttons,
  cards) · `--radius-lg` 14px (large surfaces, modals) · `--radius-pill` 999px
  (tags, status pills). Nothing rounder than 14px except pills — the editorial
  register breaks at "soft."
- **Shadows are minimal.** `--shadow-sm` for hover-lift on interactive cards
  only; `--shadow-md` for floating elements (menus, popovers, toasts). No
  shadow at rest, no glow, no colored shadows, no inner shadows. Prefer a
  1px `--border-default` + a subtle background shift over a shadow.

## Motion

- Default transition: `200ms cubic-bezier(0.2, 0, 0, 1)` (`--duration-base`, `--ease-out`) — calm ease-out, no bounce, no overshoot.
- Hover: background-color shift only, **no scale**. Press: `scale(0.99)` + darker background.
- Reveals: fade + 4px translate, never slide-in-from-edge.
- Always respect `prefers-reduced-motion`.

## Focus states — non-negotiable

Every interactive element needs a visible focus ring:
`box-shadow: var(--focus-ring)` (`0 0 0 3px var(--teal-100), 0 0 0 4px var(--teal-500)`).
Pellucid is an accessibility company — this is a feature, not noise. Never
`outline: none` without a replacement.

## Cards

A "card": `--paper-50` on a `--paper-100` page (or reverse), `1px solid
var(--border-default)`, `--radius-md`, no shadow at rest, `--shadow-sm` on
hover **only if interactive**. Never: colored left-border accents, gradient
borders, drop shadows as default.

## Iconography

[Lucide](https://lucide.dev) via CDN — MIT-licensed, 1.5px stroke, no
attribution needed:

```html
<script src="https://unpkg.com/lucide@latest"></script>
<script>lucide.createIcons();</script>
```

20px inline with body text, 16px in dense UI. Stroke stays at Lucide's
default 1.5 — never thickened. Color is `currentColor` by default. No emoji,
no flat unicode glyphs (❌ ✓ ★) — use Lucide's `check`/`x`/`star` instead.
Every icon must label, indicate state, or be an affordance — never pure
decoration.

## Using this in a new project

1. Copy `tokens.css` (and `assets/` if you need the logo) into the project.
2. Link it after the Google Fonts stylesheet:
   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   <link href="https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400;1,6..72,500&family=Manrope:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
   <link rel="stylesheet" href="tokens.css">
   ```
3. Build with the tokens (`var(--brand)`, `var(--space-4)`, …) and semantic
   classes — never a raw hex, px value, or font-family string outside this file.
4. Skim `components.html` for patterns (buttons, badges, forms, cards) before
   inventing new ones.
