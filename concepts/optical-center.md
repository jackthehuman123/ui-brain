---
type: concept
description: "Center by perceived mass, not bounding box: nudge play icons right, lift text and lone shapes slightly above center"
domain: layout-and-spacing
aliases: [optical alignment, visual center, optical balance, play icon offset, cap-height centering]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/text-box-trim
---
# Optical center

**Rule:** Align by perceived mass, not bounding boxes. Shift asymmetric glyphs (play triangles, arrows, chevrons) toward their light side, center text on its cap height rather than its line box, and place a lone element slightly above the geometric center of its container.

**Why:** The eye judges position by visual weight. A triangle's mass sits near its base; text boxes include empty ascender and descender space. Mathematically centered items look off.

**Values:**
- Right-pointing triangle: its centroid sits 1/3 of the width from the base, so shift it right by about **w/6** to center its mass *(geometry)*.
- Lone content in a frame (empty states, splash logos): **unverified**, raise it by about 3–5% of the container height.
- Button text: trim the line box to cap height and alphabetic baseline, then center *(MDN `text-box-trim`)*.

**Failure looks like:** A play button that looks pushed left inside its circle. Button labels that look low (extra descender space below). Icons next to text that sit visibly high or low. Splash logos that look like they're sliding down.

**Detect in review:** Zoom a screenshot to 400% and compare visible gaps on each side of the glyph, not box edges. In code: icon buttons centered with flex and no offset for directional glyphs; text in fixed-height buttons with asymmetric padding hacks.

**Implementation:**
- Web: `.play svg{translate:8% 0}`; `.btn{text-box: trim-both cap alphabetic}` where supported, else tune the padding per font.
- iOS: SF Symbols are optically centered; custom glyphs need `.offset(x:)`. Use `.alignmentGuide` with `firstTextBaseline` for icon+text.
- Android: Material icons are optically centered; offset custom vectors in the asset itself.
- Game UI: bake the offset into the sprite's pivot (Unity) or image padding (Roblox), not in layout code.

**Related:** [[kerning]] · [[matched-icon-weight]] · [[concentric-radius]]
