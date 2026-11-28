# Blog post schedule: December 2026 (Saturdays)

Four posts, one per Saturday: **Dec 5, Dec 12, Dec 19, Dec 26**.

Every topic below is an analytics method an SME can apply to data it already collects, and none
repeats a post already published (Jul 20 through Nov 28). Already covered, so excluded: AI for
decisions, lead conversion, inventory control, market basket, portfolio optimization, capital
budgeting, customer segmentation, working capital in inventory, SPC quality, OTIF, demand
forecasting, pricing, staffing / queueing, A/B testing, depot and route planning, cash buffers,
churn, supplier reliability, and job sequencing.

The four topics come from the gaps still listed in `post-schedule-2026-Q4.md`: product
profitability, receivables, expense controls and year-end planning. Each post links back to
earlier ones, in line with the blog's theme of replacing gut feel with a number.

---

## Saturday 5 December 2026

### Which of your products actually make money?

**Summary:** Revenue rankings hide the fact that the best seller can be the worst earner once
handling, returns and shelf space are counted. The post shows how to calculate contribution
margin per product, spread overheads with simple activity-based costing, and find each product's
break-even volume. It then uses a small linear program to find the product mix that earns the
most under a capacity limit (shelf space, machine hours or staff time). The worked example
compares the current mix with the optimal one and puts a profit figure on the difference.
Readers get a ranked list of products to push, reprice or drop before the January planning
round.

- **Method:** contribution margin, activity-based cost allocation, break-even volume, product-mix
  optimization (linear programming)
- **Demo output:** margin waterfall, revenue-vs-margin scatter, current vs. optimal mix table
- **Links back to:** pricing, capital budgeting, inventory control

---

## Saturday 12 December 2026

### Why is the cash from your sales arriving so late?

**Summary:** A sale is not cash until the customer pays, and year-end is when slow payers hurt
most. This post covers the other half of working capital, the money owed *to* you. It explains
how to measure days sales outstanding (DSO), build an ageing table, and calculate the collection
effectiveness index. It then profiles each customer's payment behaviour to separate the
habitually late from the occasionally late. The output is a prioritized "call these first" list
that ranks overdue invoices by the cash they will release, plus an estimate of what late payment
costs in financing terms. Readers learn to chase the right invoices, in the right order, before
the holidays.

- **Method:** DSO, ageing buckets, collection effectiveness index, payment-behaviour scoring,
  cost of financing overdue balances
- **Demo output:** ageing table, DSO trend, customer payment profiles, prioritized dunning list
- **Links back to:** working capital in inventory, cash buffers, churn

---

## Saturday 19 December 2026

### Are there expenses in your books that shouldn't be there?

**Summary:** Duplicate invoices, payments split to stay under an approval limit and out-of-pattern
spend are common in small companies, and they are usually found by accident. This post applies
four simple tests to a year of expense lines: fuzzy duplicate matching on vendor, amount and
date; a first-digit (Benford's law) check on amounts; a look for clusters of payments just under
approval thresholds; and z-score or IQR outliers by vendor. Each test is explained in plain
language and runs in Excel. The result is a short, prioritized review list and a checklist for
the year-end close. It also explains why a flag is a question to ask, not an accusation.

- **Method:** duplicate detection, Benford's law, threshold clustering, outlier detection (z-score / IQR)
- **Demo output:** flagged lines by test, Benford chart, vendor outlier list, review checklist
- **Links back to:** SPC control charts (the same "is this normal variation?" idea), supplier
  reliability

---

## Saturday 26 December 2026

### What should be on your one-page dashboard for 2027?

**Summary:** The year-end reflection post. After a year of methods, the owner still has to
decide which numbers to look at every week. This post picks 10 to 12 indicators, one or two
from each area covered this year (cash, receivables, margin, stock, forecast accuracy, on-time
delivery, quality, supplier reliability, churn). It arranges them as a KPI tree so each number
shows what drives it, and separates leading indicators (which warn early) from lagging ones
(which confirm after the fact). It shows how to set 2027 targets from the historical
distribution instead of round numbers, and how to use control-chart thinking to tell a real
move in a KPI from noise. It ends with a one-page dashboard layout, and a short "what to do
when this number moves" note for each tile.

- **Method:** leading vs. lagging indicators, KPI trees, data-driven target setting, control
  charts for KPIs, dashboard layout principles
- **Demo output:** a one-page workbook dashboard with one tile per topic of the year
- **Links back to:** nearly every post since July (the year-in-review)

---

## Backup topic

If a slot needs swapping or the year-end dashboard post is better placed in January:

### Why did you miss budget, and what should next year's look like?

**Summary:** The annual review usually stops at "we were 8% under budget." Variance analysis
explains why, by splitting the gap into price, volume and mix effects, and shows it as a
waterfall chart. The post then turns the findings into a driver-based rolling forecast for 2027,
so the budget does not go stale by March.

- **Method:** price / volume / mix variance, flexible budget, variance bridge, rolling forecast
- **Links back to:** product profitability, demand forecasting

---

## Notes

- Posts are on Saturdays, unlike the Monday cadence in the Q4 schedule. If a post slips, keep the
  order: the Dec 26 dashboard builds on the earlier ones.
- File names follow the existing convention: `2026-12-05-which-of-your-products-actually-make-money.md`,
  and so on, with no YAML front matter.
- Reusing one synthetic company across the December demos (products, then receivables, then
  expenses, then dashboard) keeps the numbers consistent between posts.
- The 13-week cash flow forecast from the old plan is left out: the Nov 7 cash post already
  covers cash planning. Receivables (Dec 12) is a different angle on the same problem.
