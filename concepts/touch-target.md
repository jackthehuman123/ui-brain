---
type: concept
description: "Hit areas ≥ platform minimum (44pt iOS, 48dp Android, 24px WCAG AA) regardless of visual size"
domain: accessibility
aliases: [touch target, tap target, hit target, target size, minimum target, 44pt, 48dp]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
  - https://developer.apple.com/design/human-interface-guidelines/accessibility
  - https://m3.material.io/foundations/designing/structure
---
# Touch target

**Rule:** Every interactive element gets a hit area at least as big as its platform's minimum, even if it *looks* smaller. Adjacent targets need spacing so the hit areas don't overlap.

**Why:** Fingers are imprecise (and more so for motor-impaired users and on the move), so small targets cause mis-taps and repeated attempts.

**Values:** constants live in [[platforms/web]], [[platforms/ios]] and [[platforms/android]]:
- iOS **44×44 pt** · Android/Material **48×48 dp** · WCAG 2.2 2.5.8 AA **24×24 CSS px** (or 24px spacing), 2.5.5 AAA **44×44**.
- Inline text links are exempt from 2.5.8, but links in dense lists aren't free from the problem.
- Game UI on phones: thumb-operated action buttons need well above the minimum (**unverified**, ≥ 60–80pt for primary actions).

**Failure looks like:** 16px icon buttons with 16px hit areas. Close "×" glyphs that need two tries. Inline chips with 4px gaps. A Roblox mobile HUD with desktop-sized buttons.

**Detect in review:** Outline the computed hit areas (`button, a, [role=button]`) at 390px and measure the smallest. In code: icon buttons without padding or a min-size; `Modifier.minimumInteractiveComponentSize` disabled; Roblox buttons sized in Offset pixels.

**Implementation:**
- Web: `.icon-btn{min-width:44px;min-height:44px;display:grid;place-items:center}`
- iOS: `.frame(minWidth:44, minHeight:44).contentShape(Rectangle())`
- Android: M3 components enforce 48dp automatically.
- Roblox/Unity: transparent hit buttons larger than the icon; size with Scale and `UIAspectRatioConstraint`.

**Related:** [[fitts-law]] · [[safe-area]] · [[affordance]]
