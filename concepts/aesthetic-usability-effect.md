---
type: concept
description: "Polish raises perceived usability and forgiveness, but masks real problems; judge usability by tasks, not by praise"
domain: interaction-and-state
aliases: [overall appeal, appeal, aesthetic-usability effect, visual polish, attractive things work better]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/aesthetic-usability-effect/
---
# Aesthetic-usability effect

**Rule:** Invest in visual appeal (consistent spacing, type, color, motion), because users judge attractive interfaces as easier to use and forgive small issues. But never accept "it looks great" as evidence of usability: measure task success, and fix problems that the polish hides.

**Why:** Appeal shapes first impressions and trust, and buys patience during minor friction. The same effect makes users and stakeholders under-report real problems.

**Values:**
- Kurosu & Kashimura (Hitachi, 1995): 26 ATM layouts, 252 participants. *Perceived* ease of use correlated more with aesthetic appeal than with actual usability. *(NN/g)*
- Testing caveat: in an NN/g study, positive reactions to a site's aesthetics "masked its usability issues and made them harder to identify". *(NN/g)*

**Failure looks like:** A gorgeous homepage that fails the 5-second test ([[screens/homepage]]). Design reviews that approve on screenshots without walking the task. User tests where participants praise the look and then fail checkout. Conversely, an unpolished but functional UI distrusted by users ("looks like a scam").

**Detect in review:** Separate visual critique from task review: run the key task (find, compare, buy, configure) and record success and time independently of opinions. In AI-generated design reviews, list both "polish issues" and "task blockers"; a pretty screen with any task blocker fails.

**Implementation:**
- Polish comes from the vault's details: [[tracking]], [[concentric-radius]], [[consistent-light-source]], [[matched-icon-weight]], [[easing]].
- Usability evidence comes from tasks: success rate, time on task, errors, not from ratings alone.
- Game UI: appeal (art direction, juice) drives retention and store conversion, but new-player funnels still need playtest data on where players drop.

**Related:** [[jakobs-law]] · [[affordance]] · [[squash-and-stretch]]
