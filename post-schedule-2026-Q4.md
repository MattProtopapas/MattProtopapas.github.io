# Blog post schedule: October – December 2026

One post per week, published on Mondays (matching the Jul 20 / Jul 27 / Aug 3 / Sep 7 cadence).
Every topic is an analytics method an SME can apply to data it already collects, following the
blog's running theme: **replace gut feel with a number.**

## What has already been covered (do not repeat)

| Date | Post | Method |
|---|---|---|
| 2026-07-21 | Can AI really help business decisions | Strategic / tactical / operational framing |
| 2026-07-22 | Lead conversion analytics | Funnel conversion, CAC, CLV |
| 2026-07-27 | Inventory control for SMEs | ABC classes, EOQ, reorder points, safety stock |
| 2026-08-03 | Market basket analysis | Association rules (support, confidence, lift) |
| 2026-08-07 | Portfolio optimization | Markowitz mean-variance |
| 2026-08-08 | Which capital projects to fund | Capital budgeting: NPV, IRR, payback |
| 2026-08-09 | Customer profiling and segmentation | RFM, clustering |
| 2026-08-27 | Working capital tied up in inventory | Inventory turns, DIO, cost of capital by unit |
| 2026-08-29 | Keeping quality under control | SPC control charts, Cp/Cpk capability |
| 2026-09-07 | Orders on time and in full | OTIF, 3PL / warehouse KPIs, root-cause Pareto |

Gaps worth filling: forecasting (nothing yet), pricing, staffing, experimentation, sales pipeline,
churn, the *inbound* supply side, product profitability, receivables, cash flow, expense controls,
and planning / KPI design for the new year.

## Conventions (from the existing posts)

- Filename is a question slug: `YYYY-MM-DD-how-can-....md`. Recent posts have **no YAML front
  matter** and no body H1; Jekyll derives the title from the slug.
- Opening: a concrete "gut feel" scenario, then a paragraph linking 2–3 earlier posts with
  "replace gut feel with a number", then bold the method name.
- Section skeleton: *What X actually gives you* → *A practical example, using this repo's own
  results* → 2–3 finding sections → *The business impact, in real numbers* → *What to actually do
  with this, this week* → *Try it yourself* (Downloading the code / Running the demo) →
  *Understanding the results* → *The limits worth keeping in mind*.
- Each post is backed by a public demo repo: synthetic data generator → validate → analyze,
  run with `--seed 42`, outputs an Excel workbook. Screenshots are Excel tabs captured via COM,
  trimmed, max 700 px wide, saved as `assets/images/<date>-<name>.png`.

## Schedule

Status legend: `[ ]` not started · `[d]` demo repo done · `[w]` draft written · `[x]` published

### October — getting ready for peak season

- [w] **2026-10-05 — How can a small business forecast next month's demand?**
  - *Why SMEs care:* Q4 ordering decisions are being made now; every inventory post so far assumed
    demand was known. This closes that loop.
  - *Method:* seasonal naive baseline, moving average, Holt-Winters (ETS); MAE / MAPE on a
    holdout; forecast bias; how forecast error feeds safety stock.
  - *Demo:* 3 years of weekly sales for ~30 SKUs with trend + seasonality + promo spikes;
    workbook with per-SKU forecast vs actual, accuracy league table, "which SKUs are forecastable".
  - *Links back to:* inventory control (2026-07-27), working capital (2026-08-27).

- [ ] **2026-10-12 — How should a small company set its prices?**
  - *Why SMEs care:* most SMEs price at cost-plus or copy a competitor; holiday promotions are
    about to be planned with no idea of elasticity.
  - *Method:* price elasticity from historical price/volume, log-log regression, contribution
    margin impact, markdown depth vs. lift, break-even lift for a discount.
  - *Demo:* transactions with several historical price points per product; workbook with
    elasticity per product, "safe to raise" vs "price-sensitive" lists, promo scenario table.
  - *Links back to:* market basket (2026-08-03), lead conversion (2026-07-22).

- [ ] **2026-10-19 — How many staff do you actually need on a Saturday?**
  - *Why SMEs care:* shops, cafés, call desks and clinics over- or under-staff by habit; wages are
    usually the biggest controllable cost.
  - *Method:* arrival rate by hour/day, Erlang C / simple queueing, service-level targets
    (e.g. 80 % served within 5 min), staffing curve, cost of idle time vs. cost of lost customers.
  - *Demo:* POS / ticket timestamps for 6 months; workbook with hourly heatmap of arrivals,
    required-staff grid per hour, current roster vs. required, cost comparison.
  - *Links back to:* OTIF (2026-09-07, same "customer's side of the fence" framing).

- [ ] **2026-10-26 — Did that promotion actually work? A/B testing for small businesses**
  - *Why SMEs care:* Black Friday emails, discount codes and layout changes get judged on
    "sales went up"; nobody checks whether the difference is noise.
  - *Method:* two-proportion z-test / chi-square for conversion, t-test for basket value, minimum
    sample size, confidence intervals, common pitfalls (peeking, seasonality, novelty).
  - *Demo:* email campaign split with control/treatment groups; workbook with results, p-values,
    CIs, sample-size calculator tab, "how long to run the next test".
  - *Links back to:* lead conversion (2026-07-22), pricing (2026-10-12).

### November — customers, suppliers and margins

- [ ] **2026-11-02 — How much of your sales pipeline will actually close this quarter?**
  - *Why SMEs care:* B2B SMEs plan hiring and cash on a pipeline total that is mostly wishful
    thinking; year-end quota pressure makes it worse.
  - *Method:* stage-weighted pipeline, historical win rates by stage / deal size / age,
    logistic regression for win probability, pipeline coverage ratio, slippage analysis.
  - *Demo:* CRM export of ~1,500 opportunities over 2 years; workbook with win-rate matrix,
    weighted forecast vs. naive total vs. actual, "stale deals" list.
  - *Links back to:* lead conversion (2026-07-22), demand forecasting (2026-10-05).

