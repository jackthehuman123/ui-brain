---
type: component
description: "Select-only combobox: opens from trigger, full keyboard + typeahead, check marks selection, ~5–15 options"
aliases: [dropdown, select, picker, listbox, menu select, select-only combobox]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/combobox/examples/combobox-select-only/
---
# Select

**Use when:** picking one value from a short, known list (about 5–15 options, **unverified** range). **Don't use when:** there are 2–5 options visible at once (use [[components/radio]]), the list is long or searchable (use [[components/combobox]]), or you're triggering actions (use a menu).

**Anatomy:** label → trigger (current value + chevron) → popup listbox → options (check mark + label + optional meta).

**Required states:** closed · open · option active (`aria-activedescendant`) · selected · disabled · error.

**Rules:**
- APG select-only combobox: the trigger has `role="combobox"`, `aria-expanded`, `aria-controls`. ↓/Enter/Space open; arrows, Home and End move; typing jumps (typeahead); Enter selects; Escape closes; focus stays on the trigger.
- The popup grows from the trigger edge (`transform-origin: top`) and closes the same way → [[origin-aware-animation]]. A second click reverses mid-flight → [[interruptible-animation]].
- Selection is marked with a check, not only a tint. Option rows ≥ 44px → [[touch-target]].
- The popup is "raised": lighter in dark mode → [[dark-mode-depth]]. Option radius < popup radius → [[concentric-radius]].
- The chevron rotates with the motion token (respects reduced motion) → [[reduced-motion]].

**Values:** open ~200 ms ease-out, close shorter ([[animation-duration]]). Typeahead buffer resets after ~500 ms (**unverified**).

**Platform variants:**
- Web: a native `<select>` is fine when you don't need custom styling. Customizable `<select>` (`appearance: base-select`) where supported.
- iOS: `Picker` (menu style). Android: M3 `ExposedDropdownMenuBox` (read-only).
- Game UI: left/right cycling selectors suit controllers better than popups.

**Failure looks like:** A popup that scales from its center. Focus moving into the list so typeahead breaks. Selection shown only by background color. A chevron spinning with reduced motion on.

**Review checks:**
- [ ] Keyboard: open, move, typeahead, select, Escape, all from the trigger
- [ ] Popup origin at the trigger; reversible mid-animation
- [ ] Check mark on the selected option

Reference test: `~/Documents/github/ui-test/components/select`

**Related:** [[components/combobox]] · [[hicks-law]] · [[components/radio]]
