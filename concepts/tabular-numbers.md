---
type: concept
description: "Use tabular (fixed-width) digits for numbers that change in place or align in columns; proportional in prose"
domain: typography
aliases: [tabular figures, tnum, monospaced digits, tabular-nums, lining figures]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric
  - https://developer.apple.com/documentation/swiftui/font/monospaceddigit()
  - https://docs.unity3d.com/Packages/com.unity.textmeshpro@4.0/manual/RichTextMonospace.html
---
# Tabular numbers

**Rule:** Use tabular (equal-width) digits for anything that updates in place (timers, counters, prices, scores) or aligns in columns (tables, specs, stats). Keep proportional digits in running text.

**Why:** Proportional digits have different widths ("1" is narrow), so changing values make text jitter sideways, and column totals don't line up.

**Values:**
- OpenType feature `tnum`; CSS `font-variant-numeric: tabular-nums`. *(MDN)*
- Right-align numeric columns, or align them on the decimal point. Keep the same decimal places within a column.
- Fonts without a `tnum` feature need a monospace fallback for the digits.

**Failure looks like:** A countdown whose colon shifts every second. A price toggle ($12 ↔ $120) that nudges the "/ month" label. Leaderboard scores with ragged right edges.

**Detect in review:** Record or step through any changing number and watch for horizontal jitter. Check that numeric columns align on their right edges. In code: numeric UI without `tabular-nums`, `.monospacedDigit()` or `tnum`.

**Implementation:**
- Web: `.num, td.num, time { font-variant-numeric: tabular-nums; }`
- iOS: `.font(.body.monospacedDigit())` or `Text(...).monospacedDigit()`
- Android: `TextStyle(fontFeatureSettings = "tnum")`
- Unity TMP: `<mspace=0.6em>12:04</mspace>`, or a font with `tnum` baked into the atlas.
- Roblox: no OpenType features. Use a monospace font (e.g. `RobotoMono`) for scores and timers, or place each digit in a fixed-width label.

**Related:** [[layout-shift]] · [[tracking]]
