# ADR-005: Validate HMAC-signed QR tokens with GPS geofencing for checkpoints

| Field | Value |
|---|---|
| Status | Accepted (after Lesson 7) |
| Date | Lesson 7 |

**Context.** During checkpoint exploration (`AD-UC-04`), visitors scan QR codes placed at physical park landmarks to earn XP, badges, and redeemable loyalty coins (`FR-04-02-BE`). Static, predictable QR codes could be photographed and shared remotely, allowing users outside the park to farm rewards unfairly.

**Decision.** Require every checkpoint QR code to embed an HMAC-signed checkpoint token, and validate both the cryptographic signature and the visitor's real-time GPS coordinates against a configured geofence radius around the landmark before unlocking storybooks or crediting rewards.

**Consequences.** Remote QR sharing and replay spoofing are prevented, preserving the economic integrity of loyalty coins and F&B vouchers. Visitors must grant location permission when scanning, and the system provides a fallback manual code entry flow when camera conditions are poor.