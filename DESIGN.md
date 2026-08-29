# Design

<!-- impeccable:design-schema 1 -->

## World

**Night Sky / Aurora Star Chart.** A deep indigo-black sky carrying a starfield and soft aurora light — violet, coral, cyan, gold moving through the dark. This isn't decorative sci-fi: Tito's own product is *The Emotional Star Map*, which literally maps feeling onto constellation. The site lives in the same sky the product describes, rather than illustrating it from outside.

This is the world's second visual identity in this build. The first, **Hand-Processed Film** (a 16mm-archive metaphor — frame numbers, sprocket chrome, light-leak orange on warm near-black), shipped first and is preserved in git history and the Revision history section below. The user asked for a full revamp toward "prism, corals, rays of light, magical worlds... neon with black night skies," which is a change of world, not a palette tweak on the old one — handled accordingly.

Direction contract lives in an HTML comment at the top of `index.html`'s `<body>`.

## Tokens

Defined in `assets/css/theme.css`, shared by every page.

| Token | Value | Role |
|---|---|---|
| `--leader` | `#0a0a18` | Page ground — deep indigo-black night sky |
| `--leader-2` | `#13132a` | Raised surface (nav, card bars) |
| `--leader-3` | `#1c1c3a` | Card surface |
| `--base-gray` | `#8d89ab` | Muted labels/metadata (AA-safe: ≥4.9:1 everywhere) |
| `--emulsion` | `#aca8cc` | Body text on dark |
| `--paper` | `#f2eefc` | Headings, cool starlight white |
| `--violet` (+ `-rgb`) | `#c4a3fa` | **Ambient structural color** — the sky itself: eyebrows, card borders, list marks, hover states. Present everywhere a mark repeats |
| `--coral` (+ `-rgb`) | `#ff8095` | **The rare accent** — primary CTAs, the hero "live" dot, one featured price. 2–3 uses per page, never a repeated wayfinding mark |
| `--cyan` (+ `-rgb`) | `#7fe3f5` | **Atmosphere only** — aurora glows and gradients on large surfaces. Never carries small text, so legibility never depends on it |
| `--gold` (+ `-rgb`) | `#ffc978` | **Atmosphere only** — sparing warm counterpoint in glows/gradients |
| `--rule` / `--rule-strong` | `rgba(196,189,224,.14/.28)` | Hairlines |

Color strategy: **two functional colors + two atmosphere-only colors**, not one accent on black. Violet does the ambient/structural work that repeats 5–8× per page (eyebrows, borders, hovers); coral is spent on 2–3 genuinely rare, active moments. Cyan and gold never carry text — they exist purely in the starfield/aurora wash and photo glows, so a low-vision reader never depends on a color that was never contrast-checked for text. Glow *is* used here (box-shadow blur on buttons, the eyebrow dot, the "live" dot) — unlike the first pass, this isn't an accidental AI-default tell, it's the explicit brief ("neon... rays of light... magical").

## Atmosphere

- **Starfield** — `body::before`, eight small radial-gradient points fixed to the viewport, tiled at 340px, opacity 0.4. Cheap, no image asset.
- **Aurora wash** — `body::after`, three large soft radial gradients (violet upper-left, cyan upper-right, coral lower-center) fixed behind all content. Applied once globally, not per-section.
- **Photo treatment** — hero and about photos: `grayscale()` + `contrast()` + `brightness()` only (no color filter), with a two-layer overlay: a plain dark gradient for caption legibility (`::before`) and a violet/coral/cyan radial-gradient glow in `mix-blend-mode: screen` (`::after`) — light appears to fall across the photo rather than a color filter sitting on top of it.
- **Divider** — a violet-to-cyan gradient hairline (was a dashed/dotted rule in the first pass).

## Type

