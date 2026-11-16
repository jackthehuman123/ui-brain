---
type: checklist
description: "Yes/no motion checks: interruptibility, easing, duration, stagger, origin, staging, principles"
domain: motion
---
# Motion review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] Every state animation retargets mid-flight with no jump, queue or input lockout → [[interruptible-animation]]
- [ ] Every property that changes with the state is transitioned → [[interruptible-animation]]
- [ ] Animations are defined between named states, not imperative chains → [[pose-to-pose]]
- [ ] Entering uses ease-out, exiting ease-in, linear only for loops, springs for gestures → [[easing]]
- [ ] Durations: ~100 ms feedback, 200–300 ms panels, exits shorter than entrances, nothing routine over 400 ms → [[animation-duration]]
- [ ] Stagger total ≤ ~300 ms, and it never replays on filter or sort → [[stagger]]
- [ ] Overlays grow from their trigger or attached edge and return there → [[origin-aware-animation]]
- [ ] Shared-element morphs move exactly one element and survive a back gesture mid-flight → [[shared-element-transition]]
- [ ] Only one prominent motion per transition, and backgrounds dim or freeze behind overlays → [[staging]]
- [ ] Taps never bounce; only gesture-driven motion overshoots → [[follow-through]]
- [ ] Press feedback starts on press, at a scale suited to the stakes → [[squash-and-stretch]]
- [ ] Wind-ups only precede big or irreversible actions, never frequent ones → [[anticipation]]
- [ ] Secondary motion is smaller and no longer than the primary → [[secondary-action]]
- [ ] Long diagonal moves travel on arcs → [[arcs]]
- [ ] Reduce-motion swaps movement for fades and keeps feedback → [[reduced-motion]]
