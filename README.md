⚡ EV Adoption & Renewable Energy — A State-Level Analysis

Does a cleaner electricity grid actually predict higher EV adoption?
I tested this assumption statistically across all 50 US states + DC — and the answer surprised me.

Show Image
Show Image
Show Image
Show Image
Show Image


🔑 TL;DR


Renewable energy share does NOT reliably predict EV adoption (r = 0.24, p = 0.088 — not statistically significant).
States with the cleanest grids (Vermont, 99.8% renewable) rank among the lowest in EV adoption, while California (43.5% renewable) leads the country by a wide margin.
The real driver appears to be policy — ZEV mandates and purchase incentives — not grid composition.




📌 Table of Contents


Project Overview
Key Findings
Datasets
Data Cleaning Challenges
Tech Stack
Repo Structure
How to Run
Dashboard
Limitations
Author



🎯 Project Overview

Clean energy and EV adoption are usually talked about as if they're the same story — "green states buy EVs." This project puts that assumption to a statistical test using real 2018 vehicle registration data and 1990–2019 US energy generation records.

Questions this project answers:


Does a state's renewable energy share correlate with its EV adoption rate?
How has renewable energy generation evolved nationally (1990–2018), and which states are actually driving that growth?
Which states lead in EV adoption, and what do they have in common?
If not grid composition, what does explain EV adoption patterns?



📊 Key Findings

1. EV adoption is heavily concentrated

The distribution is right-skewed — median state sits at just 0.71 EVs per 1,000 vehicles. California is the outlier at 8.28 — 1.6x Hawaii (2nd) and ~2.1x Washington (3rd).

2. Renewable energy share does NOT predict EV adoption

Pearson correlation between renewable share and EV adoption rate:

MetricValueCorrelation coefficient (r)0.24 (weak)P-value0.088Statistically significant?❌ No (p > 0.05)

Vermont (99.8% renewable) and Idaho (81%) both show low EV adoption, while California (43.5%) and Hawaii (13%) lead the rankings. If clean electricity reliably drove EV adoption, these outliers wouldn't exist.

3. Renewable growth is a Midwest wind story, not a coastal one

National renewable share nearly doubled — 9% (1990) → 17% (2018) — with the steepest growth after 2015. The biggest movers weren't California or the Northeast; they were Kansas, Iowa, and Oklahoma, each jumping to 35%+ renewable share on the back of wind power expansion in the Great Plains. None of these states rank in the top 8 for EV adoption.

4. Policy explains the pattern better than infrastructure does

States leading in EV adoption share a common thread — coordinated EV policy, not clean grids:


California — ZEV mandate + Clean Vehicle Rebate Project (direct cash rebates)
9-state ZEV coalition (CT, ME, MD, MA, NJ, NY, OR, RI, VT) — coordinated mandates & incentives with California
Colorado — independent state tax credit for EV purchases


Takeaway: grid decarbonization and EV adoption are two separate policy levers. A state can lead on one without leading on the other — and most states do exactly that.


🗂 Datasets

FileDescriptionStates_Electric_Vehicle_Registrations_2018.xlsxState-level EV registration counts, 2018States_All_Vehicle_Registrations_2018.xlsxTotal motor vehicle registrations per state, 2018 (used to normalize EV counts)States_Annual_Energy_Generation_Sources_1990_2019.xlsxAnnual electricity generation by state, producer type, and energy sourcestate_codes.xlsxState name ↔ 2-letter code reference table


🧹 Data Cleaning Challenges

Real government datasets rarely arrive analysis-ready. Notable issues resolved in this project:


Inconsistent state naming — Washington D.C. appeared as "Dist. of Col.", "District of Columbia", and "District Of Columbia" across the four files. Standardized casing/naming before every join to avoid silent row drops.
Producer-type double-counting — the energy dataset reports generation across 6 overlapping producer categories. Filtered to "Total Electric Power Industry" only to avoid inflating generation totals.
Malformed government headers — the vehicle registration file has a multi-row merged header starting 12 rows into the sheet, with footnote markers (e.g. (2)) embedded in state names.


Result: all core datasets matched at 51/51 states (50 states + DC) with zero unresolved nulls after cleaning.


🛠 Tech Stack


Python — pandas, numpy (data cleaning & merging)
Matplotlib / Seaborn — statistical visualizations
SciPy — Pearson correlation & significance testing
Power BI — interactive dashboard (state filter, correlation view, adoption rankings)



📁 Repo Structure

ev_adoption_analysis/
│
├── data/
│   ├── raw/                          # original 4 source files
│   └── clean/                        # cleaned CSVs after preprocessing
│
├── notebooks/
│   ├── 01_clean_data.ipynb           # import + cleaning
│   ├── 02_merge_master.ipynb         # merge into master dataset
│   ├── 03_eda.ipynb                  # distributions, summary stats
│   ├── 04_correlation.ipynb          # correlation + significance testing
│   ├── 05_timeseries.ipynb           # renewable energy trend 1990-2018
│   └── 06_geospatial.ipynb           # state-level adoption & renewable maps
│
├── dashboard/
│   └── EV_Renewable_Dashboard.pbix   # Power BI dashboard
│
├── report/
│   └── EV_Renewable_Energy_Analysis_Report.pdf
│
└── README.md


▶️ How to Run

bashgit clone https://github.com/mynkbhardwaj87007-spec/ev_adoption_analysis.git
cd ev_adoption_analysis
pip install pandas numpy matplotlib seaborn scipy openpyxl

Run notebooks in order (01 → 06) inside the notebooks/ folder. Each notebook reads from data/clean/ and expects the previous notebook's output to exist first.


📈 Dashboard

An interactive Power BI dashboard accompanies this analysis, allowing you to:


Filter by individual state
Explore the renewable share vs. EV adoption scatter plot
View EV adoption and renewable share rankings side by side


(Screenshot/link here once uploaded)


⚠️ Limitations


EV registration data is available for a single year (2018) only — true time-series modeling of EV adoption over time wasn't possible with this dataset.
Policy impact was assessed qualitatively from publicly documented programs, not a structured policy dataset — this identifies a likely explanation rather than statistically proving it.
Correlation ≠ causation — unobserved factors like urban density, charging infrastructure, and regional EV manufacturer presence weren't directly measured.



👤 Author

Mayank Bhardwaj
Aspiring Data Analyst | Python · SQL · Power BI | BCA 2026

LinkedIn · GitHub


⭐ If you found this analysis interesting, consider starring the repo!
