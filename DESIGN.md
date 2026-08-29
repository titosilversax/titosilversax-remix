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
| `--leader` | `#171310` | Page ground — warm film-base near-black, not a neutral designer-app black |
| `--leader-2` | `#201a15` | Raised surface (nav, card bars) |
| `--leader-3` | `#2b2318` | Card surface |
| `--base-gray` | `#9d917f` | Muted labels/metadata (AA-safe: ≥5.0:1 on every ground) |
| `--emulsion` | `#b7ab9b` | Body text on dark |
| `--paper` | `#efe6d3` | Headings, warm ivory print stock |
| `--sepia` (+ `--sepia-rgb`) | `#c39a5c` | **Ambient structural color** — eyebrows, list marks, card borders, hover states. Present on every page, everywhere, the way real chemical staining is |
| `--light-leak` (+ `--light-leak-rgb`) | `#e0752f` | **The rare accent** — primary CTAs, the hero "live" dot, one featured price. 2–3 uses per page, never a repeated wayfinding mark |
| `--rule` / `--rule-strong` | `rgba(183,171,155,.16/.3)` | Hairlines |

Color strategy: **two colors with distinct jobs**, not one neon accent on black — the trap this build fell into on the first pass and corrected after the fact (see Revision history below). Sepia carries ambient/structural weight (it's *everywhere*: eyebrows, card top-borders, list marks, secondary hovers); orange is spent on 2–3 genuinely rare, active moments per page. Buttons are flat ink with a hard offset shadow (`3px 3px 0 rgba(0,0,0,.3)`) — no blurred glow anywhere in the system; stamped ink and printed paper don't glow.

## Type

- **Display** — `Anton`, uppercase, for h1–h4 and stamped headlines. Not a training-data default; chosen for its stamped/edge-code character.
- **Body/UI** — `Archivo` (400–800, 500 italic).
- **Metadata/mono** — `JetBrains Mono` (400/500/700) for frame numbers, eyebrows, badges, footer legal text, price notes.

## Components (`assets/css/theme.css`)

- `.eyebrow` — mono kicker, sepia text + dot, optional `.frame-no` prefix ("FRAME 01") in `--base-gray`. Appears 5–8× per page, which is exactly why it's sepia, not orange.
- `.btn-primary` / `.btn-secondary` — stamped film-leader tab buttons, flat fill, hard offset shadow (no blur/glow).
- `.frame-card` — the reusable content unit: a `__bar` (frame number + tag) over a `__body`. Every card gets a sepia top border by default; `.frame-card--lit` swaps that to orange to mark the one featured/recommended item — color is never only on the "special" card.
- `.faq-item` — `<details>/<summary>` pattern, unchanged interaction, sepia hover/icon (repeats too often per page for the rare accent).
- Film grain — one cheap SVG `feTurbulence` overlay on `body::before`, `mix-blend-mode: overlay`, opacity 0.05. Applied once globally, not per-section.

Removed as dead CSS during the palette revision: `.badge` and `.sprockets` were defined but never referenced by any page's markup.

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

## Revision history

**Palette rework.** The first pass shipped near-black + one orange accent with blurred glow on buttons and the eyebrow dot — a named AI-cluster look (`new-work.md`'s own calibration section warns against exactly this: "near-black with one neon accent and glowing edges"). Caught by the user on review. Fixed the mechanism, not just the hue: warmed the ground away from a neutral designer-app black, gave sepia/brass real structural work across every repeated element (eyebrows, card borders, list marks, hovers), and cut orange down to 2–3 genuinely rare uses per page (primary CTA, one "live" signal, one featured price). Killed every blurred box-shadow glow in favor of flat fills with a hard offset shadow. All contrast ratios re-verified ≥4.5:1 after the change.

**Inner Life of Sound rename.** The 1:1 peer-support coaching offering (previously unnamed on the live site, called "The Deep Navigation" only in the legal docs) is now named **Inner Life of Sound** everywhere it appears — Offers page process section, home page reel-index teaser, and both Privacy and Terms in `/legal`. Its sliding-scale pricing language was removed (no sliding scale); the CTA is now "Apply Now," linking to a Google Doc application (replacing the old Microsoft Forms link). "Modal Sound Sessions" (the separate $150 single-session offering) and the "state-certified peer support specialist" credential/disclaimer language are unrelated to this rename and were left untouched.
