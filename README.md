# MySen — Digital Experience & Operations Platform for Dam Sen Cultural Park

> **Course:** DBIZ2 — System Analysis & Design (Group F)  
> **Client / Domain:** Dam Sen Cultural Park (Phú Thọ Tourist Service JSC)  
> **Target Channels:** Visitor Mobile App (iOS/Android) & Partner/Admin Web Portal

---

## 1. Project Overview & Problem Statement

**MySen** is an integrated digital ecosystem designed to modernize the visitor experience and park operations at **Dam Sen Cultural Park** (Ho Chi Minh City). The platform addresses three core operational and visitor pain points:
1. **Ticketing & Entry Friction:** Eliminating manual ticket-booth queues via dynamic QR e-tickets integrated with **MoMo** and **VNPay** (`F-02`).
2. **Wayfinding & Real-Time Crowd Visibility:** Providing an interactive park map with live attraction status, walking directions, and queue wait times (`F-03`).
3. **Visitor Engagement & Partner Ecosystem:** Transforming passive sightseeing into an interactive heritage quest using **HMAC-signed QR plaques + GPS geofencing** (`F-04`), paired with loyalty coin rewards (`Xu`), F&B partner voucher redemption, and community sharing (`F-05`, `F-06`).

---

## 2. Repository Working Rules (Single Source of Truth)

To ensure full traceability for DBIZ3 implementation and academic review, all team members adhere to the following repository conventions:

1. **Lowercase Directory & File Paths:** All directories under `docs/` use lowercase kebab-case (`docs/activity/`, `docs/external-design/`, `docs/use-case/`). Only `README.md` and standardized ID prefixes (`ADR-`, `AD-UC-`, `SD-UC-`, `S-Fxx-yy`) use uppercase letters.
2. **Strict Traceability:** Every System Requirement (`SyR`) traces back to a Stakeholder Requirement (`StR`) in `cvca.md`; every Functional Requirement (`FR`) maps to Use Cases (`UC`), Activity Diagrams (`AD-UC`), Sequence Diagrams (`SD-UC`), and Screen Specs (`S-Fxx-yy`).
3. **Clear Transaction Separation:** Real-money purchases (**E-Tickets**, `F-02`) are strictly separated from loyalty-point exchanges (**Loyalty Vouchers** redeemed with `Xu`, `F-04`).
4. **Annotated Screens & Screen Rules:** Every `screen-spec-S-Fxx-yy.md` must include an annotated mockup (`img/<Screen-ID>-numbered.png`) matching column `#` in its Element Inventory, plus localized **Screen-Level Rules (`SR-nnn`)** and all UI states (*Default, Empty, Loading, Error, Success*).
5. **Design Token Compliance:** All wireframes and mockups strictly follow the colour palette, typography (`Be Vietnam Pro`), spacing, and WCAG 2.2 accessibility rules defined in `docs/external-design/ui-conventions.md`.

---

## 3. Repository Structure

```text
DBIZ2.Group-F.MySen/
├── README.md                                  # Master entry point & traceability index
└── docs/
    ├── project/
    │   └── w0-scope.md                        # Project scope, actors, Use Case & Screen inventory
    ├── context/
    │   ├── cvca.md                            # Customer Value Chain Analysis & Stakeholder Reqs (StR)
    │   └── context-diagram.md                 # System boundary, external APIs & Release 2 deferrals
    ├── architecture/
    │   ├── architecture.md                    # 3-Layer architecture & SyR-to-StR traceability matrix
    │   └── adr/
    │       ├── ADR-001-dual-channel-ui.md     # Mobile App (Visitors) vs. Web Portal (Admin/Partners)
    │       ├── ADR-002-oauth2-otp-auth.md     # Google OAuth 2.0 & SMS/Email OTP authentication
    │       ├── ADR-003-payment-webhooks.md    # Asynchronous MoMo & VNPay webhook reconciliation
    │       ├── ADR-004-streak-scheduler.md    # Timed job scheduler & FCM/APNs streak reminders
    │       └── ADR-005-qr-gps-anticheat.md    # HMAC-signed QR tokens + GPS geofence validation
    ├── function-list/
    │   └── w1-function-list.md                # Detailed FR-xx-yy specifications & EARS criteria
    ├── use-case/
    │   ├── use-case-diagram.md                # Master Use Case diagram & traceability table
    │   ├── SD-UC-01.md                        # Sequence: SSO / OTP Registration & Sign In
    │   ├── SD-UC-02.md                        # Sequence: E-Ticket Purchase & Payment Webhook
    │   ├── SD-UC-04.md                        # Sequence: Checkpoint QR Scan, GPS Check & Reward
    │   └── SD-UC-05.md                        # Sequence: Coin-to-Voucher Redemption & POS Scan
    ├── activity/
    │   ├── activity-index.md                  # Activity coverage matrix, Block 1 audit & object states
    │   └── AD-UC-01.md .. AD-UC-08.md         # Swimlane Mermaid activity diagrams & branch tests
    └── external-design/
        ├── ui-conventions.md                  # Design tokens, formats, WCAG rules & numbering map
        └── screens/
            ├── screen-spec-S-F00-01.md .. screen-spec-S-F06-01.md
            └── img/                           # 3x PNG mockups & *-numbered.png visual guides
```

