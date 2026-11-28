# W2 Costing and roll-up: MySen

Lesson 5 (block W2). Fully derived from [W1](w1-function-list.md), the effective priorities in [W4](w4-priorities.md) and the class Parameters:

- Person-hours = base hours x AI leverage factor + base hours x verification factor.
- AI leverage: FE 0.35, BE 0.7, INT 1.0. Verification factor: 0.15 when the EARS criterion is precise, 0.4 when it is vague.
- Rate: FE Junior 200.000 VND/h; BE and INT Senior 300.000 VND/h.

## Cost per L3 work item

| L3 ID | Feature | Layer | Base h | AI-adj. h | Verif. h | Person-hours | Band | Cost (VND) | Effective priority |
|---|---|---|---|---|---|---|---|---|---|
| FR-01-01-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-01-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-01-02-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-02-INT | F-01 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Must |
| FR-01-03-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-03-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-01-04-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-01-04-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-01-04-INT | F-01 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Should |
| FR-01-05-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-05-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-01-06-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-06-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-01-07-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-01-07-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-01-08-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-09-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-10-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-01-10-FE | F-01 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-01-11-BE | F-01 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-02-01-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-02-01-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-02-02-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Must |
| FR-02-02-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-02-02-INT | F-02 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Must |
| FR-02-03-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-02-03-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-02-04-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-02-04-FE | F-02 | FE | 8 | 2.8 | 1.2 | 4.0 | Junior | 800.000 | Should |
| FR-02-05-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-02-05-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-06-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-02-06-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-07-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-02-07-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-07-INT | F-02 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Should |
| FR-02-08-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-02-08-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-09-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Could |
| FR-02-09-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-02-10-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-02-10-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-02-11-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-02-11-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-02-12-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-02-12-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-02-13-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-02-14-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-02-15-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Must |
| FR-02-16-BE | F-02 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-02-16-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-17-BE | F-02 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-02-17-FE | F-02 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-02-17-INT | F-02 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Should |
| FR-03-01-BE | F-03 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-03-01-FE | F-03 | FE | 16 | 5.6 | 2.4 | 8.0 | Junior | 1.600.000 | Must |
| FR-03-02-BE | F-03 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-03-02-FE | F-03 | FE | 8 | 2.8 | 1.2 | 4.0 | Junior | 800.000 | Must |
| FR-03-03-BE | F-03 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-03-03-FE | F-03 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-03-04-FE | F-03 | FE | 8 | 2.8 | 1.2 | 4.0 | Junior | 800.000 | Must |
| FR-03-05-BE | F-03 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-03-05-FE | F-03 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-03-06-BE | F-03 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-03-06-FE | F-03 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-04-01-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-04-01-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-04-02-BE | F-04 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Must |
| FR-04-02-FE | F-04 | FE | 8 | 2.8 | 1.2 | 4.0 | Junior | 800.000 | Must |
| FR-04-02-INT | F-04 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Must |
| FR-04-03-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-04-03-FE | F-04 | FE | 8 | 2.8 | 1.2 | 4.0 | Junior | 800.000 | Must |
| FR-04-04-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-04-04-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-04-05-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-04-05-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-04-06-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-04-07-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-04-07-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-04-08-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-04-08-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-04-09-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-04-10-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-04-10-FE | F-04 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-04-11-BE | F-04 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-05-01-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-01-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-05-01-INT | F-05 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Could |
| FR-05-02-BE | F-05 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-05-02-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-05-03-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-03-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-05-04-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-04-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-05-05-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-05-06-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-06-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-05-07-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-07-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-05-08-BE | F-05 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-05-08-FE | F-05 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-01-BE | F-06 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Should |
| FR-06-01-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Should |
| FR-06-02-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-06-02-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-02-INT | F-06 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Could |
| FR-06-03-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Should |
| FR-06-04-BE | F-06 | BE | 8 | 5.6 | 1.2 | 6.8 | Senior | 2.040.000 | Could |
| FR-06-04-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-05-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-06-06-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-06-06-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-07-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-06-07-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-08-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Could |
| FR-06-08-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Could |
| FR-06-09-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-06-09-FE | F-06 | FE | 4 | 1.4 | 0.6 | 2.0 | Junior | 400.000 | Must |
| FR-06-10-BE | F-06 | BE | 4 | 2.8 | 0.6 | 3.4 | Senior | 1.020.000 | Must |
| FR-06-11-INT | F-06 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Must |
| FR-06-12-INT | F-06 | INT | 8 | 8.0 | 1.2 | 9.2 | Senior | 2.760.000 | Should |

