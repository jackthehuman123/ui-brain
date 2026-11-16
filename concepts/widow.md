---
type: concept
description: "No single-word last lines in headings or short text: text-wrap balance on headings, pretty on paragraphs, nbsp for pairs"
domain: typography
aliases: [widows, orphan, orphans, runt, text-wrap balance, text-wrap pretty, rag]
platforms: [web, all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/text-wrap-style
  - https://developer.chrome.com/docs/modern-web-guidance/guides/visual-design/improve-text-layout-and-legibility
---
# Widow

**Rule:** Headings, buttons, cards and short paragraphs must not end on a single short word. Balance headings and use "pretty" wrapping on paragraphs. Bind names, numbers and units with non-breaking spaces.

**Why:** A lone last word reads as an error, pulls the eye, and wastes a line of height in tight components.

**Values:**
- `text-wrap: balance` is applied only up to **6 lines** in Chromium and **10** in Firefox; past that it falls back to normal wrapping. *(Chrome docs, MDN)*
- `text-wrap: pretty` avoids short last lines in paragraphs. Support varies by browser, and unsupported browsers ignore it safely.
- Non-breaking spaces between a number and its unit (`30 °C`, `340 g`) and in short brand phrases.

**Failure looks like:** A hero H1 with "ends." alone on line 3. A card title "Field-proven / bestsellers" balanced badly. "30 / °C" split across lines in a spec strip.

**Detect in review:** Screenshot every heading and card title at 390px, 768px and 1440px and look for single-word last lines. In code: headings without `text-wrap: balance`, and numbers with units separated by normal spaces.

**Implementation:**
- Web: `h1,h2,h3,.card-title { text-wrap: balance } p { text-wrap: pretty }`. Use `&nbsp;` between value and unit.
- iOS: SwiftUI has no balance. Use `.lineLimit` with `.minimumScaleFactor` sparingly, or rewrite the copy.
- Android: `LineBreak.Heading` / `LineBreak.Paragraph` in `TextStyle`.
- Game UI: check every localization; German and French lengthen strings by 20–35% (**unverified** range) and create new widows.

**Related:** [[line-length]] · [[leading]]
