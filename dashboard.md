# Duka Electronics — Live Dashboard

**Public Looker Studio link:** [https://datastudio.google.com/reporting/07215be6-57da-4893-8c54-35303f7320d5]

The dashboard covers H1 2026 (Jan 1 – Jun 29) and is built from `duka_sales.csv` (1,000 orders). It is designed for the board to explore the same data behind the one-page report, with live filters for date range, product, branch and channel.

## What the dashboard shows

| Component | Purpose |
|---|---|
| **Scorecards** (Revenue, Orders, Avg Order Value) | Headline H1 figures at a glance |
| **Monthly trend** (time series) | Shows H1 revenue was stable (KES 10.9M–13.5M) |
| **Product revenue breakdown** (bar) | Laptops = 48% of revenue |
| **Branch / Channel breakdown** (bar) | Nairobi anchors ~30%; In-store ~47% |
| **Filter controls** (date range, product, branch, channel) | Lets viewers drill into any segment |

## Screenshots

### Desktop view

![Desktop dashboard](figures/dashboard_desktop.png)

*Shows scorecards, monthly trend, product and branch breakdowns, and filter controls on one page.*

### Mobile view

![Mobile dashboard](figures/dashboard_mobile.png)

*Mobile-optimized page (720 × 1280 px) with stacked scorecards, full-width trend, and large touch-friendly filters. Built separately because Looker Studio does not auto-adapt to phone screens.*

## How to use it

1. Open the public link on any device.
2. Use the **date range** control to narrow the period (all data is within H1 2026).
3. Use the **product**, **branch** and **channel** drop-downs to filter every chart on the page simultaneously.
4. The scorecards and charts update live — no refresh needed.

## Data notes

- Source: `duka_sales.csv`, generated with seed 2026 (unchanged generator in `generate_data.py`).
- Revenue = `quantity × unit_price`.
- All 1,000 orders fall between 2026-01-01 and 2026-06-29.
- These are associations in a simulated dataset — the dashboard supports exploration, not causal claims.
