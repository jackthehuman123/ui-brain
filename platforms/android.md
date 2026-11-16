---
type: platform
description: "Android/Material 3 constants: type-scale tracking tokens, touch target, insets"
platforms: [android]
status: draft
last_verified: 2026-11-16
sources:
  - https://github.com/material-components/material-components-android/blob/master/lib/java/com/google/android/material/typography/res/values/tokens.xml
---
# Android / Material 3 constants

## M3 type-scale tracking *(M3 tokens, letter spacing in em)*
| Role | Size (sp) | Tracking (em) | Tracking (sp) |
|---|---|---|---|
| Display Large | 57 | −0.0044 | −0.25 |
| Headline Large | 32 | 0 | 0 |
| Title Large | 22 | 0 | 0 |
| Body Large | 16 | +0.031 | +0.5 |
| Body Medium | 14 | +0.018 | +0.25 |
| Label Large | 14 | +0.007 | +0.1 |
| Label Small | 11 | +0.045 | +0.5 |

Used by [[tracking]].

## Touch target
Minimum **48×48 dp**. *(Material)*

## Insets / edge-to-edge
Apps targeting **SDK 35 (Android 15)** are drawn edge-to-edge by default. Call `enableEdgeToEdge()` and pad with `WindowInsets.safeDrawing` (or Scaffold padding values). The theme opt-out stops working at targetSdk 36 (third-party reports).

## Dark mode
M3 tonal surfaces: `surfaceContainerLowest`, `Low`, the default, `High`, `Highest`. These replace M2's elevation overlays (white at about 5% for 1dp up to 16% for 24dp).
