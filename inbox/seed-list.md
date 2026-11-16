---
type: inbox
---
# Phase 2 seed list (awaiting template approval)

## Original list
kerning · optical center · tabular numbers · layout shift · tracking ✅ · optimistic update · x-height · touch target · leading · origin-aware animation · OKLCH ✅ · widow · safe area · stagger · line length · affordance · combobox · interruptible animation ✅ · progressive disclosure · shared element transition · concentric radius · alpha borders · OKLCH palettes · OKLCH gradients · matched icon weight · masked edges · blurred icon swaps · dark mode depth · dynamic viewport · multiply blending

## Added 2026-11-16: animation principles (→ motion)
squash and stretch · anticipation wind-up · staging the focus · pose to pose · follow through · slow in and slow out · moving in arcs · secondary action · snappy timing · exaggerated feedback · solid drawing in 3D · overall appeal

Proposed merges (to confirm in Phase 2, after research):
- **slow in / slow out** → `easing` (UI curves and durations; strong candidate)
- **snappy timing** → `animation-duration` (per-size and per-distance ranges from M3/HIG)
- **squash and stretch + exaggerated feedback** → one note on press/impact feedback (scale on press; game-UI juice)
- **follow through + secondary action** → possibly one note (overshoot, settle, trailing elements)
- **pose to pose, solid drawing in 3D, overall appeal**: weak fit for app UI. Likely sections in a game-UI note or candidates only. Kept off the core list unless research finds concrete UI values.

## Added 2026-11-16: UX laws (domain TBD)
Fitts's law · bigger hit areas · Hick's law · Miller's law · Doherty threshold · Postel's law · Jakob's law · frequency of use

Proposed placement:
- **Fitts's law + bigger hit areas** → `fitts-law` with a link to `touch-target` (hit area ≠ visual size; constants live in `platforms/`)
- **Doherty threshold** → interaction-and-state (400 ms response target; relates to optimistic update)
- **Hick's, Miller's, Jakob's, Postel's laws and frequency of use** → either interaction-and-state, or a new `ux-laws` domain (decision for the owner)
- Caution: Miller's law (7±2) is widely misapplied to menu length. The note must say what it does *not* justify.

## Status 2026-11-16: Phase 2 complete
All seed terms are written as concept notes, except:
- **combobox** → `components/combobox.md` (component layer)
- **bigger hit areas** → merged into `fitts-law`
- **exaggerated feedback** → merged into `squash-and-stretch`
- **slow in and slow out** → `easing` · **snappy timing** → `animation-duration` · **staging the focus** → `staging` · **moving in arcs** → `arcs`
- **solid drawing in 3D** → `consistent-light-source` · **overall appeal** → `aesthetic-usability-effect`
- **OKLCH palettes / gradients** → separate notes `oklch-palettes`, `oklch-gradients`
- Added from the harvests: `contrast-ratio`, `font-loading`, `reduced-motion`
