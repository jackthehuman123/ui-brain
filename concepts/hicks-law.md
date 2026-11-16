---
type: concept
description: "Decision time grows with equally weighted choices: cut, group or recommend; not for known-item lookup"
domain: interaction-and-state
aliases: [Hick's law, Hick-Hyman law, choice overload, decision time, too many options]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://lawsofux.com/hicks-law/
---
# Hick's law

**Rule:** When users must *choose* among options, every added equally weighted option slows the decision. Reduce the options, group them, or highlight a recommended default, especially at decision points like plans, onboarding and checkout.

**Why:** Comparing options costs time and causes hesitation or abandonment. A clear default turns a comparison into a confirmation.

**Values:**
- `RT = a + b · log₂(n + 1)` for n equally probable choices. *(Hick 1952; lawsofux)* Growth is logarithmic: going from 2 to 4 options costs as much as 8 to 16.
- It does **not** apply when users know what they want (known-item lookup in a long menu or alphabetical list). Then scanning and search matter, and a long well-ordered list can beat a nested one.
- Mark one recommended option ("Most popular") when options are comparable.

**Failure looks like:** Pricing with five equal tiers and no recommendation. Onboarding asking users to pick from 20 interests at once. A primary toolbar with 12 equal icons. Splitting a known list into many nested submenus "to reduce choices", which makes lookup slower.

**Detect in review:** Count the equal-weight options at each decision point. Flag decision screens with more than about 3–5 peers and no default (**unverified** threshold). Check that long lists are sorted and searchable rather than nested.

**Implementation:**
- Highlight one plan: a visual weight difference plus a "Recommended" label.
- Long option sets: search plus sensible ordering; see [[components/combobox]].
- Advanced options: [[progressive-disclosure]].
- Game UI: limit loadout or shop choices on first exposure, and unlock more over time.

**Related:** [[millers-law]] · [[progressive-disclosure]] · [[frequency-of-use]] · [[fitts-law]]