---

## 4. Naming & ID Conventions

| Artifact Type | Pattern | Example | Description |
| :--- | :--- | :--- | :--- |
| **Stakeholder Req** | `StR-nn` | `StR-01` | Business/user need derived from `cvca.md` |
| **System Req** | `SyR-nn` | `SyR-04` | Technical/architectural requirement linked to `StR` |
| **Feature** | `F-nn` | `F-04` | Core functional module (`F-01` to `F-06`) |
| **Functional Req** | `FR-nn-mm` | `FR-04-02` | Atomic functional requirement (no `-FE`/`-BE` suffix) |
| **Use Case** | `UC-nn` | `UC-04` | User goal in `use-case-diagram.md` |
| **Activity Diagram** | `AD-UC-nn` | `AD-UC-04` | Swimlane workflow for a single `Must`/`Should` UC |
| **Sequence Diagram** | `SD-UC-nn` | `SD-UC-02` | System interaction & external API sequence |
| **Screen ID** | `S-Fnn-mm` | `S-F04-01` | UI screen specification & numbered mockup |
| **Screen Rule** | `SR-nnn` | `SR-001` | Localized UI validation/state rule inside a Screen Spec |
| **Architecture Decision** | `ADR-nnn` | `ADR-005` | Architectural trade-off & technical decision record |

---

## 5. Team Ownership Matrix

| Member | Primary Modules & Artifacts | Screen Specs Owned |
| :--- | :--- | :--- |
| **Nguyễn Hải Long** (Lead / Integrator) | `README.md`, `architecture.md`, `ADR-001`–`005`, `activity-index.md`, `F-04` (`UC-04`, `AD-UC-04`, `SD-UC-04`) | `S-F04-01`, `S-F04-02` |
| **Hiệp** | `context-diagram.md`, `F-01` Auth/Profile & `F-06` Admin Portal (`UC-01`, `UC-08`, `UC-09`, `SD-UC-01`) | `S-F00-01`, `S-F01-01`, `S-F06-01` |
| **Nguyệt Minh** | `F-02` E-Ticketing & Payment Integration (`UC-02`, `UC-10`, `AD-UC-02`, `SD-UC-02`) | `S-F02-01`, `S-F02-02`, `S-F02-03` |
| **Phúc An** | `w0-scope.md`, `F-03` Interactive Park Map & Wayfinding (`UC-03`, `AD-UC-03`) | `S-F03-01` |
| **Bảo Ngân** | `w1-function-list.md`, `F-04` Loyalty Streaks & Voucher Catalog (`UC-05`, `AD-UC-05`, `SD-UC-05`) | `S-F04-03`, `S-F04-04` |
| **Hương Ly** | `cvca.md`, `F-05` Social Gallery & Partner Space Rental (`UC-06`, `UC-07`, `AD-UC-06`, `AD-UC-07`) | `S-F05-01`, `S-F05-02` |

---

## 6. Package Status & Reading Order

Follow the reading order below to review the complete analysis and design package from business context down to UI specifications:

1. **Scope & Problem Context:**
   * [Project Scope & Inventory](docs/project/w0-scope.md)
   * [Customer Value Chain Analysis (CVCA)](docs/context/cvca.md)
   * [System Context Diagram](docs/context/context-diagram.md)
2. **Architecture & Technical Decisions:**
   * [3-Layer System Architecture & SyR Traceability](docs/architecture/architecture.md)
   * [ADR-005: Anti-Cheat QR & GPS Geofencing](docs/architecture/adr/ADR-005-qr-gps-anticheat.md)
3. **Requirements & Behavioral Flows:**
   * [Detailed Function List (`FR-01-01` .. `FR-06-04`)](docs/function-list/w1-function-list.md)
   * [Use Case Diagram & Overview](docs/use-case/use-case-diagram.md)
   * [Activity Diagram Index & Object States](docs/activity/activity-index.md)
   * Core Sequence Diagrams: [SD-UC-01](docs/use-case/SD-UC-01.md) | [SD-UC-02](docs/use-case/SD-UC-02.md) | [SD-UC-04](docs/use-case/SD-UC-04.md) | [SD-UC-05](docs/use-case/SD-UC-05.md)
4. **External Design (UI/UX Specifications):**
   * [UI Conventions, Design Tokens & Numbering Guide](docs/external-design/ui-conventions.md)
   * Featured Screen Specs: [S-F03-01 (Park Map)](docs/external-design/screens/screen-spec-S-F03-01.md) | [S-F04-01 (Quest Hub & QR Scanner)](docs/external-design/screens/screen-spec-S-F04-01.md) | [S-F04-02 (Storybook & Badge Unlock)](docs/external-design/screens/screen-spec-S-F04-02.md)