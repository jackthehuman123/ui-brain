---
type: concept
description: "Multiply white-background shots into a tinted plate; the plate (not the theme) must be light; isolate the layer"
domain: color
aliases: [mix-blend-mode multiply, blend modes, background-blend-mode, product image on gray]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/mix-blend-mode
  - https://developer.mozilla.org/en-US/docs/Web/CSS/isolation
---
# Multiply blending

**Rule:** To place white-background images (product shots, scans, logos) on a tinted card, use `multiply`. White becomes the surface color and the darks stay. The condition is the **immediate surface under the image**, not the app theme: a light plate keeps multiply on even in dark mode. Isolate the blend to the card.

**Why:** White boxes inside gray or beige cards look like unprocessed assets and break grid rhythm. Multiply removes them without re-exporting the images.

**Values:**
- `multiply`: result = image × backdrop. White (1) leaves the backdrop unchanged; black stays black. *(MDN)*
- Works only when the image background is pure or near-pure white **and** the plate behind it is light. Over a dark plate, multiply makes the whole image muddy.
- Tinted surface for product grids: a light, low-chroma tone (e.g. `oklch(.96 .01 H)`).

**Failure looks like:** Product images in white rectangles on gray cards. Multiply switched off for the dark *theme* while the plate stays light, which brings the white boxes back (component test #3). Multiplied images over a dark plate. A blend that leaks onto siblings.

**Detect in review:** Look for visible white boxes around product photos on non-white surfaces. In code: blend mode toggled by theme instead of by plate lightness; no `isolation: isolate` on the card.

**Implementation:**
- Web: `.media{background:var(--plate);isolation:isolate} .media img{mix-blend-mode:multiply}`. In dark theme keep `--plate` light (e.g. `oklch(.93 .01 70)`); switch to `normal` only if the plate itself goes dark.
- iOS: `.blendMode(.multiply)` on the image within a `.compositingGroup()`.
- Android: `Modifier.graphicsLayer { compositingStrategy = Offscreen }` plus a `BlendMode.Multiply` draw.
- Game UI: Roblox GUI has no blend modes, so bake the background into the asset. Unity UI needs a custom shader.

**Related:** [[oklch-gradients]] · [[dark-mode-depth]]
