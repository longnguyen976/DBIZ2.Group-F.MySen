# CVCA: MySen App Platform

Lesson 3 (Prof. Seki, CVCA to Context Diagram). The Customer Value Chain Analysis lists every
stakeholder of the Dam Sen Cultural Park ecosystem and what flows between them: money (`$`), information (`i`),
goods or services (`service`), and regulations/approvals (`reg`). It is drawn to map value exchanges,
identify operational problems, and derive stakeholder requirements.

| Field | Value |
|---|---|
| Version | v1.0 (Lesson 3) |
| Next | [Context Diagram](context-diagram.md) |

## 1. Value chain (with the new system)

```mermaid
flowchart LR
  MYSEN(["MySen App Platform<br>(new system)"])

  %% End-user & customer
  VIS["Visitors / GenZ Customers"]

  %% Internal operating organisation
  DSP["DSP Management<br>(Phu Tho Tourist Service JSC)"]
  FIN["Finance & Operation Dept"]
  MKT["Marketing & Sales Dept"]
  IT["IT & Technical Dept"]
  LEG["Legal & Compliance Dept"]

  %% Partner / affiliated service
  EDT["EdTech Partners"]
  FNB["F&B, Sports & Retail Brands"]
  ART["Indie Artists & Creators"]
  TOU["Tourism & Accommodation"]
  INT["Internal Units<br>(Water Park, Dalat, Dong Ha)"]

  %% Enabler / constraint
  PAY["Payment Gateway<br>(MoMo / VNPay EIF)"]
  GOV["Government Authorities"]

  %% Flows: DSP Management
  DSP -->|"$: investment & operating budget"| MYSEN
  DSP -->|"i: park content, operating info & requirements"| MYSEN
  MYSEN -->|"$: rental & sponsorship revenue, ROI"| DSP

  %% Flows: EdTech Partners
  EDT -->|"$: rental fees & sponsorship"| MYSEN
  EDT -->|"service: educational content & workshops"| MYSEN
  MYSEN -->|"service: student-visitor reach & rental space"| EDT

  %% Flows: F&B, Sports & Retail Brands
  FNB -->|"$: rental fees & utilities sponsorship"| MYSEN
  FNB -->|"service: on-site traffic & voucher redemption"| MYSEN
  MYSEN -->|"service: rental space & audience reach"| FNB

  %% Flows: Indie Artists & Creators
  ART -->|"service: performances, fan traffic & streamed content"| MYSEN
  MYSEN -->|"service: event-slot approval & audience exposure"| ART

  %% Flows: Finance & Operation Dept
  MYSEN -->|"i: revenue reconciliation record"| FIN
  FIN -->|"i: ticket catalogue, wait-time & status updates"| MYSEN

  %% Flows: Payment Gateway & Visitors
  VIS -->|"$: ticket & voucher payments (e-wallet / card)"| PAY
  PAY -->|"$: daily settlement of ticket revenue"| FIN
  MYSEN -->|"i: payment & refund requests"| PAY
  PAY -->|"i: payment confirmation (webhook) & settlement data"| MYSEN
  MYSEN -->|"service: e-tickets, map, quests, rewards & recommendations"| VIS
  VIS -->|"i: profile, behaviour events, feedback & gallery posts"| MYSEN

  %% Flows: Internal Units & Tourism
  INT -->|"i: tour packages, availability & booking status"| MYSEN
  MYSEN -->|"service: cross-park tourist traffic & bookings"| INT
  TOU -->|"i: accommodation, ecotourism & package data"| MYSEN
  MYSEN -->|"service: park visitor traffic & package bookings"| TOU

  %% Flows: IT, Marketing, Legal & Government
  IT -->|"i: role set-up, deployment & maintenance"| MYSEN
  MYSEN -->|"i: audit log & server failure alerts"| IT
  MKT -->|"i: campaigns, promo codes & push content"| MYSEN
  MYSEN -->|"i: visitor-flow & revenue dashboard"| MKT
  LEG -->|"reg: regulations, licences & approvals (manual entry)"| MYSEN
  MYSEN -->|"i: compliance report (file export)"| LEG
  GOV -->|"reg: regulations, licences & approvals"| LEG
  LEG -->|"i: compliance & tax reports"| GOV
  GOV -.->|"i: automatic sync (out of scope)"| MYSEN
```

Before MySen, park ticketing, checkpoint exploration, partner booth promotions, and visitor engagement operated across disconnected offline channels (paper tickets, static maps, manual spreadsheets), causing long queues at gates and limited visibility into real-time visitor flow.

## 2. Problems and opportunities

| # | Stakeholder | Problem or opportunity |
|---|---|---|
| P-1 | Visitors / GenZ Customers, Finance & Operation Dept | On-site ticket queues are slow during peak hours, and visitors lack a unified digital wallet for e-tickets and cashless payments. |
| P-2 | Visitors / GenZ Customers | Traditional park visits lack interactive storytelling, real-time navigation, and gamified incentives to explore lesser-known attractions. |
| P-3 | F&B, Sports & Retail Brands, EdTech Partners, Indie Artists | Commercial partners and creators lack a digital channel to reach visitors on-site, manage space/event-slot bookings, and redeem loyalty vouchers. |
| P-4 | Marketing & Sales Dept, DSP Management | Management lacks real-time visitor-flow analytics, automated campaign/notification tools, and cross-unit booking visibility across affiliated parks. |
| P-5 | Legal & Compliance Dept, IT & Technical Dept | Compliance reporting and audit monitoring require structured digital exports and role-based system governance. |

## 3. Stakeholder requirements

Written as "<stakeholder> shall be able to ...", following Prof. Seki's Lesson 4 design process. They become system requirements in [the architecture](../architecture/architecture.md).

| ID | Stakeholder requirement | From |
|---|---|---|
| StR-01 | Visitors, partners, and internal staff shall be able to securely access the platform according to their assigned roles. | P-5 |
| StR-02 | Visitors shall be able to purchase e-tickets via online payment gateways and store QR tickets in a digital wallet. | P-1 |
| StR-03 | Visitors shall be able to navigate park zones and view real-time attraction details through an interactive map. | P-2 |
| StR-04 | Visitors shall be able to scan checkpoint QR codes to unlock interactive stories, earn XP, and collect badges. | P-2 |
| StR-05 | Visitors shall be able to earn loyalty coins from daily check-ins and redeem them for partner F&B vouchers. | P-2, P-3 |
| StR-06 | Visitors shall be able to share event photos in a community gallery, and commercial partners shall be able to submit space rental requests. | P-3 |
| StR-07 | Administrators and marketing staff shall be able to run promotional campaigns, send push notifications, and monitor visitor-flow and revenue analytics. | P-4, P-5 |