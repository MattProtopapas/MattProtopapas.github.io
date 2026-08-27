An [earlier post on this blog](/2026/07/27/inventory-control-for-Small-and-Medium-companies/)
asked the classic operations question about stock: *how many units should we order, and
when?* This post asks the finance question that sits one level above it: **how much working
capital should be tied up in inventory in the first place — and is each part of the business
currently holding too much, or too little?**

It's a question most companies never actually put a number on. Inventory shows up on the
balance sheet as a single line, receivables as another, payables as a third — and as long as
the totals look stable year over year, nobody asks whether each individual business unit,
product line, or warehouse is running the right *policy*. Yet the two ways of getting it
wrong are both expensive, and they're invisible in the totals: a unit holding too much
inventory is quietly paying its cost of capital on money frozen in stock, while a unit
holding too little is quietly losing sales and goodwill to stockouts. Firm-wide, the two
errors can even cancel out on paper — which is exactly what makes them dangerous.

Previous posts here have made the same argument for
[stock reordering](/2026/07/27/inventory-control-for-Small-and-Medium-companies/),
[capital proposals](/2026/08/08/how-can-companies-decide-which-capital-projects-to-fund/), and
[customer bases](/2026/08/09/how-can-companies-profile-and-segment-their-customers/):
replace gut feel with a number, using data the company already collects. **Working-capital
analysis** — the operating-cycle / cash-cycle framework and the carrying-cost vs.
shortage-cost trade-off from Ross, Westerfield & Jaffe's *Corporate Finance* (Ch. 27,
"Short-Term Finance and Planning") — does exactly that for short-term finance. Every input
it needs is already sitting in the company's financial statements: sales, cost of goods
sold, and the beginning and ending balances of inventory, receivables, and payables.

## What working-capital analysis actually gives you

| Benefit | Why it matters |
|---|---|
| **A number for how long cash is trapped** | The **cash conversion cycle (CCC)** — days in inventory, plus days in receivables, minus days in payables — measures the time between paying suppliers and collecting from customers. A long CCC isn't "bad operations," it's a financing requirement with a dollar cost attached. |
| **The financing gap, in dollars** | `CCC × (COGS ÷ 365)` converts that cycle into the amount of working capital the cash cycle leaves unfunded by trade credit — the gap that, as the textbook puts it, must be closed either by borrowing or by holding a liquidity reserve. |
| **An optimal inventory level, not just a current one** | Modeling carrying costs (which rise with inventory investment) against shortage costs (which fall with it) yields an optimal investment level **I\*** — so every unit's actual inventory can be compared against where it *should* be. |
| **A policy label per unit, not a firm-wide average** | Each business unit gets flagged as **flexible** (over-invested — capital earning less than its cost), **restrictive** (under-invested — elevated stockout risk), or **near-optimal**. Averages across units hide exactly this. |
| **Bad records never reach the analysis** | Negative COGS, negative inventory, a blank cost of capital, duplicate unit IDs — a validation layer rejects these with a stated reason before they can silently distort a cycle or a cost figure. |
| **One workbook the CFO's office can actually open** | The output is a formatted, color-coded Excel file — input data, per-unit analysis with the off-policy rows highlighted, and a per-segment rollup — not a notebook or a database query. |

## A practical example, using this repo's own results

