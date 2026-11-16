---
type: checklist
description: "Yes/no visual-detail checks: icon weight, edge fades, icon swaps, light consistency"
domain: iconography-and-visual-detail
---
# Iconography and visual detail review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Icons come from one family and match the stroke weight and cap height of adjacent text → [[matched-icon-weight]]
- [ ] Overflowing scrollers fade with a mask (not an overlay), only at edges with more content → [[masked-edges]]
- [ ] In-place icon state changes crossfade with blur and scale, at a fixed container size → [[blurred-icon-swaps]]
- [ ] All shadows, highlights and 3D renders share one light direction → [[consistent-light-source]]