- **Headings — every real `<h1>`–`<h4>`** — `Italianno`, `--ff-script`. Regular weight only (Italianno ships no bold; forcing `font-weight: 700` would fake-bold and break the calligraphic strokes, so headings use 400 throughout). Mixed-case (no `text-transform: uppercase`), `letter-spacing: normal`, `line-height: 1.25–1.3` (Italianno's swashes need more room than a bolder script). Sizes run noticeably larger than a bold-sans heading would need — Italianno's thin strokes and low x-height read smaller at a given font-size, so every heading tier was bumped up when the face changed (v2.2, see Revision history) to stay legible. One deliberate exception: the 24 numbered clause headers inside `/legal`'s Privacy and Terms text (`.doc-body h2`, e.g. "1. Who We Are") stay in plain `Archivo` bold — regulatory text a reader needs to scan quickly, not brand expression. The page's own title ("Privacy & Terms", a real `<h1>`) is still script.
- **Display — numerals and non-heading marks only** — `Anton`, uppercase. Prices (`$27`), roman numerals (inside-numeral), reel-index digits (`01`–`04`), the footer wordmark span. These aren't semantic headings and stay in the bold sans for scannability — a price in cursive script would hurt conversion, not serve the brief.
- **Body/UI** — `Archivo` (400–800, 500 italic).
- **Metadata/mono** — `JetBrains Mono` (400/500/700) for star/section labels, badges, footer legal text, price notes.

## Composition — home page only

`/` (`index.html`) runs a different structural pattern from the rest of the site, locked via a surface-scope concept round (seed key `f11a7960`, card "The Unfolding Map") after the user pointed out that every prior revision — film world, aurora world, cursive type — had only reskinned the original site's stacked-section layout (hero split / about split / offers grid / contact) rather than reimagining it. This round changed composition only; the world (tokens, type) above is unchanged.

- **No hero split.** `.hero-map` has no headline-left/photo-right columns. A built inline SVG constellation (`.constellation`, seven points, no image asset) fills the first viewport; a circular photo medallion and the name-as-chart-label float asymmetrically over it (medallion upper-right, label lower-left on desktop; stacked centered on mobile) rather than dividing the space in half.
- **The thread.** `.thread-wrap` / `.thread-line`: one continuous vertical line (violet → cyan → coral gradient, 2px, low opacity) runs from the end of the hero through About, Offers, Community, and Contact. Sections sit at `z-index: 1` above the line, so it submerges under dense content and resurfaces in the padding gaps between sections (`.thread-node`, a small glowing dot marking each gap) — the page reads as one followed thread, not independent stacked boxes with dividers between them.
- **Offers as nodes, not a grid.** `.offers-thread` uses a 3-column grid (`1fr / 48px gutter / 1fr`) with each of the four offers explicitly placed on its own row, alternating left/right of the thread (`.thread-offer--left` / `--right`), each with a short connector tick reaching toward the gutter. Replaces the previous `.reel-index` plain list.
- **The living aurora.** A small inline script tracks scroll position into `--scroll-progress` (0–1) on `<html>`; `body::after`'s aurora wash (in `theme.css`, shared by every page) reads that variable in a `hue-rotate()` filter, so the sky itself drifts as you travel down the thread rather than sitting as a static repeating backdrop. On every other page `--scroll-progress` is never set, so the filter's `var(--scroll-progress, 0)` fallback keeps them static — this is a home-page-only behavior riding on a site-wide token.

Two catalog challengers were weighed against the assigned structure during the concept round and donated disciplines without becoming their own build: a Miura-fold deployable-sheet challenger (declined; donated the "compact-to-full unfolding" idea, echoed in the constellation building outward from the medallion) and a suminagashi fluid-ink-basin challenger (declined; donated the living/responsive-background idea, built as the scroll-linked hue-rotate rather than a full WebGL fluid solver, which was judged too heavy for this surface). A provenance-ribbon challenger (a continuous custody-chain-through-time structure) was judged competitive but not adopted as its own card — its "one continuous thread" idea is what the assigned direction already was.

**Not yet extended to other pages.** `/offers`, `/compendium`, `/practice`, `/legal`, `/thank-you*` still run the original stacked-section composition (world-only revisions, never re-composed). If the thread/node pattern should carry through the rest of the site, that's a follow-up, not implied by this pass.

## Components (`assets/css/theme.css`)

- `.eyebrow` — mono kicker, violet text + a violet dot with a small glow, optional `.frame-no` prefix (e.g. "STAR 01") in `--base-gray`.
- `.btn-primary` / `.btn-secondary` — coral flat fill with a real soft glow (`0 0 22px rgba(coral,.35)`) on primary; outline on secondary.
- `.frame-card` — the reusable content unit: a `__bar` (star number + tag) over a `__body`. Every card gets a violet top border by default; `.frame-card--lit` swaps that to coral (plus a faint glow) to mark the one featured/recommended item.
- `.faq-item` — `<details>/<summary>` pattern, violet hover/icon.

## Pages built in this world

- `/` — flagship, structurally distinct from the rest of the site: see Composition above. No hero split, one continuous thread from hero to contact, offers as alternating nodes.
- `/offers` — 4 `.frame-card` product grid, the **Inner Life of Sound** process section, FAQ, contact.
- `/compendium`, `/practice` — long-form single-column sales pages; scroll-reveal + mouse-parallax behavior preserved, restyled only.
- `/legal` — merged `/privacy` + `/terms`, two anchored sections, legal text unchanged verbatim.
- `/thank-you`, `/thank-you-practice` — kept as separate routes (their Meta Pixel Purchase-event logic differs per product).

Wayfinding vocabulary changed with the world: "FRAME NN" / "REEL X" (film-can language) became a single sequential "STAR NN" numbering per page. The film-specific chrome that had no honest night-sky equivalent was dropped outright rather than reskinned: the hero's fake film-frame corner tag ("03A"), the compendium cover's corner tag ("7A"), and the nav's fabricated edge-code ("7247 · E7 · 16MM") are gone; the nav kicker is now "Modal Star Chart."

## What the world does NOT touch

- Product photography and the compendium cover/TOC art — real assets, only CSS filters/overlays applied.
- All copy, pricing, FAQ answers, and legal text — preserved verbatim.

## Known follow-ups (not done in this pass)

- No image-generation tool was available in this session, so every pass here was **code-led**: no comp was rendered before build. `.impeccable/config.json` still records `buildPath: comp` as the user's standing preference for whenever image generation is available.
- No automated finish-reviewer subagent was available in this harness; the finish pass was a self-review (detector run + full desktop/mobile screenshot QA, contrast re-verified after each token change).
- Original site copy carries pre-existing em-dash density on the Offers page (flagged advisory by the detector) — it's the client's own original marketing copy, left untouched.

## Revision history

**v1 — Hand-Processed Film.** Locked via a direction round (concept-seed key `f69801ae`) as a competitive challenger over the assigned direction ("The Working Manuscript"). Replaced the prior "mystic night sky" purple/gold world (Cormorant Garamond + Great Vibes + Inter) entirely. Shipped across all 7 pages.

**v1.1 — Palette self-correction.** v1's first pass had near-black + one orange accent with blurred glow on buttons and the eyebrow dot — a named AI-cluster look (`new-work.md`'s own calibration section warns against exactly this). Caught on review before the user's next message. Warmed the ground, gave brass/sepia real structural work everywhere a mark repeated, cut orange to 2–3 rare uses per page, killed all blurred glow for flat fills with a hard offset shadow.

