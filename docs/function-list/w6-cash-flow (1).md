# W6 Cash flow and investment decision: Dien Hong System

> Project cash-flow model for Dien Hong. Build costs and the Must-set contingency are taken from W2 and the project assumptions. Operating costs, annual benefits, discount rate, evaluation horizon and adoption ramp-up are team estimates for this coursework, not verified client financial data.

## 1. Assumptions

| Assumption | Value |
|---|---|
| Discount rate (hurdle rate) | 10% per year |
| Evaluation horizon | 4 years |
| Annual running cost | Must: 12,000,000 · Base: 14,000,000 · Optimistic: 15,000,000 VND/year (hosting, database, backups, notification services, maintenance and support) |
| Contingency | 10% of the Must cost = 3,928,000 VND, same in every scenario |
| Estimated operating scale | 60 residents · 15 nurses |
| Staff time value | 50,000 VND/hour |
| Steady-state annual benefit | Must: 52,000,000 · Should: 8,580,000 · Could: 2,860,000 VND |
| Adoption ramp-up (share of steady-state benefit) | Year 1: 60% · Year 2: 85% · Year 3 to 4: 100% |

Where the benefit comes from (team estimates, to be validated with the care facility): reduced time spent managing resident records, updating resident information and handling alerts (Must), based on an estimated 15 minutes saved per resident per week and an additional 5 staff hours saved per week; reduced manual follow-up and faster access to resident profiles and condition history (Should), estimated at an additional 3.3 staff hours saved per week; and improved administrative efficiency through optional dashboard and reporting functions (Could), estimated at an additional 1.1 staff hours saved per week. The calculation assumes 60 residents, 15 nurses, a staff time value of 50,000 VND/hour and 52 weeks per year.

Benefits are treated as estimated operational savings and staff time value, not direct sales revenue. Must benefits are 1,040 hours × 50,000 VND = 52,000,000 VND/year. Should adds 3.3 × 52 × 50,000 = 8,580,000 VND/year; Could adds 1.1 × 52 × 50,000 = 2,860,000 VND/year.

## 2. Scenario baseline

| Scenario | Scope | Build cost (VND) | Contingency (VND) | Year-0 investment (VND) |
|---|---|---:|---:|---:|
| Pessimistic: Must only | Must only | 39.280.000 | 3.928.000 | 43.208.000 |
| Base: Must + Should | Must + Should | 55.340.000 | 3.928.000 | 59.268.000 |
| Optimistic: full scope | Must + Should + Could | 65.600.000 | 3.928.000 | 69.528.000 |

Build costs follow the W2 headline figures: Must only = 39,280,000 VND; Must + Should = 55,340,000 VND; full scope = 65,600,000 VND. The contingency is 10% of the Must-only cost and is included once in Year 0 for each scenario. No additional 20% contingency is added to the Could pool.

## 3. Cash flow by scenario

All amounts are in VND. Year 0 includes build cost plus contingency. Annual benefits follow the adoption ramp-up. Running costs are incurred from Year 1 to Year 4.

### 3.1 Pessimistic: Must only

- Steady-state annual benefit: **52.000.000 VND**.
- Annual running cost: **12.000.000 VND**.
- Initial investment in Year 0: **43.208.000 VND**.

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 |
|---|---:|---:|---:|---:|---:|
| Benefits | 0 | 31.200.000 | 44.200.000 | 52.000.000 | 52.000.000 |
| Running cost | 0 | -12.000.000 | -12.000.000 | -12.000.000 | -12.000.000 |
| Investment (build + contingency) | -43.208.000 | 0 | 0 | 0 | 0 |
| **Net cash flow** | **-43.208.000** | **19.200.000** | **32.200.000** | **40.000.000** | **40.000.000** |
| Cumulative net cash flow | -43.208.000 | -24.008.000 | 8.192.000 | 48.192.000 | 88.192.000 |
| PV of net cash flow (10%) | -43.208.000 | 17.454.545 | 26.611.570 | 30.052.592 | 27.320.538 |

### 3.2 Base: Must + Should

- Steady-state annual benefit: **60.580.000 VND**.
- Annual running cost: **14.000.000 VND**.
- Initial investment in Year 0: **59.268.000 VND**.

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 |
|---|---:|---:|---:|---:|---:|
| Benefits | 0 | 36.348.000 | 51.493.000 | 60.580.000 | 60.580.000 |
| Running cost | 0 | -14.000.000 | -14.000.000 | -14.000.000 | -14.000.000 |
| Investment (build + contingency) | -59.268.000 | 0 | 0 | 0 | 0 |
| **Net cash flow** | **-59.268.000** | **22.348.000** | **37.493.000** | **46.580.000** | **46.580.000** |
| Cumulative net cash flow | -59.268.000 | -36.920.000 | 573.000 | 47.153.000 | 93.733.000 |
| PV of net cash flow (10%) | -59.268.000 | 20.316.364 | 30.985.950 | 34.996.243 | 31.814.767 |

