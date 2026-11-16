---
type: concept
description: "Cap body text at ~45–90 characters per line (aim ~65); set max-width in ch, not px"
domain: typography
aliases: [measure, line width, characters per line, CPL, max-width ch]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://practicaltypography.com/line-length.html
  - https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html
---
# Line length

**Rule:** Keep body text at 45–90 characters per line, aiming for about 65. Set the limit in `ch`, so it scales with the font, not the viewport.

**Why:** Long lines make the eye lose its place on the return sweep. Very short lines break reading rhythm and produce ragged edges and [[widow]]s.

**Values:**
- 45–90 characters including spaces, or 2–3 alphabets per line. *(Butterick)*
- WCAG AAA: no more than **80** characters for blocks of text. *(WCAG SC 1.4.8)*
- Short marketing ledes: **unverified**, about 30–45ch (they're scanned, not read).

**Failure looks like:** Full-width paragraphs on desktop running 150+ characters. A hero lede wrapping one word per line on mobile because of a fixed px width. Dense table cells forced to wrap at 20 characters.

**Detect in review:** Count characters on a representative line in the screenshot at 1440px and 390px. In code: text containers with no `max-width`, or a `max-width` in px on body copy.

**Implementation:**
- Web: `.prose { max-width: 65ch; }` and `.lede { max-width: 34ch; }`. Combine with [[widow]] control for headings.
- iOS: `readableContentGuide` (UIKit) constrains text width on iPad. In SwiftUI, cap with `.frame(maxWidth:)` derived from font size.
- Android: constrain with `Modifier.widthIn(max = …)` on large screens.
- Game UI: dialog and tooltip boxes need a max width in characters. Set Roblox `TextWrapped` with a fixed-width frame, and use the TMP rect width.

**Related:** [[leading]] · [[widow]] · [[x-height]]
