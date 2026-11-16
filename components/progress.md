---
type: component
description: "Determinate when total known (percent, count, ETA); spinner only for unknown waits past ~300 ms"
aliases: [progress bar, spinner, loader, loading indicator, activity indicator]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/response-times-3-important-limits/
  - https://www.w3.org/WAI/ARIA/apg/practices/range-related-properties/
---
# Progress

**Use when:** showing that work is happening. Use a determinate bar when the total is known, and a spinner (indeterminate) when it isn't. **Don't use when:** the wait is under ~300 ms (show nothing), or content structure is known (use a skeleton sized like the content; see [[layout-shift]]).

**Anatomy:** label → bar (track + fill) → value text (count · percent · time left) · or spinner + status text.

**Required states:** hidden (fast) · indeterminate · determinate (0–100) · complete · error/paused.

**Rules:**
- `role="progressbar"` with `aria-valuenow/min/max` plus a human `aria-valuetext` ("5 of 8 files, 63%").
- Spinners appear only after ~300 ms so fast responses never flash. Past ~1 s, show a busy state; past ~10 s, show percent-done and time left → [[doherty-threshold]].
- Fill moves with `transform: scaleX()` on the motion token → [[layout-shift]], [[reduced-motion]].
- Spinner rotation is linear and infinite (the only place linear easing belongs) → [[easing]]. Under reduced motion it becomes an opacity pulse.
- Numbers tabular → [[tabular-numbers]]. The loading message is a `role="status"` live region with text.

**Values:** spinner delay ~300 ms (**unverified** practice); NN/g limits 0.1 / 1 / 10 s. Bar height 4–8px with a track boundary ≥ 3:1 if the bar conveys information → [[contrast-ratio]].

**Platform variants:**
- iOS: `ProgressView(value:)` / `ProgressView()`.
- Android: M3 `LinearProgressIndicator(progress = …)` / `CircularProgressIndicator()`.
- Game UI: loading screens show a percent plus tips; long installs show size and time left; never a fake progress bar that stalls at 99%.

**Failure looks like:** A spinner flashing for 100 ms on every click. A 12-second export with only a spinner. A bar that animates `width`, causing layout work. A percent that jitters in width. A spinner still rotating under reduced motion.

**Review checks:**
- [ ] No spinner for waits < 300 ms
- [ ] Determinate with value text when the total is known; ETA past 10 s
- [ ] Transform-only fill; reduced-motion pulse

Reference test: `~/Documents/github/ui-test/components/progress`

**Related:** [[doherty-threshold]] · [[components/button]] (loading state) · [[optimistic-update]]
