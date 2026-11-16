---
type: concept
description: "Accept input liberally (spaces, case, formats, paste) and normalize it yourself; output in one strict format"
domain: interaction-and-state
aliases: [Postel's law, robustness principle, input tolerance, forgiving formats, input normalization]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://lawsofux.com/postels-law/
  - https://datatracker.ietf.org/doc/html/rfc761
---
# Postel's law

**Rule:** Be liberal in what you accept from users and strict in what you produce. Accept phone numbers with spaces or dashes, emails with stray whitespace or capitals, dates in common formats, and pasted values with extra characters, then normalize them yourself. Reject only what you truly can't interpret, and say how to fix it.

**Why:** Users type the way they think and paste from anywhere. Rejecting reasonable input for formatting reasons is the system's failure, and a top cause of form errors.

**Values:**
- Origin: the "robustness principle" in RFC 761 (TCP, 1980): "be conservative in what you do, be liberal in what you accept from others". *(RFC 761; lawsofux)*
- Normalize: trim whitespace; lowercase emails' domains; strip spaces and dashes from card and phone numbers; accept `,` or `.` decimal separators per locale.
- Still validate meaning: tolerance is about format, not about accepting wrong data.

**Failure looks like:** "Phone number must not contain spaces". Card fields that reject pasted numbers with spaces. Date fields accepting only `MM/DD/YYYY` with no hint. Password fields that block paste (also a WCAG 3.3.8 failure). Search that fails on a trailing space.

**Detect in review:** Paste messy but valid input into every field: leading and trailing spaces, mixed case, separators, full-width digits. In code: regexes that encode formatting instead of meaning; `maxlength` that blocks pasted values containing separators.

**Implementation:**
- Web: normalize on `blur`/submit, not on each keystroke (which moves the caret). Use `inputmode="numeric"` instead of `type="number"` for codes and cards.
- iOS/Android: keep formatting masks forgiving, and allow paste of formatted strings.
- Game UI: chat commands and codes accept case-insensitive input with flexible whitespace.

**Related:** [[components/form]] · [[millers-law]] · [[jakobs-law]]
