# W1 Function List: MySen

Lesson 5 (block W1). L2 = a business behaviour the client signs off, with its EARS criterion and function-point type. L3 = one work item in one layer (FE, BE, INT), sized S = 4 h, M = 8 h, L = 16 h. Initial priority is set here; the effective priority comes from [W4](w4-priorities.md).

Sources swept, one diagram per pass: Use Case (`UC-01`..`UC-11`), Activity (`AD-UC-01`..`AD-UC-11`), Sequence, Context, CVCA, Architecture + ADR (`ADR-001`..`ADR-005`).

## L2 functions

| Feature | L2 ID | L2 function name | Actor | EARS acceptance criterion | Source trace | Initial priority | FP type |
|---|---|---|---|---|---|---|---|
| F-01 | FR-01-01 | Register an account and verify it with OTP | Visitor / GenZ Customer | WHEN a visitor submits an unregistered phone or email, valid password, and terms consent, the system SHALL hold a pending registration (`purpose = register`), trigger OTP verification, and activate the account upon valid OTP confirmation; IF the phone or email is already registered or input is invalid, THEN the system SHALL reject registration and preserve the form inputs. | UC:UC-01; AD-UC-01; ADR-002 | Must | EI |
| F-01 | FR-01-02 | Issue and deliver a one-time password (OTP) | System | WHEN a registration or password-reset flow requests verification, the system SHALL generate a 6-digit OTP valid for 5 minutes, store only its cryptographic hash, deliver it via SMS/email provider, and mark it single-use upon verification; IF delivery fails or the OTP is invalid/expired, THEN the system SHALL reject verification and allow requesting a new OTP (invalidating the previous code). | UC:UC-01; AD-UC-01; Context: Messaging Providers | Must | EI |
| F-01 | FR-01-03 | Sign in with password | Visitor / GenZ Customer | WHEN a visitor submits credentials for an unlocked active account, the system SHALL verify the password against its stored salted hash and start an authenticated session; IF credentials do not match, THEN the system SHALL return a generic invalid-credentials error without disclosing whether the account exists. | UC:UC-01; AD-UC-01; ADR-002 | Must | EQ |
| F-01 | FR-01-04 | Sign in with Google (SSO) | Visitor / GenZ Customer | WHEN a visitor selects "Continue with Google" and Google Identity returns a valid ID token, the system SHALL sign in the linked MySen account or create a new account from the Google profile; IF the user cancels or the ID token is invalid/expired, THEN the system SHALL abort sign-in and display a failure notice. | UC:UC-01; AD-UC-01; Context: Google Identity | Should | EI |
| F-01 | FR-01-05 | Reset a forgotten password | Visitor / GenZ Customer | WHEN a visitor verifies an OTP with `purpose = reset` and submits a new password meeting password policy, the system SHALL replace the stored password hash, revoke all other active sessions of the account, and require fresh sign-in; IF the new password violates policy, THEN the system SHALL reject the change and keep the existing password. | UC:UC-01; AD-UC-01 | Must | EI |
| F-01 | FR-01-06 | Sign out | Visitor / GenZ Customer | WHEN an authenticated user selects "Log out", the system SHALL revoke the current refresh token, clear local secure token storage, and return the user to the sign-in screen. | UC:UC-01; AD-UC-01 | Must | EI |
| F-01 | FR-01-07 | View and edit profile | Visitor / GenZ Customer | WHEN an authenticated visitor opens their profile and submits valid edits (display name, date of birth, avatar), the system SHALL validate field rules, save the updated profile, and display the new values. | UC:UC-01 (linear flow) | Must | EI |
| F-01 | FR-01-08 | Enforce basic role-based access control | System | IF an authenticated caller requests an API endpoint or admin action outside their assigned role permissions, THEN the system SHALL refuse access with HTTP 403 and leave protected records unchanged. | Architecture; AD-UC-10; ADR-002 | Must | NC |
| F-01 | FR-01-09 | Store passwords as salted hashes | System | WHEN storing a newly registered or reset password, the system SHALL hash the password with a per-user salt using bcrypt or Argon2 and never persist or log plaintext secrets. | Architecture; AD-UC-01; ADR-002 | Must | NC |
| F-01 | FR-01-10 | Manage sessions with JWT access and refresh tokens | System | WHEN authentication succeeds, the system SHALL issue a signed JWT access token (15-minute TTL) and a single-use rotating refresh token held in secure client storage. | Architecture; AD-UC-01; ADR-002 | Must | NC |
| F-01 | FR-01-11 | Lock sign-in after repeated failed attempts | System | IF an account or pending registration reaches 5 consecutive failed password or OTP verification attempts, THEN the system SHALL block further attempts for 15 minutes and display the remaining lock time. | BR-01; AD-UC-01 | Must | NC |
| F-02 | FR-02-01 | Browse E-Ticket catalogue | Visitor / GenZ Customer | WHEN a visitor opens the E-Ticket catalogue, the system SHALL display active ticket types, unit prices, and conditions, validate positive quantities (`> 0`) for available stock before checkout handoff without creating an Order, and show empty or retry states when data is unavailable. | UC:UC-02; AD-UC-02A | Must | EQ |
| F-02 | FR-02-02 | Ticket checkout & payment (incl. manual refund workflow) | Visitor / GenZ Customer, Staff & Admin | WHEN a signed-in visitor confirms a valid ticket selection, the system SHALL create a unique `PENDING` Order (15-minute expiry), verify idempotent MoMo/VNPay payment callbacks, and issue single-use E-Ticket QR codes once upon `PAID`; WHEN a visitor submits a refund request for an eligible paid ticket, the system SHALL queue it (`REVIEWING`) for Staff/Admin manual approval before triggering original-gateway refund and invalidating the QR. | UC:UC-02; AD-UC-02B; ADR-003 | Must | EI |
| F-02 | FR-02-03 | View & manage ticket wallet | Visitor / GenZ Customer | WHEN a signed-in visitor opens Ticket Wallet, the system SHALL verify ownership and list tickets by `ACTIVE`, `USED`, and `EXPIRED`, showing scannable QR codes only for `ACTIVE` valid tickets while hiding QR credentials for `USED`/`EXPIRED`/invalidated tickets and exposing conditional refund entry to `FR-02-02`. | UC:UC-02; AD-UC-02C | Must | EQ |
| F-03 | FR-03-01 | View interactive park map and points of interest | Visitor / GenZ Customer | WHEN a visitor opens the interactive map, the system SHALL load park map layers and POI metadata and render a 2.5D/3D park map with categorized POI markers. | UC:UC-03; AD-UC-03 | Must | EQ |
| F-03 | FR-03-02 | View current visitor location on the park map | Visitor / GenZ Customer | WHILE the map screen is open and device location permission is granted, the system SHALL continuously read GPS/Beacon coordinates and update the visitor's position marker; IF permission is denied, THEN the system SHALL keep the map functional without the position marker. | UC:UC-03; AD-UC-03 | Must | EQ |
| F-03 | FR-03-03 | Search attractions and points of interest | Visitor / GenZ Customer | WHEN a visitor searches for an attraction or POI, the system SHALL display location, `Open`/`Closed` status, wait time, and walking time; IF no exact match exists, THEN the system SHALL suggest similar names; IF closed or data fails to load, THEN the system SHALL display "Currently closed" or a retry error. | UC:UC-03; AD-UC-03 | Must | EQ |
| F-03 | FR-03-04 | Get walking directions to a selected destination | Visitor / GenZ Customer | WHEN a visitor requests directions to an `Open` attraction with current location available, the system SHALL compute the pedestrian route on-device via Map SDK and display the path, walking time, and distance. | UC:UC-03; AD-UC-03 | Must | EQ |
| F-03 | FR-03-05 | View real-time attraction wait time and operating status | Visitor / GenZ Customer | WHILE a visitor views an attraction's detail card, the system SHALL periodically poll the latest queue wait time and operating status (`Open` or `Closed`) and refresh the displayed values. | UC:UC-03; AD-UC-03 (added after Lesson 7) | Should | EQ |
| F-03 | FR-03-06 | Update attraction wait time and operating status | Staff & Admin | WHEN authorized Operations Staff submit a new queue wait time or `Open`/`Closed` status for an attraction, the system SHALL save the updated state and confirm completion so subsequent visitor reads reflect the change. | UC:UC-03; AD-UC-03 | Must | EI |
| F-04 | FR-04-01 | Display Quest Hub & scan checkpoint QR | Visitor / GenZ Customer | WHEN a visitor opens Quest Hub or taps "Scan QR", the system SHALL display active park quests, checkpoint progress, and coin balance, and capture the checkpoint QR payload together with current device GPS coordinates. | UC:UC-04; AD-UC-04 | Must | EQ |
| F-04 | FR-04-02 | Validate checkpoint QR & GPS geofence (Anti-cheat) | System | WHEN a checkpoint scan payload is received, the system SHALL verify the QR HMAC signature, expiration timestamp, and GPS distance within the checkpoint geofence (`<= 30 m`); IF invalid or out of bounds, THEN the system SHALL reject the scan with HTTP 403 and display "Invalid Checkpoint Location". | UC:UC-04; AD-UC-04; ADR-005 | Must | NC |
| F-04 | FR-04-03 | Unlock and display heritage storybook chapter | Visitor / GenZ Customer | WHEN checkpoint validation (`FR-04-02`) succeeds, the system SHALL unlock the corresponding cultural story chapter and render its text, illustration, and optional audio narration on the Storybook Reader screen. | UC:UC-04; AD-UC-04 | Must | EQ |
| F-04 | FR-04-04 | Credit quest XP, coins & unlock zone badge | System | WHEN a visitor completes a verified checkpoint for the first time, the system SHALL credit XP and coins to the user's wallet, award the zone badge without duplication on replays, and trigger the Badge Unlock modal. | UC:UC-04; AD-UC-04 | Must | EI |
| F-04 | FR-04-05 | Claim daily login streak reward | Visitor / GenZ Customer | WHEN a signed-in visitor opens the app and has not yet claimed today's daily reward, the system SHALL credit `+100 coins`, increment the consecutive login streak counter, and record the daily claim. | UC:UC-05; AD-UC-05 | Must | EI |
| F-04 | FR-04-06 | Prevent duplicate daily reward claims | System | IF a visitor attempts to claim the daily login reward more than once within the same calendar day (UTC+7), THEN the system SHALL block duplicate coin credit and display "Daily reward already claimed". | BR-02; UC:UC-05; AD-UC-05 | Must | NC |
| F-04 | FR-04-07 | Award coins for verified park GPS check-in | Visitor / GenZ Customer | WHEN a visitor performs a QR/GPS check-in verified by `GPS Service` inside park boundaries, the system SHALL award activity-based coins; IF location verification fails, THEN the system SHALL reject check-in and show an error. | UC:UC-05; AD-UC-05; Context: GPS Service | Must | EI |
| F-04 | FR-04-08 | Award loyalty coins for eligible POS/ticket purchases | F&B Partner POS | WHEN `F&B Partner POS` or ticketing submits an eligible, non-duplicate `transactionID` linked to a `userID`, the system SHALL credit purchase-based loyalty coins; IF duplicate or ineligible, THEN the system SHALL ignore the transaction without crediting coins. | UC:UC-05; AD-UC-05; Context: F&B Partner POS | Should | EI |
| F-04 | FR-04-09 | Monitor daily streak & send at-risk / reset notifications | System | WHEN the scheduled end-of-day job runs and a user has not logged in today, the system SHALL send a "streak is at risk" reminder and, if still inactive at day cutoff, reset the streak counter to `0` and notify "Your streak has ended". | UC:UC-05; AD-UC-05; ADR-004 | Should | EO |
| F-04 | FR-04-10 | Evaluate normal & major loyalty milestones | System | WHEN a user's coin balance reaches a normal threshold (`1,000 / 1,500 / 2,000`) or major threshold (`5,000 / 15,000 / 25,000`), the system SHALL unlock normal rewards directly, whereas major rewards SHALL remain locked until a verified physical park visit or qualifying purchase record exists. | BR-03; UC:UC-05; AD-UC-05 | Should | EI |
| F-04 | FR-04-11 | Prevent duplicate milestone reward claims | System | IF a milestone threshold has already been claimed by the user, THEN the system SHALL prevent duplicate entitlement issuance and display "Reward already claimed". | BR-03; UC:UC-05; AD-UC-05 | Should | NC |
| F-04 | FR-04-12 | Redeem loyalty coins for F&B / retail vouchers | Visitor / GenZ Customer | WHEN a visitor selects an F&B voucher and has sufficient coin balance, the system SHALL atomically deduct the coin cost, issue a unique voucher code, and record redemption history; IF balance is insufficient, THEN the system SHALL reject redemption and show an insufficient-coins alert. | UC:UC-05; AD-UC-05 | Should | EI |
| F-04 | FR-04-13 | Verify and redeem voucher at F&B Partner POS | F&B Partner POS | WHEN a visitor presents a voucher code at `F&B Partner POS` and POS requests verification, the system SHALL check validity, expiration, and unused status, mark valid vouchers `REDEEMED`, and return approval; IF expired or already used, THEN the system SHALL reject redemption. | UC:UC-05; AD-UC-05; Context: F&B Partner POS | Should | EI |
| F-05 | FR-05-01 | Post a photo to the Social Gallery | Visitor / GenZ Customer | WHEN an authenticated visitor uploads a photo with caption and location tag, the system SHALL store the image on Cloud Storage/CDN, save post metadata, and publish it to the public feed if it passes automated content filtering; IF upload fails, THEN the system SHALL abort creation and allow retry. | UC:UC-11; AD-UC-11; Context: Cloud Storage / CDN | Should | EI |
| F-05 | FR-05-02 | Moderate Social Gallery content | Staff & Admin, Visitor / GenZ Customer | WHEN a post is flagged by automated rules or reported by a visitor, the system SHALL hide the post immediately and place it in the moderation queue until Staff/Admin review and either remove the post (notifying the author) or restore it to the public feed. | UC:UC-11; AD-UC-11 | Must | EI |
| F-05 | FR-05-03 | View the Social Gallery feed | Visitor / GenZ Customer | WHEN a visitor opens the Social Gallery tab, the system SHALL query published posts ordered newest-first with paginated infinite scroll and serve thumbnails via CDN; IF no published posts exist, THEN the system SHALL display "gallery is empty". | UC:UC-11; AD-UC-11 | Should | EQ |
| F-05 | FR-05-04 | Publish Indie artist performance schedule | Indie Artists & Creators | WHEN an authenticated Indie artist submits a performance request (date, time slot, stage, category), the system SHALL create a `PENDING` event listing and allow resubmission if rejected. | UC:UC-07; AD-UC-07 | Should | EI |
| F-05 | FR-05-05 | Approve event before publishing | Staff & Admin | WHEN an artist submits a schedule or Staff/Admin approves a `PENDING` listing, the system SHALL verify no time/stage clash exists against already `APPROVED` events, publish clash-free approved events to the calendar, and notify the creator of approval, rejection reason, or schedule conflict. | UC:UC-07; AD-UC-07 | Must | EI |
| F-05 | FR-05-06 | View public event calendar | Visitor / GenZ Customer | WHEN a visitor opens the Events tab and filters by date or category, the system SHALL query and list all `APPROVED` performances matching the filter, or display "no events found" when empty. | UC:UC-07; AD-UC-07 | Should | EQ |
| F-05 | FR-05-07 | Manage rental spaces | Staff & Admin | WHEN authorized Operations Staff create or update a rental space listing (location, size, price, `Available`/`Booked` status), the system SHALL store the listing details and mark the space `Booked` upon request approval. | UC:UC-06; AD-UC-06 | Should | EI |
| F-05 | FR-05-08 | Partner submits a rental-space request | F&B / Retail Partners, Staff & Admin | WHEN a signed-in partner requests an `Available` rental space, the system SHALL create a `PENDING` request, notify Operations Staff, update status to `APPROVED` or `REJECTED` (with reason) upon review, notify the partner, and allow resubmission; IF the space is unavailable, THEN the system SHALL reject submission. | UC:UC-06; AD-UC-06 | Should | EI |
| F-06 | FR-06-01 | Manage marketing campaigns and promotion codes | Marketing & Sales Dept | WHEN Marketing staff submit valid campaign details (name, active period, audience, discount rule, code batch size), the system SHALL store the campaign in `Scheduled` state, generate promo codes, activate the campaign at start time, and expose a code-check endpoint for checkout (`F-02`); IF invalid, THEN the system SHALL show validation errors and keep form data. | UC:UC-08; AD-UC-08 | Must | EI |
| F-06 | FR-06-02 | Send a push notification to an audience | Marketing & Sales Dept | WHEN Marketing staff compose a push notification for opted-in devices, the system SHALL send immediately or queue until scheduled time, dispatch batches via `FCM/APNs`, record per-device delivery status, and remove invalid device tokens. | UC:UC-08; AD-UC-08; Context: Messaging Providers | Should | EO |
| F-06 | FR-06-03 | Prevent a promotion code from being redeemed beyond its limit | System | WHEN a visitor enters a promotion code at checkout, the system SHALL atomically verify that the campaign is `Active`, the code is unexpired, and total redemptions remain below the batch usage limit; IF expired or exhausted, THEN the system SHALL reject redemption and return the reason. | BR-04; UC:UC-08; AD-UC-08 | Must | NC |
| F-06 | FR-06-04 | View real-time park occupancy & revenue dashboard | Staff & Admin | WHEN Staff/Admin open the Analytics tab, the system SHALL aggregate and display KPI cards for active park check-ins, ticket sales revenue, and F&B voucher redemption volume. | UC:UC-09 | Should | EQ |
| F-06 | FR-06-05 | Analyze quest completion & attraction popularity metrics | Staff & Admin | WHEN Staff/Admin filter analytics by date range or park zone, the system SHALL compute checkpoint scan heatmaps, quest completion funnels, and attraction wait-time trends. | UC:UC-09 | Should | EO |
| F-06 | FR-06-09 | Manage staff roles and permissions | IT & Technical Dept | WHEN an authorized IT Admin (`FR-01-08`) assigns a role to a staff account, the system SHALL store the role assignment and enforce the updated permissions from the staff member's next request. | UC:UC-10; AD-UC-10 | Must | EI |
| F-06 | FR-06-10 | Record an audit log of admin actions | System | WHEN an admin or staff user creates, changes, or deletes privileged records (campaigns, staff roles, compliance parameters), the system SHALL append an immutable audit record capturing who, what, when, and source device. | Architecture; AD-UC-08; AD-UC-10 | Must | NC |
| F-06 | FR-06-11 | Deploy automatically through a CI/CD pipeline | IT & Technical Dept | WHEN a change is merged into the main branch, the system SHALL build and run automated tests, halt on failure, deploy passing builds to staging for IT review, promote approved builds to production, and support one-step rollback on incidents. | Architecture; UC:UC-10; AD-UC-10; ADR-001 | Must | NC |
| F-06 | FR-06-12 | Monitor servers and alert on failure | System | WHILE the periodic health-check scheduler runs, the system SHALL probe server health and 5-minute error rates, and alert the IT team by email/chat whenever a health check fails or error rate exceeds `5%` for 5 minutes. | Architecture; UC:UC-10; AD-UC-10 | Should | NC |

