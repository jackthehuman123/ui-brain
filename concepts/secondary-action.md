---
type: concept
description: "Supporting motion (icon morph, badge bump) reinforces the main action at smaller amplitude and never competes with it"
domain: motion
aliases: [secondary motion, supporting animation, micro-interaction detail, badge bump]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/animation-duration/
---
# Secondary action

**Rule:** Supporting motion (a chevron rotating as a panel opens, a cart badge bumping as an item is added, a hamburger icon morphing into an X) reinforces the primary action. It must be smaller in amplitude, no longer than the primary motion, and finish with it or before it.

**Why:** Secondary motion confirms the result where the eye isn't ("the item went *there*") without stealing focus from the main change.

**Values:**
- Duration ≤ the primary motion's; see [[animation-duration]].
- Amplitude: **unverified**, roughly a quarter of the primary's scale change or less (e.g. a badge bumps to 1.15 while a sheet moves the full screen).
- One secondary action per primary action is usually enough.

**Failure looks like:** A cart badge that bounces bigger than the add-to-cart confirmation. Several decorative motions fighting during one transition. A chevron that rotates after the panel has finished opening (out of sync). Secondary motion that loops indefinitely.

**Detect in review:** For each transition, list primary vs secondary motion. Check that the secondary motion starts at or after the primary, ends no later, and has the smaller amplitude. Remove any secondary motion that confirms nothing.

**Implementation:**
- Web: drive both from the same state change and transition, e.g. `[aria-expanded=true] .chev{rotate:180deg}` on the same duration token.
- iOS: SF Symbol effects (`.symbolEffect(.bounce)`, `.contentTransition(.symbolEffect(.replace))`) are built-in secondary actions.
- Android: `AnimatedContent` for icon swaps; `animateFloatAsState` for badge scale.
- Game UI: currency counters tick up (with [[tabular-numbers]]) while the reward flies in; sound and particles are secondary too.

**Related:** [[staging]] · [[squash-and-stretch]] · [[blurred-icon-swaps]] · [[follow-through]]
