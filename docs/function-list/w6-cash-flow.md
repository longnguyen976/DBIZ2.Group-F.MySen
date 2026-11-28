# W6 Cash flow and investment decision: MySen

Lesson 6 (Capital Budgeting). Takes the three scenarios from [W5](w5-handover.md).

## 1. Assumptions

| Assumption | Value |
|---|---|
| Discount rate (hurdle rate) | 12% per year |
| Evaluation horizon | 5 years |
| Annual running cost | 15% of build cost per year (cloud hosting, CDN, SMS/OTP gateway, push & map API maintenance) |
| Contingency | 10% of the Must cost = 4.824.000 VND, same in every scenario |
| Steady-state annual benefit | Must 32.000.000 · Should 18.000.000 · Could 4.000.000 VND |
| Adoption ramp-up (share of steady-state benefit) | Year 1: 40% · Year 2: 70% · Year 3 to 5: 100% |

Where the benefit comes from (team estimates, to be validated with Đầm Sen Park management after the first operating quarter): reduced manual box-office queuing and paper ticket printing costs plus higher digital conversion (Must), incremental repeat park visits, F&B voucher cross-selling, and automated turnstile/refund operations (Should), and ancillary partner booth/event monetization plus cohort analytics optimization (Could).

## Pessimistic: Must only

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 12.800.000 | 22.400.000 | 32.000.000 | 32.000.000 | 32.000.000 |
| Running cost | 0 | -7.236.000 | -7.236.000 | -7.236.000 | -7.236.000 | -7.236.000 |
| Investment (build + contingency) | -53.064.000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -53.064.000 | 5.564.000 | 15.164.000 | 24.764.000 | 24.764.000 | 24.764.000 |
| Cumulative net cash flow | -53.064.000 | -47.500.000 | -32.336.000 | -7.572.000 | 17.192.000 | 41.956.000 |
| PV of net cash flow | -53.064.000 | 4.967.857 | 12.088.648 | 17.626.533 | 15.737.976 | 14.051.764 |

## Base: Must + Should

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 20.000.000 | 35.000.000 | 50.000.000 | 50.000.000 | 50.000.000 |
| Running cost | 0 | -12.096.000 | -12.096.000 | -12.096.000 | -12.096.000 | -12.096.000 |
| Investment (build + contingency) | -85.464.000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -85.464.000 | 7.904.000 | 22.904.000 | 37.904.000 | 37.904.000 | 37.904.000 |
| Cumulative net cash flow | -85.464.000 | -77.560.000 | -54.656.000 | -16.752.000 | 21.152.000 | 59.056.000 |
| PV of net cash flow | -85.464.000 | 7.057.143 | 18.258.929 | 26.979.318 | 24.088.677 | 21.507.747 |

## Optimistic: full scope

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 21.600.000 | 37.800.000 | 54.000.000 | 54.000.000 | 54.000.000 |
| Running cost | 0 | -16.227.000 | -16.227.000 | -16.227.000 | -16.227.000 | -16.227.000 |
| Investment (build + contingency) | -113.004.000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -113.004.000 | 5.373.000 | 21.573.000 | 37.773.000 | 37.773.000 | 37.773.000 |
| Cumulative net cash flow | -113.004.000 | -107.631.000 | -86.058.000 | -48.285.000 | -10.512.000 | 27.261.000 |
| PV of net cash flow | -113.004.000 | 4.797.321 | 17.197.863 | 26.886.077 | 24.005.426 | 21.433.416 |

## Results

| Metric | Pessimistic: Must only | Base: Must + Should | Optimistic: full scope |
|---|---|---|---|
| Year-0 investment (VND) | 53.064.000 | 85.464.000 | 113.004.000 |
| Steady-state benefit per year (VND) | 32.000.000 | 50.000.000 | 54.000.000 |
| NPV at 12% (VND) | 11.408.778 | 12.427.814 | -18.683.897 |
| IRR | 18.8% | 16.5% | 6.4% |
| Simple payback (years) | 3.31 | 3.44 | 4.28 |
| Profitability index | 1.21 | 1.15 | 0.83 |
| Decision signal | ACCEPT | ACCEPT | REJECT / REVIEW |

Reading: the Base scenario (`Must + Should`, `80.640.000 VND` build cost / `85.464.000 VND` Year-0 total investment) delivers the highest positive NPV (`12.427.814 VND`) and clears the 12% hurdle rate with a `16.5%` IRR, making it the recommended baseline presented to the client. Including all `Could` items in Year 0 increases build and annual running costs faster than incremental benefit, turning NPV negative (`-18.683.897 VND`) and dropping IRR to `6.4%`; therefore, `Could` items remain strictly in the scope contingency pool rather than committed scope.

Formulas: $\text{NPV} = \sum_{t=0}^{5} \frac{\text{Net cash flow}_t}{(1 + r)^t}$; $\text{IRR}$ is the discount rate $r$ at which $\text{NPV} = 0$; simple payback interpolates inside the year in which cumulative net cash flow turns positive; $\text{Profitability Index} = 1 + \frac{\text{NPV}}{\text{Investment}}$.