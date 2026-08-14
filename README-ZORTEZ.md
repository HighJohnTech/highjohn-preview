# Pre-Production Polish — Mobile Nav Fix + Zortez Scroll Cue

Both requested fixes are done, verified against a real Chromium browser via Playwright (not simulation — same approach as the Zortez browser QA round). One of the two turned out to be a bigger fix than expected once I actually tested it live; details below.

## 1. Mobile navigation — hamburger/drawer, built and debugged live

Added a proper hamburger menu: burger button, off-canvas drawer, scrim backdrop, all wired with keyboard support (Escape closes, focus moves into the drawer on open and back to the burger on close — standard accessible off-canvas-menu behavior).

**What real-browser testing caught that code review couldn't:** the drawer and scrim were both silently getting clipped to 60px tall instead of the full viewport. Root cause — `<nav>` has `backdrop-filter: blur()` for its frosted-glass look, and per the CSS spec, `backdrop-filter` (like `transform` or `filter`) creates a new **containing block** for any `position: fixed` descendant. Since the drawer and scrim were nested inside `<nav>`, their "fixed" positioning was being measured against nav's own 60px box instead of the actual browser viewport. This is a genuinely obscure CSS interaction — the kind of thing that looks completely correct in the CSS itself and only shows up once you actually measure the rendered element.

**Fix:** moved the drawer and scrim out of `<nav>`'s DOM subtree entirely — they're now siblings right after `</nav>`, not children of it. The `backdrop-filter` blur effect on the nav bar itself is completely untouched.

Verified directly, not assumed:
```
Drawer full height: True {'w': 320, 'h': 844}
Scrim full viewport: True {'w': 390, 'h': 844}
```
Before the fix, both reported `h: 60`.

**Also found and cleaned up while debugging:** two separate, independent implementations of the nav-toggle logic had ended up in the codebase — one inside `main.js`, one as a standalone `nav.js` — both wired to the same buttons. That would have double-fired every click. Kept `nav.js` (it had the more complete focus-management) and removed the duplicate from `main.js`, which is now byte-for-byte identical to the pre-this-round baseline. Also found and removed a matching duplicate CSS block (two full sets of mobile-nav rules at two different breakpoints, silently conflicting) — down to one canonical version now.

**13/13 real-browser checks pass**: burger visibility, drawer/scrim full-viewport sizing, open/close, focus management, Escape, scrim-click, all-links-visible-without-scrolling, link-click navigates, desktop unaffected (no burger, links stay inline), and resize-past-breakpoint auto-closes the drawer.

## 2. Zortez "More ways I can help" scroll cue

A subtle bottom fade appears in `.zortez-panel-body` whenever there's more content below the visible area, and disappears once you've scrolled to the bottom. Pure CSS gradient overlay (`transparent` → the panel's own background color), positioned as a sibling to the scrollable body so it can't itself be scrolled away, `pointer-events: none` so it never blocks clicks on what's underneath.

Driven by one small JS function comparing `scrollHeight`/`scrollTop`/`clientHeight`, called on panel open, on scroll, on window resize, and when "More ways I can help" is toggled (since expanding it changes whether there's overflow at all).

## Verification

- **26/26 Zortez jsdom tests** still pass — untouched by either fix, re-confirmed.
- **7/7 cooldown tests** still pass.
- **All 4 JS files** (`main.js`, `nav.js`, `zortez.js`, `leak-calculator.js`) syntax-checked clean.
- **Confirmed Zortez and the nav fix coexist correctly** on the same live page — Zortez still auto-opens and plays video normally with the new nav code present.
- **Exact diff against the last delivered package**: 7 files changed — `nav.html`, `zortez-assistant.html` (1 line — the scroll-cue element), `default.html` (1 line — the nav.js script tag), `main.css`, `zortez.css` (7 lines — scroll-cue rules), the new `nav.js`, and `zortez.js` (scroll-cue logic only). `main.js` confirmed identical to baseline after removing the duplicate.

## What still needs your eyes

Everything above is objectively measured or directly observed in a real browser — but "does the drawer feel good sliding in," "is the scroll fade actually subtle enough," and the original open items (orbit feel, timing) are still genuinely yours to judge on a real device, exactly as planned.

Not starting Phase 1D. Ready for the real GitHub Pages / device preview you mentioned before this goes anywhere near `main`.
