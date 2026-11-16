---
type: checklist
description: "Yes/no interaction checks: feedback timing, signifiers, disclosure, UX laws, placement"
domain: interaction-and-state
---
# Interaction and state review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Every input shows visual feedback within 100 ms; busy past 1 s, percent-done past 10 s → [[doherty-threshold]]
- [ ] Frequent reversible actions update optimistically and roll back visibly on failure → [[optimistic-update]]
- [ ] Everything clickable looks clickable, and nothing static does → [[affordance]]
- [ ] Frequent options are up front, rare ones one step away, and depth is ≤ 2 levels → [[progressive-disclosure]]
- [ ] Frequent and primary targets are large and close; hit areas extend beyond the visuals → [[fitts-law]]
- [ ] Decision points offer few equal-weight options or mark a recommended one → [[hicks-law]]
- [ ] Users never have to remember values across steps; long codes are chunked → [[millers-law]]
- [ ] Inputs accept messy but valid formats and normalize them → [[postels-law]]
- [ ] Navigation and controls follow platform conventions unless a tested reason exists → [[jakobs-law]]
- [ ] Placement and size follow measured usage frequency → [[frequency-of-use]]
- [ ] The task is judged by success and time, not by how polished the screen looks → [[aesthetic-usability-effect]]