**Inner Life of Sound rename (content, not visual).** The 1:1 peer-support coaching offering (previously unnamed on the live site, called "The Deep Navigation" only in the legal docs) renamed to **Inner Life of Sound** across Offers, home, and `/legal`. Sliding-scale pricing language removed; CTA is now "Apply Now" linking to a Google Doc application (replacing the old Microsoft Forms link). "Modal Sound Sessions" and the peer-support-specialist credential language are unrelated and untouched.

**v2 — Night Sky / Aurora Star Chart.** User request: "revamp the color scheme to something moreso looking like prism, corals, rays of light, magical worlds... neon with black night skies." Judged as a world change, not a token edit, given the film-archive vocabulary (frame numbers, sprockets, edge-codes) had no honest translation into a celestial palette. Renamed the functional tokens (`--sepia`→`--violet`, `--light-leak`→`--coral`) rather than just recoloring them, added two atmosphere-only prism colors (`--cyan`, `--gold`), added the starfield/aurora-wash background, reworked hero/about photo treatment from a single-color light-leak sweep to a multi-color screen-blend glow, and swept every page's wayfinding text from film vocabulary to "STAR NN." Glow returns deliberately here — this world's brief explicitly asked for neon and rays of light, so a soft box-shadow bloom on the coral accent is the brief being honored, not the v1 mistake recurring.

**v2.1 — Cursive headings.** User request: "every heading to be a cursive font." Added `--ff-script` (`Dancing Script`) and repointed every real `<h1>`–`<h4>` to it, dropping `text-transform: uppercase` and positive letter-spacing globally (both break a script face's letter-joins) and loosening line-height for descenders. Two things deliberately did *not* become cursive despite living inside `<h*>`-adjacent markup or looking heading-like: the 24 numbered clause headers in `/legal` (plain text a reader needs to scan, not brand voice) and the `--ff-display` (Anton) elements that were never semantic headings in the first place — prices, roman numerals, reel-index digits, the footer wordmark. Bumped several small heading sizes (card/process/inside titles, thank-you headlines) up to compensate for script's lower apparent x-height at a given font-size.

**v2.2 — Italianno swap.** User feedback: Dancing Script "is a little girly"; named `Italianno` as the replacement. Swapped the Google Fonts import and `--ff-script` value; Italianno ships regular weight only, so every heading rule that forced `font-weight: 700` was dropped to 400 (a synthetic-bold script face breaks its own calligraphic strokes). Italianno's thinner stroke and lower x-height read noticeably smaller than Dancing Script at the same font-size, so every heading tier was sized up again and given more line-height room for its swashes. The v2.1 exceptions (legal clause headers, non-heading Anton elements) carried forward unchanged.

**v3 — Home page recomposed ("The Unfolding Map").** User feedback, verbatim in substance: every revision so far was "a near carbon copy" of the original site with a different palette — accurate. v1, v1.1, v2, v2.1, and v2.2 all changed color and type and never once touched composition; home kept the original site's hero-split/about-split/offers-grid/contact skeleton through every pass. Ran the surface-scope concept round the process actually calls for here (`concept-seed.mjs --scope surface`, seed key `f11a7960`) instead of continuing to default to that one obvious structure, and rebuilt `/` per the locked card. See Composition above for what changed. Scope: home page only, by the terms of the decision round the user answered ("the home page's structure") — the rest of the site's composition is an open follow-up.
