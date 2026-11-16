---
type: checklist
description: "Yes/no accessibility checks: contrast, target size, motion, text spacing, forms"
domain: accessibility
---
# Accessibility review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Text ≥ 4.5:1 (large ≥ 3:1), UI boundaries and icons ≥ 3:1, in all states and themes → [[contrast-ratio]]
- [ ] Hit areas ≥ 44pt iOS / 48dp Android / 24px WCAG AA floor → [[touch-target]]
- [ ] Reduce-motion is honored, and auto-moving content over 5 s can be paused → [[reduced-motion]]
- [ ] The layout survives WCAG 1.4.12 text-spacing overrides → [[tracking]] · [[leading]]
- [ ] Form fields have visible labels, linked errors and autocomplete, and never block paste → [[components/form]]
- [ ] Comboboxes and custom widgets follow WAI-ARIA APG roles and keys → [[components/combobox]]
- [ ] Links and controls don't rely on color alone → [[affordance]]
