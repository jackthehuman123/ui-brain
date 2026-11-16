---
type: component
description: "Native dialog: focus trap, Escape, focus returns; scrim; exit faster than enter; destructive focuses Cancel"
aliases: [dialog, modal dialog, alert dialog, confirmation dialog, popup]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog
---
# Modal

**Use when:** a decision or short task must be completed before continuing (confirm, a short form). **Don't use when:** the info is non-blocking (use [[components/toast]]), the action is reversible (do it and offer undo; see [[optimistic-update]]), or the content is long (use a page or sheet).

**Anatomy:** scrim → container → title → description/body → actions (least destructive first in focus order) → optional close (×).

**Required states:** opening · open · closing · (form) submitting/error.

**Rules:**
- Web: `<dialog>.showModal()` gives top layer, inert background, Escape and focus restoration. `aria-labelledby` + `aria-describedby`.
- Initial focus goes on the least destructive action (Cancel) for destructive dialogs, otherwise the first field. Focus returns to the trigger on close.
- Scrim + optional blur; background motion pauses; page scroll locked → [[staging]].
- Enter ~220 ms ease-out with scale 0.96 → 1; exit ~150 ms ease-in → [[animation-duration]], [[easing]].
- Destructive dialogs don't close on a scrim click (only Cancel, × or Escape). Name the object in the title ("Delete 'Karakoram 2026'?").
- The dialog surface is the most elevated layer → [[dark-mode-depth]].

**Values:** width ~min(440px, 100vw − 32px). Title ≤ 2 lines. Buttons ≥ 44px.

**Platform variants:**
- iOS: `.alert` for binary confirms, `.confirmationDialog` for action sheets, `.sheet` for tasks.
- Android: M3 `AlertDialog`; full-screen dialogs for longer tasks.
- Game UI: pause gameplay input under modals; B/Escape cancels; the default focus avoids the destructive option.

**Failure looks like:** "Are you sure?" for every delete instead of undo. Focus left on the page behind. A scrim click that discards a half-filled form. Same-speed enter and exit. A title that says "Confirm" without naming what.

**Review checks:**
- [ ] Opens modal; focus inside on the safest action; Escape closes
- [ ] Focus returns to the trigger; scroll locked; scrim present
- [ ] Exit faster than enter

Reference test: `~/Documents/github/ui-test/components/modal`

**Related:** [[staging]] · [[components/button]] · [[components/toast]]
