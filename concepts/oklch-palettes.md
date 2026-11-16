---
type: concept
description: "Scales: L ramp at near-fixed H, C peaking mid-dark and clamped per step; pick text pairs by measured contrast"
domain: color
aliases: [color scale, palette ramp, tonal palette, 50-950 scale, color tokens]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://tailwindcss.com/docs/colors
  - https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl
  - https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
---
# OKLCH palettes

**Rule:** Build each hue's scale as a ramp in L. Let C rise toward the middle-dark steps and fall at both ends (to fit the gamut). Allow a small H drift. Assign text/background pairs by **measured** contrast, not by step number.

**Why:** The gamut narrows near white and black, so constant C either clips at the ends or dulls the middle.

**Values (Tailwind v4 blue, a shipping OKLCH palette):** *(Tailwind docs)*
| step | 50 | 100 | 300 | 500 | 700 | 900 | 950 |
|---|---|---|---|---|---|---|---|
| L | .970 | .932 | .809 | .623 | .488 | .379 | .282 |
| C | .014 | .032 | .105 | .214 | **.243** | .146 | .091 |
| H | 254.6 | 255.6 | 251.8 | 259.8 | 264.4 | 265.5 | 267.9 |

C peaks at 700, not 500, and H drifts about 13° toward violet as blue darkens.
- Backgrounds with L ≥ 0.87 pair safely with black text *(Evil Martians)*. Every other pair needs a 4.5:1 check.
- Neutrals: a low C (0.005–0.03) on the brand hue reads as tinted gray. (Tailwind gray-500 is C .027 at H 264.)

**Failure looks like:** Washed-out mid steps (constant low C), or clipped, hue-shifted extremes (constant high C). A "500" text color that passes on white for blue but fails for yellow.

**Detect in review:** Plot L and C per step; L should be monotonic and C single-peaked. Check that every step is in gamut. Confirm the contrast of each documented pair.

**Implementation:** Generate the scale in a script or tool (Harmonizer, oklch.com), store it as tokens, and export RGB/P3 for native and game engines. See [[oklch]] for gamut overrides.

**Related:** [[oklch]] · [[contrast-ratio]] · [[dark-mode-depth]]
