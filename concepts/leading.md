---
type: concept
description: "Body line-height 1.4–1.5 (unitless), headings 1.1–1.25; tighten as size grows; survive a 1.5 user override"
domain: typography
aliases: [line-height, line height, line spacing, leading]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://practicaltypography.com/line-spacing.html
  - https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html
  - https://m3.material.io/styles/typography/type-scale-tokens
---
# Leading

**Rule:** Set line-height as a unitless ratio per type-scale step: about 1.4–1.5 for body, 1.1–1.25 for headings, and tighter as size grows. Never set one global value.

**Why:** The eye needs vertical room to find the next line. Large text has more built-in space, so the same ratio looks loose on headings and cramped on small text.

**Values:**
- Body: 120–145% of the point size *(Butterick)*. M3 Body Large is 16/24 = 1.5 *(M3 tokens)*.
- Headings: **unverified**, 1.1–1.25 (common practice; follows the tighten-with-size rule).
- Accessibility: content must survive a user line-height of **1.5** and paragraph spacing of **2×** font size. *(WCAG 2.2 SC 1.4.12)*
- Long line length needs more leading; see [[line-length]].

**Failure looks like:** Display headlines whose lines float apart. Dense body text at 1.2. Multi-line buttons or labels clipped when the user raises line-height. Unequal space above and below icons aligned to text.

**Detect in review:** `line-height` in px (doesn't scale), or the same value on `h1` and `p`. Fixed `height` on text containers. Screenshot: line gap on display text larger than the cap height.

**Implementation:**
- Web: `p { line-height: 1.5 } h1 { line-height: 1.1 }`. Use unitless values so they inherit as ratios. Use `text-box-trim` (where supported) to trim surplus leading above and below.
- iOS: text styles include leading. Use `.lineSpacing()` only for custom styles; it adds space between lines, it doesn't set line-height.
- Android: `TextStyle(lineHeight = 24.sp)` plus `LineHeightStyle` to control trimming.
- Unity TMP: Line Spacing (em/100 units, like character spacing).
- Roblox: `TextLabel.LineHeight` is a multiplier.

**Related:** [[line-length]] · [[x-height]] · [[tracking]]
