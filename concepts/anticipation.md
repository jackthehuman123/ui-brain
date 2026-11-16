---
type: concept
description: "Short wind-up before big or irreversible motion (hold-to-confirm, charge, chest shake); never before frequent actions"
domain: motion
aliases: [anticipation wind-up, wind-up, pre-motion, hold to confirm, telegraphing]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/videos/play/wwdc2018/803/
---
# Anticipation

**Rule:** Add a brief wind-up before large, surprising or irreversible motion, so the user reads what's about to happen: a reward chest that shakes before opening, a hold-to-confirm ring, a slight pull-back before a launch. Never add anticipation to frequent or routine actions, where it reads as lag.

**Why:** The wind-up prepares the eye and builds expectation. For destructive actions, a visible charge-up gives the user a moment to cancel.

**Values:**
- UI wind-up length: **unverified**, ≤ ~100 ms for transitions, so it stays within feedback latency; see [[doherty-threshold]].
- Hold-to-confirm: **unverified**, 0.5–1.5 s fill, cancellable on release, with visible progress.
- Game telegraphing (enemy attacks, timed events): long enough to react to; tune by playtest.

**Failure looks like:** A menu button that dips before opening on every tap. A delete that fires instantly with no chance to back out. Boss attacks with no tell. A reward screen that skips straight to "+500", deflating the moment.

**Detect in review:** Time the gap between input and the main motion: frequent actions should start the main motion immediately. Check that destructive actions have either a wind-up/hold or an undo. Make sure wind-ups can be cancelled (release, escape).

**Implementation:**
- Web: hold-to-confirm with `pointerdown` → a CSS `transition` on a progress ring, cancelled on `pointerup`/`pointerleave`.
- iOS: `.onLongPressGesture(minimumDuration:)` with a visible progress state.
- Android: `detectTapGestures(onPress = { … tryAwaitRelease() })` driving progress.
- Game UI: a pre-tween (scale 0.95, shake) chained before the main tween. It must be skippable on tap.

**Related:** [[squash-and-stretch]] · [[follow-through]] · [[staging]]
