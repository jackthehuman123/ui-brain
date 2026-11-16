---
type: component
description: "Non-blocking status: pre-existing live region, one at a time, ~5 s (~10 s with action), pause on hover, undo"
aliases: [snackbar, notification, flash message, alert banner, transient message]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html
  - https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable.html
---
# Toast

**Use when:** confirming a completed action or reporting a non-blocking status, often with Undo. **Don't use when:** the user must decide something (use [[components/modal]]), or the error belongs to a field (inline error; see [[components/text-field]]).

**Anatomy:** live region (always in the DOM) → toast (message · optional single action · dismiss).

**Required states:** entering · shown · paused (hover/focus) · leaving · queued.

**Rules:**
- The live region (`role="status"`, `aria-live="polite"`) exists before any message is inserted (WCAG 4.1.3). Use `role="alert"` only for urgent errors.
- One toast at a time; the rest queue → [[staging]].
- Auto-dismiss, but pause while hovered or focused, and allow manual dismiss (WCAG 2.2.1).
- At most one action, usually Undo, which replaces "Are you sure?" → [[optimistic-update]].
- Enters from its edge and leaves faster → [[origin-aware-animation]], [[animation-duration]]. Clears the bottom safe area → [[safe-area]].

**Values:** ~5 s plain, ~10 s with an action (**unverified**; Material's 4–10 s range is unconfirmed this session). Enter ~220 ms, exit ~150 ms. Width ≤ 440px.

**Platform variants:**
- iOS: no system toast. Use a custom banner, or inline confirmation for important results.
- Android: M3 `Snackbar` via `SnackbarHostState` (queues automatically).
- Game UI: notification feed in a corner, queued, never covering critical HUD; achievements stack with a cap.

**Failure looks like:** Three toasts stacked at once. An Undo that vanishes in 2 s. A live region created together with the message (not announced). Toasts covering the bottom nav or home indicator. Errors that only appear in a toast and are then gone.

**Review checks:**
- [ ] Live region pre-exists; one visible at a time
- [ ] Hover/focus pauses; dismiss button ≥ 44px
- [ ] Undo restores state; exit faster than enter

Reference test: `~/Documents/github/ui-test/components/toast`

**Related:** [[optimistic-update]] · [[staging]] · [[components/modal]]
