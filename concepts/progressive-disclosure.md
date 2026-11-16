---
type: concept
description: "Show frequent options up front and defer rare or advanced ones one step away; never more than 2 disclosure levels"
domain: interaction-and-state
aliases: [disclosure, show more, advanced settings, accordion, expand collapse, staged disclosure]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/progressive-disclosure/
---
# Progressive disclosure

**Rule:** Show the options most users need, most of the time, up front. Defer rare, advanced or risky options behind one clearly labeled step ("Advanced", "More options", an accordion). Stop at two levels.

**Why:** A short initial set is faster to scan and harder to misuse, and the full power is still one click away for those who need it.

**Values:**
- Initial display: "everything that users frequently need". Secondary: things needed "on rare occasions". *(NN/g)*
- Levels: designs beyond **2** disclosure levels "typically have low usability". If you need three, simplify or group. *(NN/g)*
- The split comes from data (task analysis, frequency of use, analytics), not guesses. See [[frequency-of-use]].

**Failure looks like:** A settings page with 40 equal-weight toggles. Essential fields hidden under "More". Accordions inside accordions inside tabs. A disclosure label that doesn't say what's inside ("Details"). Expanding content that shifts the button the user just tapped.

**Detect in review:** Count disclosure depth on each path. For each hidden item, ask whether most users need it; if yes, it's hidden wrongly. Check that triggers say what they reveal and show their state (`aria-expanded`, a chevron).

**Implementation:**
- Web: `<details>/<summary>`, or a button with `aria-expanded` + `aria-controls`; animate height interruptibly (grid-rows `0fr→1fr`). See [[interruptible-animation]].
- iOS: `DisclosureGroup`; a "Show more" row in lists.
- Android: an expandable `Card` or `ListItem` with `AnimatedVisibility`.
- Game UI: a basic/advanced tab in settings; tutorials reveal mechanics as they become relevant.

**Related:** [[hicks-law]] · [[frequency-of-use]] · [[staging]] · [[components/form]]
