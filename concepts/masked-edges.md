---
type: concept
description: "Fade scrollable content out at clipped edges with a gradient mask (not an overlay) so overflow reads as more content"
domain: iconography-and-visual-detail
aliases: [fade edges, scroll fade, edge mask, mask-image, overflow hint, scroll shadow]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/mask-image
---
# Masked edges

**Rule:** Where content scrolls or overflows (carousels, tab bars, chip rows, long lists in cards), fade it to transparent at the clipped edge with a **mask**, not a color overlay. Show the fade only on edges that actually have more content.

**Why:** A hard cut looks like a bug or an end. A gradient *overlay* only works on one known background color and breaks on images, tints and dark mode. A mask fades the content itself, so it works on any surface.

**Values:**
- `mask-image` is Baseline across browsers since **Dec 2023** (unprefixed: Chrome/Edge 120, Firefox 53, Safari 15.4). Keep `-webkit-mask-image` for older Safari. *(MDN)*
- Fade length: **unverified**, ~16–48px, or about one item's partial width, so a cut item reads as "more".
- Hide the fade at the scroll start and end (toggle via scroll position or scroll-driven animation).

**Failure looks like:** Chip rows that end in a half-cut chip with no fade. A white gradient overlay showing as a white smear on dark mode or photo backgrounds. A permanent fade at the start of a list the user hasn't scrolled. Fades covering tappable content with no padding to scroll it clear.

**Detect in review:** Horizontal scrollers and clipped containers: is there a cue that more content exists? In code: `linear-gradient(to right, #fff, transparent)` overlays (color-dependent); fades not toggled at the scroll ends.

**Implementation:**
- Web: `.scroller{mask-image:linear-gradient(to right,transparent,#000 24px,#000 calc(100% - 24px),transparent)}`. Toggle the start and end stops with classes from `scroll` events, or `animation-timeline: scroll()`.
- iOS: a `.mask` with a `LinearGradient` on the ScrollView's content.
- Android: `Modifier.graphicsLayer{compositingStrategy=Offscreen}.drawWithContent{ drawContent(); drawRect(brush, blendMode=BlendMode.DstIn) }`.
- Roblox: a `CanvasGroup` with a `UIGradient` (transparency sequence) to fade its children (**unverified** across all devices; test performance). Unity: `RectMask2D` with softness.

**Related:** [[progressive-disclosure]] · [[alpha-borders]] · [[multiply-blending]]
