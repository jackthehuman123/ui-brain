---
type: concept
description: "Icon stroke weight and size match the adjacent text's weight and cap height; one icon family and stroke per UI"
domain: iconography-and-visual-detail
aliases: [icon weight, stroke weight, icon size, SF Symbols weight, Material Symbols weight, icon consistency]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/sf-symbols
  - https://developer.apple.com/design/human-interface-guidelines/icons
  - https://developers.google.com/fonts/docs/material_symbols
---
# Matched icon weight

**Rule:** An icon next to text matches that text's stroke weight and sits on its cap height. Use one icon family and one stroke weight per context, and step the icon weight up or down with the label's weight.

**Why:** Icons are read as part of the line of type; a mismatched stroke dominates or looks broken.

**Values:**
- SF Symbols: **9 weights** matching SF font weights and **3 scales** relative to cap height; scales keep the weight match. *(Apple HIG)*
- Material Symbols axes: weight **100–700**, grade **−25–200**, optical size **20–48**, fill 0–1. Match grade to text, and use a low grade (−25) for light icons on dark backgrounds to reduce glare. *(Google Fonts guide)*
- Outline icon sets (Lucide, Heroicons) ship ~1.5–2px at 24px: scale the stroke with the icon, or switch sizes deliberately. **unverified** mapping: 1.5px ↔ regular 14–16px text, 2px ↔ medium/semibold.

**Failure looks like:** Mixed icon sets (rounded Material next to sharp Feather). Thick nav icons with thin labels. Icons sitting 2px below the text baseline. Filled and outline icons mixed without meaning (fill should mean the selected state).

**Detect in review:** Zoom to 400% and compare the icon stroke with the letter stems of its label. Check that every icon comes from one family. In code: several icon libraries imported; hardcoded `stroke-width` per icon; icons sized in px unrelated to the font-size.

**Implementation:**
- Web: `svg{width:1.25em;height:1.25em;stroke-width:1.75}` (scales with font-size). Material Symbols: `font-variation-settings:'wght' 400,'GRAD' 0,'opsz' 24`.
- iOS: `Image(systemName:)` inherits `.font()` weight; use `.imageScale()` for emphasis.
- Android: Material Symbols with matching `wght`; `Icon` size 24dp default.
- Game UI: render all icons from one source style at one stroke; export per size class rather than scaling one PNG everywhere.

**Related:** [[optical-center]] · [[blurred-icon-swaps]] · [[consistent-light-source]]
