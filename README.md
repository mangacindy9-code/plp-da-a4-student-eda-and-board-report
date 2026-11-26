# PLP DA Assignment 4 — Student EDA & Duka Board Report

Two engagements in one repository:

1. **County education office** — exploratory analysis of 1,200 student records to identify who is at risk of poor performance and what factors are associated with better results (`student_eda.ipynb`).
2. **Duka Electronics board** — a one-page visual report and a live dashboard telling the H1 2026 sales story and recommending where to focus in H2 (`board_report.ipynb`, `reports/duka_board_report.png`, and the [live Looker Studio dashboard](https://datastudio.google.com/reporting/07215be6-57da-4893-8c54-35303f7320d5)).

---

## How to run

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Regenerate the datasets (seed 55 and seed 2026, unchanged generators)
python generate_data.py

# 3. Open the notebooks and run top to bottom
jupyter notebook student_eda.ipynb
jupyter notebook board_report.ipynb
Repository layout
text
├── README.md
├── requirements.txt
├── generate_data.py                 # both generators, unchanged
├── student_performance.csv          # 1,200 students (seed 55)
├── duka_sales.csv                   # 1,000 orders (seed 2026)
├── student_eda.ipynb                # Engagement 1: 5-step EDA
├── board_report.ipynb               # Engagement 2: storyboard + charts + makeover
├── dashboard.md                     # Looker Studio link + screenshots
├── figures/                         # EDA charts + before/after makeover
└── reports/
    └── duka_board_report.png        # one-page board report


Engagement 1 — County education office
Question: which learners are most at risk of poor performance, and what factors are associated with better results?

Method: five-step EDA framework — Structure, Univariate, Bivariate, Multivariate, Hypotheses. average_score is the mean of math, english and science; performance_band uses pd.cut (At Risk < 60, Meeting 60–74, Exceeding ≥ 75).

Five key EDA insights
School type shows the largest categorical gap. Private students average ~76.0 vs Public ~70.5 — a 5–6 point gap that persists within every attendance band and every study-hour quartile (multivariate pivot tables).

Study hours and attendance are the strongest positive correlates of average_score. attendance_rate has the strongest correlation with average score (r ≈ 0.56), followed by study_hours (r ≈ 0.27). Both positive and moderate.

Gender shows essentially no gap. Female 72.1 vs Male 71.9 — 0.2 points, far below the natural spread. Not a useful targeting dimension.

County differences are small. Nairobi has the highest At Risk share (9.2%, 17 students) vs Nakuru lowest (6.4%, 13) — only 2.8 percentage points apart. With ~200 students per county, this is too small to rank counties.

study_hours contains outliers. A few students report unusually high weekly hours; retained as plausible, but medians are reported alongside means so the centre is not distorted by the tail.

Trend line: average_score vs study_hours fitted with np.polyfit gives a slope of ≈ 2.2 points per weekly study hour and R² ≈ 0.10. Each extra study hour is associated with a score about 2.2 points higher. The R² is low, so study hours alone are a poor predictor of an individual's score; the line is an association, not a causal effect, and many other factors (attendance, school type, prior attainment) also matter.

Recommendations
Target by individual risk band, not by county. Because At Risk shares are similar across all six counties (6–9%) and the spread is only ~3 points, a universal programme that screens each learner using performance_band will reach the right students more reliably than county-level quotas. Priority to learners flagged At Risk (average_score < 60).

Pair study-time support with attendance monitoring, focused on Public-school learners. Both study hours and attendance are positively associated with scores, and the school-type gap is widest for Public-school students. Structured study time and attendance follow-up for At Risk learners in Public schools is likely to yield the largest gains — while noting these are associations, so the programme should be piloted and evaluated rather than assumed to work.

Limitations
Observational data of 1,200 students; every finding is an association, not a causal effect. Confounders — household income, teacher quality, prior attainment, school resources — are unmeasured and could drive both school type and scores. Study hours are self-reported and may be inflated. County samples (~200 each) are small, so the county ranking should not be over-read. The trend line has a low R² and should not be used to predict individual scores. The data are synthetic, so findings illustrate method rather than describing real learners.

Engagement 2 — Duka Electronics board report
Audience: the Duka Electronics board — non-technical directors reading on phones before a meeting.
Decision: where to focus investment in H2 2026.
Big Idea: H1 revenue was stable at KES 86.8M, but 48% came from laptops alone and 70% from laptops plus tablets — so the H2 growth question is how to protect and extend the high-value product franchise, not how to chase more unit volume in low-value lines.

One-page report (embedded):

https://reports/duka_board_report.png

Live dashboard: Scorecards, monthly trend, product and branch breakdowns, and filter controls (date range, product, branch, channel). A mobile page (720 × 1280 px) is built separately because Looker Studio does not auto-adapt to phone screens.

The storyboard (audience, decision, Big Idea, SCR), the chart-by-chart code with insight titles computed in code, and the before/after chart makeover with a design-change explanation are all in board_report.ipynb.

Duka key numbers
H1 2026 revenue: KES 86,792,500 across 1,000 orders; average order value ≈ KES 86,793.

Product revenue: Laptop 48%, Tablet 22%, Phone 10%, Headphones 2%, Charger <1%.

Branch revenue: Nairobi 30%, Mombasa 16%, Nakuru 14%, Kisumu 13%, Eldoret 10%.

Channel revenue: In-store 47%, Online 26%, Phone order 9%.

Monthly revenue: stable at KES 10.9M–13.5M, peak April (KES 13.5M).

Recommendations for H2
Protect the laptop franchise — supply, pricing and staff expertise on the 48%-of-revenue product line.

Lift average order value in Online and Phone-order channels — they are under-indexing on revenue relative to their order share.

Treat chargers and headphones as footfall drivers, not revenue targets — high unit volume, negligible revenue.

Watch Nairobi — it anchors ~30% of revenue; a disruption there would be felt across the business.

Board Summary (150 words)
Duka Electronics closed H1 2026 with KES 86.8 million in revenue across 1,000 orders, averaging KES 86,793 per order. Monthly revenue was stable at KES 10.9–13.5 million, so the half was neither a boom nor a crisis. What the headline hides is concentration: laptops alone are 48% of revenue and laptops plus tablets are 70%, while chargers — a third of all units sold — contribute less than 1% of revenue. In-store remains the primary channel at 47% of revenue, and Nairobi anchors 30%. The recommendation for H2 is to protect the laptop franchise (supply, pricing, staff expertise), look for ways to lift average order value in the Online and Phone-order channels, and treat low-value accessories as footfall drivers rather than revenue targets. These are associations in a simulated dataset, offered to focus the board's discussion — not as proven causal effects.

Notes on the data
Both datasets are synthetic, generated by generate_data.py with seeds 55 and 2026. Findings illustrate analytical method, not real-world causal effects. All conclusions in both engagements are framed as associations, with limitations stated explicitly.

Peer feedback
Posted in the cohort Discord channel, with written feedback on two peers' one-page reports (per the assignment instructions).

---

## Two things to check before you commit

1. **The correlation values in insight #2.** Run this and replace the numbers if needed:

```python
df["average_score"] = df[["math","english","science"]].mean(axis=1)
print(df[["average_score","attendance_rate","study_hours"]].corr().round(2))
Expected: attendance_rate ≈ 0.55–0.60, study_hours ≈ 0.25–0.30. If yours differ, update the README — a reviewer comparing README to notebook will spot a mismatch.

The Looker Studio link. Open it in incognito. If it asks for sign-in, fix sharing before committing
