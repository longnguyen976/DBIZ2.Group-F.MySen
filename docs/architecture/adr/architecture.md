# Architecture: MySen Platform

Lesson 4 (Prof. Seki, architectural design). The steps follow the design process of the lecture:
stakeholder requirements, system requirements, functional design, physical design, three layers.
Decisions are recorded as ADRs in [`adr/`](adr/).

| Field | Value | 
| ----- | ----- | 
| Version | v2 | 
| Inputs | [CVCA](../context/cvca.md) (stakeholder requirements), [Context Diagram](../context/context-diagram.md), [Use Case Diagram](../use-case/use-case-diagram.md) | 

## 1. System requirements

| ID | System requirement | From | 
| ----- | ----- | ----- | 
| SyR-01 | The system shall authenticate visitors, commercial partners, indie artists, and staff with role-based access control. | StR-01 (`F-01` / `UC-01`) | 
| SyR-02 | The system shall let visitors browse and purchase e-tickets via payment gateways, request manual refunds, and hold QR tickets in a digital wallet. | StR-02 (`F-02` / `UC-02`) | 
| SyR-03 | The system shall provide an interactive 2.5D/3D park map with POI search, pedestrian navigation, and real-time attraction wait times. | StR-03 (`F-03` / `UC-03`) | 
| SyR-04 | The system shall let visitors scan checkpoint QR codes with HMAC and GPS geofence anti-cheat verification to unlock storybooks, XP, and badges. | StR-04 (`F-04` / `UC-04`) | 
| SyR-05 | The system shall track daily login streaks, award loyalty coins, evaluate milestones, and let visitors redeem F&B vouchers at partner POS. | StR-04 (`F-04` / `UC-05`) | 
| SyR-06 | The system shall provide a moderated social photo gallery, indie artist performance scheduling, and a space rental workflow for partners. | StR-05 (`F-05` / `UC-06`, `UC-07`, `UC-11`) | 
| SyR-07 | The system shall let administrators and IT staff manage marketing campaigns, send push notifications, view analytics, assign roles, and monitor system health. | StR-06 (`F-06` / `UC-08`, `UC-09`, `UC-10`) | 

The detailed, testable version of each requirement is an EARS row in
[W1](../function-list/w1-function-list.md).

## 2. Functional design

The system requirements divided into subordinate functions.

| Function | Serves | 
| ----- | ----- | 
| Identify the user and enforce role permissions | all | 
| List ticket types, process orders, payment callbacks, and manual refunds | SyR-02 | 
| Manage digital ticket wallet and validate QR passes at turnstiles | SyR-02 | 
| Serve 2.5D/3D map layers, POI metadata, wait times, and walking routes | SyR-03 | 
| Validate checkpoint QR tokens & GPS proximity; unlock lore and badges | SyR-04 | 
| Track daily streaks, coin ledger, milestones, and POS voucher redemptions | SyR-05 | 
| Manage social gallery moderation, indie event schedules, and partner rentals | SyR-06 | 
| Run timed streak resets, order expirations, campaign activations, and alerts | SyR-02, SyR-05, SyR-07 | 
| Manage campaigns, dispatch push messages, and aggregate analytics | SyR-07 | 
| Send notifications | SyR-01, SyR-02, SyR-05, SyR-06, SyR-07 | 

## 3. Physical design

Each function allocated to an element of the system.

```
flowchart TB
  subgraph P["1 Presentation layer"]
    WEB["Responsive web app & portal: visitor, partner, artist, and staff screens"]
  end
  subgraph B["2 Business layer"]
    direction LR
    AUTH["Auth & RBAC service"]
    TKT["Ticketing & wallet service"]
    MAP["Map & POI service"]
    GAME["Gamification & loyalty service"]
    SOC["Social, events & partner service"]
    ADM["Campaign & analytics service"]
    SCH["Scheduler (ADR-004)"]
    NOT["Notification adapter"]
  end
  subgraph D["3 Data access layer"]
    DB[("MySen relational database")]
    OBJ[("Cloud storage / CDN")]
  end
  SSO["Google Identity<br>(external)"]
  PAY["Payment gateway: VNPay / MoMo<br>(external)"]
  GPS["Device GPS & location service<br>(external)"]
  POS["F&B partner POS<br>(external)"]
  MSG["Messaging providers: FCM / APNs / SMS / Email<br>(external)"]

  P --> B
  B --> D
  WEB -.-> SSO
  WEB -.-> GPS
  TKT -.-> PAY
  GAME -.-> GPS
  GAME -.-> POS
  SOC -.-> OBJ
  NOT -.-> MSG
  SCH --> TKT
  SCH --> GAME
  SCH --> ADM

```

