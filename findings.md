# COVID-19 Early Case Trend Analysis & Recovery Insights

**HealthGuard Analytics Pvt. Ltd.**

## Dataset Overview

- 4212 patient records, 14 columns
- Key columns (`confirmed_date`, `state`) are fully populated (0% missing)
- Several fields critical to the original brief — `infection_reason`, `infection_order`, `contact_number`, `birth_year` — are 93–99% missing
- This sparsity is a defining constraint of the analysis and is called out explicitly below rather than glossed over

## 1. Who is getting infected?

- Age data exists for only 292 of 4212 patients (~7%)
- Among those, the average age is ~47 years (median 48), ranging from 2 to 83
- Gender distribution: see `02_gender_distribution.png`
- **Caveat:** age findings represent a small, possibly non-representative subset of the full case count

## 2. How are infections spreading?

- `infection_reason` recorded for only ~3% of patients
- Top recorded reasons are shown in `05_infection_reasons.png`
- Given the scale of missingness, this cannot be treated as a representative picture of transmission routes across the whole outbreak — only of the subset where the reason happened to be logged

## 3. What are the recovery trends?

- Only 28 of 4212 patients had a recorded `released_date`, enabling recovery-time calculation
- Average recovery time: ~15.1 days (min 7, max 24, std ~5.6)
- This is broadly consistent with early published COVID recovery timelines, despite the small sample

## 4. Which regions are most impacted?

- See `04_region_distribution.png` for the top 15 regions by confirmed case count
- Cases are concentrated in a small number of regions rather than evenly spread

## 5. What factors influence recovery time?

Correlation analysis (recovery_days vs. age, contact_number, infection_order):

| Variable | n | Correlation with recovery_days |
|---|---|---|
| age | 28 | -0.076 (negligible) |
| contact_number | 24 | -0.244 (weak, unreliable at this n) |
| infection_order | 24 | 0.018 (negligible) |

**Conclusion:** No statistically meaningful relationship was found between these factors and recovery duration. The one mild signal (contact_number) is based on only 24 patients and should not be treated as a reliable trend. A linear regression model was not built, since a near-zero/inconsistent correlation on a sample this small would not produce a meaningful or trustworthy R² — visual and correlation evidence already answer the question (no detectable effect, insufficient data to say more).

## Overall Limitation

This dataset captures an early-outbreak snapshot, where most patients (~98%) were still in `isolated` status with outcomes not yet resolved. Several fields needed for deeper analysis were sparsely filled at this stage of data collection. Conclusions here should be read as **indicative of the available subset**, not the full case population.

## Files

- `analysis.py` — full analysis code
- `outputs/01_patient_outcomes.png` through `06_recovery_vs_age.png` — visualizations
