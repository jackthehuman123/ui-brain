---
type: checklist
description: "Yes/no typography checks: tracking, kerning, leading, measure, widows, numerals, x-height, font loading"
domain: typography
---
# Typography review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Tracking is set per type-scale step in em, and all-caps letter strings have +0.05–0.12em → [[tracking]]
- [ ] No hand-copied tracking on system fonts (SF applies its own curve) → [[tracking]]
- [ ] Font kerning is on, and display headlines show no gapping pairs (To, AV, LT) → [[kerning]]
- [ ] Body line-height is about 1.4–1.5 and headings tighter, all unitless → [[leading]]
- [ ] Body text measure is 45–90 characters (≈ 65ch max-width) at desktop width → [[line-length]]
- [ ] No heading, button or card title ends on a single word at 390/768/1440px → [[widow]]
- [ ] Numbers that change in place or align in columns use tabular figures → [[tabular-numbers]]
- [ ] Mixed families or fallbacks match x-height (font-size-adjust or per-family sizes) → [[x-height]]
- [ ] The web font swap causes no visible reflow (metric-matched fallback, ≤ 2 preloads) → [[font-loading]]
- [ ] The layout survives letter-spacing 0.12em and line-height 1.5 overrides without clipping → [[tracking]] · [[leading]]
