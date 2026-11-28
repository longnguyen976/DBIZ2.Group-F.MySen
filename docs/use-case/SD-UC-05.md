# Sequence Diagram: SD-UC-05 Redeem Points for Voucher & Rewards

Lesson 4, analysis level: how the parts of MySen talk to each other when a visitor exchanges earned loyalty coins for an F&B voucher and redeems it at a partner booth. Automated daily streak resets and reminders (`ADR-004`) are shown in the activity diagram [AD-UC-05](../activity/AD-UC-05.md).

| Field | Value |
| --- | --- |
| Use case | UC-05 Redeem Points for Voucher & Rewards |
| Version | v1.0 |
| FRs | FR-04-06 to FR-04-10 |

## Diagram

```mermaid
sequenceDiagram
  actor Visitor as Park Visitor
  participant App as MySen Mobile App
  participant Game as Gamification & Loyalty Service
  participant DB as MySen Database
  participant PartnerPOS as F&B Partner Voucher Service / POS
  actor Partner as Commercial Partner

  %% Phase 1: Exchange Loyalty Coins for Voucher
  Visitor->>App: Browse Voucher Catalog (S-F04-04) & select reward
  App->>Game: Request voucher exchange (userId, voucherTemplateId)
  Game->>DB: Verify coin balance & voucher stock availability
  DB-->>Game: Sufficient balance & stock confirmed

  alt Sufficient Coins & Stock
    Game->>DB: Deduct loyalty coins & create ISSUED voucher record
    DB-->>Game: Voucher ID & signed QR payload
    Game-->>App: Return active voucher QR code
    App-->>Visitor: Display voucher QR in My Vouchers wallet
  else Insufficient Coins or Out of Stock
    Game-->>App: Return rejection reason
    App-->>Visitor: Display insufficient balance / unavailable notice
  end

  %% Phase 2: Redeem Voucher at Partner Booth
  Visitor->>Partner: Present voucher QR code at F&B outlet
  Partner->>PartnerPOS: Scan voucher QR code
  PartnerPOS->>Game: Submit voucher redemption request
  Game->>DB: Validate voucher status (ISSUED & not expired)
  DB-->>Game: Valid voucher confirmed
  Game->>DB: Mark voucher status as REDEEMED
  DB-->>Game: Redemption timestamp saved
  Game-->>PartnerPOS: Confirm valid redemption
  PartnerPOS-->>Partner: Approve discount / F&B item handover
  Game-->>App: Push redemption confirmation to visitor
```

## Notes

* **Lifelines:** Align directly with the elements in [architecture.md](../architecture/architecture.md) and external entities in [context-diagram.md](../context/context-diagram.md).
* **Separation of Concerns:** Loyalty coin voucher redemption (`UC-05`) is strictly separated from real-money e-ticket purchases (`UC-02`).