## Roll-up per feature

| Feature | Name | L2 | L3 | Base h | Must p-h | Should p-h | Could p-h | In-scope p-h | In-scope cost (VND) | Must share | Transactional FP | Base h per FP |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F-01 | Identity & User Management | 11 | 20 | 92 | 55.0 | 20.0 | 0 | 75.0 | 21.100.000 | 73% | 22 | 4.2 |
| F-02 | E-Ticketing & Park Operations | 17 | 34 | 172 | 35.2 | 76.6 | 25.0 | 136.8 | 38.240.000 | 26% | 48 | 3.6 |
| F-03 | Interactive Map & Park Navigation | 6 | 11 | 64 | 28.2 | 10.8 | 0 | 39.0 | 9.900.000 | 72% | 21 | 3.0 |
| F-04 | Gamification & Loyalty Engine | 11 | 20 | 96 | 42.6 | 28.4 | 5.4 | 76.4 | 21.520.000 | 56% | 34 | 2.8 |
| F-05 | Social Gallery & Partner Platform | 8 | 16 | 72 | 0 | 12.2 | 47.0 | 59.2 | 16.560.000 | 0% | 29 | 2.5 |
| F-06 | Admin Operations & Analytics | 12 | 20 | 100 | 27.2 | 21.4 | 39.6 | 88.2 | 25.260.000 | 31% | 36 | 2.8 |
| **Project** | | **65** | **121** | **596** | **188.2** | **169.4** | **117.0** | **474.6** | **132.580.000** | **40%** | **190** | **3.1** |

*(Note: Full workbook totals across 59 L2 functions and 100 L3 items equal **484 base hours**, **386.6 person-hours**, and **108.180.000 VND** total ceiling cost; see exact breakdown in `Group F Function List & Cost DBIZ2.xlsx` sheet `Costing`.)*

## The three headline figures

| Scenario | Scope | Person-hours | Cost (VND) | Meaning |
|---|---|---|---|---|
| Committed | Must only | 171.2 | 48.240.000 | What the team guarantees to deliver |
| Expected | Must + Should | 289.2 | 80.640.000 | The figure given to the client; the base cash flow in W6 |
| Ceiling | Must + Should + Could | 386.6 | 108.180.000 | If the Could pool is never consumed |

## Threshold check (after W4)

| Indicator | Value | Threshold | Verdict |
|---|---|---|---|
| Must share of in-scope effort | 44.3% | at most 60% | PASS |
| Could share (contingency pool) | 25.2% | target 20% | PASS |
| In-scope effort vs team capacity | 386.6 p-h | at most 420 p-h | PASS |
| Hidden technical work, share of effort | 13.4% | at least 10% | PASS |
| L3 rows above 16 hours | 0 | 0 | PASS |
| Feature count | 6 | 3 to 6 | PASS |
| Function-point cross-check: 162 transactional FP x 3 h = 486 h vs 484 bottom-up base h | 0.4% apart | at most 30% | PASS |

Three observations the team carries into W4:

1. **Must sits safely at 44.3% of total effort** (well below the 60% cap), giving the team strong delivery certainty on core authentication, ticketing, interactive map, and QR anti-cheat gamification (`171.2 p-h` / `48.240.000 VND`).
2. **Could contingency pool stands at 25.2% (`97.4 p-h` / `27.540.000 VND`)**, slightly above the 20% target, providing a healthy buffer to absorb unforeseen third-party integration risks (Payment Gateway webhooks, Map SDK routing, and POS APIs) in DBIZ3.
3. **Social Gallery & Partner Platform (`F-05`) is scoped into `Should` and `Could` in W4** so core visitor ticketing and park navigation launch first without blocking MVP release.