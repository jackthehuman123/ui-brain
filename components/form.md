---
type: component
aliases: [forms, web form, input form, sign-up form, checkout form, form validation]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/form-design-placeholders/
  - https://baymard.com/blog/inline-form-validation
  - https://baymard.com/blog/checkout-flow-average-form-fields
  - https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose.html
  - https://www.w3.org/WAI/WCAG22/Understanding/redundant-entry.html
  - https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
  - https://www.w3.org/WAI/WCAG22/Understanding/error-identification.html
---
# Form

**Use when:** collecting input the system can't infer. **Don't use when:** you already know the value (prefill or skip it) or a single control would do (a toggle doesn't need a submit form).

**Anatomy:** visible label → optional hint → field → error message (in that order, stacked) · submit button with a verb label · optional: section headings, progress for multi-step flows.

**Required states (per field):** default · focus-visible · filled · error · disabled (avoid) · read-only. **Form:** submitting (button shows progress, input not lost) · submit failed · success.

**Rules:**
- Labels stay visible outside the field. Placeholders are hints only, never labels; they vanish on input and some screen readers skip them. *(NN/g)*
- Validate when the user leaves the field or submits, not on each keystroke. Remove the error **as soon as** the value is fixed. *(Baymard)*
- Errors say what's wrong and how to fix it, in text next to the field, linked with `aria-describedby`. *(WCAG 3.3.1, 3.3.3)*
- Ask only what you need, and never ask twice in one flow; reuse earlier answers. *(WCAG 3.3.7, Baymard)*
- Tag personal fields with `autocomplete` tokens so browsers and password managers can fill them. *(WCAG 1.3.5)*
- Never block paste or autofill on password or code fields. *(WCAG 3.3.8)*
- Size and type fields to their content (`type="email"`, `inputmode="numeric"`). A ZIP field shouldn't be full width.
- Controls meet the touch-target minimum → [[touch-target]], `platforms/`.

**Values:**
- Checkout: most sites need **8** fields; the 2024 average was **11.3**. *(Baymard 2024)*
- iOS web: input font-size **≥ 16px**, or Safari zooms in on focus. *(Practitioner consensus; no Apple doc found.)*

**Platform variants:**
- Web: `<label for>`, `autocomplete`, `inputmode`, `aria-invalid` + `aria-describedby` on error. Don't disable submit; validate on submit and move focus to the first error.
- iOS: `textContentType` (UIKit) / `.textContentType()` (SwiftUI) for autofill; set the keyboard type and return-key action per field.
- Android (Compose): `KeyboardOptions(keyboardType, imeAction)`; autofill via `semantics { contentType }` (check your Compose version).
- Game UI: avoid text entry where you can (Roblox `TextBox` raises an on-screen keyboard on mobile and console). Use pickers/steppers, and keep the field visible above the keyboard.

**Failure looks like:** Placeholder-only labels, so users forget what a field was. Red errors appearing while the first character is typed. Errors that stay after the fix. "Invalid input" with no guidance. A whole form wiped after a failed submit. Paste blocked on password.

**Review checks:**
- [ ] Every field has a visible label outside the input
- [ ] Validation fires on blur/submit, and errors clear on fix
- [ ] Error text explains the fix and is linked to its field
- [ ] Personal fields carry `autocomplete`; paste allowed on password and code fields
- [ ] Mobile web inputs are ≥ 16px
- [ ] No field asks for data already given or derivable

**Related:** [[combobox]] · [[progressive-disclosure]] · [[optimistic-update]] · [[touch-target]] · [[affordance]]
