# Sleep Quality Analysis: Lifestyle Factors and Sleep (Python EDA)

Exploratory data analysis of the **Health Sleep Statistics** dataset (100 participants, 12 variables) to examine which lifestyle factors are associated with self-reported sleep quality, using descriptive statistics, correlation analysis, linear regression and independent-samples t-tests.

> University data-mining course project (team work). 

## Objectives
- Describe the dataset (size, types, missing values, duplicates).
- Measure how age, sleep duration, physical activity, calories burned, diet, sleep disorders and medication use relate to sleep quality.
- Test group differences (gender, sleep disorder, medication) with t-tests.
- Summarize the findings as a simple lifestyle guide.

## Dataset
| Item | Value |
|---|---|
| File | `data/Health_Sleep_Statistics.csv` |
| Records / columns | 100 / 12 |
| Missing values / duplicate rows | 0 / 0 |
| Numeric | User ID, Age (22–50), Sleep Quality (4–9), Daily Steps (3,000–11,000), Calories Burned (2,000–2,900) |
| Categorical | Gender (f/m), Bedtime, Wake-up Time, Physical Activity Level (low/medium/high), Dietary Habits (unhealthy/medium/healthy), Sleep Disorders (yes/no), Medication Usage (yes/no) |
| Derived | Sleep Duration Hours = (wake-up − bedtime) mod 24 (range 4.5–9.0 h) |

**Source and license: `<TODO: add the original dataset link and license>`.** Verify redistribution rights before keeping the CSV in a public repository.

## Methods
1. Load and inspect (`shape`, `info`, `describe`, missing values, duplicates).
2. Encode ordinal categories (activity: low/medium/high → 1/2/3; diet: unhealthy/medium/healthy → 1/2/3); convert `HH:MM` times to decimal hours.
3. Visualize with bar plots, histograms, box plots, count plots and a correlation heatmap.
4. Fit single-variable `LinearRegression` models and report R² (in-sample).
5. Run independent-samples t-tests (`scipy.stats.ttest_ind`).

## Key results (reproduced from the included CSV)
| Analysis | Result |
|---|---|
| Age vs. sleep quality | Pearson r = −0.848; slope −0.174 per year; intercept 13.27 |
| Sleep duration → quality | R² = 0.84 |
| Calories burned → quality | R² = 0.948 |
| Gender (m vs f) | mean quality 5.58 vs 8.42; t = −14.32 |
| Sleep disorder (yes vs no) | mean quality 4.62 vs 7.84; t = −14.12 |
| Medication (yes vs no) | t = −8.08 (Welch) |
| Strongest correlations with quality | Daily Steps 0.976, Calories Burned 0.974, Sleep Duration 0.919, Dietary Habits 0.903, Physical Activity 0.875 |

## Limitations (please read)
- **Association, not causation.** The data are observational; "medication lowers sleep quality" or "gender determines sleep quality" are not supported by these tests.
- **Strong confounding.** In this dataset women average 29.4 years vs 42.6 for men, 40 of 50 men report unhealthy diet vs 1 of 50 women, and sleep disorders occur in 25 of 50 men vs 1 of 50 women. The gender difference therefore cannot be separated from age, diet and disorder status.
- **Bedtime encoding.** Bedtime is stored as clock hours (22.0–23.75 and 0.25–1.5), so after-midnight bedtimes get *smaller* numbers; its correlation (+0.853) is distorted by this wrap-around. Re-encode (e.g. hours since 18:00) before interpreting it.
- **Single-variable, in-sample models.** No train/test split or cross-validation; R² values describe fit on the same 100 rows.
- **Small, very regular dataset** (correlations up to 0.98). Its provenance is unverified, so results should not be generalized to real populations.
- Re-running the time-conversion cell twice breaks the notebook (it overwrites `Bedtime`/`Wake-up Time` in place); restart and run all cells instead.

## Repository structure
```
sleep-quality-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/Health_Sleep_Statistics.csv
├── notebooks/sleep_quality_eda.ipynb
└── docs/
    ├── presentation/sleep-data-analysis-presentation.pdf
```

## Run it
```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/sleep_quality_eda.ipynb
```
Run all cells from the `notebooks/` folder so the relative data path resolves.

## Future improvements
- Multiple regression or tree-based models with a train/test split; control for age and gender.
- Fix the bedtime encoding; add confidence intervals and effect sizes.
- Verify dataset provenance and compare with an independent dataset.

## Authors and attribution
Team course project. 
