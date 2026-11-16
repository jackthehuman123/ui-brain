---
type: concept
description: "Keep font kerning on everywhere; hand-kern only display text ≥ ~32px; never fix pair gaps with letter-spacing"
domain: typography
aliases: [kern, pair kerning, font-kerning, optical kerning]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/font-kerning
---
# Kerning

**Rule:** Leave the font's built-in kerning on. Hand-kern only large display text (logos, hero headlines) where specific pairs gap. Never use `letter-spacing` to fix a pair: that changes every gap.

**Why:** Kerning tables correct pair-specific gaps (AV, To, LT, r.). Turning them off makes text look unevenly spaced; tracking can't fix one pair without breaking the others.

**Values:**
- CSS `font-kerning: auto` is the default, and browsers may disable kerning on small text. *(MDN)* Use `normal` to force it on where it matters.
- Hand-kerning threshold: **unverified**, ~32px and up, where pair gaps become visible at reading distance.
- Problem pairs to check in display text: `AV AW AY LT LY TA To Te Ty Va Wa Yo r. r, f'`.

**Failure looks like:** A hero headline where "To" or "AV" gaps visibly. Wordmarks with uneven rhythm. Kerning disabled globally by a reset (`font-kerning: none`, `font-feature-settings: "kern" 0`).

**Detect in review:** Squint at display text and look for gaps between pairs wider than others. In code: `font-kerning: none`, `"kern" 0`, `text-rendering: optimizeSpeed` on headings, or per-letter `<span>`s with letter-spacing. Logos made of live text instead of an outlined SVG.

**Implementation:**
- Web: `h1 { font-kerning: normal; }`. Outline logos as SVG.
- iOS: system fonts kern automatically. `.kerning(_:)` adjusts it in points; use it only for display pairs.
- Android: kerning is on by default in Compose `Text`.
- Unity TMP: keep kerning enabled in the text component's font features (the menu location differs by TMP version).
- Roblox: no kerning control. Use image labels for wordmarks.

**Related:** [[tracking]] · [[optical-center]]