- [ ] **2026-11-09 — Which customers are about to leave, and can you stop them?**
  - *Why SMEs care:* subscription, service-contract and repeat-purchase businesses lose customers
    silently; win-back is far cheaper before the customer has gone.
  - *Method:* defining churn for non-contract businesses, features from RFM and behaviour,
    logistic regression / decision tree, lift and gains chart, expected value of an intervention.
  - *Demo:* customer base with monthly activity; workbook with churn-risk ranked list, model
    accuracy, "top 100 to call this week" with expected revenue saved.
  - *Links back to:* segmentation (2026-08-09), lead conversion (2026-07-22).

- [ ] **2026-11-16 — Which suppliers are quietly costing you money?**
  - *Why SMEs care:* OTIF covered the outbound side; the inbound side (late, short or defective
    deliveries) drives the safety stock and stockouts from the inventory posts.
  - *Method:* supplier scorecard: on-time %, fill rate, lead-time mean and variability, defect
    PPM, price variance; weighted score; lead-time variability → safety stock cost.
  - *Demo:* purchase orders and receipts for ~25 suppliers; workbook with scorecard, lead-time
    distribution per supplier, "cost of unreliability" per supplier.
  - *Links back to:* OTIF (2026-09-07), inventory control (2026-07-27), SPC (2026-08-29).

- [ ] **2026-11-23 — Which of your products actually make money?**
  - *Why SMEs care:* revenue rankings hide the fact that the best seller may be the worst earner
    once handling, returns and shelf space are counted.
  - *Method:* contribution margin per product, simple activity-based cost allocation, break-even
    volume, product-mix optimization with a linear program under a capacity constraint.
  - *Demo:* product master with costs, sales and capacity usage; workbook with margin waterfall,
    revenue-vs-margin scatter, optimal mix vs. current mix and the profit difference.
  - *Links back to:* pricing (2026-10-12), capital budgeting (2026-08-08).

- [ ] **2026-11-30 — Why is the cash from your sales arriving so late?**
  - *Why SMEs care:* receivables are the other half of working capital; year-end is when slow
    payers hurt most.
  - *Method:* DSO, ageing buckets, collection effectiveness index, customer payment-behaviour
    scoring, prioritised dunning list, cost of financing late payments.
  - *Demo:* invoice and payment ledger for 2 years; workbook with ageing table, DSO trend,
    customer payment profiles, "call these first" list with cash impact.
  - *Links back to:* working capital in inventory (2026-08-27), churn (2026-11-09).

### December — cash, controls and planning for 2027

- [ ] **2026-12-07 — Will you run out of cash in January? A 13-week cash flow forecast**
  - *Why SMEs care:* December sales, January tax and rent, and slow receivables collide; a
    rolling 13-week view is the single most useful finance tool an SME can build.
  - *Method:* direct-method weekly cash forecast, receipts from receivables ageing (2026-11-30),
    payments from purchase commitments, scenario ranges (base / slow-collections / lost customer).
  - *Demo:* combines the receivables, payables and payroll data; workbook with weekly cash
    curve, minimum cash point, scenario fan, "actions that move the curve".
  - *Links back to:* receivables (2026-11-30), demand forecast (2026-10-05), inventory working
    capital (2026-08-27).

- [ ] **2026-12-14 — Are there expenses in your books that shouldn't be there?**
  - *Why SMEs care:* year-end close; duplicate invoices, split payments to dodge approval limits
    and out-of-pattern spend are common and usually found by accident.
  - *Method:* duplicate detection (fuzzy match on amount / vendor / date), Benford's law on
    amounts, threshold clustering just under approval limits, z-score / IQR outliers by vendor.
  - *Demo:* 20,000 expense lines with a handful of planted anomalies; workbook with flagged
    lines by test, Benford chart, vendor outlier list, review checklist.
  - *Links back to:* SPC (2026-08-29, same "is this normal variation?" idea).

- [ ] **2026-12-21 — Why did you miss budget, and what should next year's look like?**
  - *Why SMEs care:* the annual budget review usually stops at "we were 8 % under"; variance
    analysis says *why*, and a rolling forecast stops the budget going stale by March.
  - *Method:* price / volume / mix variance decomposition, flexible budget, variance bridge
    (waterfall), driver-based rolling forecast.
  - *Demo:* budget vs. actual by product and month for one year; workbook with variance bridge,
    volume-vs-price-vs-mix table by product line, 2027 driver-based forecast template.
  - *Links back to:* product profitability (2026-11-23), demand forecast (2026-10-05).

- [ ] **2026-12-28 — What should be on your one-page dashboard for 2027?**
  - *Why SMEs care:* year-end reflection post. Ties the whole year of posts together: which
    10–12 numbers an SME owner should look at weekly, and how to set targets for them.
  - *Method:* leading vs. lagging indicators, KPI trees (cash ← receivables, margin, stock),
    target setting from the historical distribution, control-chart thinking for KPIs (when a
    KPI move is real), dashboard layout principles.
  - *Demo:* a single workbook / Power BI-style one-pager fed by the earlier demo datasets;
    one tile per post of the year, with the "what to do when it moves" note on each.
  - *Links back to:* every post since July (this is the year-in-review).

## Working notes

- Publish Mondays; if a post slips, keep the slot order (each post links back to the previous
  ones and the December posts build on November's data).
- Reuse the same synthetic company across the November–December finance posts (receivables →
  cash flow → variance → dashboard) so the numbers reconcile between posts.
- Keep the Excel-workbook-plus-Python-scripts demo format; SME readers are Excel-first.
