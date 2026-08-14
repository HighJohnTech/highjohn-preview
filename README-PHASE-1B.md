# Phase 1B — Services, About, Work + Navigation

Built on top of `highjohn-phase1a-confirmed.zip`, which was inspected first (see the Phase 1B inspection report in chat) and confirmed structurally clean before anything here started.

## What's new

- **`/services`** — routing/overview page. Loops over the same `_data/services.yml` that powers the homepage grid. Every card's CTA currently goes to booking (`?service=` pre-filled) since no child pages exist yet — **zero dead links**.
- **`/about`** — the homepage's full founder/story content, moved here in full, plus a new intro section (AI Architect / AI Systems Consultant positioning) and a closing section reinforcing business-first / systems-thinking / security-conscious framing, using language already established and approved — nothing new fabricated.
- **`/work`** — the proof layer. 4 items, each with a distinct, color-coded badge: SB Trust & Legal Consultants and Kouncil Place as **Client Work** (lime), the AI Front Desk as **Demo** (gray), the GoHighLevel MCP Server as **Experiment / Open Source** (gold). No stats, no testimonials, no invented case studies.

## Bug fix

`var(--white)` → `var(--paper)` in both `contact.html` and `index.html` — `--white` was never a defined CSS variable, so that line's color declaration was silently dropped by the browser. Fixed in both places, same undefined-variable bug, same fix.

## Data model change

`_data/services.yml` — every service now carries a `slug` (the future page URL segment) and `page_live: false`. `/services` checks this flag per service: `false` → booking CTA (current state, all 8), `true` → real link to `/services/{slug}/`. When Phase 1C ships a child page, flipping that one flag to `true` is the only change needed — the template doesn't need touching.

## Navigation

- Services: `#standalone` anchor → real `/services/` page
- About: `#about` anchor → real `/about/` page
- **New:** Work → `/work/`
- Unchanged: Home, Contact, Shop, Start, and the booking CTA — all still exactly where Phase 1A left them

## Homepage — conservative, as agreed

**Nothing was removed.** The full 8-service grid and the full story/bio section are both still on the homepage, byte-for-byte identical to Phase 1A. Two small teaser links were added — "View all services →" above the grid, "Read the full story →" above the bio — pointing to the new pages. That's the entire homepage diff, confirmed by direct line-by-line comparison against the Phase 1A baseline (7 lines changed total, including the bug fix).

This is intentionally temporary — per your note, once Phase 1C ships the first service pages, the next round should start actually shortening the homepage instead of leaving the full sections duplicated.

## Verification method (same limitation as Phase 1A)

No Jekyll installed in this environment, so no live build/screenshot. Same approach as before: manually resolved every `{% include %}`, `{% for %}`, and `{% if %}` the way Liquid would, and confirmed:
- All 8 `/services` cards render with correct booking links (verified each one individually — see chat)
- All 3 new pages resolve with zero leftover template syntax
- `index.html` diffed line-by-line against the Phase 1A baseline — only the 4 intended changes appear, nothing else moved
- `nav.html`, `contact.html`, `services.yml` diffed the same way — each shows exactly the intended edit and nothing else

**Please still verify on an actual GitHub Pages branch preview or local Jekyll build before merging** — this simulation is solid but isn't a substitute for the real thing.

## Explicitly not done (per instructions)

- Homepage has **not** been shortened yet — that starts after Phase 1C
- No `/services/*` child pages — that's Phase 1C
- No AI concierge — still just the reserved mount-point comment in `_layouts/default.html`
