---
type: concept
description: "Place controls by usage frequency: frequent = big, close, one tap; rare = behind a step; use analytics"
domain: interaction-and-state
aliases: [frequency of use, usage frequency, priority placement, primary vs secondary actions, hot path]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/progressive-disclosure/
  - https://lawsofux.com/fittss-law/
---
# Frequency of use

**Rule:** Rank actions by how often they're used, and let that rank drive placement, size and depth. The top actions get the most reachable, largest, zero-step spots. Rare actions move behind a menu or disclosure. Re-rank from real usage data, not from stakeholder priority.

**Why:** Every step and every centimeter is paid on each use. Optimizing the hot path saves far more time than polishing rare flows, and it keeps rare, risky actions away from accidental taps.

**Values:**
- Split visible vs deferred by frequency (task analysis, analytics, field studies). *(NN/g progressive disclosure)*
- Placement follows [[fitts-law]]: frequent → large and close (thumb zone on phones, edges and corners on desktop).
- Shortcuts: frequent desktop actions get keyboard shortcuts. Shown in menus and tooltips.

**Failure looks like:** "Compose" buried in an overflow menu while "Settings" sits in the tab bar. Destructive "Delete account" next to the frequent "Save". A game's most-used ability on the hardest-to-reach button. Navigation ordered by org chart instead of use.

**Detect in review:** Pull the event counts for the top 10 actions and map them to their location, size and tap depth; mismatches are findings. Check that rare, destructive actions sit at least one step away from frequent ones.

**Implementation:**
- Web: primary actions in the persistent header or toolbar; secondary actions in an overflow menu; `accesskey` or app shortcuts for power users.
- iOS: tab bar for the top 3–5 destinations; swipe actions for frequent row operations.
- Android: FAB for the single most frequent creation action; the nav bar for top destinations.
- Game UI: default keybinds and thumb positions for the most-used abilities, with remapping allowed.

**Related:** [[fitts-law]] · [[progressive-disclosure]] · [[hicks-law]] · [[touch-target]]
