---
type: concept
description: "Use the font's tracking curve; else lowercase ≈0, tighten display slightly, +0.05–0.12em on caps letters; store in em"
domain: typography
aliases: [letter-spacing, letter spacing, character spacing, cspace]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/typography
  - https://d.rsms.me/inter-website/v3/dynmetrics/
  - https://practicaltypography.com/letterspacing.html
  - https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html
  - https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.2/manual/RichTextCharacterSpacing.html
---
# Tracking

**Rule:** Tracking is a per-font curve over size. Use the font's published curve (SF, Inter, M3). Otherwise: lowercase ≈ 0, large display slightly tighter, all-caps **letter strings** +0.05–0.12em. Store it in `em` per type-scale step.

**Why:** Fonts are spaced for one size range. Caps lack ascenders and descenders, so their shapes merge without extra space.

**Values:**
- SF Pro and M3 curves: [[platforms/ios]], [[platforms/android]]. SF *loosens* above ~24pt, so "tighten big text" is wrong for SF. *(Apple HIG)*
- Inter: `−0.0223 + 0.185·e^(−0.1745·px)` → 16px −0.011em, ≥32px −0.022em. *(rsms; units assumed em/px, **unverified**)*
- Caps and small caps: 0.05–0.12em *(Butterick)*. Large all-caps display: low end, **unverified** 0.02–0.05em (the caps and display rules pull opposite ways).
- Don't track numerals or symbols as if they were caps ("−17%" reads as separate tokens).
- The layout must survive `letter-spacing: 0.12em` *(WCAG 2.2 SC 1.4.12)*.

**Failure looks like:** Gappy display headlines. Caps labels with touching letters ("RN" reads as "M"). Negatively tracked body text. A px value that's only right at one size.

**Detect in review:** `letter-spacing` in px. One value for headings and body. `uppercase` without tracking. Negative tracking under 14px. `.tracking()` on SF. `!important` on letter-spacing. Inject `*{letter-spacing:.12em!important}` and look for clipping.

**Implementation:**
- Web: `--display-tracking: -0.022em; .caps{letter-spacing:.08em}`
- iOS: text styles apply SF tracking. `.tracking()` is in **points**, so use em × size.
- Android: `letterSpacing = 0.03.em`
- Unity TMP: Inspector 1 = 0.01em. `<cspace=0.05em>` is real em.
- Roblox: no tracking property. Pick a font spaced for the size.

**Related:** [[kerning]] · [[leading]] · [[x-height]] · [[tabular-numbers]]