## L3 work items

| L3 ID | L2 ID | Layer | L3 work item | Size | Base hours | EARS precise? | Hidden work? |
|---|---|---|---|---|---|---|---|
| FR-01-01-FE | FR-01-01 | FE | Screen: registration form, terms consent & 6-digit OTP countdown (`S-F00-01`) | S | 4 | Yes | No |
| FR-01-01-BE | FR-01-01 | BE | API: duplicate phone/email check, pending registration & account activation | M | 8 | Yes | No |
| FR-01-02-BE | FR-01-02 | BE | API: 6-digit OTP generation, hashed storage (5-min TTL) & single-use verification | S | 4 | Yes | No |
| FR-01-02-INT | FR-01-02 | INT | Integration: SMS gateway & email provider OTP delivery with retry fallback | M | 8 | Yes | No |
| FR-01-03-FE | FR-01-03 | FE | Screen: password sign-in form & lock-out message (`S-F00-01`) | S | 4 | Yes | No |
| FR-01-03-BE | FR-01-03 | BE | API: verify password credentials against stored salted hash | S | 4 | Yes | No |
| FR-01-04-FE | FR-01-04 | FE | Action: "Continue with Google" SSO button & OAuth callback (`S-F00-01`) | S | 4 | Yes | No |
| FR-01-04-INT | FR-01-04 | INT | Integration: Google OAuth 2.0 / OIDC ID token verification & account linking | M | 8 | Yes | No |
| FR-01-05-FE | FR-01-05 | FE | Screen: forgot password request & new password policy UI (`S-F00-01`) | S | 4 | Yes | No |
| FR-01-05-BE | FR-01-05 | BE | API: reset password hash update & multi-device session revocation | M | 8 | Yes | No |
| FR-01-06-FE | FR-01-06 | FE | Action: log-out trigger & client secure storage cleanup (`S-F01-01`) | S | 4 | Yes | No |
| FR-01-06-BE | FR-01-06 | BE | API: revoke refresh token on sign out | S | 4 | Yes | No |
| FR-01-07-FE | FR-01-07 | FE | Screen: visitor profile view & edit form (`S-F01-01`) | S | 4 | Yes | No |
| FR-01-07-BE | FR-01-07 | BE | API: get and update visitor profile | S | 4 | Yes | No |
| FR-01-08-BE | FR-01-08 | BE | Middleware: role-based access control (RBAC) check on protected routes | M | 8 | Yes | Yes |
| FR-01-09-BE | FR-01-09 | BE | Module: per-user salted password hashing (`bcrypt` / `Argon2`) | S | 4 | Yes | Yes |
| FR-01-10-FE | FR-01-10 | FE | Storage: encrypted secure storage for JWT access & refresh tokens | S | 4 | Yes | Yes |
| FR-01-10-BE | FR-01-10 | BE | Service: JWT access token (15m) & rotating refresh token issuer | M | 8 | Yes | Yes |
| FR-01-11-BE | FR-01-11 | BE | Guard: failed-attempt counter & 15-minute lock-out enforcement | S | 4 | Yes | Yes |
| FR-02-01-FE | FR-02-01 | FE | Screen: E-Ticket catalogue, quantity picker & empty/retry states (`S-F02-01`) | S | 4 | Yes | No |
| FR-02-01-BE | FR-02-01 | BE | API: active ticket catalogue, unit pricing & stock availability check | S | 4 | Yes | No |
| FR-02-02-FE | FR-02-02 | FE | Screen: checkout summary, payment selector & refund modal (`S-F02-02`, `S-F02-03`) | M | 8 | Yes | No |
| FR-02-02-BE | FR-02-02 | BE | API: order creation (15-min TTL), single QR issuance & manual refund workflow | M | 8 | Yes | No |
| FR-02-02-INT | FR-02-02 | INT | Integration: MoMo & VNPay payment webhook verification & refund gateway | L | 16 | Yes | No |
| FR-02-03-FE | FR-02-03 | FE | Screen: Ticket Wallet (`Active`, `Used`, `Expired`) & QR viewer (`S-F02-03`) | S | 4 | Yes | No |
| FR-02-03-BE | FR-02-03 | BE | API: ticket ownership & authoritative QR credential validation | S | 4 | Yes | No |
| FR-03-01-FE | FR-03-01 | FE | Screen: interactive 2.5D/3D park map canvas & POI markers (`S-F03-01`) | L | 16 | Yes | No |
| FR-03-01-BE | FR-03-01 | BE | API: park map layer metadata & POI master list | M | 8 | Yes | No |
| FR-03-02-FE | FR-03-02 | FE | Component: location permission handler & live position marker (`S-F03-01`) | S | 4 | Yes | No |
| FR-03-02-INT | FR-03-02 | INT | Integration: device GPS / BLE Beacon location stream via Map SDK | M | 8 | Yes | No |
| FR-03-03-FE | FR-03-03 | FE | Component: POI search bar, fuzzy suggestions & detail card (`S-F03-01`, `S-F03-02`) | M | 8 | Yes | No |
| FR-03-03-BE | FR-03-03 | BE | API: POI search & similar-name suggestion query | S | 4 | Yes | No |
| FR-03-04-FE | FR-03-04 | FE | Component: client-side Map SDK pedestrian routing & distance overlay (`S-F03-02`) | M | 8 | Yes | No |
| FR-03-05-BE | FR-03-05 | BE | API: periodic attraction queue wait-time & status polling | S | 4 | Yes | No |
| FR-03-06-FE | FR-03-06 | FE | Screen: Staff attraction wait-time & `Open`/`Closed` update form (`S-F06-01`) | S | 4 | Yes | No |
| FR-03-06-BE | FR-03-06 | BE | API: update attraction queue wait time & operating status | S | 4 | Yes | No |
| FR-04-01-FE | FR-04-01 | FE | Screen: Quest Hub progress list & Camera QR Scanner (`S-F04-01`) | M | 8 | Yes | No |
| FR-04-01-BE | FR-04-01 | BE | API: active quests, checkpoint list & user completion status | S | 4 | Yes | No |
| FR-04-02-BE | FR-04-02 | BE | Validator: HMAC QR signature & GPS geofence (`<= 30 m`) anti-cheat check | M | 8 | Yes | Yes |
| FR-04-03-FE | FR-04-03 | FE | Screen: Storybook Reader with cover art, text & audio player (`S-F04-02`) | M | 8 | Yes | No |
| FR-04-03-BE | FR-04-03 | BE | API: story chapter unlock state & multimedia content delivery | S | 4 | Yes | No |
| FR-04-04-FE | FR-04-04 | FE | Modal: Badge Unlock celebration & XP/Coin reward summary (`S-F04-02`) | S | 4 | Yes | No |
| FR-04-04-BE | FR-04-04 | BE | Engine: idempotent XP/Coin crediting & zone badge assignment | M | 8 | Yes | No |
| FR-04-05-FE | FR-04-05 | FE | Screen: Daily Check-in Streak calendar & `+100 coins` claim UI (`S-F04-03`) | S | 4 | Yes | No |
| FR-04-05-BE | FR-04-05 | BE | API: daily login streak increment & `+100 coins` ledger credit | S | 4 | Yes | No |
| FR-04-06-BE | FR-04-06 | BE | Guard: same-day duplicate daily reward claim prevention | S | 4 | Yes | Yes |
| FR-04-07-BE | FR-04-07 | BE | API: park GPS check-in validation & coin reward calculation | S | 4 | Yes | No |
| FR-04-08-INT | FR-04-08 | INT | Integration: F&B Partner POS & Ticketing transaction webhook for coin earning | M | 8 | Yes | No |
| FR-04-09-BE | FR-04-09 | BE | Job: end-of-day streak-at-risk reminder & midnight reset scheduler (`ADR-004`) | M | 8 | Yes | Yes |
| FR-04-10-BE | FR-04-10 | BE | Engine: normal & major milestone evaluator with verified visit check | M | 8 | Yes | No |
| FR-04-11-BE | FR-04-11 | BE | Guard: duplicate milestone reward claim prevention | S | 4 | Yes | Yes |
| FR-04-12-FE | FR-04-12 | FE | Screen: Voucher Catalogue & coin redemption confirmation (`S-F04-04`) | S | 4 | Yes | No |
| FR-04-12-BE | FR-04-12 | BE | API: atomic coin deduction, voucher code issuance & redemption history | M | 8 | Yes | No |
| FR-04-13-INT | FR-04-13 | INT | Integration: F&B Partner POS voucher verification & redemption callback | M | 8 | Yes | No |
| FR-05-01-FE | FR-05-01 | FE | Screen: Social Gallery photo composer with caption, location & retry (`S-F05-01`) | M | 8 | Yes | No |
| FR-05-01-BE | FR-05-01 | BE | API: post creation & automated keyword/rule moderation filter | M | 8 | Yes | No |
| FR-05-01-INT | FR-05-01 | INT | Integration: Cloud Storage / CDN photo upload & thumbnail URL service | M | 8 | Yes | No |
| FR-05-02-FE | FR-05-02 | FE | Action & Screen: post report button & Admin moderation queue (`S-F05-01`, `S-F06-01`) | S | 4 | Yes | No |
| FR-05-02-BE | FR-05-02 | BE | API: auto-hide flagged/reported posts & Admin remove/restore workflow | M | 8 | Yes | No |
| FR-05-03-FE | FR-05-03 | FE | Screen: Social Gallery photo grid with infinite scroll & empty state (`S-F05-01`) | M | 8 | Yes | No |
| FR-05-03-BE | FR-05-03 | BE | API: paginated published posts query (newest-first) | S | 4 | Yes | No |
| FR-05-04-FE | FR-05-04 | FE | Screen: Indie artist performance schedule submission form (`S-F05-02`) | S | 4 | Yes | No |
| FR-05-04-BE | FR-05-04 | BE | API: create `PENDING` event listing & artist status notifications | S | 4 | Yes | No |
| FR-05-05-FE | FR-05-05 | FE | Screen: Admin event approval/rejection review panel (`S-F06-01`) | S | 4 | Yes | No |
| FR-05-05-BE | FR-05-05 | BE | API: two-stage clash detection (on submit & approval) & calendar publishing | M | 8 | Yes | No |
| FR-05-06-FE | FR-05-06 | FE | Screen: public event calendar with date & category filters (`S-F05-02`) | S | 4 | Yes | No |
| FR-05-06-BE | FR-05-06 | BE | API: query approved events by date and category | S | 4 | Yes | No |
| FR-05-07-BE | FR-05-07 | BE | API: rental space CRUD & availability state lock (`Available`/`Booked`) | S | 4 | Yes | No |
| FR-05-08-FE | FR-05-08 | FE | Screen: partner rental request form & Admin approval dashboard (`S-F06-01`) | M | 8 | Yes | No |
| FR-05-08-BE | FR-05-08 | BE | API: rental request workflow (`PENDING` -> `APPROVED`/`REJECTED`) & alerts | S | 4 | Yes | No |
| FR-06-01-FE | FR-06-01 | FE | Screen: marketing campaign creator & promo batch form (`S-F06-01`) | M | 8 | Yes | No |
| FR-06-01-BE | FR-06-01 | BE | API: campaign lifecycle scheduler (`Scheduled` -> `Active`) & code generator | M | 8 | Yes | No |
| FR-06-02-FE | FR-06-02 | FE | Screen: push notification composer, audience picker & scheduler (`S-F06-01`) | S | 4 | Yes | No |
| FR-06-02-BE | FR-06-02 | BE | Service: opted-in audience resolver & scheduled push queue worker | M | 8 | Yes | No |
| FR-06-02-INT | FR-06-02 | INT | Integration: FCM/APNs batch push delivery & invalid-token cleanup | M | 8 | Yes | No |
| FR-06-03-BE | FR-06-03 | BE | Guard: atomic promo code usage-cap & expiry check for checkout | M | 8 | Yes | Yes |
| FR-06-04-FE | FR-06-04 | FE | Screen: Admin real-time occupancy & revenue KPI dashboard (`S-F06-01`) | M | 8 | Yes | No |
| FR-06-04-BE | FR-06-04 | BE | API: real-time park occupancy, ticket sales & voucher aggregation | M | 8 | Yes | No |
| FR-06-05-FE | FR-06-05 | FE | Chart: quest completion funnel & attraction wait-time trend views (`S-F06-01`) | M | 8 | Yes | No |
| FR-06-05-BE | FR-06-05 | BE | API: historical quest & attraction telemetry analytics query | M | 8 | Yes | No |
| FR-06-09-FE | FR-06-09 | FE | Screen: IT Admin staff role & permission assignment UI (`S-F06-01`) | S | 4 | Yes | No |
| FR-06-09-BE | FR-06-09 | BE | API: persist staff role assignment & sync permissions immediately | S | 4 | Yes | No |
| FR-06-10-BE | FR-06-10 | BE | Module: append-only immutable audit log writer (who, what, when, device) | M | 8 | Yes | Yes |
| FR-06-11-INT | FR-06-11 | INT | Pipeline: automated CI/CD build, tests, staging gate & one-step rollback | M | 8 | Yes | Yes |
| FR-06-12-INT | FR-06-12 | INT | Monitoring: 5-minute error-rate (`> 5%`) health probe & IT email/chat alert | M | 8 | Yes | Yes |

48 L2 functions, 85 L3 work items, 524 base hours. No row is above the 16-hour ceiling.

NC rows (`FR-01-08`, `FR-01-09`, `FR-01-10`, `FR-01-11`, `FR-04-02`, `FR-04-06`, `FR-04-11`, `FR-06-03`, `FR-06-10`, `FR-06-11`, `FR-06-12`) score zero function points but carry real work: that gap is why the function-point count is only a cross-check.