---
type: concept
description: "Use the font's tracking curve; else lowercase ≈0, tighten display slightly, +0.05–0.12em on all caps; store in em"
domain: typography
aliases: [letter-spacing, letter spacing, character spacing, cspace]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/typography
  - https://github.com/material-components/material-components-android/blob/master/lib/java/com/google/android/material/typography/res/values/tokens.xml
  - https://d.rsms.me/inter-website/v3/dynmetrics/
  - https://practicaltypography.com/letterspacing.html
  - https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html
  - https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.2/manual/RichTextCharacterSpacing.html
  - https://devforum.roblox.com/t/ability-to-set-thickness-of-text-strokes-letter-spacing-on-textlabels-textbuttons/34423
---
# Tracking

**Rule:** Tracking is a curve over font size, specific to each font. Use the font's published curve if it has one (SF, Inter, M3 tokens). If not, keep lowercase near 0, tighten large display text slightly, and always add 0.05–0.12em to all caps. Store it in `em` alongside each type-scale step, never as one global value.

**Why:** Fonts are spaced for one size range. Outside it, gaps look loose at large sizes and letters crowd at small sizes. All caps have no ascenders or descenders to separate letter shapes, so they need extra space.

**Values:**
- **SF Pro (iOS), pt → 1/1000 em:** 11 → +6 · 15 → −16 · 17 → **−26** · 20 → −23 · 24 → +3 · 28 → +14 · 34 → **+12** · 48 → +8 · 80 → 0. *(Apple HIG tracking table)* SF loosens again above ~24pt, so "tighten big text" is **wrong for SF**. macOS uses a separate table. The full tables will go in `platforms/ios.md`.
- **Inter:** `tracking = −0.0223 + 0.185·e^(−0.1745·size)`, which gives 12 → 0.000 · 16 → −0.011 · 24 → −0.020 · ≥32 → −0.022. *(rsms Inter dynamic metrics)* Units aren't stated; em-per-px is assumed (**unverified**).
- **Material 3 (sp → em):** Display Large 57 → −0.004 · Title Large → 0 · Body Large 16 → +0.031 · Label Large 14 → +0.007 · Label Small 11 → +0.045. *(M3 tokens)*
- **All caps / small caps:** +5–12%, i.e. `0.05–0.12em`, which matters most at small sizes. Lowercase normally needs no tracking. *(Butterick)*
- **Accessibility floor:** the layout must survive a user override of `letter-spacing: 0.12em` with nothing clipped. *(WCAG 2.2 SC 1.4.12)*

**Failure looks like:** A display headline with visible gaps between letters (or SF headings squeezed tight by hand-copied negative values). All-caps buttons with letters touching ("RN" reads as "M"). Body text tracked negatively. A px value that only looks right at one size.

**Detect in review:**
- Code: `letter-spacing` in px. One value shared by headings and body. `uppercase` without positive tracking. Negative tracking under ~14px. `.tracking()` on the system font. `!important` on letter-spacing (blocks the 1.4.12 override).
- Screenshot: in display text, gaps between letters wider than the counters. In caps labels, stems nearly touching.
- Accessibility check: inject `*{letter-spacing:.12em!important}` and look for truncation.

**Implementation:**
- Web: put a tracking token on each step: `--display-tracking: -0.022em; .caps{text-transform:uppercase;letter-spacing:.08em}`.
- iOS: use text styles (`.font(.title)`); SF applies the HIG curve itself. For custom fonts, `.tracking(_:)` takes **points**, so use em × current size.
- Android (Compose): `letterSpacing = 0.03.em` (prefer em over sp).
- Unity (TMP): in the Inspector, Character Spacing 1 = 0.01em. Rich text `<cspace=0.05em>` uses real em.
- Roblox: no tracking property exists. Choose a font whose default spacing fits the size.

**Related:** [[kerning]] · [[leading]] · [[x-height]] · [[line-length]] · [[tabular-numbers]]
