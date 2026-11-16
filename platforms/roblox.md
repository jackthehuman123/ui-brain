---
type: platform
description: "Roblox UI constants: TopbarInset, ScreenInsets modes, scaling rules, text/font limits"
platforms: [roblox]
status: draft
last_verified: 2026-11-16
sources:
  - https://create.roblox.com/docs/reference/engine/enums/ScreenInsets
  - https://create.roblox.com/docs/reference/engine/classes/GuiService
  - https://create.roblox.com/docs/reference/engine/classes/TweenService
---
# Roblox constants

## Insets
- `ScreenGui.ScreenInsets`: `CoreUISafeInsets` (default; clear of device cutouts **and** the Roblox top bar) · `DeviceSafeInsets` (cutouts only) · `TopbarSafeInsets` (the area inside the top bar) · `None`.
- The top bar inset reads **58px** in Roblox's `GetInsetArea` sample and current clients, but it varies by device and menu state. Read `GuiService.TopbarInset` and listen for changes; don't hardcode it. TopbarSafeInsets is reported wrong on some consoles (DevForum).

## Scaling
- Size and position HUD with **Scale** (UDim2 scale components) plus `UIAspectRatioConstraint`, not Offset. Use `UIScale` for global sizing. Test on phone, tablet, desktop and console (10-foot) views.

## Text
- No letter-spacing or kerning control and no OpenType features: pick fonts accordingly, use a monospace font for numbers, and image labels for wordmarks.
- `TextLabel.LineHeight` is a multiplier.

## Animation
- `TweenService`: a new tween on the same property cancels the old one. Tweens take no initial velocity.

## Blend modes
- None for GUI objects; bake effects into image assets.
