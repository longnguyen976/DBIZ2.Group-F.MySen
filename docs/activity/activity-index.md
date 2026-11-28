# Activity Diagram Index: MySen

One row per use case in the Use Case inventory (`UC-01` to `UC-11`). Every use case appears, even when it needs no diagram, so a reader can see that the decision was made on purpose.

## Inputs check (Block 1: what Lesson 3 and Lesson 4 gave us)

| # | Finding | Source to fix | Action | Owner | Status |
|---|---|---|---|---|---|
| 1 | Daily streak evaluation and midnight streak reset require an automated scheduled job not explicitly defined in early sequence drafts | Architecture | Added `ADR-004` ("Add a scheduler for timed jobs") and modelled `S2` time trigger in `AD-UC-05` | Nguyễn Hải Long | Done |
| 2 | Anti-cheat verification for park checkpoints requires cryptographic QR signatures combined with GPS geofencing ($\le 30\text{ m}$) | Architecture | Added `ADR-005` ("HMAC-signed QR tokens + GPS geofence validation") and decision `d1` in `AD-UC-04` | Nguyễn Hải Long | Done |
| 3 | Asynchronous MoMo/VNPay payment callbacks and manual admin refund approval were mixed in early checkout drafts | Sequence Diagrams & W1 | Standardized `SD-UC-02` and structured `AD-UC-02B` with idempotent webhook verification (`d2`), 15-min expiry (`d5`), and manual refund branch (`d6`–`d8`) | Nguyễn Thị Nguyệt Minh | Done |
| 4 | `UC-02` spans three distinct functional flows (Catalogue, Checkout/Refund, Wallet) that exceed the single-diagram node readability limit | Activity Diagrams | Split `UC-02` coverage into three focused activity files (`AD-UC-02A.md`, `AD-UC-02B.md`, `AD-UC-02C.md`) mapped 1-to-1 to `FR-02-01`..`FR-02-03` | Nguyễn Thị Nguyệt Minh | Done |
| 5 | `F&B Partner POS` and `Cloud Storage / CDN` appeared in activity flows for voucher redemption and photo uploads but needed alignment with external lanes | Context Diagram | Aligned external lanes across `AD-UC-05` (`F&B Partner POS`, `GPS Service`) and `AD-UC-11` (`Cloud Storage / CDN`) | Bảo Ngân & Trần Hương Ly | Done |
| 6 | Several AD files contained placeholder FR codes (`FR-04-??`), `-BE`/`-FE` suffixes, or empty lesson-8 screen mappings | Activity & Function List | Standardized all FR IDs against `w1-function-list.md` (`FR-01-01`..`FR-06-12`) and linked screens `S-F00-01`..`S-F06-01` | All Owners / Integrator | Done |

## Use cases

Rule used in this course: draw an activity diagram for every **Must** use case that has at least one decision, more than one lane, or a time trigger. A use case that is a single display step gets `"not needed"` and a one-line reason.

| Use case | Name | Feature | Priority | Activity diagram | Status | Reason if not needed |
|---|---|---|---|---|---|---|
| UC-01 | Register / Log in | F-01 | Must | `AD-UC-01.md` | Reviewed | |
| UC-02 | Purchase E-Tickets & Manage Wallet | F-02 | Must | `AD-UC-02A.md`<br>`AD-UC-02B.md`<br>`AD-UC-02C.md` | Draft | Split into 3 diagrams matching `FR-02-01` (Catalogue), `FR-02-02` (Checkout & Refund), and `FR-02-03` (Wallet) |
| UC-03 | Interactive Map & Navigation | F-03 | Must | `AD-UC-03.md` | Draft | |
| UC-04 | Participate in Gamification & Challenges | F-04 | Must | `AD-UC-04.md` | Reviewed | |
| UC-05 | Earn Loyalty Coins & Redeem Vouchers | F-04 | Must | `AD-UC-05.md` | Draft | |
| UC-06 | Manage Rental Space & Sponsorship Deals | F-05 | Should | `AD-UC-06.md` | Draft | |
| UC-07 | Register Indie Artist Performance Schedule | F-05 | Should | `AD-UC-07.md` | Draft | |
| UC-08 | Manage Marketing & Promotion Campaigns | F-06 | Must | `AD-UC-08.md` | Reviewed | |
| UC-09 | Analyze Customer & Park Analytics | F-06 | Should | not needed | | Read-only dashboard aggregation and chart filtering (`FR-06-04`, `FR-06-05`); single actor lane (`Staff & Admin`) with no multi-step state transitions |
| UC-10 | Manage & Maintain System Infrastructure | F-06 | Must | `AD-UC-10.md` | Reviewed | |
| UC-11 | Post & Browse Social Gallery | F-05 | Must | `AD-UC-11.md` | Draft | |

## Object state lists collected from all diagrams

Object state lists collected from all diagrams (copy into the data model in DBIZ3):

| Object | States | Source Diagram(s) |
|---|---|---|
| User Account | Pending (OTP verification), Active, Locked (15-min cooldown) | `AD-UC-01` |
| OTP Token | Issued (5-min TTL), Used, Expired | `AD-UC-01` |
| Ticket Selection | Valid (local pre-checkout) | `AD-UC-02A` |
| Order | `PENDING`, `PAID`, `EXPIRED` | `AD-UC-02B` |
| Payment Attempt | Initiated, `SUCCESS`, `FAILED`, `CANCELLED`, Unknown (reconciliation) | `AD-UC-02B` |
| E-Ticket | Not Issued, `ACTIVE` (issued), `USED`, `EXPIRED`, Invalidated (refunded) | `AD-UC-02B`, `AD-UC-02C` |
| Refund Request | `REVIEWING`, `PENDING` (gateway), `COMPLETED`, Rejected, Failed | `AD-UC-02B` |
| Attraction / POI | `Open`, `Closed` | `AD-UC-03` |
| Location Permission | `Granted`, `Denied` | `AD-UC-03` |
| Checkpoint & Story Chapter | Locked, Verified (QR + GPS), Unlocked | `AD-UC-04` |
| Zone Badge | Locked, Awarded | `AD-UC-04` |
| Daily Login Streak | Active (incremented), At Risk, Reset (`0`) | `AD-UC-05` |
| Milestone Reward | Locked (pending threshold or physical visit), Unlocked, Claimed | `AD-UC-05` |
| Loyalty Voucher | Issued (active), `REDEEMED`, Expired | `AD-UC-05` |
| Rental Space | `Available`, `Booked` | `AD-UC-06` |
| Rental Request | `PENDING`, `APPROVED`, `REJECTED` | `AD-UC-06` |
| Event Listing | `PENDING`, `APPROVED` (published), `REJECTED` | `AD-UC-07` |
| Social Gallery Post | Pending Filter, `Published`, `Hidden` (flagged/reported), `Removed` | `AD-UC-11` |
| Marketing Campaign | `Scheduled`, `Active`, Ended | `AD-UC-08` |
| Promotion Code | Active, Redeemed, Exhausted (usage limit reached), Expired | `AD-UC-08` |
| Release Build | Built, Tested, Staging, Production, Rolled Back | `AD-UC-10` |