This repository — **[Inventories-Finance-Demo](https://github.com/MattProtopapas/Inventories-Finance-Demo)**
— ships with a full worked example instead of a hypothetical one. Running it with the
defaults simulates a company generating financial records for **150 business units** (seed
42, plus one deliberately duplicated row), with **5% of rows deliberately corrupted** to
prove the validation step actually rejects bad data rather than silently letting it
through: **142 rows pass, 9 are rejected.**

Every record carries what a real management-accounting extract would: annual credit sales,
COGS, beginning/ending inventory, receivables and payables balances, the unit's cost of
capital, its storage-cost rate, and its estimated stockout risk. That's the raw material
every downstream number in the workbook is calculated from.

![Sample of the Input Data tab](/assets/images/2026-08-27-input-data.jpg)

## Catching bad records before they pollute the analysis

Before any cycle or cost is computed, every row is checked against a strict pydantic
schema, and the rejects are written to a plain-text report with the exact reason each one
failed:

```text
Working-capital data validation report
=======================================
Total rows read:   151
Rows passed:       142
Rows rejected:     9

Rejected rows:
  - Line 22 (unit_id=BU-00021): region: String should have at least 1 character
  - Line 32 (unit_id=BU-00031): cogs: Input should be greater than 0
  - Line 36 (unit_id=BU-00035): ending_inventory: Input should be greater than or equal to 0
  - Line 47 (unit_id=BU-00046): cost_of_capital: Input should be a valid number, unable to parse string as a number
  - Line 92 (unit_id=BU-00090): cogs: Input should be greater than 0
  - Line 99 (unit_id=BU-00097): stockout_risk_pct: Input should be less than 1
  - Line 140 (unit_id=BU-00138): stockout_risk_pct: Input should be less than 1
  - Line 141 (unit_id=BU-00139): ending_inventory: Input should be greater than or equal to 0
  - Line 152 (unit_id=BU-00150): duplicate unit ID, dropped
```

None of these are exotic errors — a negative COGS or a duplicated unit ID is exactly the
kind of thing a hurried consolidation spreadsheet produces. Left in, a negative COGS
doesn't just skew one unit's numbers: it flips the sign of a days-in-inventory calculation
and quietly corrupts every average built on top of it. That's the entire case for
validating before analyzing.

## The per-unit picture: two ways to be wrong, both highlighted

With 142 clean units to work from, the analysis computes each unit's days in inventory
(DIO), days in receivables (DSO), days in payables (DPO), operating cycle, cash conversion
cycle, financing gap, carrying cost, shortage exposure, and — the number everything else is
judged against — the **optimal inventory investment I\***. Units sitting well above I\* are
highlighted amber (flexible / over-invested); units well below are highlighted red
(restrictive / under-invested):

![Sample of the Cycle & Cost Analysis tab](/assets/images/2026-08-27-cycle-cost-analysis.jpg)

Across the 142 units, the averages look unremarkable: 65.6 days in inventory, 48.0 days in
receivables, 44.0 days in payables — an operating cycle of 113.7 days and an average cash
conversion cycle of **69.7 days**. A CFO glancing at those firm-wide figures would see
nothing alarming.

The per-unit view tells a completely different story. **Only 22 of the 142 units — about
one in seven — are actually near their optimal inventory investment.** The other 120 split
almost evenly into the two failure modes: **63 units are restrictive (under-invested)**,
running elevated stockout risk, and **57 are flexible (over-invested)**, sitting on capital
earning less than it costs. The spread in the cash cycle is just as wide: from **185.8
days** at the worst over-invested unit (Sanchezfort Segment, Consumer Packaged Goods — six
months between paying suppliers and collecting from customers) down to **−14.8 days** at
the other extreme (Dicksonberg Group, also Consumer Packaged Goods). Seven units have a
*negative* cash conversion cycle — they collect from customers before their suppliers'
invoices come due, so trade credit finances the whole operation. Same company, same
segment, opposite policies.

### The trap hiding in the totals

Here's the number that makes the per-unit view worth the effort. The over-invested units
are collectively holding about **$99.0 million more inventory than their optimum**; the
under-invested units are collectively **$89.4 million short** of theirs. Net those against
each other and the firm-wide inventory balance looks roughly right — off by only about $10
million on hundreds of millions of working capital. **The totals almost perfectly conceal
the fact that 120 of 142 units are running the wrong policy.** One side of the business is
paying carrying costs on capital it shouldn't be holding while the other side is losing
sales it shouldn't be losing, and the consolidated balance sheet shows nothing wrong at
all.

Meanwhile the financing requirement is real and enormous: the cash cycles across all 142
units add up to a total **financing gap of $508.7 million** — working capital that trade
credit doesn't cover and that has to be funded by borrowing or by holding a liquidity
reserve, at whatever that funding costs.

## The segment rollup: where to look first

The third tab rolls everything up by business segment — unit counts, average cash cycle,
total financing gap, total carrying cost, total shortage exposure, and the policy mix:

![Sample of the Segment Summary tab](/assets/images/2026-08-27-segment-summary.jpg)

Three things jump out of this run's summary:

- **Food & Beverage carries the largest financing gap** — $85.1 million across 23 units,
  with one of the longest average cash cycles (80.6 days). For a segment whose products
  are perishable and whose margins are typically thin, that's the first place a treasurer
  should be asking why so much of the cycle is unfunded by trade credit.
- **Consumer Electronics has zero near-optimal units.** All 16 units are off-policy — 10
  restrictive, 6 flexible. Whatever inventory policy that segment is following, it isn't
  one anchored to the carrying-vs-shortage trade-off.
- **Pharmaceuticals and Consumer Packaged Goods run the shortest average cycles** (57.9 and
  57.0 days) — yet Pharmaceuticals still posts the second-largest financing gap ($77.7
  million), simply because its 24 units move so much volume. A short cycle isn't the same
  thing as a small funding requirement.

That's the value of the rollup: it doesn't replace the per-unit tab, it tells you which
slice of the per-unit tab to read first.

## What to actually do with this, this week

1. Pull last year's figures per business unit (or product line, or warehouse — whatever
   slice you manage): credit sales, COGS, and beginning/ending balances for inventory,
   receivables, and payables. Add each unit's cost of capital, storage-cost rate, and an
   honest estimate of stockout risk.
