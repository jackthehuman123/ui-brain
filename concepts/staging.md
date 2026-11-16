---
type: concept
description: "One focal motion at a time; dim or blur the rest when an overlay takes focus; animate toward where the user acts next"
domain: motion
aliases: [staging the focus, focus, scrim, choreography, visual hierarchy in motion, modal backdrop]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/motion
---
# Staging

**Rule:** Present one idea at a time. During a transition only one region moves prominently; when an overlay takes focus, the background dims or blurs and stops moving. End motion where the user's next action is.

**Why:** Peripheral vision is drawn to any motion. Two simultaneous animations split attention, so the user misses the one that mattered.

**Values:**
- Modal scrim: **unverified**, black at ~30–60% opacity (dark mode needs more), or a backdrop blur, with text behind it no longer competing.
- Concurrent prominent motions: **1** (secondary actions excepted; see [[secondary-action]]).
- Content behind a modal: background animations (carousels, video, ambient motion) pause while it's open.

**Failure looks like:** A toast sliding in while a sheet opens and a list re-sorts. A modal over an auto-playing hero video. Onboarding tooltips appearing on top of an animating chart. A game HUD flashing three notifications at once.

**Detect in review:** Record a key flow and count regions in motion per transition. Open each overlay and check that the background is dimmed or blurred and still. Queue notifications instead of stacking them simultaneously.

**Implementation:**
- Web: `<dialog>` with `::backdrop{background:oklch(0 0 0/.45);backdrop-filter:blur(4px)}`; pause videos on open; a toast queue with one visible at a time.
- iOS: `.sheet` and `.fullScreenCover` dim automatically; queue custom banners.
- Android: M3 dialogs and sheets provide the scrim; use `SnackbarHostState`, which queues.
- Game UI: during a reward or level-up moment, fade non-essential HUD to ~50% and freeze ambient UI tweens. Queue achievement popups.

**Related:** [[stagger]] · [[secondary-action]] · [[dark-mode-depth]] · [[progressive-disclosure]]
