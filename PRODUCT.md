# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Primary: feeling-first musicians and improvisers — especially saxophonists and songwriters — who want to write and play music that matches an emotional or spiritual state rather than starting from theory. They arrive as self-serve buyers of digital guides/soundscapes (The Emotional Star Map, The Saxophonist's Compendium, A Contemplative Music Practice in a Box) and may also be fans discovering Tito's own playing.

Secondary: people in heavier life transitions (grief, identity, burnout, cultural disconnection) who want human, relationship-based support and find Tito through his peer-support credential and music. They may move from a digital product into 1:1 sessions or the 90-Day Intensive, but this is explicitly a smaller, adjacent offering, not the funnel's main path (confirmed).

## Product Purpose

The site is Tito Silversax's (Alberto Martir's) artist site and digital storefront. It exists to sell feeling-first, spirit-first musical tools and soundscapes to musicians who are tired of theory-first instruction, and secondarily to open a path into deeper 1:1 peer-support work for people navigating hard emotional terrain. Success is digital product sales (Kit-based checkout) and, secondarily, applications/bookings for 1:1 work — plus growing the Meditative Musicians community and Tito's own audience as a performing/recording saxophonist.

## Positioning

Tito combines two things a typical music-education product or a typical wellness/peer-support offer does not: rigorous harmonic/physical knowledge of modal music (world tuning systems, harmonic physics, sacred geometry) *and* lived mystical/spiritual and peer-support credentialing (contemplative Christian faith, Taíno roots, mystical experience, state-certified peer support specialist). The product mechanism is mapping emotional/spiritual states directly onto musical modes — skipping conventional music theory — taught by someone who is simultaneously a serious working improviser (Cleveland jazz/improv scene) and a credentialed peer-support practitioner. A neighboring music-theory product or a neighboring wellness product could not truthfully claim both halves.

## Operating Context

- Static HTML/CSS/JS, no framework, deployed on Vercel (titosilversax.com) with `vercel.json` handling redirects/rewrites/security headers.
- Commerce and email run through Kit (formerly ConvertKit); legacy Gumroad links have been migrated off (see git history: "Move ... checkout from Gumroad to Kit").
- `api/kit-purchase.js`: a Vercel serverless function bridging Kit's purchase webhook to Meta's Conversions API for server-side ad attribution (requires `META_CAPI_ACCESS_TOKEN` and `KIT_WEBHOOK_SECRET` env vars).
- Community lives on Skool ("Meditative Musicians"), linked from the site, not hosted on it.
- Socials: YouTube, Instagram, Bandcamp (all @titosilversax).
- Site structure: `/home` (artist bio/about, redirected from `/`), `/offers` (product hub, renamed from `/offerings`), `/compendium` and `/practice` (dedicated product pages), `/privacy`, `/terms`, plus `/thank-you` and `/thank-you-practice` funnel pages.
- The site previously existed under a different concept, "Tito Dreaming With Me," framed around peer support/healing first; it was renamed to the current ambient-saxophonist framing (commit: "Rename /titodreamingwithme to /home"). Old URLs 301-redirect to the new structure. Treat the peer-support framing as real but secondary per the confirmed emphasis, not as the site's identity to restore.

## Capabilities and Constraints

- Three live digital products: **The Emotional Star Map** (free 6-page guide + a $27 "Songwriter's Edition" full system), **The Saxophonist's Compendium** ($27, PDF & EPUB — harmonic physics, world tuning systems, sacred geometry, spiritual practice), **A Contemplative Music Practice in a Box** ($97 — ten modal journeys, ten 30-minute drone soundscapes, a five-movement ritual).
- 1:1 peer-support work exists (a "90-Day Intensive" with sliding-scale pricing, reached via application/voice-memo/email) but has no dedicated product page in the current build — only a process explainer and FAQ entry on `/offers`. Don't inflate its build-out to match the digital products without being asked.
- Legal/ethical line the copy already draws and must never be blurred: **"This is peer support, not therapy or medical treatment."** Any new copy involving the peer-support side must preserve this distinction.
- Spiritual claims are handled carefully: an FAQ was deliberately reframed from a "mysticism" framing to "Do I need to be religious?" (git: "Reframe mysticism FAQ as religiosity question") — the material stays substantive (references Kabbalah, Sufism, sound as sacred practice) but is framed as accessible to musicologists and mystics alike, never requiring belief.
- Copy has been deliberately edited to remove AI-pattern phrasing and unverifiable claims (git: "Correct compendium FAQ claims about exercises," "Remove fingering and overtone-practice claims from listings," "Tighten compendium copy: remove AI-pattern phrasing") — new copy must stay in Tito's specific, concrete voice and never restate claims the product doesn't actually make.

## Brand Commitments

- Public name/identity: **Tito Silversax** (real name Alberto Martir, credited by full name on product pages: "By Tito Silversax (Alberto Martir)"). This is the committed brand going forward; "Tito Dreaming With Me" is retired.
- Existing visual assets present in the repo: `images/logo.PNG` / `logo.webp`, `home/favicon.png`, `home/og-preview.png`, `home/portrait.jpg`, `home/contact-bg.jpg`, `images/tito-playing.webp`, `images/tito-portrait.webp`, `images/compendium-cover.jpg/webp`, `images/TOC.jpg/webp`, `images/background.png/webp`.
- Voice reference points named in the copy itself: Sam Newsome, Toru Takemitsu, Debussy, Satie, Beethoven, Tomasz Stańko, Stephan Micus, Coltrane, Miles Davis — used as the artist's own stated influences, not brand-voice instructions to imitate wholesale.
- Bilingual note: earlier copy mentioned Spanish availability; a later commit removed the Spanish-availability line from the offers page (git: "Remove Spanish availability line from offers page") — treat current English-only presentation as the confirmed state unless the user says otherwise.

## Evidence on Hand

- Real product copy, pricing, and FAQs for all three digital products (`compendium/index.html`, `practice/index.html`, `offers/index.html`).
- One real attributed testimonial: Terry W., "Compendium reader" (`compendium/index.html`).
- Real photography and cover art already in the repo (see Brand Commitments asset list above).
- `titodreaming-snapshot.md` and `titodreaming-*.png` / `redesign-*.png` / `compendium-mobile*.png` / `offerings-*.png` at the repo root are prior design-exploration screenshots/snapshots, not current product truth — treat them as historical evidence of the old direction, not as content or design instructions to carry forward.
- No case studies, press, or additional testimonials beyond the one noted above — do not fabricate more.

## Product Principles

1. Feeling and lived spiritual/emotional experience come before music theory in every product and every explanation — the mechanism is "map the feeling to the mode," not "learn the rule."
2. Substance stays real: harmonic physics, world tuning systems, and spiritual/sacred-practice references are treated seriously and specifically, never watered down or generalized into vague inspirational language.
3. Digital products are the primary business; 1:1 peer-support work is real but secondary — don't rebalance the site's weight toward it without being asked.
4. The peer-support/therapy line is never blurred, and spiritual claims stay invitational (musicologist or mystic, either welcome) rather than prescriptive.
5. Copy stays in Tito's specific, concrete, claim-checked voice — no AI-pattern phrasing, no unverifiable claims, no invented proof.
