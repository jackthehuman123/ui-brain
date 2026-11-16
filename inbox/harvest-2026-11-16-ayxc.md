---
type: inbox
source: ~/Documents/github/ui-test/ayxc/REVIEW.md
---
# Harvest: ayxc homepage (2026-11-16)

Proposals only. Notes are unchanged until the owner approves.

## Rule changes
- **screens/homepage** → Detect: a flat token contrast check is not enough for text over imagery (eyebrow measured 6.80:1 against the bg token but **4.23:1** at its worst rendered pixel). Method: rasterize the hero art + scrim to a canvas and sample every pixel under each text line box (`ui-test/tools/ayxc-test.html`).
- **tracking** → add a resolution for **large all-caps display text**, where the caps rule (+0.05–0.12em) and the display rule (tighten) conflict. Research needed before writing a value.
- **oklch** → second confirmation of the gamut-clamp rule: dark orange at L .52 C .16 is out of sRGB (max ≈ .148).

## Layer structure: confirmed
The project-type → screen → component path produced a complete page plan. Concept notes were opened only for values. Keep the layering rule: screens and components restate rules in one line and link down.

## New candidates
- components: `product-card`, `navigation-bar`, `mobile-drawer`, `segmented-control`
- concepts: `font-loading` (CLS from web fonts: `size-adjust`/fallback metrics, `font-display`), `easing`, `animation-duration`
- `review-tooling` (already a candidate): add the about:blank readiness trap, the `fonts.ready` hang under virtual time, and smooth-scroll vs scripted screenshots
