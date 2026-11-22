# Sequence Diagram: SD-UC-04 Scan Checkpoint QR & Gamification

Lesson 4, analysis level: how the parts of MySen talk to each other when a visitor scans a physical checkpoint QR code to verify proximity (`ADR-005`), unlock a story chapter, and earn XP and badges. The visitor's choices and fallback manual entry flow are shown in the activity diagram [AD-UC-04](../activity/AD-UC-04.md).

| Field | Value |
| --- | --- |
| Use case | UC-04 Scan Checkpoint QR & Gamification |
| Version | v1.0 |
| FRs | FR-04-01 to FR-04-05 |

## Diagram

```mermaid
sequenceDiagram
  actor Visitor as Park Visitor
  participant App as MySen Mobile App
  participant GPS as Device GPS / Location API
  participant Game as Gamification & Loyalty Service
  participant CheckIn as Park Check-in System
  participant DB as MySen Database

  Visitor->>App: Open Quest Hub (S-F04-01) & scan checkpoint QR
  App->>GPS: Request current device coordinates
  GPS-->>App: Return latitude & longitude
  App->>Game: Submit HMAC-signed QR token + GPS coordinates

  Game->>CheckIn: Verify QR signature & geofence radius (ADR-005)
  CheckIn-->>Game: Validation result (VALID / OUT_OF_RANGE / INVALID_QR)

  alt Validation == VALID
    Game->>DB: Check if checkpoint already completed by visitor
    DB-->>Game: Checkpoint status (NEW)
    Game->>DB: Record check-in, award XP & unlock badge
    DB-->>Game: Updated quest progress, XP & badge record
    Game-->>App: Return story chapter content & badge unlock reward
    App-->>Visitor: Display Storybook Reader (S-F04-02) & Badge Modal (M-F04-01)
  else Validation != VALID
    Game-->>App: Return validation error reason
    App-->>Visitor: Show error alert or manual checkpoint code prompt
  end
```

## Notes

* **Lifelines:** Align directly with the elements in [architecture.md](../architecture/architecture.md) and external entities in [context-diagram.md](../context/context-diagram.md).
* **Anti-cheat Security:** Both the cryptographic QR signature and GPS geofence must pass before XP or badges are credited (`ADR-005`).