---
type: concept
description: "Stagger list entrances by a small per-item delay with a hard cap on total time; first view only, never on repeat"
domain: motion
aliases: [staggered animation, cascade, sequential reveal, delay per item, choreography]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/animation-duration/
---
# Stagger

**Rule:** When a group enters together, offset each item by a small delay to show order and grouping, and cap the **total** stagger so the last item starts quickly. Stagger only the items visible on first entry, and never on repeat views or on content the user is waiting to act on.

**Why:** A cascade directs the eye through the list's order and makes many items read as one gesture. Uncapped stagger turns a 12-item grid into seconds of waiting.

**Values:**
- Per-item delay: **unverified**, 20–50 ms (common practice).
- Total stagger cap: **unverified**, ≤ ~300 ms, so the last item starts within the same window NN/g gives for a substantial transition (200–300 ms). *(NN/g, by analogy)*
- Items beyond the cap enter together with the last staggered one.
- Each item's own animation follows [[animation-duration]] and [[easing]].

**Failure looks like:** A search-results list that drips in one row at a time. Stagger that replays every time a filter changes. Off-screen items still animating when scrolled into view seconds later. Buttons that can't be clicked until their delay passes.

**Detect in review:** Compute `last delay + item duration` and flag anything over ~500 ms. Check whether the stagger re-runs on filter, sort or tab switches. Confirm items are interactive immediately, not after their delay.

**Implementation:**
- Web: `style="--i: 3"` with `transition-delay: calc(min(var(--i), 8) * 30ms)`; skip it under `prefers-reduced-motion`.
- iOS: `.animation(.snappy.delay(Double(min(i, 8)) * 0.03), value: shown)`.
- Android: `AnimatedVisibility` with `tween(delayMillis = min(i, 8) * 30)`.
- Game UI: reward and inventory reveals may stagger longer, but tapping skips to the end state.

**Related:** [[animation-duration]] · [[staging]] · [[reduced-motion]]
