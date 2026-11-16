---
type: platform
description: "iOS/iPadOS constants: SF Pro tracking table, touch target, safe areas, text minimums"
platforms: [ios]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/typography
---
# iOS / iPadOS constants

## SF Pro tracking (iOS, iPadOS, visionOS) *(Apple HIG tracking table)*
| pt | 1/1000 em | pt |
|---|---|---|
| 11 | +6 | +0.06 |
| 12 | 0 | 0 |
| 13 | −6 | −0.08 |
| 15 | −16 | −0.23 |
| 16 | −20 | −0.31 |
| 17 | −26 | −0.43 |
| 19 | −24 | −0.45 |
| 20 | −23 | −0.45 |
| 22 | −12 | −0.26 |
| 24 | +3 | +0.07 |
| 28 | +14 | +0.38 |
| 34 | +12 | +0.40 |
| 48 | +8 | +0.35 |
| 64 | +4 | +0.22 |
| 80 | 0 | 0 |

macOS uses a separate table (e.g. 10pt +12, 13pt −6, 26pt +8). System text styles apply these automatically; use the table only for custom styles built on SF. Used by [[tracking]].

## Touch target
Minimum hit area **44×44 pt** for all controls. *(Apple HIG)*

## Safe area
SwiftUI and UIKit layouts respect safe areas by default. Use `.ignoresSafeArea()` on backgrounds only. Insets vary by device and orientation; read them from `GeometryProxy.safeAreaInsets` / `view.safeAreaInsets`, never hardcode them.

## Dark mode
Two background sets: **base** (dimmer) and **elevated** (brighter, used automatically for popovers and sheets). Use semantic colors (`systemBackground`, `secondarySystemBackground`).
