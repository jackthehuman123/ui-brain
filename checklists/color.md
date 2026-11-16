---
type: checklist
description: "Yes/no color checks: OKLCH tokens, gamut, palettes, gradients, borders, dark-mode depth, contrast"
domain: color
---
# Color review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Color tokens are authored in OKLCH, with states derived by L shifts at fixed H → [[oklch]]
- [ ] Every token is inside sRGB, with P3 variants only under @media (color-gamut: p3) → [[oklch]]
- [ ] Relative-color state shifts clamp C at the new L → [[oklch]]
- [ ] Palette steps have monotonic L and single-peaked C, and each documented text pair is measured → [[oklch-palettes]]
- [ ] Gradients interpolate in Oklab (or a deliberate oklch hue arc) with no gray midpoints → [[oklch-gradients]]
- [ ] Decorative borders are translucent foreground color; control boundaries are solid and ≥ 3:1 → [[alpha-borders]]
- [ ] In dark mode every raised or selected surface is lighter than what's beneath it → [[dark-mode-depth]]
- [ ] White-background images on tinted surfaces use multiply (light mode only), isolated → [[multiply-blending]]
- [ ] All text and UI-boundary pairs pass contrast in light and dark, including text on imagery at its worst pixel → [[contrast-ratio]]
