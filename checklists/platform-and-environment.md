---
type: checklist
description: "Yes/no platform checks: safe areas, viewport units, platform constants"
domain: platform-and-environment
---
# Platform and environment review pass

Answer each item yes/no. Every "no" is a finding; open the linked note for values and fixes.

- [ ] No hardcoded inset numbers; live safe-area APIs are used on every platform → [[safe-area]] · [[platforms/web]] · [[platforms/roblox]] · [[platforms/unity]]
- [ ] Android SDK 35+ builds apply insets after edge-to-edge → [[safe-area]] · [[platforms/android]]
- [ ] Full-height web sections use svh (or dvh for app shells), never bare 100vh → [[dynamic-viewport]]
- [ ] Roblox HUD uses CoreUISafeInsets and Scale sizing, and reads TopbarInset at runtime → [[platforms/roblox]]
- [ ] Touch targets meet the platform minimum on each shipped platform → [[touch-target]]
