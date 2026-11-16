---
type: concept
description: "Make frequent targets bigger and closer; extend hit areas beyond visuals; use screen edges and corners on desktop"
domain: interaction-and-state
aliases: [Fitts's law, Fitts law, bigger hit areas, hit area, hitbox, target acquisition, thumb zone]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://lawsofux.com/fittss-law/
  - https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
---
# Fitts's law

**Rule:** The time to hit a target grows with distance and shrinks with size. Make frequent and important targets large and close to where the pointer or thumb already is, extend **hit areas** beyond the visible shape, and space adjacent targets apart.

**Why:** Small, distant targets cost time and cause mis-taps, worst on touch, for motor-impaired users and in motion (walking, gaming).

**Values:**
- `MT = a + b · log₂(D/W + 1)` (Shannon formulation): doubling the width or halving the distance gives the same gain. *(Fitts 1954; MacKenzie)*
- Minimum sizes: [[touch-target]] and `platforms/`.
- Desktop screen edges and corners act as infinitely deep targets because the cursor stops there (macOS menu bar, Windows Start).
- Hit area > visual: a 24px icon can sit in a 44–48px hit box.

**Failure looks like:** Tiny "×" close buttons in corners on mobile. Primary actions at the top of tall phone screens. Destructive and confirm buttons touching. Game ability buttons smaller than the thumb that uses them. Links with only the text as the target in dense lists.

**Detect in review:** Overlay the hit areas (e.g. outline every `button, a`) and compare with the visual size. Measure the distance from the thumb's resting zone to the primary action on a 390px phone. Check the spacing between adjacent destructive and safe actions.

**Implementation:**
- Web: padding or `::after{content:"";position:absolute;inset:-10px}` to enlarge hit areas without changing visuals.
- iOS: `.contentShape(Rectangle())` with a padded frame.
- Android: `Modifier.minimumInteractiveComponentSize()` (on by default for M3 components).
- Roblox: put a transparent `TextButton` over small icons; size mobile action buttons with Scale.
- Unity: enlarge the `Image` raycast area with transparent padding, or use `raycastPadding`.

**Related:** [[touch-target]] · [[frequency-of-use]] · [[hicks-law]]
