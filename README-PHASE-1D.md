# Phase 1D — Remaining Four Service Pages

Built on top of `highjohn-zortez-v4.zip`, the confirmed pre-production source of truth. Homepage and nav diffed and confirmed byte-for-byte identical to v4 — nothing about the site's architecture, Zortez, or navigation was touched this round.

## New pages (4)

- `services-ai-consulting.html` → `/services/ai-consulting/`
- `services-cybersecurity.html` → `/services/cybersecurity/`
- `services-marketing-revenue-systems.html` → `/services/marketing-revenue-systems/`
- `services-technology-partnership.html` → `/services/technology-partnership/`

Same structure and rules as the Phase 1C four: own URL, title, meta description, problem framing, capability grid, an honest "how it's positioned" section, FAQ, and a Systems Audit CTA. Flat-file-at-root naming, consistent with every other page in this project.

**Claim-safety held throughout** — this mattered most on the Cybersecurity page, since it's the one most likely to accidentally reintroduce something already corrected earlier in this project. Its "how it's positioned" section uses the exact language already reviewed and approved on the About page and FAQ ("security considered from the architecture stage," CCNA/Kali/Metasploit as training, HIPAA-*aware*, not HIPAA-compliant) — checked directly against the previously prohibited phrases ("completely secure," "multiple enterprise clients," "real credentials in ethical hacking," etc.) and confirmed zero hits across all 4 new pages.

**One new thing**: Marketing & Revenue Systems' FAQ cross-links to Automation & CRM Systems (`/services/automation-crm/`, already live since Phase 1C) — real internal linking between two services that naturally connect, not a placeholder.

## Changed files (1)

`_data/services.yml` — `page_live` flipped to `true` for exactly these 4 services. Diffed directly: 4 lines changed, nothing else in the file touched. This was the only change needed for `/services/` to route all 8 cards to real pages — the conditional logic from Phase 1B/1C did the rest with zero template edits, exactly as designed.

## Verification

- **All 18 pages** checked for front matter and correct, unique permalinks.
- **Liquid syntax balanced**, zero unresolved tags, across every file.
- **Zero raw booking URLs** outside the shared `cta-book` include.
- **All 8 services confirmed routing to real dedicated pages** — checked individually, not assumed:

  | Service | Routes to |
  |---|---|
  | ai-consulting | `/services/ai-consulting/` |
  | web-design-development | `/services/web-design-development/` |
  | custom-apps-software | `/services/custom-apps-software/` |
  | ai-agents-front-desk | `/services/ai-agents-front-desk/` |
  | automation-crm | `/services/automation-crm/` |
  | cybersecurity | `/services/cybersecurity/` |
  | marketing-revenue-systems | `/services/marketing-revenue-systems/` |
  | technology-partnership | `/services/technology-partnership/` |

  Zero booking-link fallbacks remain — every one of the 8 official services now has a real, independent URL.
- **Homepage confirmed untouched** — diffed directly against v4, byte-for-byte identical. Still the conservative 9-item structure from Phase 1B/1C — not reopened into a one-page site.
- **Nav confirmed untouched** — diffed directly against v4, byte-for-byte identical. No changes to the mobile hamburger/drawer fix or Zortez from this round.
- **Full package diff against v4**: `services.yml` (4-line change) plus the 4 new files — nothing else moved.

Same standing caveat as every phase: no live Jekyll build available in this environment, so this is template-simulation + diff verification, not a live render. Please check on a branch preview before merging.

## Explicitly not done (per instructions)

- No analytics — still not installed, still not started.
- No conversational/LLM Zortez — still guided-navigation only.
- No SEO work beyond what's already built into each page's own title/meta description.
- Homepage still has its two lightweight teaser links (to `/services/` and `/about/`) from Phase 1B and nothing more — full homepage shortening is still a future decision, not made here.

All 8 official High John Technology service categories now have dedicated, independent pages. Phase 1 core architecture is complete.
