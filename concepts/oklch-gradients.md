---
type: concept
description: "Interpolate gradients in oklab (CSS default) to avoid gray mid-points; use oklch only for deliberate hue sweeps"
domain: color
aliases: [gradient interpolation, color-interpolation-method, in oklch, in oklab, gradient banding]
platforms: [web, all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/color-interpolation-method
  - https://developer.mozilla.org/en-US/docs/Web/CSS/hue-interpolation-method
  - https://www.w3.org/TR/css-color-4/
---
# OKLCH gradients

**Rule:** Interpolate gradients in **Oklab** (the CSS default for non-legacy colors) so mid-points don't go gray or muddy. Use `in oklch` only for intentional hue sweeps, and pick the hue arc explicitly. Fade to transparent with the same color at zero alpha.

**Why:** sRGB interpolation between complementary colors passes through desaturated gray. Oklab keeps lightness perceptually even. OKLCH rotates hue, which is vivid but can detour through unexpected hues.

**Values:**
- Default interpolation space for gradients and `color-mix()`: **Oklab**. `in oklch` defaults to `shorter hue`; alternatives are `longer`, `increasing` and `decreasing`. *(MDN)*
- Achromatic stops (white, black, gray) have no meaningful hue. In `oklch` the other stop's hue is used, so check white↔color gradients visually.
- Fades: `linear-gradient(oklch(.7 .18 45), oklch(.7 .18 45 / 0))` keeps the hue to the end.

**Failure looks like:** Blue→yellow passing through gray. A brand gradient that sweeps through green because the hue took the long arc. A scrim fading to `transparent` that turns gray on old engines. Visible bands in large dark gradients.

**Detect in review:** Gradients written with hex/rgb stops and no interpolation method on complementary colors. `in oklch` without a hue method. Large, low-contrast dark gradients with visible steps; add subtle noise **(unverified fix; test on 8-bit displays)**.

**Implementation:**
- Web: `linear-gradient(in oklab, …)` (explicit for clarity) or `linear-gradient(in oklch longer hue, …)` for rainbows.
- Native and game engines interpolate in sRGB. Pre-bake 3+ intermediate stops computed in Oklab, or ship the gradient as an image.

**Related:** [[oklch]] · [[oklch-palettes]] · [[multiply-blending]]
