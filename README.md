# Italy Bank: Profitability & Risk Dashboard

*Power BI case study · Corporate Banking · FY2025*

## 1. Business Context

Italy Bank lends to corporate clients through four products (Working Capital Revolver, Corporate Term Loan, Trade Finance Loan, Equipment Finance Loan) across eight branches. Management reviews performance every month, but profitability, funding cost, margins, overdue loans and provisions sit in separate views. Leadership has the data, yet not the complete picture.

## 2. Business Problem

Management needs one decision-ready view that answers five questions:

1. Why are profit and margins changing?
2. Is loan growth actually profitable?
3. How much is funding cost reducing Net Interest Margin (NIM)?
4. Where is credit stress building?
5. How much are provisions reducing net profit?

## 3. Objectives

- Build a single Power BI dashboard that connects earnings, margins, credit risk and provisions.
- Explain *why* profit and margin move, not only *what* moved, using a profitability bridge and margin decomposition.
- Detect abnormal KPIs automatically and point leadership to where to look first.
- Let users choose a period and scenario, then drill from portfolio to client to facility.
- Turn each insight into a recommended action that a manager can approve or challenge.

## 4. Stakeholders and Decisions Supported

| Stakeholder | Decision to support | Where in the dashboard |
| --- | --- | --- |
| Head of Corporate Banking / CFO | Where to grow, reprice or cut back; profit outlook | Executive Overview, Profitability Bridge |
| Treasury / ALM | Funding mix and repricing when Cost of Funds spikes | Margin Pressure |
| Chief Risk Officer | Watchlist, provisioning review, concentration limits | Credit Risk & Exposure, Client Matrix |
| Relationship Managers | Which clients and facilities need action now | Client Summary, Facility Detail |

## 5. Dataset

Source file: `Bank_data.xlsx`

| Table | Grain | Size | Content |
| --- | --- | --- | --- |
| Fact\_Banking\_Monthly | Facility × month | 2,880 rows × 23 columns (240 facilities × 12 months) | Principal balances, limits, overdue, DPD, risk grade, interest income and expense, fee income, operating expense, provision, tax |
| Dim\_Client | Client | 120 | Industry, client segment |
| Dim\_Product | Product | 4 | Product name |
| Dim\_Branch | Branch | 8 | Branch name, region |

## 6. KPI Framework

| Group | KPIs | Type |
| --- | --- | --- |
| Size and earnings | Loan Book | Snapshot |
| Income statement | Interest Income, Interest Expense, NII, Fee Income, Operating Income, Operating Expense, Provision Expense, Tax, Net Profit | Flow |
| Margins | NIM, Yield on Advances, Cost of Funds, Spread, Net Profit Margin, Cost-to-Income | Ratio |
| Credit risk | Overdue Principal, High-Risk Exposure, Facility Limit, Available Limit, Days Past Due | Snapshot |
| Credit ratios | NPL Ratio (DPD > 90), High-Risk %, Limit Utilisation, Provision / Operating Income, Risk-adjusted Return | Ratio |

Three calculation rules apply to every KPI:

1. **Flow** KPIs add up within the selected period.
2. **Snapshot** KPIs take the latest available snapshot on or before the selected date and are never summed across months.
3. **Ratios** are recomputed from numerator and denominator, annualised with 365 / period days, using day-weighted average balances.

A calculation group (Normal, MTD, QTD, Rolling 3M) applies one shared period rule to every measure through `SELECTEDMEASURE()`.

## 7. Deliverables

| Page | Question it answers |
| --- | --- |
| Executive Overview | How is the bank doing, and what is abnormal? |
| Margin Pressure | How much is funding cost reducing NIM, and which products earn most? |
| Profitability Bridge | Where does income go before it becomes Net Profit? |
| Credit Risk & Exposure | Where is credit stress building, and how concentrated is it? |
| Client Matrix | Which clients are profitable but risky, or risky and unprofitable? |
| Client Summary (drill-through) | Is this client worth keeping, repricing or restricting? |
| Facility Detail (drill-through) | Which facility is overdue, by how much, and how much limit is left? |

<img src="pictures\Executive overview.png" width="400"> <img src="pictures\Margin pressure.png" width="400">
<img src="pictures\Profitability.png" width="400"> <img src="pictures\Credit risk & exposure.png" width="400">
<img src="pictures\Risk matrix.png" width="400"> <img src="pictures\Client summary.png" width="400">
<img src="pictures\Facility detail.png" width="400">
## 8. Approach

1. **Frame the problem:** clarify decisions, KPIs and definitions with stakeholders. 
2. **Model:** star schema with one fact table, three dimensions and a date table.
3. **Measure (DAX):** Flow, Snapshot and Ratio measures, then the scenario calculation group.
4. **Visualise and narrate:** one story per page, insight text with a recommended action.

## 9. Headline Findings

- NIM averages 5.05% for the year but drops to 4.15% in June when Cost of Funds spikes.
- High-Risk Exposure is 3.73bn (18.0% of Loan Book) while the NPL ratio is only 0.87%, so rating-based risk is far wider than DPD-based NPL.
- Trade Finance earns the highest NIM (5.61%) while Working Capital Revolver is the largest book.
- Provision is concentrated in a small number of client groups.

## 10. Success Criteria

- Every headline KPI reconciles to an independent control total.
- Each of the five business questions is answered by at least one visual.
- Abnormal months are flagged without manual searching.
- A manager can go from portfolio to client to facility in three clicks.
- Every insight text carries a clear action.

## 11. Assumptions and Open Questions

- High-Risk is a rating-based flag, not a DPD rule. The official definition of High-Risk and NPL should be confirmed.
- Average Earning Assets appears to exclude stressed facilities. The exclusion rule should be confirmed.
- Cost of Funds is nearly identical across products, so product NIM differences reflect pricing, not funding.
- No budget or target is provided. Benchmark definition: \[prior period / budget / average, to be confirmed\].

## 12. Repository Structure

```
├── data/                 # source Excel file and data dictionary
├── file/              # .pbix file and DAX measure library
├── pdf/                # file pdf dashboard
├── pictures/                 # screenshots every page in dashboard
└── README.md
```

## 13. Skills Demonstrated

Problem structuring · Star schema modelling · DAX (time intelligence, snapshot logic, calculation groups) · Dashboard storytelling for executives · Credit risk and profitability analytics

