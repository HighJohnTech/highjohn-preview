# Phase 1C — First Four Service Pages

Built on top of Phase 1B (`highjohn-phase1b.zip`), which was diffed against and confirmed untouched — `index.html`, `nav.html`, `about.html`, and `contact.html` are all byte-for-byte identical to Phase 1B. Nothing regressed.

Note on this being greenlit: your Zortez message referred to "the currently approved Phase 1C service-page build" and listed completing Phase 1C as the immediate next step — I've taken that as approval to proceed. Flagging it since there wasn't a standalone "Phase 1C: approved" line the way earlier phases had one.

## New pages (4)

- `services-ai-agents-front-desk.html` → `/services/ai-agents-front-desk/`
- `services-automation-crm.html` → `/services/automation-crm/`
- `services-web-design-development.html` → `/services/web-design-development/`
- `services-custom-apps-software.html` → `/services/custom-apps-software/`

Each has its own URL, title, meta description, problem framing, capability breakdown, a "how it's built" section (explicitly stating we extend GoHighLevel/existing systems rather than defaulting to n8n/Make), an FAQ, and its own Systems Audit CTA. None of them borrow homepage anchor links — these are real, independent pages, per the requirement.

Filename note: kept the same flat-file-at-root convention every other page in this project uses (`systems-audit.html`, `terms-and-conditions.html`, etc.) rather than introducing a nested `/services/` directory — the `permalink` front matter gives each the correct final URL either way, and this stays consistent with everything already built.

## Changed files (2)

- **`_data/services.yml`** — `page_live` flipped to `true` for exactly these 4 services, `false` still on the other 4. This is the only change needed for `/services` to start linking to real pages instead of booking — verified individually below, no template edits required.
- **`work.html`** — the AI Front Desk demo entry now cross-links to its new dedicated service page.

## Zortez architecture note

Per your message, I updated the reserved mount-point comment in `_layouts/default.html` with the actual planned file structure (`_includes/zortez-assistant.html`, `_data/zortez.yml`, `assets/css/zortez.css`, `assets/js/zortez.js`, `assets/media/zortez/`) and the real z-index values Zortez will need to sit above (confirmed: nav is `100`, the film-grain overlay is `200` — so Zortez needs `300+`). Nothing else Zortez-related was touched — no widget, no third-party chatbot, no character work.

## Verification results

- All 14 pages now in the site (10 from before + 4 new) checked for front matter, and every permalink resolves to the right URL.
- Liquid syntax balanced across every file, zero unresolved `{% %}` or `{{ }}` tags.
- Zero raw booking URLs outside the shared `cta-book` include.
- Every include reference resolves to a real file.
- **Routing verified individually for all 8 services**: the 4 now-live ones (`web-design-development`, `custom-apps-software`, `ai-agents-front-desk`, `automation-crm`) correctly resolve to their real page URLs; the other 4 (`ai-consulting`, `cybersecurity`, `marketing-revenue-systems`, `technology-partnership`) still correctly fall through to booking with the right `?service=` param. Zero dead links.
- `index.html`, `nav.html`, `about.html`, `contact.html` diffed directly against the Phase 1B zip — all four are byte-for-byte identical. Nothing outside the intended scope moved.

Same caveat as every prior phase: no Jekyll available in this environment, so this is manual Liquid-simulation + diff verification, not a live render. Please check on a GitHub Pages branch preview or local build before merging.

## What's next

Per your execution order: after this is reviewed, the remaining four service pages (`ai-consulting`, `cybersecurity`, `marketing-revenue-systems`, `technology-partnership`) are Phase 1D. The Zortez implementation plan (component architecture, UX flow, mocks, animation approach, accessibility, analytics) comes after that, once you say to start it — not built or coded yet, per your explicit instruction.
