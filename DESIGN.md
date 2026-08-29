# Design

<!-- impeccable:design-schema 1 -->

## World

**Hand-Processed Film.** A strip of 16mm carrying scratches, uneven chemistry, and light leaks — the emulsion itself joins the recording. Tito is a recording artist first; every soundscape and guide is a session that survived being made. The site treats itself as the archive that recovered them: numbered reels, frame-banded content, sprocket chrome, one hard accent (light-leak orange) marking whatever is alive on the page right now.

Locked via a direction round (concept-seed key `f69801ae`) as a competitive challenger over the assigned direction ("The Working Manuscript" — hand-copied jazz real-book pages). Replaced the prior world entirely (dark purple/gold "mystic night sky," Cormorant Garamond + Great Vibes + Inter).

Direction contract lives in an HTML comment at the top of `index.html`'s `<body>`.

## Tokens

Defined in `assets/css/theme.css`, shared by every page (no more per-page duplicated `<style>` blocks).

| Token | Value | Role |
|---|---|---|
| `--leader` | `#0e0f10` | Page ground |
| `--leader-2` | `#17181a` | Raised surface (nav, card bars) |
| `--leader-3` | `#202224` | Card surface |
| `--base-gray` | `#8a8f93` | Muted labels/metadata (AA-safe: 5.9:1 on `--leader`) |
| `--emulsion` | `#a6abb0` | Body text on dark |
| `--paper` | `#ece8de` | Headings, near-white warm |
| `--sepia` | `#c8b089` | Chemical-stain accent (quotes, `<em>`) |
| `--light-leak` | `#ff8a33` | The one hard accent — CTAs, active state, signal |
| `--light-leak-2` | `#d1631f` | Button gradient dark end (kept ≥4.5:1 under `--leader` text) |
| `--rule` / `--rule-strong` | `rgba(166,171,176,.16/.3)` | Hairlines |

Color strategy: **Committed** — near-black neutral ground, light-leak orange carries the CTA/active layer only, never scattered as decoration.

## Type

- **Display** — `Anton`, uppercase, for h1–h4 and stamped headlines. Not a training-data default; chosen for its stamped/edge-code character.
- **Body/UI** — `Archivo` (400–800, 500 italic).
- **Metadata/mono** — `JetBrains Mono` (400/500/700) for frame numbers, eyebrows, badges, footer legal text, price notes.

## Components (`assets/css/theme.css`)

- `.eyebrow` — mono kicker with a lit dot, optional `.frame-no` prefix ("FRAME 01").
- `.btn-primary` / `.btn-secondary` — stamped film-leader tab buttons (small perforation notches on primary).
- `.frame-card` — the reusable content unit: a `__bar` (frame number + tag) over a `__body`. `.frame-card--lit` marks the "recommended"/active variant with an orange border glow.
- `.badge` — outlined mono tag, three color variants (free/recommended/new).
- `.sprockets` — decorative perforation column, used sparingly (hero edge only).
- `.faq-item` — `<details>/<summary>` pattern, unchanged interaction, restyled to the mono/orange system.
- Film grain — one cheap SVG `feTurbulence` overlay on `body::before`, `mix-blend-mode: overlay`, opacity 0.05. Applied once globally, not per-section.

## Pages built in this world

- `/` (was `/home`) — flagship: full-bleed frame-strip hero (duotone photo, light-leak sweep, sprocket edge-code), session-notes about section, reel-index offerings teaser, community, contact.
- `/offers` — 4 frame-card product grid, process steps, FAQ, contact.
- `/compendium`, `/practice` — long-form single-column sales pages; scroll-reveal + mouse-parallax behavior preserved from the prior build, restyled only.
- `/legal` — merged `/privacy` + `/terms` into one page, two anchored sections (`#privacy`, `#terms`), jump nav. Legal text unchanged verbatim.
- `/thank-you`, `/thank-you-practice` — kept as separate routes (not merged) because their Meta Pixel Purchase-event logic differs per product; restyled only.

## What the world does NOT touch

- Product photography (`tito-portrait.webp`, `tito-playing.webp`) — real photos, only duotone/light-leak CSS filters applied, not replaced.
- The compendium book cover and TOC image — real product assets, shown with a light overlay only.
- All copy, pricing, FAQ answers, and legal text — preserved verbatim; this was a visual redesign, not a content rewrite.

## Known follow-ups (not done in this pass)

- No image-generation tool was available in this session, so this was a **code-led** build throughout: no comp was rendered before build; ambition lived in the direction contract's FIRST VIEWPORT block instead. `.impeccable/config.json` still records `buildPath: comp` as the user's standing preference for whenever image generation is available.
- No automated finish-reviewer subagent was available in this harness; the finish pass was a self-review (detector run + full desktop/mobile screenshot QA across all 7 pages, one contrast-token fix applied before it shipped anywhere).
- Original site copy carries pre-existing em-dash density on the Offers page (flagged advisory by the detector) — it's the client's own original marketing copy, left untouched.