2. Run it through this repo's pipeline (or a similar tool), swapping the Faker-based
   generator for your real export — the two downstream scripts don't care where the CSV
   came from.
3. Check the **validation report** first. A negative COGS or a duplicated unit ID is a more
   common consolidation error than it looks, and it will corrupt every downstream average
   if it isn't caught.
4. On the **Cycle & Cost Analysis** tab, sort by `recommended_adjustment` and read both
   ends: the amber rows are where capital can be released, the red rows are where stockout
   exposure is quietly accumulating.
5. Don't stop at the firm-wide totals — this run's totals looked fine while 120 of 142
   units were off-policy. The whole point is the per-unit comparison against I\*.
6. Re-run it quarterly. Sales mix, supplier terms, and interest rates all move the optimum,
   so last year's policy answer is already stale.

## Try it yourself: a demo you can run in minutes

To make this concrete, this repository —
**[Inventories-Finance-Demo](https://github.com/MattProtopapas/Inventories-Finance-Demo)**
— is a small, self-contained, open-source demo. It:

1. Generates (or accepts your own) business-unit financial records, using
   [Faker](https://faker.readthedocs.io/) for realistic synthetic data, with a configurable
   share deliberately corrupted.
2. Validates every row against [pydantic](https://docs.pydantic.dev/) data contracts —
   negative costs, impossible balances, out-of-range risk percentages, duplicate IDs — so
   corrupted rows are rejected with a clear reason instead of silently entering the
   analysis.
3. Computes the full short-term-finance picture per unit — DIO, DSO, DPO, operating cycle,
   cash conversion cycle, financing gap, carrying cost, shortage exposure, the optimal
   inventory investment, and a policy signal.
4. Writes everything — validated inputs, the per-unit analysis with off-policy rows
   color-highlighted, and the per-segment summary — into a single styled Excel workbook.

### Downloading the code (no Git experience needed)

You don't need to know Git or the command line to get the code onto your computer:

1. Go to the repository: **[github.com/MattProtopapas/Inventories-Finance-Demo](https://github.com/MattProtopapas/Inventories-Finance-Demo)**
2. Click the green **`<> Code`** button near the top of the page.
3. Click **"Download ZIP"** in the dropdown.
4. Right-click the downloaded ZIP and choose **"Extract All..."** to unzip it into a
   regular folder.
5. Open that folder — that's the project. Ask your AI tool of choice (I used Claude) to set
   up a Python environment and install the dependencies listed in `requirements.txt` — no
   coding experience required to get it running.

If you're comfortable with Git,
`git clone https://github.com/MattProtopapas/Inventories-Finance-Demo.git` does the same
thing in one step.

### Running the demo

The repository includes a full `README.md`, but the short version, from PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt

python generate_data.py --count 150 --error-rate 0.05 --seed 42
python validate_data.py
python analyze_working_capital.py
```

That run produces `output/working_capital_analysis.xlsx` — the same workbook, with the same
numbers, that every screenshot in this post was taken from. A handful of CLI options let
you reshape the exercise without touching any code:

| Script | Flag | Default | Description |
|---|---|---|---|
| `generate_data.py` | `--count` | `150` | Number of fake business units to generate |
| | `--error-rate` | `0.05` | Fraction of rows deliberately corrupted (`0` for a clean dataset) |
| | `--seed` | none | Random seed, for reproducible output |
| `validate_data.py` | `--input` / `--output` / `--report` | `data/…` | Validate a custom file, choose where the clean data and rejection report go |
| `analyze_working_capital.py` | `--input` / `--output` | `data/…`, `output/…` | Analyze a custom file, choose where the workbook goes |

Because every script can point at a custom input path, you can drop in your own real
business-unit data (matching the columns in `finance_common.py`) and run it straight
through validation and analysis, skipping the generator entirely.

> **Note:** the data generated by this demo is synthetic and randomly generated, and this
> project is intended for educational and demonstration purposes only — the carrying-cost
> and shortage-cost model is deliberately simple, and the policy thresholds are
> illustrative, not calibrated against any real business. See the repository's
> [Disclaimer & EULA](https://github.com/MattProtopapas/Inventories-Finance-Demo/blob/main/DISCLAIMER.md)
> for details. It's a starting point for understanding how working-capital analysis works,
> not a treasury system.

## Understanding the results

`working_capital_analysis.xlsx` has three tabs, each one a stage of the story: **Input
Data** (the 142 validated records the analysis ran on), **Cycle & Cost Analysis** (the
calculated metrics per business unit, sorted by cash conversion cycle, with restrictive
rows highlighted red and flexible rows highlighted amber), and **Segment Summary** (the
per-segment rollup of unit counts, average cash cycle, total financing gap, total carrying
cost, total shortage exposure, and the policy-signal mix). Alongside the workbook, the
pipeline leaves `data/validation_report.txt` — the plain-text record of every rejected row
and why — which is worth attaching to any result you circulate, so the question "what did
you exclude?" already has an answer.

## The limits worth keeping in mind

Working-capital analysis, like the other tools covered on this blog, is a genuinely useful
framework with real limits:

- **The shortage-cost model is the soft spot.** Carrying costs are observable (cost of
  capital, storage rates); shortage costs — lost sales, lost goodwill, disrupted
  production — have to be estimated, and I\* moves with that estimate. Treat the
  flexible/restrictive labels as a screening signal, not a verdict.
- **It's a snapshot built on averages.** Beginning/ending balance averages smooth over
  seasonality; a unit that looks near-optimal on annual figures can be badly over- and
  under-stocked at different points in the same year.
- **A long cash cycle isn't automatically a problem.** Some businesses deliberately run
  flexible policies — deep service commitments, long production runs — and fund them
  knowingly. The framework prices that choice; it doesn't forbid it.
- **The demo's parameters are illustrative.** The cost rates, risk percentages, and
  near-optimal band in this repo aren't calibrated to any real firm; a real deployment
  should sanity-check the resulting policy mix against what the business actually knows
  about itself.

None of that makes the exercise less worthwhile. It just means the output of a
working-capital run is an input to a financing and inventory-policy decision, not the
decision itself — in the same way the reorder points, project rankings, and customer
segments from earlier posts are inputs to a decision, not a replacement for judgment. Used
that way, the cash-cycle framework turns "our inventory levels feel about right" into
"here are the 120 of 142 units running the wrong policy, the $99 million we could release,
and the $508.7 million of cash cycle we're currently funding without ever having decided
to" — a genuinely useful upgrade for any company's short-term financial planning, using
nothing more than the figures already sitting in its financial statements.
