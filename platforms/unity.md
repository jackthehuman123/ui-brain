---
type: platform
description: "Unity UI constants: Screen.safeArea, CanvasScaler setup, TextMeshPro spacing units"
platforms: [unity]
status: draft
last_verified: 2026-11-16
sources:
  - https://docs.unity3d.com/ScriptReference/Screen-safeArea.html
  - https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.2/manual/RichTextCharacterSpacing.html
---
# Unity constants

## Safe area
`Screen.safeArea` returns a pixel `Rect`. Fit the root panel's anchors to it and re-apply on resolution and orientation change.

## Scaling
`CanvasScaler` → *Scale With Screen Size*: set a reference resolution and a Match (width↔height) value. Test the narrowest and widest aspect ratios you ship.

## TextMeshPro units
- Inspector Character, Word, Line and Paragraph spacing: **1 = 0.01em** (since TMP 2.1).
- Rich text tags take real units: `<cspace=0.05em>`, `<mspace=0.6em>` (monospace digits), `<line-height=…>`.

## Animation
`Mathf.SmoothDamp` / `Vector3.SmoothDamp` carry `ref currentVelocity`, so they retarget without a jump.
