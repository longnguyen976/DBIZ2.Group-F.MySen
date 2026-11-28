# W0 Scope: MySen Platform

Lesson 5 (Function List workshop, block W0). Inputs: CVCA, Context Diagram, Use Case Diagram, System Architecture at v2.

## Table 1. Use case inventory

| Use case ID | Use case name | Primary actor | Assigned feature | Login required |
|---|---|---|---|---|
| UC-01 | Register & Log in | Visitor, Partner, Staff | F-01 | No |
| UC-02 | Purchase E-Tickets & Manage Wallet | Visitor / GenZ Customer | F-02 | Yes |
| UC-03 | Interactive Map & Navigation | Visitor / GenZ Customer | F-03 | No (Browse) / Yes (Save) |
| UC-04 | Gamification & Interactive Park Challenges | Visitor / GenZ Customer | F-04 | Yes |
| UC-05 | Earn Loyalty Coins & Redeem Vouchers | Visitor / GenZ Customer, F&B Partner POS | F-04 | Yes |
| UC-06 | Manage Rental Space & Sponsorship Deals | F&B / Retail Partners, Staff & Admin | F-05 | Yes (Partner / Staff) |
| UC-07 | Register Indie Artist Performance Schedule | Indie Artists & Creators, Staff & Admin | F-05 | Yes (Artist / Staff) |
| UC-08 | Manage Marketing & Promotion Campaigns | Marketing & Sales Dept | F-06 | Yes (Staff/Admin) |
| UC-09 | Analyze Customer & Park Analytics | Staff & Admin, Marketing & Sales Dept | F-06 | Yes (Staff/Admin) |
| UC-10 | Manage & Maintain System Infrastructure | IT & Technical Dept | F-06 | Yes (IT Admin) |
| UC-11 | Post & Browse Social Gallery | Visitor / GenZ Customer, Staff & Admin | F-05 | No (Browse) / Yes (Post/Moderate) |

---

## Table 2. Feature list

| Feature ID | Feature name (business noun) | Scope in one sentence | Primary actors served | Owner | Use cases covered |
|---|---|---|---|---|---|
| F-01 | Identity & User Management | Core visitor/staff authentication, OTP verification, Google SSO, password recovery, RBAC enforcement, and session security. | Visitor, Partner, Indie Artist, Staff | Lê Thành Hiệp | UC-01 |
| F-02 | E-Ticketing & Park Operations | E-ticket catalogue browsing, MoMo/VNPay checkout, QR ticket wallet, manual refund workflow, and turnstile entry scanning. | Visitor / GenZ Customer, Staff & Admin | Nguyễn Thị Nguyệt Minh | UC-02 |
| F-03 | Interactive Map & Park Navigation | 2.5D/3D interactive park map, live GPS/beacon positioning, POI search, walking directions, and real-time attraction wait times. | Visitor / GenZ Customer, Staff & Admin | Nguyễn Thị Phúc An | UC-03 |
| F-04 | Gamification & Loyalty Engine | Heritage QR checkpoint quests, anti-cheat geofencing, storybook reader, daily login streaks, coin rewards, and F&B voucher redemption. | Visitor / GenZ Customer, F&B Partner POS | Nguyễn Hải Long & Đoàn Thị Bảo Ngân | UC-04, UC-05 |
| F-05 | Social Gallery & Partner Platform | Moderated visitor photo gallery, Indie artist performance scheduling, and commercial space rental requests for park partners. | Visitor, Indie Artist, F&B/Retail Partner, Staff | Trần Hương Ly | UC-06, UC-07, UC-11 |
| F-06 | Admin Operations & Analytics | Marketing campaign & promo code management, push notifications, park/customer analytics dashboards, RBAC assignment, audit logs, and CI/CD monitoring. | Staff & Admin, Marketing, IT Dept | Lê Thành Hiệp | UC-08, UC-09, UC-10 |

Feature count: 6 (allowed 3 to 6): PASS. Coverage against CVCA: all primary actors (Visitor/GenZ Customer, Indie Artists & Creators, F&B/Retail Partners, Staff & Admin, Marketing & Sales, IT & Technical) are served.

---

## Table 3. Won't-have (recorded scope exclusions)

| Excluded from scope | How it surfaced | Reason for exclusion |
|---|---|---|
| AR (Augmented Reality) Park Experience | Student / Stakeholder meeting | High 3D asset and mobile hardware complexity; deferred to Release 2 in favor of 2.5D map and QR storytelling. |
| Third-party Ticket Reseller API | Commercial Partner inquiry | Initial release focuses on direct-to-consumer digital ticketing; external B2B OTA API scheduled for future phase. |
| Automatic Cash Refund for Tickets | User survey & Financial review | Refunds require manual Staff/Admin verification (`REVIEWING` state) before gateway execution to prevent fraud and financial risk. |
| Native Desktop Application | Team discussion | Staff, Marketing, and IT Admin portals run entirely on responsive web layout; native desktop wrapper is not required. |

---

## Table 4. Data functions (Function Point Analysis)

| Data group | ILF / EIF | Why | Function points |
|---|---|---|---|
| User Accounts, Roles & Audit Logs | ILF | User profiles, salted credentials, OTP tokens, staff RBAC assignments, and immutable admin audit trails maintained by MySen | 10 |
| E-Tickets, Orders & Refunds | ILF | Ticket SKUs, `PENDING`/`PAID`/`EXPIRED` orders, QR credentials, turnstile logs, and manual refund requests | 10 |
| Park Map POIs & Wait-Time States | ILF | 2.5D/3D map coordinates, park zones, attraction metadata, and real-time queue wait-time/open status | 7 |
| Quests, Story Chapters, Coins & Vouchers | ILF | Checkpoint definitions, user quest progress, story unlocks, daily streak counters, coin ledger, and F&B vouchers | 10 |
| Social Posts, Events & Rental Spaces | ILF | Social gallery posts/moderation flags, Indie artist event schedules, and partner booth rental spaces/requests | 10 |
| Campaigns, Promo Codes & Analytics Snapshots | ILF | Marketing campaign rules, promo code usage caps, push logs, and aggregated park occupancy/revenue metrics | 7 |
| Payment Gateways (MoMo / VNPay) | EIF | External payment execution, status reconciliation, and refund callback interface | 5 |
| Google Identity & Messaging Providers (SMS/Email/FCM) | EIF | External OAuth 2.0/OIDC verification and SMS/email/push notification delivery services | 5 |
| **Total data-function points** | | | **64** |

---

## Business Rules

| BR | Rule |
|---|---|
| BR-01 | An account or pending registration is locked for 15 minutes after 5 consecutive failed password or OTP verification attempts (`FR-01-11`). |
| BR-02 | Daily login streak rewards (`+100 coins`) can be claimed at most once per calendar day (UTC+7), and consecutive streaks reset to `0` at end-of-day cutoff if no login occurs (`FR-04-06`, `FR-04-09`). |
| BR-03 | Major loyalty milestone rewards (`5,000 / 15,000 / 25,000 coins`) require a verified physical park visit/purchase and can be claimed only once per user (`FR-04-10`, `FR-04-11`). |
| BR-04 | A promotion code can be redeemed at checkout only while its campaign is `Active`, unexpired, and total redemptions remain strictly below the batch usage limit (`FR-06-03`). |
| BR-05 | Unpaid `PENDING` ticket orders expire automatically after 15 minutes (`FR-02-14`), and all ticket refunds require manual Staff/Admin approval (`FR-02-04`) before gateway refund execution. |