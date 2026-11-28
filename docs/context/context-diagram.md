# Context Diagram: MySen Platform

Lesson 3. MySen Platform is one black box in the middle (covering scope F-01 to F-06 across the mobile app, partner screens, and admin back-office); around it are the external entities (people, organisations, and external systems/services) it exchanges data with. The Context Diagram answers "what does the system interact with?"; the [Use Case Diagram](../use-case/use-case-diagram.md) answers "who wants the system to do what?".

| Field | Value |
|---|---|
| Version | v2 |
| Built from | [CVCA](cvca.md): every stakeholder and external service that exchanges information with MySen Platform |

## Diagram

```mermaid
flowchart LR
  %% System under development
  MYSEN(("MySen Platform<br>(mobile app, partner screens<br>& admin back-office)"))

  %% External entities: people & organisations
  VIS["Visitor / GenZ Customer"]
  PRT["F&B / Retail / EdTech Partners"]
  ART["Indie Artists & Creators"]
  DSP["DSP Management & Departments<br>(incl. Operations Staff)"]
  MKT["Marketing & Sales Dept"]
  IT["IT & Technical Dept"]
  GOV["Government Authorities<br>(deferred to Release 2)"]

  %% External entities: systems & services
  AUTH["Google Identity<br>(OAuth 2.0 / OpenID Connect)"]
  MSG["Messaging Providers<br>(SMS / Email / Push: FCM, APNs)"]
  PAY["Payment Gateway<br>(MoMo / VNPay)"]
  FNB["F&B Partner Voucher<br>(Service / POS)"]
  MAP["Map SDK &<br>(GPS / Beacon Service)"]
  CHK["Park Check-in System"]
  CDN["Cloud Storage / CDN"]
  SUB["Subsidiary & Tourism Systems<br>(Sai Gon-Da Lat JSC, Dam Sen Water Park)"]

  %% Flows: People & Organisations
  VIS -->|"registration, sign-in & profile data;<br>orders, map & search requests;<br>QR scans, reward claims, posts"| MYSEN
  MYSEN -->|"e-tickets & vouchers, map info,<br>coins, rewards, notifications"| VIS

  PRT -->|"rental-space requests,<br>service listings & promotions"| MYSEN
  MYSEN -->|"request status & notifications"| PRT

  ART -->|"performance schedule submissions"| MYSEN
  MYSEN -->|"approval / conflict notices"| ART

  DSP -->|"park content, ticket catalogue,<br>wait times, compliance rules"| MYSEN
  MYSEN -->|"compliance reports, revenue<br>reconciliation, ops notices"| DSP

  MKT -->|"campaigns, promotion codes,<br>push content & audience"| MYSEN
  MYSEN -->|"visitor-flow & revenue<br>dashboards, campaign status"| MKT

  IT -->|"role assignments, deployment<br>& monitoring configuration"| MYSEN
  MYSEN -->|"audit log, health alerts"| IT

  GOV -.->|"regulations & licences (auto-sync)"| MYSEN
  MYSEN -.->|"compliance reports (auto-submit)"| GOV

  %% Flows: Systems & Services
  MYSEN -->|"sign-in request (OAuth 2.0)"| AUTH
  AUTH -->|"ID token, identity assertion"| MYSEN

  MYSEN -->|"OTP messages, push notifications"| MSG
  MSG -->|"delivery status, invalid tokens"| MYSEN

  MYSEN -->|"payment & refund requests"| PAY
  PAY -->|"payment result, refund result,<br>settlement data"| MYSEN

  MYSEN -->|"availability query, voucher<br>request, redemption result"| FNB
  FNB -->|"availability, voucher code,<br>redemption requests"| MYSEN

  MYSEN -->|"map, POI & route requests"| MAP
  MAP -->|"map layers, coordinates,<br>walking routes"| MYSEN

  CHK -->|"check-in data (user, location, time)"| MYSEN
  MYSEN -->|"validation result"| CHK

  MYSEN -->|"uploaded gallery media"| CDN
  CDN -->|"stored-media URLs"| MYSEN

  MYSEN -->|"package, availability &<br>booking requests"| SUB
  SUB -->|"package details, availability,<br>booking status"| MYSEN
```

Time is not an external entity: timed behaviour (such as midnight daily streak resets and scheduled campaign notifications) is modelled as time-triggered flows in the Use Case and Activity Diagrams. Direct automated sync with Government Authorities is marked as deferred (`Won't-have` in Release 1).

## Data crossing the boundary

These are the core data groups exchanging across the system boundary, aligned with [W0 Scope](../function-list/w0-scope.md).

| Data group | Kept by | Reaches MySen Platform from |
|---|---|---|
| User accounts, roles & profiles | MySen Platform & Google Identity (read-only OAuth) | Visitor / GenZ Customer, Google Identity, IT & Technical Dept |
| E-tickets, orders & payment settlements | MySen Platform | Visitor / GenZ Customer, DSP Management, Payment Gateway (MoMo / VNPay) |
| Park map layers, POIs & wait times | MySen Platform & Map SDK | DSP Management & Operations Staff, Map SDK & GPS/Beacon Service |
| Quests, check-ins, XP, coins & badges | MySen Platform | Visitor / GenZ Customer, Park Check-in System |
| F&B loyalty vouchers & redemptions | MySen Platform & F&B Partner Voucher Service | Visitor / GenZ Customer, F&B Partner Voucher Service / POS |
| Social gallery media & community posts | MySen Platform & Cloud Storage / CDN | Visitor / GenZ Customer, Cloud Storage / CDN |
| Partner rentals, schedules & tour packages | MySen Platform & Subsidiary Systems | F&B / Retail / EdTech Partners, Indie Artists, Subsidiary & Tourism Systems |
| Campaigns, notifications & operational analytics | MySen Platform | Marketing & Sales Dept, Messaging Providers (FCM / APNs / SMS) |

## Change log

| Version | When | Change | Why |
|---|---|---|---|
| v1 | Lesson 3 | First version mapping core stakeholders and external systems from CVCA | Baseline context boundary for MySen Platform (F-01 to F-06) |
| v2 | Lesson 7 | Added Messaging Providers (FCM/APNs/SMS) and Park Check-in System details | Activity modeling (`AD-UC-04`, `AD-UC-05`) required push reminders and real-time checkpoint validation |