Solid arrows run from layer to layer; dotted arrows go to external systems. Inside the business
layer, the Scheduler starts timed jobs on the Ticketing, Gamification, and Campaign services, and
every service sends messages through the Notification adapter.

| Function | Element | Layer | 
| ----- | ----- | ----- | 
| Identify the user and enforce role permissions | Web app & Auth/RBAC service with Google Identity ([ADR-002](adr/ADR-002-auth-rbac.md)) | Presentation, Business, external | 
| List ticket types, process orders, callbacks, and refunds | Ticketing & wallet service with Payment gateway ([ADR-003](adr/ADR-003-payment-gateway.md)) | Business, external | 
| Manage digital wallet and turnstile QR validation | Ticketing & wallet service | Business | 
| Serve 2.5D/3D map layers, wait times, and routes | Web app & Map/POI service with Device GPS | Presentation, Business, external | 
| Validate checkpoint QR & GPS anti-cheat; unlock lore | Gamification & loyalty service with Device GPS ([ADR-005](adr/ADR-005-qr-gps-anticheat.md)) | Business, external | 
| Track daily streaks, milestones, and POS vouchers | Gamification & loyalty service with F&B partner POS | Business, external | 
| Manage social gallery, indie events, and partner rentals | Social, events & partner service with Cloud storage / CDN | Business, Data access | 
| Run timed streak resets, order expirations, and campaign triggers | Scheduler starts Ticketing, Gamification, and Campaign services ([ADR-004](adr/ADR-004-scheduler-notifications.md)) | Business | 
| Manage campaigns, analytics, roles, and audit logs | Campaign & analytics service | Business | 
| Send notifications | Notification adapter with Messaging providers | Business, external | 
| Keep users, tickets, POIs, quests, coins, posts, campaigns, and logs | MySen relational database | Data access | 

All screens of Lesson 8 (`S-F00-01` to `S-F06-01`) are elements of the presentation layer. Their data sources are the data groups of [W0 Table 4](../function-list/w0-scope.md).

## 4. Decisions

| ADR | Decision | Status | 
| ----- | ----- | ----- | 
| [ADR-001](adr/ADR-001-responsive-pwa-and-portal.md) | One responsive web app (PWA) and portal for visitors, partners, artists, and staff, no native app | Accepted | 
| [ADR-002](adr/ADR-002-auth-rbac.md) | Token-based authentication (JWT) with OTP, Google SSO, and RBAC | Accepted | 
| [ADR-003](adr/ADR-003-payment-gateway.md) | Process e-ticket payments and refunds through external payment gateways (VNPay / MoMo) | Accepted | 
| [ADR-004](adr/ADR-004-scheduler-notifications.md) | Add a scheduler for timed jobs and a unified notification adapter for push/SMS/email | Accepted (after Lesson 7) | 
| [ADR-005](adr/ADR-005-qr-gps-anticheat.md) | Validate HMAC-signed QR tokens combined with GPS geofencing (`<= 30 m`) for checkpoint check-ins | Accepted (after Lesson 7) | 

## Change log

| Version | When | Change | Why | 
| ----- | ----- | ----- | ----- | 
| v1 | Lesson 4 | Web app, Auth/RBAC, Ticketing, Map/POI, Gamification, Social/Partner, Campaign/Analytics, Notification adapter, database | Baseline scope from CVCA and Use Case Diagram | 
| v2 | Lesson 7 | Added Scheduler (`ADR-004`) and QR/GPS anti-cheat (`ADR-005`) | `AD-UC-04` and `AD-UC-05` showed timed streak resets, 15-minute order expiry, and checkpoint spoofing risks (Inputs check rows 1–3 in [activity-index](../activity/activity-index.md)) | 
