# # HealthConnect Clinic — No-Show Analytics: Final Analysis

**AnalystLab Africa Experience Lab · Data Analytics Track**
**Author:** Simbarashe Mandiveyi

> **How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?**

HealthConnect Clinic is a fictional healthcare provider. This repository contains my Data Analytics track work across the 8-week Experience Lab: from a first look at 5,000 appointment records to a validated, tested set of findings and a Power BI dashboard.

## Headline result

**48.5% of scheduled appointments end in a no-show.** Two factors explain most of the pattern, and a small segment is worth targeting first.

| Finding | Evidence |
|---|---|
| **Booking lead time is the strongest driver** | No-show rate rises from 29.5% (booked within 7 days) to 63.9% (31–60 days). Cramér's V = 0.267; odds ratio 1.037 per extra day (p < 0.001) after controlling for other factors. |
| **Prior no-show history is the most consistent signal** | 46.3% with no prior no-shows to 70.3% with 3+. Cramér's V = 0.124; holds in all 4 appointment types with zero exceptions. |
| **A targetable high-risk segment** | Patients with 2+ prior no-shows **and** 15+ day lead time: 7.9% of appointments, 69.1% no-show rate vs 51.2% overall (n = 372). Bringing it to the average would recover roughly 67 slots in this dataset. |
| **Distance and reminders matter, but less** | Distance: V = 0.064. Reminder sent: odds ratio 0.80 (p = 0.002). Both are real but secondary. |
| **Not meaningful drivers** | Appointment type, age group, gender, day of week and time of day: V < 0.05 and not significant once other factors are controlled for. |

## What I did, week by week

| Week | Focus | Main output |
|---|---|---|
| 4 | Problem understanding, data quality review, business questions, candidate KPIs | Initial analysis notebook and document |
| 5 | Cleaning, EDA, 5 KPIs with chi-square tests, dashboards | Analytics notebook and report, interactive Excel dashboard |
| 6 | Went deeper: effect sizes, multivariate logistic regression, lead-time × history risk matrix | Advanced analytics notebook and report, feature-recommendation file for the Data Science track |
| 7 | Testing: re-verified KPIs and dashboard filters against the raw data, checked findings across sub-segments and on a 70/30 split, fixed a misleading heatmap | Testing and refinement notebook and report |
| 8 | Consolidated final KPIs, dashboard, insights and recommendations; Power BI build | Final analytics notebook and report, executive summary, 14-slide presentation |

## Methods

- **Cleaning:** original data never modified; missing `reminder_channel` values encoded as "None"; missing distance and waiting time flagged, not imputed; banded versions of lead time, prior no-shows and distance.
- **Significance and effect size:** chi-square tests plus Cramér's V, so statistically significant but practically negligible effects are not over-read.
- **Multivariate check:** logistic regression across seven variables to confirm each driver holds independently.
- **Testing:** dashboard and KPI values recomputed independently in pandas across multiple filter combinations; segment stability and held-out-split checks; low-sample cells (n < 30) flagged in the risk matrix.
- **Cancelled appointments** are kept out of no-show *rates* (Attended + No-Show base) throughout, and counted in overall totals.

## Tools

Python (pandas, NumPy, SciPy, statsmodels, matplotlib) · Jupyter · Power BI Desktop · Microsoft Excel · Microsoft Word / PowerPoint

## Dashboards

- **Power BI (Executive Overview page):** 6 KPI cards, outcome and demographic charts, 6 slicers. Every figure was checked against the data. See `HealthConnect_PowerBI_Page1_Executive_Overview.png`.
- **Excel interactive dashboard:** 10 dropdown filters driving live KPI cards and charts (Week 5).
- **Matplotlib final dashboard:** six panels covering outcomes, lead time, prior history, validated risk matrix, effect sizes and odds ratios (Week 8 notebook).
- **Build guides:** step-by-step Power BI and Tableau guides with the Power Query / DAX / calculated-field code.

## Repository structure

```
├── data/
│   ├── HealthConnect_Appointment_Data.csv                # original (not modified)
│   ├── HealthConnect_Appointment_Data_cleaned.csv        # cleaned and banded
│   └── HealthConnect_Appointment_Data_PowerBI_Ready.csv  # BI-ready, with sort helpers and flags
├── reference/
│   ├── EffectSizeRef.csv
│   └── OddsRatioRef.csv
├── week4/   initial analysis notebook, document, project summary
├── week5/   analytics notebook, report, Excel dashboard, project summary
├── week6/   advanced analytics notebook, report, project summary,
│            HealthConnect_DataScience_Feature_Recommendations.csv
├── week7/   testing and refinement notebook, report, project summary
├── week8/   final analytics notebook, report, executive summary, presentation
├── powerbi/ dashboard
└── README.md
```

Adjust the folders to match how you actually organise the repo.

## Known limitations and open items

- Findings show **association, not causation**, especially the reminder effect.
- The multivariate model explains a modest share of the variation (pseudo R² ≈ 0.081): good for ranking drivers, not for scoring individual patients.
- About 15% of appointments fall on Sundays, although the clinic's knowledge base says it is closed on Sundays. This is unresolved and was excluded from the analysis.
- The data covers **Jan 2025 – Jun 2026**. That is enough to check month-to-month stability (no significant trend found) but not to claim seasonality.
- **Power BI:** only the Executive Overview page is built. The month chart there pools months by name across two years, which makes July–December volume look like a drop; it needs a Year-Month axis (see Section 2.2b of the Week 8 notebook). The Tableau guide is documentation only; no Tableau workbook was built.
- The data is fictional and synthetic; findings illustrate the method and are not claims about a real clinic.

## Cross-track work

The wider project also had Data Science, ML Engineering, Generative AI and Project Management tracks. My main handoff to Data Science was a ranked, validated feature list (`HealthConnect_DataScience_Feature_Recommendations.csv`), re-tested on a held-out split in Week 7.

## Contact

[Your LinkedIn] · [Your email] · Built as part of the AnalystLab Africa Experience Lab internship programme.
