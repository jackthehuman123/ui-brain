---
type: concept
description: "Don't make users hold more than ~4 chunks in memory; chunk long strings; 7±2 does NOT limit menu length"
domain: interaction-and-state
aliases: [Miller's law, 7 plus or minus 2, working memory, chunking, cognitive load]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://lawsofux.com/millers-law/
  - https://www.cambridge.org/core/journals/behavioral-and-brain-sciences/article/magical-number-4-in-shortterm-memory-a-reconsideration-of-mental-storage-capacity/44023F1147D4A1D44BDC0AD226838496
---
# Miller's law

**Rule:** Don't require users to *remember* things across steps. Keep what they need visible, and chunk long strings (codes, numbers, IDs) into groups of about 3–4. Miller's 7±2 is not a limit on how many items a menu or nav may show: visible options don't load memory.

**Why:** Working memory holds very little, and every value the user must carry to the next screen is a chance to forget and error.

**Values:**
- Miller (1956): 7 ± 2, which Miller himself framed loosely. Cowan (2001): **about 4 chunks** for young adults. *(Cowan, BBS 2001)*
- Chunking: phone numbers `415 555 0132`; card numbers in groups of 4; confirmation codes `K7Q-4MP-2XR`.
- Visible lists may exceed 7 items when they're well ordered; see [[hicks-law]].

**Failure looks like:** A 2FA screen that hides the code-entry hint after the code arrives. A comparison page that forces the user to remember plan A's price while viewing plan B. A navigation cut to exactly 7 items "because of Miller's law". 16-character codes shown as one unbroken string.

**Detect in review:** For each multi-step flow, list what the user must recall from earlier steps, and show it instead. Check long codes and numbers for grouping. Challenge any design rationale that cites 7±2 for visible lists.

**Implementation:**
- Web: show order summaries persistently in checkout; `autocomplete="one-time-code"`; format codes with visual spacing, not literal spaces in the value.
- iOS: `.textContentType(.oneTimeCode)` for SMS autofill.
- Android: SMS Retriever / autofill hints for codes.
- Game UI: keep quest objectives on screen (a tracker) rather than asking players to memorize NPC instructions.

**Related:** [[hicks-law]] · [[progressive-disclosure]] · [[postels-law]]
