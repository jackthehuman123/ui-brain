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

**Rule:** Author and adjust UI colors in OKLCH. Derive states and scales by changing **L** while keeping **H** fixed and keeping **C** inside the gamut. Still check every text/background pair with a real contrast ratio, because equal L is not equal contrast.

**Why:** OKLCH is perceptually uniform. Equal changes in L look like equal changes in lightness across hues, and changing L doesn't change the hue. HSL lightness isn't uniform: yellow and blue at "50%" look nothing alike, so HSL scales and hover states come out uneven.

**Values:**
- `oklch(L C H)`: L from 0–1 (or 0–100%). C ≥ 0; it has no upper bound but in practice stays under 0.5. H in degrees. *(MDN)* Maximum in-gamut C depends on L, H and the target gamut (sRGB vs P3), so there is no single safe C.
- Support: Baseline widely available since May 2023 (Chrome/Edge 111, Safari 15.4, Firefox 113). *(MDN)*
- Gradients and `color-mix()` default to **Oklab** interpolation. `in oklch` defaults to `shorter hue`. *(MDN, CSS Color 4)* See [[oklch-gradients]].
- ΔL needed for 4.5:1 text contrast: **unverified**, roughly ≥ 0.40–0.50 ΔL as a rule of thumb. Never ship without computing WCAG contrast; see [[contrast-ratio]].

**Failure looks like:** In a scale built from hex or HSL, `yellow-500` looks much lighter than `blue-500`, so badges in the "same" step don't match. Hover states built with `lighten()` drift in hue or barely change. Colors with too much chroma get clipped on sRGB screens, which shifts the hue and causes banding. Two colors with the same L but different hues are treated as accessible without anyone measuring contrast.

**Detect in review:**
- Code: `lighten()` / `darken()` / HSL math in the token pipeline. Hand-picked hex scales with no source space. `oklch()` values with high C and no gamut check (`@media (color-gamut: p3)` or a clamp in the build step).
- Screenshot: desaturate it. The same step across hues should read as the same gray. Uneven grays mean the scale isn't perceptual.

**Implementation:**
- Web: `--accent: oklch(0.62 0.19 255);`. For states, relative color syntax: `oklch(from var(--accent) calc(l + 0.08) c h)`. Check its support separately from `oklch()`.
- iOS: there's no OKLCH initializer. Convert at build time and ship `Color(.displayP3, red:green:blue:)` or asset-catalog colors.
- Android (Compose): `ColorSpaces.Oklab` exists for `convert()`, but rendering is RGB. Generate sRGB/P3 tokens from the OKLCH source.
- Roblox / Unity: `Color3` and `Color` are RGB only. Keep OKLCH as the source of truth in the token file and export RGB.

**Related:** [[oklch-palettes]] · [[oklch-gradients]] · [[dark-mode-depth]] · [[alpha-borders]] · [[multiply-blending]] · [[contrast-ratio]]
