# Use Case Diagram: MySen Platform

Lesson 4 (Prof. Seki). Who wants MySen Platform to do what. Mermaid has no native UML use case diagram type, so the diagram below is drawn as a flowchart: actors on the outside, use cases (rounded) grouped by domain inside the system boundary. In a drawing tool, standard UML notation (stick figures, ovals, and `<<include>>` stereotypes) is used.

| Field | Value |
|---|---|
| Version | v2 |
| Actors | Park Visitor, Partner, Staff & Admin (primary); Payment Gateway (MoMo/VNPay), GPS Service, Push Provider (FCM/APNs) (secondary) |

## Diagram

```mermaid
flowchart LR
  %% Primary Actors
  VIS["Park Visitor"]
  PRT["Partner"]
  ADM["Staff & Admin"]

  %% System Boundary
  subgraph MYSEN["MySen Platform Boundary"]
    subgraph G1["UC-01 & UC-02: Auth & Ticketing"]
      UC_AUTH(["Register & Sign In (SSO/OTP)"])
      UC_BUY(["Purchase E-Ticket & Pay"])
      UC_REF(["Request Refund / Cancel"])
      UC_TKT(["Receive & Validate QR Ticket"])
    end

    subgraph G2["UC-03 & UC-04: Vouchers & Navigation"]
      UC_MAP(["View Park Map & Location"])
      UC_DIR(["Get Directions & Wait Times"])
      UC_RED(["Redeem Points for Voucher"])
      UC_OUT(["Redeem Voucher at Outlet"])
    end

    subgraph G3["UC-05 & UC-06: Gamification & Rewards"]
      UC_SCN(["Scan Checkpoint QR & Anti-cheat"])
      UC_STR(["Track Storyline Progress"])
      UC_CLM(["Claim Daily & Milestone Rewards"])
    end

    subgraph G4["UC-07 to UC-09: Operations & Analytics"]
      UC_RNT(["Submit Rental Request & Tour"])
      UC_SOC(["Post / View Social Gallery"])
      UC_CMP(["Manage Campaigns & Push"])
      UC_ANL(["View Analytics & Reconcile"])
    end
  end

  %% Secondary Actors (External Services)
  PAY["Payment Gateway<br>(MoMo/VNPay)"]
  GPS["GPS Service"]
  FCM["Push Provider<br>(FCM/APNs)"]

  %% Primary Actor Associations
  VIS --- UC_AUTH
  VIS --- UC_BUY
  VIS --- UC_REF
  VIS --- UC_TKT
  VIS --- UC_MAP
  VIS --- UC_DIR
  VIS --- UC_RED
  VIS --- UC_SCN
  VIS --- UC_STR
  VIS --- UC_CLM
  VIS --- UC_SOC

  PRT --- UC_OUT
  PRT --- UC_RNT

  ADM --- UC_CMP
  ADM --- UC_ANL

  %% Secondary Actor / <<include>> Relationships
  UC_BUY -.->|"&lt;&lt;include&gt;&gt;"| PAY
  UC_REF -.->|"&lt;&lt;include&gt;&gt;"| PAY
  UC_DIR -.->|"&lt;&lt;include&gt;&gt;"| GPS
  UC_SCN -.->|"&lt;&lt;include&gt;&gt;"| GPS
  UC_CMP -.->|"&lt;&lt;include&gt;&gt;"| FCM
```

The full use case inventory, with features and login rules, is W0 Table 1 in [w0-scope.md](../function-list/w0-scope.md).

## Sequence diagrams

One sequence diagram per core use case, at analysis level: the lifelines are the elements of the [physical design](../architecture/architecture.md).

| Use case | Sequence diagram | Status |
|---|---|---|
| UC-01 Register & Sign In | SD-UC-01 | Open: to be drawn (Owner: Hiệp) |
| UC-02 Purchase E-Ticket & Pay | [SD-UC-02](SD-UC-02.md) | Core flow (Owner: Nguyệt Minh) |
| UC-04 Scan Checkpoint QR & Gamification | [SD-UC-04](SD-UC-04.md) | Core flow (Owner: Long) |
| UC-05 Redeem Points for Voucher & Rewards | [SD-UC-05](SD-UC-05.md) | Core flow (Owner: Bảo Ngân) |
| UC-03, UC-06 to UC-09 | (optional / covered by activity diagrams) | Documented in [activity-index](../activity/activity-index.md) |

## Change log

| Version | When | Change | Why |
|---|---|---|---|
| v1 | Lesson 4 | Initial use cases across Auth, Ticketing, Map, Gamification, Social, and Admin | Baseline functional scope from CVCA and Context Diagram |
| v2 | Lesson 7 | Added `<<include>>` dependencies for GPS Service (QR anti-cheat) and Push Provider (FCM/APNs) | Activity modeling (`AD-UC-04`, `AD-UC-05`) required geofence verification and automated push alerts |
