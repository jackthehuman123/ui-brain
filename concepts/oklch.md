---
type: concept
domain: color
aliases: [OKLCH, oklch(), Oklab, perceptual color space]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/oklch
  - https://developer.mozilla.org/en-US/docs/Web/CSS/color-interpolation-method
  - https://www.w3.org/TR/css-color-4/
  - https://bottosson.github.io/posts/oklab/
  - https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl
  - https://developer.android.com/reference/kotlin/androidx/compose/ui/graphics/colorspace/package-summary
---
# OKLCH

**Rule:** Author UI colors in OKLCH. Derive states and scales by changing **L** while keeping **H** fixed. Ship an sRGB-safe **C** by default and raise C only in a P3 override. Still measure contrast on every text/background pair, because equal L is not equal contrast.

**Why:** OKLCH is perceptually uniform: equal ΔL looks like an equal change in lightness across hues, and changing L doesn't move the hue. HSL "50%" yellow and blue look nothing alike, so HSL-built scales and hover states come out uneven.

**Values:**
- `oklch(L C H)`: L 0–1 (or %). C ≥ 0, unbounded in theory but < 0.5 in practice *(MDN)*. Usable UI chroma is **< 0.37** for both sRGB and P3 *(Evil Martians)*. The maximum in-gamut C depends on L and H.
- Support: Baseline widely available since May 2023 (Chrome/Edge 111, Safari 15.4, Firefox 113). *(MDN)* No polyfill needed.
- Hover/active states: `calc(l ± 0.1)` via relative color syntax. Write `0.1`, not `10%`, because `%` doesn't work in that `calc()`. *(Evil Martians)*
- Contrast: backgrounds with L ≥ 0.87 have good contrast with black text, but a 0.2 L gap can still fail, and "Just OKLCH is not enough", so check with WCAG or APCA. *(Evil Martians)*
- Gradients and `color-mix()` default to **Oklab** interpolation. `in oklch` defaults to `shorter hue`. *(MDN)* See [[oklch-gradients]].

**Failure looks like:** `yellow-500` looks far lighter than `blue-500` in the same scale. `lighten()` hovers drift in hue or barely change. P3-only chroma clipped on sRGB screens; Chrome and Safari clip instead of reducing chroma, which **shifts the hue**. Same-L text/background pairs shipped without measuring contrast.

**Detect in review:**
- Code: `lighten()`/`darken()`/HSL math in the token pipeline. Hand-picked hex scales. High-C `oklch()` outside `@media (color-gamut: p3)`. No contrast check in the token build. Run `stylelint-gamut` to flag out-of-gamut values.
- Screenshot: desaturate it. The same step across hues should read as the same gray.

**Implementation:**
- Web:
  ```css
  --accent: oklch(0.62 0.17 255);                       /* sRGB-safe */
  @media (color-gamut: p3) { --accent: oklch(0.62 0.21 255); } /* same L,H; more C */
  --accent-hover: oklch(from var(--accent) calc(l + 0.1) c h);
  ```
  Theme by swapping custom-property values under `prefers-color-scheme`, not by adding media queries to each component.
- iOS: there's no OKLCH initializer. Convert at build time to `Color(.displayP3, …)` or asset-catalog colors.
- Android (Compose): `ColorSpaces.Oklab` exists for `convert()`, but rendering is RGB. Generate sRGB/P3 tokens from the OKLCH source.
- Roblox / Unity: `Color3` and `Color` are RGB only. Keep OKLCH as the source in the token file and export RGB.

**Related:** [[oklch-palettes]] · [[oklch-gradients]] · [[dark-mode-depth]] · [[alpha-borders]] · [[multiply-blending]] · [[contrast-ratio]]
