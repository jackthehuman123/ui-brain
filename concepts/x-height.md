---
type: concept
description: "Judge size by x-height, not font-size; match x-heights when mixing fonts or fallbacks (font-size-adjust)"
domain: typography
aliases: [x height, ex-height, font-size-adjust, apparent size]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/font-size-adjust
  - https://web-platform-dx.github.io/web-features-explorer/features/font-size-adjust
---
# X-height

**Rule:** Compare and set text size by x-height, not nominal font-size. When mixing two families (or a web font and its fallback), match their x-heights rather than their font-size.

**Why:** Lowercase height drives perceived size and legibility. Two fonts at the same px can look noticeably different in size, so a body or fallback font with a small x-height reads as too small.

**Values:**
- `font-size-adjust: <x-height ÷ font-size>` scales fallbacks to the primary font's x-height. Baseline 2024 (Chrome 127, Firefox 118). *(MDN, web-features)*
- A smaller x-height needs a larger font-size or more [[leading]] to read equally well.
- Minimum body sizes per platform live in `platforms/` (web, ios, android).

**Failure looks like:** An icon font or monospace snippet that looks a size smaller than the surrounding text. Body text that "shrinks" when the web font loads. Two-family UIs where labels and values look mismatched at equal px.

**Detect in review:** Two families on one line with visibly different lowercase heights. In code: the same `font-size` on mixed families with no `font-size-adjust` or per-family size override. A fallback stack without metric overrides; see [[font-loading]].

**Implementation:**
- Web: `body { font-family: "Brand", system-ui; font-size-adjust: 0.53; }` (use the brand font's ratio), or `from-font` where supported.
- iOS/Android: custom fonts need per-family size tokens. Don't reuse the system font's sizes 1:1.
- Game UI: when replacing the default font (Roblox `FontFace`, Unity TMP font asset), re-check sizes at the smallest HUD text.

**Related:** [[leading]] · [[font-loading]] · [[tracking]]
