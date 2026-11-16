---
type: concept
description: "One light direction for all shadows, highlights and 3D-rendered icons: light from above, shadows fall down, never mixed"
domain: iconography-and-visual-detail
aliases: [solid drawing, solid drawing in 3d, light direction, shadow direction, key light, 3D icons, depth consistency]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://m2.material.io/design/environment/light-shadows.html
---
# Consistent light source

**Rule:** The whole UI shares one virtual light. Material-style UIs use a key light from above plus ambient fill, so shadows fall **down** (y offset only), highlights sit on top edges, and pressed or inset elements have their shadow inside the top edge. 3D-rendered icons and items use the same camera angle and light rig.

**Why:** Depth is read from consistent light ("solid drawing" in animation terms). Mixed directions look collaged.

**Values:**
- Material: two lights, a **key** (sharp, directional) and **ambient** (soft, diffuse). Web shadows vary the **y axis only**. *(Material Design light and shadows)*
- Shadow layering: a tight, darker contact shadow plus a large, soft ambient one reads more physical than one blur. Blur and offset grow with elevation.
- Top-edge highlight for raised controls: **unverified**, `inset 0 1px 0 oklch(1 0 0 / .1–.2)`.

**Failure looks like:** Cards shadowed to the bottom-right next to buttons shadowed straight down. 3D items lit from the left beside icons lit from the right. Bottom-edge highlights.

**Detect in review:** List every `box-shadow`/`drop-shadow` token and check that the x offsets are 0 (or consistent) and the y offsets are positive and grow with elevation. For 3D icon sets, compare the highlight and shadow positions across a grid of icons.

**Implementation:**
- Web: elevation tokens `--shadow-1: 0 1px 2px oklch(0 0 0/.12), 0 1px 3px oklch(0 0 0/.08)` growing per level. In dark mode, rely on lightness instead ([[dark-mode-depth]]).
- iOS/Android: system materials and `elevation` handle the direction. Don't hand-roll offsets per component.
- Game UI: render item and icon sprites from one scene preset (fixed camera angle, key light upper-left or top, the same rim light). Store it as a reusable prefab or rig.

**Related:** [[dark-mode-depth]] · [[matched-icon-weight]] · [[squash-and-stretch]]
