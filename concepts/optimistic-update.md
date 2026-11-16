---
type: concept
description: "Update instantly for reversible, high-success actions; sync in background; on failure roll back visibly"
domain: interaction-and-state
aliases: [optimistic UI, useOptimistic, instant feedback, latency hiding, rollback]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/response-times-3-important-limits/
  - https://react.dev/reference/react/useOptimistic
---
# Optimistic update

**Rule:** For actions that almost always succeed and are easy to reverse (like, add to cart, reorder, rename, toggle), update the UI immediately and sync in the background. On failure, roll back visibly with a reason and a retry. Never be optimistic about payments, deletes without undo, or anything with side effects others can see.

**Why:** Responses within 0.1 s feel instantaneous and 1 s keeps flow *(NN/g)*. Network round trips often exceed both, so waiting for the server makes every tap feel heavy.

**Values:**
- Target: the visual response within **0.1 s** of input *(NN/g)*; see [[doherty-threshold]].
- Eligibility: **unverified**, server success rate ≥ ~99% and an action that can be undone.
- Failure: restore the previous state **and** say so (toast or inline), keeping the user's input.

**Failure looks like:** A heart that fills, then silently un-fills five seconds later. A cart badge showing 3 when the server has 2. A spinner on a checkbox. An optimistic "Payment sent" that later fails.

**Detect in review:** Throttle the network to Slow 3G and tap each frequent action: is the UI instant? Then block the request (devtools offline): does it roll back with a message? In code: `await fetch()` before `setState` for toggles; rollback paths with no user-facing message.

**Implementation:**
- Web: React `useOptimistic`, TanStack Query `onMutate` / `onError` rollback, SWR `optimisticData`.
- iOS: update the model synchronously, revert in the `catch`, and show a banner.
- Android: update the `StateFlow` first, revert on `Result.failure`, and show a `Snackbar` with a retry action.
- Game UI: client-predict currency and inventory changes; the server corrects with a visible adjustment, never a silent change.

**Related:** [[doherty-threshold]] · [[layout-shift]] · [[interruptible-animation]]
