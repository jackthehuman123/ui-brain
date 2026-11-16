---
type: concept
description: "Feedback ~100 ms, panels and modals 200–300 ms, exits shorter than entrances; scale with distance; never past ~500 ms"
domain: motion
aliases: [snappy timing, timing, duration, transition duration, motion speed]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/animation-duration/
  - https://m3.material.io/styles/motion/easing-and-duration/tokens-specs
---
# Animation duration

**Rule:** Use the shortest duration that doesn't look jarring. About 100 ms for direct feedback, 200–300 ms for panels and modals, and longer only for big moves across large screens. Exits run shorter than entrances. Frequent actions get the shortest motion, or none.

**Why:** Animation is wait time, multiplied by every repeat.

**Values:**
- Most UI animation: **100–500 ms**. Simple feedback (toggle, checkbox): ~**100 ms**. Substantial changes (modal): **200–300 ms**. **400 ms** is very slow, for big moves on large screens. *(NN/g)*
- Exit < enter: e.g. a popup appears in 300 ms and leaves in 200–250 ms. *(NN/g)*
- Material 3 tokens span 50 ms (short1) to 1000 ms (extraLong4); long2 = 500 ms. *(M3 via secondary sources)*
- Scale with travel distance and element size. Tablets and desktop need slightly longer than phones because the distances are bigger.

**Failure looks like:** A 600 ms dropdown on every click. Identical durations for a checkbox and a full-screen sheet. Slow exits that block the next action. A "smooth" 1 s page transition users must wait through on every navigation.

**Detect in review:** List every `transition-duration` / `animation-duration` and flag anything over 400 ms that isn't a large spatial move. Check that exit durations are below entrance durations. Repeat the most frequent action 10 times: if it starts to feel slow, cut the duration.

**Implementation:**
- Web: duration tokens `--dur-1: 100ms; --dur-2: 200ms; --dur-3: 300ms` plus a reduced-motion override ([[reduced-motion]]).
- iOS: springs are specified by `duration`/`response` (perceptual), not settling time.
- Android: M3 `MotionScheme` duration tokens.
- Game UI: hit and press feedback starts on the **same frame** as the input; reward celebrations may run longer but must be skippable.

**Related:** [[easing]] · [[stagger]] · [[doherty-threshold]] · [[reduced-motion]]
