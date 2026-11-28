# W5 Baseline and handover: MySen

Lesson 5 (block W5). The baseline every later lesson and DBIZ3 refer to.

## 1. Three scenarios

| Scenario | Person-hours | Cost (VND) | Role in the cash-flow analysis (W6) |
|---|---|---|---|
| Pessimistic: Must only | 171.2 | 48.240.000 | Lowest investment, lowest benefit |
| Base: Must + Should | 289.2 | 80.640.000 | The client figure; base cash flow |
| Optimistic: full scope | 386.6 | 108.180.000 | If the Could pool is never consumed |

## 2. Assumptions

| Assumption | Value | Source |
|---|---|---|
| Junior / Senior / Expert rate | 200.000 / 300.000 / 400.000 VND per hour | Class Parameters (ITviec 2025-26 salary report) |
| AI leverage FE / BE / INT | 0.35 / 0.7 / 1.0 | Class Parameters |
| Verification factor precise / vague | 0.15 / 0.4 | Class Parameters |
| Hours per function point (cross-check only) | 3 | Class Parameters |
| Team capacity | 420 person-hours (7 people x 12 weeks x 5 h) | Class Parameters |
| Money contingency on the Must set | 10% = 4.824.000 VND | Class Parameters |

## 3. tasks.md seed (effective priority Must)

Risk order: 1 = INT (external services), 2 = BE, 3 = FE. DBIZ3 starts with the riskiest rows.

| L3 ID | Layer | Person-hours | Risk order |
|---|---|---|---|
| FR-01-02-INT | INT | 9.2 | 1 |
| FR-02-02-INT | INT | 9.2 | 1 |
| FR-04-02-INT | INT | 9.2 | 1 |
| FR-06-11-INT | INT | 9.2 | 1 |
| FR-01-01-BE | BE | 3.4 | 2 |
| FR-01-02-BE | BE | 3.4 | 2 |
| FR-01-03-BE | BE | 3.4 | 2 |
| FR-01-05-BE | BE | 3.4 | 2 |
| FR-01-06-BE | BE | 3.4 | 2 |
| FR-01-08-BE | BE | 3.4 | 2 |
| FR-01-09-BE | BE | 3.4 | 2 |
| FR-01-10-BE | BE | 3.4 | 2 |
| FR-01-11-BE | BE | 3.4 | 2 |
| FR-02-01-BE | BE | 3.4 | 2 |
| FR-02-02-BE | BE | 6.8 | 2 |
| FR-02-03-BE | BE | 3.4 | 2 |
| FR-02-14-BE | BE | 3.4 | 2 |
| FR-02-15-BE | BE | 6.8 | 2 |
| FR-03-01-BE | BE | 3.4 | 2 |
| FR-03-02-BE | BE | 3.4 | 2 |
| FR-03-03-BE | BE | 3.4 | 2 |
| FR-04-01-BE | BE | 3.4 | 2 |
| FR-04-02-BE | BE | 6.8 | 2 |
| FR-04-03-BE | BE | 3.4 | 2 |
| FR-04-04-BE | BE | 3.4 | 2 |
| FR-04-06-BE | BE | 3.4 | 2 |
| FR-06-09-BE | BE | 3.4 | 2 |
| FR-06-10-BE | BE | 3.4 | 2 |
| FR-01-01-FE | FE | 2.0 | 3 |
| FR-01-03-FE | FE | 2.0 | 3 |
| FR-01-05-FE | FE | 2.0 | 3 |
| FR-01-06-FE | FE | 2.0 | 3 |
| FR-01-10-FE | FE | 2.0 | 3 |
| FR-02-01-FE | FE | 2.0 | 3 |
| FR-02-02-FE | FE | 2.0 | 3 |
| FR-02-03-FE | FE | 2.0 | 3 |
| FR-03-01-FE | FE | 8.0 | 3 |
| FR-03-02-FE | FE | 4.0 | 3 |
| FR-03-03-FE | FE | 2.0 | 3 |
| FR-03-04-FE | FE | 4.0 | 3 |
| FR-04-01-FE | FE | 2.0 | 3 |
| FR-04-02-FE | FE | 4.0 | 3 |
| FR-04-03-FE | FE | 4.0 | 3 |
| FR-04-04-FE | FE | 2.0 | 3 |
| FR-06-09-FE | FE | 2.0 | 3 |

## 4. Open questions for the client

| # | Question | Blocking? |
|---|---|---|
| 1 | Can gate staff visually verify active in-app E-Ticket QR codes during the first launch weeks before dedicated turnstile API sync (`FR-02-05`, `FR-02-07`) is deployed? | No |
| 2 | Is 15 minutes the agreed payment expiry window for unpaid `PENDING` ticket orders (`FR-02-02`, `FR-02-14`) across both MoMo and VNPay? | Yes (`FR-02-02`, `FR-02-14`) |
| 3 | Is the 30-meter GPS geofence radius (`ADR-005`) acceptable across all outdoor heritage zones in Đầm Sen Park without causing false rejections? | Yes (`FR-04-02`) |
| 4 | Will F&B Partner POS terminals support webhook transaction callbacks at launch, or start with manual voucher code entry (`FR-04-08`, `FR-04-10`)? | No |