---
type: component
description: "Label above, hint, ≥16px input, 3:1 boundary, error with icon + fix on blur, cleared on fix, sized to content"
aliases: [text input, input field, textarea, input, text box]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/form-design-placeholders/
  - https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
---
# Text field

**Use when:** free-form input (names, emails, amounts, notes). **Don't use when:** choosing from a known set (use [[components/select]], [[components/radio]] or [[components/combobox]]). Form-level rules (validation timing, field count) live in [[components/form]].

**Anatomy:** label → hint → container (prefix · input · suffix) → error (icon + text) · optional character counter.

**Required states:** default · hover · focus-visible · filled · error · disabled · read-only.

**Rules:**
- The label sits outside and above the field; placeholders are only examples → [[components/form]].
- The container boundary is ≥ 3:1 against the page (WCAG 1.4.11). Decorative alpha borders don't qualify → [[alpha-borders]].
- Error = icon + text explaining the fix, linked by `aria-describedby`; validate on blur, clear on fix.
- Field width matches the expected content (ZIP narrow, email wide).
- Grid and flex items need `min-width: 0`, or long content overflows into neighbors (component test #3).
- Counters and amounts use tabular digits → [[tabular-numbers]].

**Values:** input font ≥ 16px (iOS web zoom; [[platforms/web]]). Height 48px. Counter shown from the start on fields with `maxlength`.

**Platform variants:**
- iOS: `TextField` with `.textContentType` and a keyboard type per field.
- Android: M3 `OutlinedTextField` with `supportingText` and `isError`.
- Game UI: avoid free text on console. When it's needed, keep the field above the on-screen keyboard.

**Failure looks like:** Placeholder-only labels. Light-gray borders at 1.5:1. Red borders with no message. An amount field pushing into its neighbor. A disabled field users can't copy from (use read-only instead).

**Review checks:**
- [ ] Label above, outside the field
- [ ] Boundary ≥ 3:1 in light and dark
- [ ] Error has an icon, a fix and `aria-describedby`
- [ ] Inputs ≥ 16px; no overflow at 390px

Reference test: `~/Documents/github/ui-test/components/text-field`

**Related:** [[components/form]] · [[postels-law]] · [[contrast-ratio]]
