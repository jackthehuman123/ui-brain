---
type: concept
description: "Blend white-background product shots into tinted surfaces with multiply; only on light surfaces, isolate the layer"
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

**Rule:** To place white-background images (product shots, scans, logos) on a tinted card, use `multiply`. White becomes the surface color and the darks stay. Apply it only on light surfaces, and isolate the blend to the card.

**Why:** White boxes inside gray or beige cards look like unprocessed assets and break grid rhythm. Multiply removes them without re-exporting the images.

**Values:**
- `multiply`: result = image × backdrop. White (1) leaves the backdrop unchanged; black stays black. *(MDN)*
- Works only when the image background is pure or near-pure white **and** the surface is light. On dark surfaces, multiply makes the whole image muddy.
- Tinted surface for product grids: a light, low-chroma tone (e.g. `oklch(.96 .01 H)`).

**Failure looks like:** Product images in white rectangles on gray cards. Multiplied images that go dark and dirty in dark mode. A blend that leaks onto text or sibling elements because nothing isolates it.

**Detect in review:** Look for visible white boxes around product photos on non-white surfaces. In code: `mix-blend-mode` with no dark-mode override, and no `isolation: isolate` on the card.

**Implementation:**
- Web: `.card{background:var(--tint);isolation:isolate} .card img{mix-blend-mode:multiply}` and `@media (prefers-color-scheme:dark){.card img{mix-blend-mode:normal}}` (give the image its own light plate).
- iOS: `.blendMode(.multiply)` on the image within a `.compositingGroup()`.
- Android: `Modifier.graphicsLayer { compositingStrategy = Offscreen }` plus a `BlendMode.Multiply` draw.
- Game UI: Roblox GUI has no blend modes, so bake the background into the asset. Unity UI needs a custom shader.

**Related:** [[oklch-gradients]] · [[dark-mode-depth]]
