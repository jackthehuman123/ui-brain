---
type: concept
description: "Author colors in OKLCH: step L at fixed H, sRGB-safe C plus a P3 override, re-clamp C after every L shift"
domain: color
aliases: [OKLCH, oklch(), Oklab, perceptual color space, relative color]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/oklch
  - https://www.w3.org/TR/css-color-4/
  - https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl
---
# OKLCH

**Rule:** Author UI colors in OKLCH. Derive states by changing **L** at a fixed **H**, ship an sRGB-safe **C** with a P3 override that raises only C, and **re-clamp C whenever L changes**. L is not contrast; measure every pair ([[contrast-ratio]]).

**Why:** Equal ΔL looks like an equal change in lightness across hues, and L shifts don't move the hue. HSL "50%" yellow and blue look nothing alike.

**Values:**
- `oklch(L C H)`: L 0–1, C ≥ 0 (in practice < 0.37 for sRGB and P3), H in degrees. Baseline since May 2023. *(MDN, Evil Martians)*
- Max in-gamut C shrinks toward L 0 and 1, and differs per hue. Examples: H 265 at L .80 ≈ 0.10; H 45 at L .78 ≈ 0.136 *(computed, Oklab matrices)*.
- State shift: `calc(l ± 0.1)` (write `0.1`, not `10%`) *(Evil Martians)*, wrapped in `min(c, <max C at the new L>)`.
- Chrome and Safari **clip** out-of-gamut colors, which shifts the hue. *(Evil Martians)*

**Failure looks like:** Uneven "500" swatches across hues. Hover states that drift in hue. A dark-mode hover (L .70 + .1, C .14) silently clipped out of gamut.

**Detect in review:** HSL or `lighten()` math in tokens. High-C `oklch()` outside `@media (color-gamut: p3)`. Relative-color states with no C clamp. Desaturate a screenshot: the same step across hues should read as the same gray. Run a gamut checker (`stylelint-gamut`, or the Oklab matrices).

**Implementation:**
- Web: `--accent: oklch(.62 .17 255); @media (color-gamut:p3){--accent: oklch(.62 .21 255)}`; `--hover: oklch(from var(--accent) calc(l + .1) min(c, .1) h)`
- iOS, Android, Roblox, Unity: no OKLCH at runtime. Keep OKLCH as the token source and export Display P3 or sRGB.

**Related:** [[oklch-palettes]] · [[oklch-gradients]] · [[contrast-ratio]] · [[dark-mode-depth]]