### 3.3 Optimistic: full scope

- Steady-state annual benefit: **63.440.000 VND**.
- Annual running cost: **15.000.000 VND**.
- Initial investment in Year 0: **69.528.000 VND**.

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 |
|---|---:|---:|---:|---:|---:|
| Benefits | 0 | 38.064.000 | 53.924.000 | 63.440.000 | 63.440.000 |
| Running cost | 0 | -15.000.000 | -15.000.000 | -15.000.000 | -15.000.000 |
| Investment (build + contingency) | -69.528.000 | 0 | 0 | 0 | 0 |
| **Net cash flow** | **-69.528.000** | **23.064.000** | **38.924.000** | **48.440.000** | **48.440.000** |
| Cumulative net cash flow | -69.528.000 | -46.464.000 | -7.540.000 | 40.900.000 | 89.340.000 |
| PV of net cash flow (10%) | -69.528.000 | 20.967.273 | 32.168.595 | 36.393.689 | 33.085.172 |

## 4. Results

| Metric | Pessimistic: Must only | Base: Must + Should | Optimistic: full scope |
|---|---:|---:|---:|
| Year-0 investment (VND) | 43.208.000 | 59.268.000 | 69.528.000 |
| Steady-state benefit per year (VND) | 52.000.000 | 60.580.000 | 63.440.000 |
| NPV at 10% (VND) | 58.231.246 | 58.845.324 | 53.086.729 |
| IRR | 55.4% | 44.8% | 37.5% |
| Simple payback (years) | 1.75 | 1.98 | 2.16 |
| Profitability index | 2.35 | 1.99 | 1.76 |

**Decision signal:** All three scenarios have positive NPV and an IRR above the 10% hurdle rate under the current team estimates. The Pessimistic scenario has the lowest initial investment and strongest IRR/payback. The Base scenario has the highest NPV, while the Optimistic scenario has a lower NPV than Base because its additional Could benefits are modest relative to its higher build and running costs.

## 5. Interpretation and recommendation

The **Base scenario (Must + Should)** is the recommended planning baseline. It is also the W2 Expected figure given to the client (55,340,000 VND build cost before contingency). It produces the highest NPV in this model while including the Should functions that improve access to resident information and reduce manual follow-up. The Must-only scenario remains a lower-cost fallback if the available budget is constrained.

The Optimistic scenario includes all Could functions, but its additional estimated benefit does not compensate fully for the higher investment and annual running cost compared with Base. The Could scope should therefore remain optional and be implemented only if the facility confirms its value or additional budget is available.

These results are conditional on the assumptions. In particular, time saved is treated as economic value; it does not automatically mean the facility reduces its payroll or receives cash income. The benefits should be validated by measuring actual staff time before and after implementation.

## 6. Formulas

- Net cash flow = Benefits − Running cost − Investment.
- Present value (PV) in year *t* = Net cash flow in year *t* ÷ (1 + *r*)^*t*.
- NPV = Sum of present values from Year 0 to Year 4.
- IRR = Discount rate at which NPV equals zero.
- Simple payback = Full years before recovery + unrecovered investment at the start of the recovery year ÷ net cash flow in the recovery year.
- Profitability index = Present value of future net cash inflows ÷ initial investment.

## 7. Limitations and items to validate

1. The operating scale (60 residents and 15 nurses) is a planning assumption supplied for this model; confirm it against the actual care facility.
2. The staff time value of 50,000 VND/hour is an assumed blended value, not a verified payroll rate.
3. The time savings (15 minutes per resident per week; 5 shared staff hours per week for Must; 3.3 hours for Should; 1.1 hours for Could) are team estimates and should be checked with staff.
4. Annual running costs (12–15 million VND depending on scope) are allowances for hosting, database, backups, notifications, maintenance and support. They are not supplier quotations.
5. The 10% discount rate, four-year horizon and adoption ramp-up are project-specific modelling assumptions, not values stated in W2. Replace them if the lecturer supplies required class parameters.
6. The contingency is calculated once as 10% of the Must cost and included in Year 0. Do not add another contingency percentage to Could.

---

**Submission note:** this cash-flow analysis uses W2 build-cost baselines and W2/W5 contingency logic. All other financial assumptions are clearly identified as team estimates for Dien Hong and should not be presented as measured client data.