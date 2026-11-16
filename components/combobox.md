---
type: component
description: "Text input + filtered listbox for long or searchable option sets; APG roles and keys; native select for short lists"
aliases: [autocomplete, typeahead, autosuggest, searchable select, select with search, combo box]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/combobox/
---
# Combobox

**Use when:** users pick from a long or searchable set (countries, products, people, tags), or may type a value not in the list. **Don't use when:** there are only a few options. Use radio buttons for 2–5, a native `<select>` for a short known list (**unverified** threshold ~10–15 items).

**Anatomy:** label → text input (`role="combobox"`) → popup `listbox` of options → optional: clear button, toggle button, "no results" row, loading row.

**Required states:** closed · open with results · open loading · open with no results · option highlighted (`aria-activedescendant`) · value selected · error · disabled.

**Rules:**
- Focus stays in the input. Arrow keys move the highlight via `aria-activedescendant`; Enter accepts; Escape closes; Alt+↓ opens without moving. *(WAI-ARIA APG)*
- Set `aria-expanded`, `aria-controls` (while open) and `aria-autocomplete` (`list`/`both`). Mark the selected option `aria-selected="true"`. *(APG)*
- Matching tolerates case, accents and spacing → [[postels-law]]. Highlight the matched substring.
- The popup opens from the input → [[origin-aware-animation]]. Option rows meet [[touch-target]].
- The visible label sits outside the field → [[components/form]].

**Values:** async search debounce **unverified** ~150–250 ms; show a loading row past ~300 ms ([[doherty-threshold]]). Keep the list height ≤ ~5–8 rows on mobile so the keyboard doesn't cover it.

**Platform variants:**
- Web: a headless library (Radix, React Aria, Headless UI, Downshift) rather than a hand-rolled one.
- iOS: `.searchable(text:)` + `.searchSuggestions`. Android: M3 `ExposedDropdownMenuBox` (editable) or `SearchBar`.
- Game UI: avoid free text on console. Use a filtered grid with category tabs.

**Failure looks like:** Focus jumping into the list (breaks typing). The listbox hidden behind the mobile keyboard. Enter submitting the whole form. No "no results" state. Exact-case matching.

**Review checks:**
- [ ] Keyboard-only: open, move, select, close, all without leaving the input
- [ ] Screen reader announces the expanded state, option count and active option
- [ ] Loading and no-results states exist
- [ ] Usable at 390px with the keyboard open

**Related:** [[hicks-law]] · [[components/form]] · [[progressive-disclosure]]
