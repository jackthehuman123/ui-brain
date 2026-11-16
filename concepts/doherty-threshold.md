---
type: concept
description: "Respond within ~400 ms, show visual feedback within 100 ms; busy state past 1 s, percent-done past 10 s"
domain: interaction-and-state
aliases: [Doherty threshold, response time, latency, perceived performance, 400ms, loading feedback]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://lawsofux.com/doherty-threshold/
  - https://www.nngroup.com/articles/response-times-3-important-limits/
  - https://web.dev/articles/inp
---
# Doherty threshold

**Rule:** The system must respond to every input within about 400 ms, and show *some* visual change within 100 ms. When real work takes longer, show progress, and make perceived speed carry the gap (skeletons, optimistic UI).

**Why:** Below the threshold users stay engaged and productive; above it they wait, wonder, and repeat taps.

**Values:**
- **400 ms**: the interaction pace at which productivity rises sharply. *(Doherty & Thadani 1982, IBM; lawsofux)*
- **0.1 s** feels instantaneous · **1 s** keeps the flow of thought (show a busy state past it) · **10 s** holds attention (use a percent-done indicator past it). *(NN/g)*
- Web INP good: **≤ 200 ms** at p75. *(web.dev)*

**Failure looks like:** A button that shows nothing for 600 ms, then navigates. Double submissions because there was no pressed or loading state. A spinner for a 12-second export with no percentage. A game menu that hitches 300 ms when opened.

**Detect in review:** Record the screen at 60 fps and count frames from input to first visual change (6 frames is ~100 ms). Run the INP field data or the Performance panel. Check that every async action has an immediate pressed/loading state and that long tasks show determinate progress.

**Implementation:**
- Web: pressed state on `pointerdown`; `aria-busy`; skeletons sized to the final content ([[layout-shift]]); break long tasks up with `scheduler.yield()` to keep INP low.
- iOS/Android: highlight state on touch-down; `ProgressView(value:)` / `LinearProgressIndicator(progress)` for long work.
- Game UI: input feedback on the same frame; preload menus to avoid open hitches; show a loading bar with a percentage for teleports and loads.

**Related:** [[optimistic-update]] · [[animation-duration]] · [[anticipation]]
