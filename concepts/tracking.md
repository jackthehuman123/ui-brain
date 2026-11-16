---
type: concept
domain: typography
aliases: [letter-spacing, letter spacing, character spacing, cspace]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://github.com/material-components/material-components-android/blob/master/lib/java/com/google/android/material/typography/res/values/tokens.xml
  - https://developer.apple.com/videos/play/wwdc2020/10175/
  - https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html
  - https://issuetracker.unity3d.com/issues/vertical-spacing-breaking-when-upgrading-to-textmeshpro-2-dot-1-0-and-higher
  - https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.2/manual/RichTextCharacterSpacing.html
  - https://devforum.roblox.com/t/ability-to-set-thickness-of-text-strokes-letter-spacing-on-textlabels-textbuttons/34423
---
# Tracking

**Rule:** Set tracking per type-scale step in `em`: tighten as size grows, loosen small text and anything set in all caps. Never use one letter-spacing value for the whole scale, and never add tracking on top of a system font that already tracks itself.

**Why:** Fonts are spaced for text sizes. At display sizes the same proportional gaps look loose and words come apart. At small sizes and in caps (no ascenders or descenders to separate shapes), letters crowd and blur together.

**Values:**
- Material 3 tokens (sp → em): Display Large 57 → −0.25 (−0.0044em) · Headline/Title Large → 0 · Body Large 16 → +0.5 (+0.031em) · Body Medium 14 → +0.25 (+0.018em) · Label Large 14 → +0.1 (+0.007em) · Label Small 11 → +0.5 (+0.045em). *(M3 tokens)*
- Apple SF Pro: the system font applies size-dependent tracking automatically, and it changes smoothly between 17 and 28 pt rather than breaking at 20 pt. *(WWDC20 10175)* Per-size numbers: **unverified**. The HIG table couldn't be retrieved and third-party copies disagree.
- All-caps labels: **unverified**, +0.05 to +0.1em (practitioner convention; M3 Label Small's +0.045em is the closest primary data point).
- Display ≥ 48px in custom fonts: **unverified**, −0.01 to −0.03em. Check against the font's own recommendations; some variable fonts (e.g. Inter) publish tracking curves.
- Accessibility floor: the layout must survive a user override of `letter-spacing: 0.12em` with nothing clipped or overlapping. *(WCAG 2.2 SC 1.4.12, AA)*

**Failure looks like:** A hero headline with visible gaps between letters. A button label in all caps where letters touch ("RN" reads as "M"). 11–12px captions that blur together. Negative tracking on body text. Tracking set in px that looks right at one size and breaks when the size token changes.

**Detect in review:**
- Code: `letter-spacing` in `px` (should be `em`). The same value on `h1` and `body`. `text-transform: uppercase` without positive letter-spacing. Negative letter-spacing on text under ~20px. `letter-spacing … !important` (blocks the 1.4.12 override).
- Screenshot: in display text, the gaps between letters look wider than the counters (the inside of "o" and "e"). In caps labels, adjacent stems almost touch.
- Accessibility check: inject `* { letter-spacing: 0.12em !important }` and look for truncation or overflow.

**Implementation:**
- Web: `h1 { letter-spacing: -0.02em } .label-caps { text-transform: uppercase; letter-spacing: 0.06em }`. Keep the value in a type-scale token next to font-size.
- iOS (SwiftUI/UIKit): use text styles (`.font(.title)`) and let SF track itself. With custom fonts, `.tracking(_:)` takes **points**, so compute em × current point size or Dynamic Type sizes will drift.
- Android (Compose): `TextStyle(letterSpacing = 0.03.em)`. Compose accepts `em`, so prefer it over `sp`.
- Unity (TextMeshPro): the Inspector's *Character Spacing* uses 1 = 0.01em (since TMP 2.1). Rich text uses real em: `<cspace=0.05em>`. Those are two different scales.
- Roblox: `TextLabel` has no letter-spacing property. Pick a font whose default spacing fits the size; per-glyph labels are rarely worth the cost.

**Related:** [[kerning]] · [[leading]] · [[x-height]] · [[line-length]] · [[tabular-numbers]]
