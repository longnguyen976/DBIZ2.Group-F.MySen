# W4 Priorities: MySen

Lesson 5 (block W4). Cut by lowering priority, never by lowering estimates. Every change names its rule.

| Rule | MoSCoW meaning | Test question |
|---|---|---|
| R1 Must | The release has no viable use without it | If it is absent on delivery day, is the release useless? |
| R2 Should | Important, but a workaround exists | Painful to leave out, yet the solution still works? |
| R3 Could | Desirable, low impact if dropped | Would anyone notice within the first month? |
| R4 Won't | Agreed out of scope for this release | Did the client accept deferring it? |

| Feature | L2 ID | L2 function name | Initial priority | Effective priority | Justification (required if changed) | Person-hours | Cost (VND) |
|---|---|---|---|---|---|---|---|
| F-01 | FR-01-01 | Register an account and verify it with OTP | Must | Must |  | 5.4 | 1.420.000 |
| F-01 | FR-01-02 | Issue and deliver a one-time password (OTP) | Must | Must |  | 12.6 | 3.780.000 |
| F-01 | FR-01-03 | Sign in with password | Must | Must |  | 5.4 | 1.420.000 |
| F-01 | FR-01-04 | Sign in with Google (SSO) | Should | Should |  | 14.6 | 4.180.000 |
| F-01 | FR-01-05 | Reset a forgotten password | Must | Must |  | 5.4 | 1.420.000 |
| F-01 | FR-01-06 | Sign out | Must | Must |  | 5.4 | 1.420.000 |
| F-01 | FR-01-07 | View and edit profile | Should | Should |  | 5.4 | 1.420.000 |
| F-01 | FR-01-08 | Enforce basic role-based access control | Must | Must |  | 3.4 | 1.020.000 |
| F-01 | FR-01-09 | Store passwords as salted hashes | Must | Must |  | 3.4 | 1.020.000 |
| F-01 | FR-01-10 | Manage sessions with JWT access and refresh tokens | Must | Must |  | 10.2 | 3.060.000 |
| F-01 | FR-01-11 | Lock sign-in after repeated failed attempts | Must | Must |  | 3.4 | 1.020.000 |
| F-02 | FR-02-01 | Browse E-Ticket catalogue | Must | Must |  | 5.4 | 1.420.000 |
| F-02 | FR-02-02 | Ticket checkout & payment | Must | Must |  | 18.0 | 5.200.000 |
| F-02 | FR-02-03 | View & manage ticket wallet | Must | Must |  | 5.4 | 1.420.000 |
| F-02 | FR-02-04 | Request manual ticket refund | Must | Should | R2: Staff can process manual refunds via back-office ledger and payment portal during initial weeks; workaround exists. | 10.8 | 2.840.000 |
| F-02 | FR-02-05 | Validate E-Ticket QR at park turnstile | Must | Should | R2: Gate staff can verify active E-Ticket QR visual pass manually at entry lanes before dedicated turnstile API sync goes live. | 5.4 | 1.420.000 |
| F-02 | FR-02-06 | View turnstile entry log & daily gate count | Should | Should |  | 5.4 | 1.420.000 |
| F-02 | FR-02-07 | Synchronize offline turnstile scans | Should | Should |  | 18.0 | 5.200.000 |
| F-02 | FR-02-08 | Manage ticket types and pricing rules | Must | Should | R2: Initial ticket SKUs and prices can be seeded via database migration for launch; dynamic UI editor is not fatal on day one. | 8.8 | 2.440.000 |
| F-02 | FR-02-09 | Generate combo & group ticket packages | Should | Could | R3: Standard single-entry tickets cover launch demand; bundled combo packages have low impact if deferred past month one. | 8.8 | 2.440.000 |
| F-02 | FR-02-10 | Send E-Ticket purchase receipt & QR backup | Should | Could | R3: Active QR passes are immediately accessible inside the in-app Ticket Wallet (`FR-02-03`); email backup is secondary. | 5.4 | 1.420.000 |
| F-02 | FR-02-11 | Apply promotion code at ticket checkout | Should | Could | R3: Launch pricing can run directly via base ticket SKUs without checkout discount codes in the first month. | 5.4 | 1.420.000 |
| F-02 | FR-02-12 | View personal order & refund history | Could | Could |  | 5.4 | 1.420.000 |
| F-02 | FR-02-13 | Export daily ticket reconciliation report | Could | Could |  | 3.4 | 1.020.000 |
| F-02 | FR-02-14 | Expire unpaid `PENDING` ticket orders | Must | Must |  | 3.4 | 1.020.000 |
| F-02 | FR-02-15 | Prevent duplicate payment webhook processing | Must | Must |  | 6.8 | 2.040.000 |
| F-02 | FR-02-16 | Handle payment reconciliation timeout | Should | Should |  | 8.8 | 2.440.000 |
| F-02 | FR-02-17 | Notify visitor on refund approval or rejection | Should | Should |  | 14.6 | 4.180.000 |
| F-03 | FR-03-01 | View interactive park map and points of interest | Must | Must |  | 11.4 | 2.620.000 |
| F-03 | FR-03-02 | View current visitor location on the park map | Must | Must |  | 7.4 | 1.820.000 |
| F-03 | FR-03-03 | Search attractions and points of interest | Must | Must |  | 5.4 | 1.420.000 |
| F-03 | FR-03-04 | Get walking directions to a selected destination | Must | Must |  | 4.0 | 800.000 |
| F-03 | FR-03-05 | View real-time attraction wait time and operating status | Should | Should |  | 5.4 | 1.420.000 |
| F-03 | FR-03-06 | Update attraction wait time and operating status | Must | Should | R2: Static operating hours in POI metadata suffice initially; live staff queue updates are painful to omit but not fatal. | 5.4 | 1.420.000 |
| F-04 | FR-04-01 | Display Quest Hub & scan checkpoint QR | Must | Must |  | 5.4 | 1.420.000 |
| F-04 | FR-04-02 | Validate checkpoint QR & GPS geofence (Anti-cheat) | Must | Must |  | 20.0 | 5.600.000 |
| F-04 | FR-04-03 | Unlock and display heritage storybook chapter | Must | Must |  | 7.4 | 1.820.000 |
| F-04 | FR-04-04 | Credit quest XP, coins & unlock zone badge | Must | Must |  | 5.4 | 1.420.000 |
| F-04 | FR-04-05 | Claim daily login streak reward | Must | Should | R2: Core park QR quest check-ins already award coins; daily login streak bonus has a clear engagement workaround. | 5.4 | 1.420.000 |
| F-04 | FR-04-06 | Prevent duplicate daily reward claims | Must | Must |  | 3.4 | 1.020.000 |
| F-04 | FR-04-07 | Award coins for verified park GPS check-in | Must | Should | R2: Checkpoint QR quests (`FR-04-01`..`04`) already reward physical park visits; standalone GPS check-in is supplementary. | 5.4 | 1.420.000 |
| F-04 | FR-04-08 | Award loyalty coins for eligible POS/ticket purchases | Should | Should |  | 5.4 | 1.420.000 |
| F-04 | FR-04-09 | Monitor daily streak & send at-risk / reset notifications | Should | Should |  | 3.4 | 1.020.000 |
| F-04 | FR-04-10 | Evaluate normal & major loyalty milestones & redeem vouchers | Should | Could | R3: Users can accumulate coins and badges during month one while partner POS voucher redemption is rolled out in phase two. | 5.4 | 1.420.000 |
| F-04 | FR-04-11 | Prevent duplicate milestone reward claims | Must | Should | R2: Tied to milestone redemption rollout; server-side claim lock is needed once milestone rewards open. | 3.4 | 1.020.000 |
| F-05 | FR-05-01 | Post a photo to the Social Gallery | Should | Could | R3: Visitors can still browse official park highlights and quests in month one without user-generated photo uploads. | 14.6 | 4.180.000 |
| F-05 | FR-05-02 | Moderate Social Gallery content | Must | Should | R2: Pre-moderated or curated feed avoids live abuse risk while full moderation queue is finalized. | 8.8 | 2.440.000 |
| F-05 | FR-05-03 | View the Social Gallery feed | Should | Could | R3: Gallery feed depends on user uploads (`FR-05-01`); low impact if deferred to post-launch community update. | 5.4 | 1.420.000 |
| F-05 | FR-05-04 | Publish Indie artist performance schedule | Should | Could | R3: Operations staff can publish weekend Indie showtimes manually in month one before self-service artist portal launches. | 5.4 | 1.420.000 |
| F-05 | FR-05-05 | Approve event before publishing | Must | Should | R2: Staff manually curate initial event listings, providing a workaround until automated stage-clash approval is live. | 3.4 | 1.020.000 |
| F-05 | FR-05-06 | View public event calendar | Should | Could | R3: Park show schedules are visible on map POI cards (`FR-03-03`) during month one. | 5.4 | 1.420.000 |
| F-05 | FR-05-07 | Manage rental spaces | Should | Could | R3: B2B booth leasing is handled offline by Đầm Sen sales team in month one; low impact on visitor app launch. | 5.4 | 1.420.000 |
| F-05 | FR-05-08 | Partner submits a rental-space request | Should | Could | R3: Partner booth inquiries can continue via existing email/contract workflow during initial app rollout. | 5.4 | 1.420.000 |
| F-06 | FR-06-01 | Manage marketing campaigns and promotion codes | Must | Should | R2: Marketing can run launch promos via push banners and static ticket pricing while self-service campaign builder follows. | 8.8 | 2.440.000 |
| F-06 | FR-06-02 | Send a push notification to an audience | Should | Could | R3: In-app announcements cover initial visitor communication; segmented push campaigns can follow after month one. | 14.6 | 4.180.000 |
| F-06 | FR-06-03 | Prevent a promotion code from being redeemed beyond its limit | Must | Should | R2: Enforced alongside promo code checkout activation (`FR-02-11` / `FR-06-01`). | 3.4 | 1.020.000 |
| F-06 | FR-06-04 | View real-time park occupancy & revenue dashboard | Should | Could | R3: Operations can query daily ticket and gate totals via database exports in month one before live BI cards ship. | 8.8 | 2.440.000 |
| F-06 | FR-06-05 | Analyze quest completion & attraction popularity metrics | Should | Could | R3: Historical funnel charts have low impact during the first month of data collection. | 3.4 | 1.020.000 |
| F-06 | FR-06-06 | Segment visitor cohorts & retention metrics | Could | Could |  | 5.4 | 1.420.000 |
| F-06 | FR-06-07 | Export customer & park analytics report | Could | Could |  | 5.4 | 1.420.000 |
| F-06 | FR-06-08 | Configure park operating hours & holiday calendar | Could | Could |  | 5.4 | 1.420.000 |
| F-06 | FR-06-09 | Manage staff roles and permissions | Must | Must |  | 5.4 | 1.420.000 |
| F-06 | FR-06-10 | Record an audit log of admin actions | Must | Must |  | 3.4 | 1.020.000 |
| F-06 | FR-06-11 | Deploy automatically through a CI/CD pipeline | Must | Must |  | 9.2 | 2.760.000 |
| F-06 | FR-06-12 | Monitor servers and alert on failure | Must | Should | R2: IT team can inspect cloud hosting logs manually during initial launch weeks; painful, not fatal. | 9.2 | 2.760.000 |