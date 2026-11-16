---
type: concept
description: "Keep interactive and critical content inside platform safe areas; backgrounds may bleed to the edges"
domain: platform-and-environment
aliases: [safe area insets, notch, display cutout, edge-to-edge, home indicator, GuiInset, TopbarInset]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.android.com/develop/ui/compose/system/setup-e2e
  - https://create.roblox.com/docs/reference/engine/enums/ScreenInsets
  - https://developer.mozilla.org/en-US/docs/Web/CSS/env
---
# Safe area

**Rule:** Backgrounds, images and scroll content extend to the screen edges. Text, controls and HUD elements stay inside the safe area, using the platform's live inset values, never hardcoded ones.

**Why:** Notches, rounded corners, home indicators, gesture bars and game top bars cover pixels. Hardcoded insets break on the next device or OS update.

**Values:** constants and APIs per platform live in [[platforms/web]], [[platforms/ios]], [[platforms/android]], [[platforms/roblox]] and [[platforms/unity]].
- Android 15+ apps that target SDK 35 are **forced edge-to-edge**, so content draws under the system bars until insets are applied. *(Android docs)*
- The Roblox top bar inset reads 58px on current clients, but it changes by device and menu state, so read `GuiService.TopbarInset` at runtime.

**Failure looks like:** A bottom tab bar hidden under the iPhone home indicator. Header buttons in the notch in landscape. An Android app on API 35 with its toolbar under the status bar. A Roblox currency counter overlapping the Roblox menu button.

**Detect in review:** Screenshot on a notched phone in **both orientations** and on a gesture-nav Android device. In code: magic numbers (`44`, `34`, `58`) used as offsets; `viewport-fit=cover` without any `env(safe-area-inset-*)`; Roblox `IgnoreGuiInset = true` with HUD content in the top 60px.

**Implementation:**
- Web: `<meta name="viewport" content="…, viewport-fit=cover">`; `padding-bottom: max(16px, env(safe-area-inset-bottom))`.
- iOS: SwiftUI respects the safe area by default; use `.ignoresSafeArea()` only on backgrounds.
- Android: `enableEdgeToEdge()` + `Modifier.windowInsetsPadding(WindowInsets.safeDrawing)` or Scaffold padding.
- Roblox: `ScreenGui.ScreenInsets = CoreUISafeInsets` (the default) for HUD.
- Unity: fit the root panel to `Screen.safeArea` and re-apply on resolution change.

**Related:** [[dynamic-viewport]] · [[touch-target]]
