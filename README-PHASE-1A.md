# Phase 1A — Jekyll Migration + Foundation Pages

**I do not have push access to your GitHub repo.** Everything below was built and verified locally. You (or a tool with repo access) need to actually commit it. Exact steps are below.

## What this is

The full Phase 1A build per your approved sequence:
1. Jekyll shared architecture (layouts, includes, data files)
2. Homepage converted onto it — **zero content changes except the ones you explicitly approved**
3. Privacy Policy converted onto it (this also fixes the phone/email mismatch between it and the homepage)
4. `/systems-audit`, `/contact`, `/shop`, `/start`, `/terms-and-conditions` — all new

## What changed on the homepage, and why

Every change traces to something you explicitly approved:

- **"Discovery Call" → "Systems Audit"**, **"Full AI Audit" → "AI Systems Blueprint"** — wherever those names appeared (pricing ladder, flagship grid, leak calculator note)
- **24-hour delivery promise removed.** Systems Audit now says findings arrive within 3–5 business days (in both the FAQ and the pricing-ladder tier card). The AI Systems Blueprint uses scope-dependent language and keeps the ~2-week figure, now explicitly attached to *that* offer only — the FAQ no longer conflates the two.
- **Every raw booking link** (12 of them across nav, hero, the leak calculator, all five pricing tiers, and the final CTA) now routes through one shared `cta-book` include with a `?service=` param, instead of being hand-typed 12 times. Change the URL once in `_data/company.yml` if it ever changes.
- **Credential/security language rewritten**: removed "completely secure," "multiple enterprise clients," "overseeing entire business operations," "High-ticket enterprise CRM operator," and the completed-tense "I'm proficient in... vulnerability assessments" line. Replaced with your preferred "CRM & Automation Systems Architect" positioning and the "security considered from the architecture stage" framing. A `NEEDS VALIDATION` HTML comment sits right next to the ethical-hacking claim in the source — visible to you/devs, not to visitors — flagging that it needs your sign-off before anything stronger goes back up.
- **Nav "Services" and "About"** still point at their homepage anchors (`#standalone`, `#about`) — those become real `/services` and `/about` pages in Phase 1B, not this one. **Nav "Contact"** now points at the new `/contact` page. The homepage's own contact section is left in place, untouched, for now — Phase 1B is when the homepage actually gets shorter, per your build sequence.

**What did NOT change:** the leak calculator math, the missed-call industries grid, the 5-stage Method section, the System layers section, the Difference section, the Resources teaser, and the previously-approved nav fix + 8 standalone-service CTAs from earlier sessions. I diffed the rendered output against the currently-live file line-by-line to confirm this — see Verification below.

## Contact info — NOT resolved, only centralized

Contact information is now confirmed and centralized in `_data/company.yml`: **(313) 546-0591** and **info@highjohn.tech**. The business location is listed as **Belleville, MI — serving clients worldwide**, with an explicit note that High John Tech has **no public physical location** and provides services remotely and by appointment. The JSON-LD uses `areaServed` rather than a postal address so the site does not imply a walk-in office.

## New pages — what's real vs. placeholder

- **`/systems-audit`** — real content, sourced from the already-published pricing/FAQ copy, now consistent.
- **`/contact`** — moved from the homepage section, same info, routes by intent (problem / diagnosis / ready-to-build) into the right next step.
- **`/shop`** — only currently *published* Gumroad products are listed (Scorecard, Zillow Blueprint, Superconductive Soul have real links from what's on file; Tokenomics 101 and Teacher Productivity Hub link to your general Gumroad storefront since I don't have their exact product URLs — don't have those, didn't guess them). Superconductive Soul is grouped under "Founder Mastery," separate from the B2B products, per your brand-separation rule.
- **`/start`** — only 4 destinations, all real: Systems Audit, Services, Shop, Contact. I left out "View Work/Demos" and freelance-platform links since `/work` doesn't exist yet (Phase 1B) and I don't have confirmed Upwork/Fiverr URLs — didn't fabricate either.
- **`/terms-and-conditions`** — a structural skeleton only, exactly as instructed. It has a visible "NEEDS LEGAL REVIEW" banner and bracketed placeholders anywhere a real legal decision is needed (governing law, liability cap, IP transfer default, digital-product refund window). This closes the dead link that was on `/privacy-policy` before, but it is **not ready to be someone's actual terms of service** — don't treat it as such until it's actually reviewed.

## Verification (since I can't run a live Jekyll build here)

This environment doesn't have Jekyll installed, so I couldn't do `jekyll serve` and screenshot it. Instead I wrote a script that manually resolves every `{% include %}` and `{% for %}` tag the way Jekyll's Liquid engine would, reconstructed the full rendered homepage, and diffed it line-by-line against the current live `index.html`. Result: every single changed line traces to something in the list above — nothing else moved. I also confirmed the Method, System, Difference, Industries, and Resources sections are **byte-for-byte identical** to what's live now.

That said, this is a simulation, not a real Jekyll build. **Please still verify on GitHub Pages' own branch preview (or `bundle exec jekyll serve` locally) before merging to `main`** — that's still the real test.

## How to apply this

```bash
# from your local clone of HighJohnTech/highjohn-site
git checkout -b phase-1a-jekyll-migration

# remove the old flat index.html/privacy-policy.html and replace with everything in this folder
# (copy the entire contents of this delivered folder into your repo root, overwriting index.html
#  and privacy-policy.html, adding everything else as new files/folders)

git add -A
git commit -m "Phase 1A: Jekyll architecture, offer renaming, /systems-audit /contact /shop /start /terms-and-conditions"
git push -u origin phase-1a-jekyll-migration
```

Then either:
- Open a PR and let GitHub Pages build a preview (if your repo/plan supports branch previews), or
- Temporarily point Pages at this branch in repo Settings → Pages to preview at a real URL, or
- Run `bundle exec jekyll serve` locally if you have Ruby/Jekyll installed

Check: nav on every page, the booking widget still opens correctly with the right pre-filled service, `/systems-audit`, `/contact`, `/shop`, `/start`, `/terms-and-conditions` all load, and the Privacy Policy's "Back to High John Tech" flow still works. Once you're satisfied, merge to `main`.

## Explicitly not done (as instructed)

- No AI assistant. `_layouts/default.html` has a labeled reserved mount-point comment and a z-index note for when you're ready to add it.
- No `/services`, `/about`, `/work` pages — Phase 1B.
- No individual `/services/*` child pages — Phase 1C/1D.
