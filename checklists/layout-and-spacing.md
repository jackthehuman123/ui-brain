---
type: checklist
description: "Yes/no layout checks: layout stability, optical centering, nested radii"
domain: layout-and-spacing
---
# Layout and spacing review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Nothing moves after load without user input (images sized, slots reserved), and CLS ≤ 0.1 → [[layout-shift]]
- [ ] Animations move with transform, not top, left, width, height or margin → [[layout-shift]]
- [ ] Directional glyphs (play, arrows) and button labels look centered, not just box-centered → [[optical-center]]
- [ ] Nested rounded corners are concentric (inner = outer − gap) → [[concentric-radius]]
- [ ] Interactive and critical content sits inside safe areas in both orientations → [[safe-area]]
