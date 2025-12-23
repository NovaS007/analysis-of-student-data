# External Factors vs. Classroom Performance (R / RMarkdown)

This repository contains an R Markdown report analyzing whether a few external factors relate to student performance in a classroom setting. The main deliverable is an HTML report generated from the `.Rmd` file.

## Project overview

Using a Kaggle dataset of ~5000 anonymized student records, this project investigates three claims:

1. Having internet access at home significantly improves a student’s final grade.
2. A student’s major has a significant impact on final grades.
3. Classroom participation significantly improves a student’s chance of passing.

## Data source

Dataset: Student Performance & Behavior Dataset (Kaggle)  
Author/uploader: Mahmoud Elhemaly (published on Kaggle Feb 16, 2025)

Link: https://www.kaggle.com/datasets/mahmoudelhemaly/students-grading-dataset/data

### Variables used

After cleaning, the analysis focuses on:

- `Department` → renamed to `Major`
- `Participation_Score` → renamed to `Participation` (0–10)
- `Total_Score` → renamed to `Final_Grade` (0–100)
- `Internet_Access_at_Home` (Yes/No) → converted to TRUE/FALSE

## Methods (high level)

Because final scores in the raw population appear non-normal (roughly uniform), the analysis uses the Central Limit Theorem (CLT) by simulating distributions of sample means:

- Sample size per simulation: n = 100  
- Number of trials: 10,000

Then it applies:

### Claim 1 — Internet access vs no internet access
- Simulates mean final grades for each group
- Pooled two-sample t-test (alternative = "greater", α = 0.05)
- Visualizations: ECDF + overlaid histograms

### Claim 2 — Major differences
- Simulates mean final grades for Business, CS, Engineering, and Mathematics
- One-way ANOVA (α = 0.05)
- Post-hoc: Tukey HSD
- Visualizations: ECDF + 2×2 histogram grid

### Claim 3 — Participation and passing
- Splits participation into High vs Low using the median participation score
- Passing defined as Final_Grade ≥ 60
- Two-proportion z-test via prop.test(correct = FALSE, alternative = "greater", α = 0.05)
- Visualizations: bar plot + pie charts

## Results summary (as reported)

- Claim 1: Not supported — no statistically significant evidence that internet access at home increases final grades.
- Claim 2: Supported — majors show statistically significant differences in average final grade; Mathematics highest and Business lowest (within the four majors analyzed).
- Claim 3: Not supported — no statistically significant evidence that higher participation increases passing probability in this dataset.

## Limitations

Important caveats for interpretation:

- The dataset’s real-world origin is unclear (where/when/how it was collected).
- The uploader notes some values may have been modified for classroom purposes.
- Results should be treated as an educational statistical analysis, not a causal or generalizable real-world conclusion.

## How to run

### 1) Clone the repo
```bash
git clone https://github.com/NovaS007/analysis-of-student-data.git
cd analysis-of-student-data
```

### 2) Install dependencies

In R-Studio
```bash
install.packages(c("tidyverse", "gridExtra", "ggplot2", "dplyr", "ggpubr", "knitr", "rmarkdown"))
```

### 3) Knit the project

In R-Studio: open the `.rmd` and click **knit** 

**OR**

run:
```bash
rmarkdown::render("External Factors vs Classroom Performance.Rmd")
```

## Repository Contents
- `External Factors vs Classroom Performance.Rmd` - the full analysis and code
- `Students_Grading_Dataset.csv` - the dataset obtained from Kaggle
- `LICENSE` - project license

## License
This project is licensed under the MIT License. See the `LICENSE` file for details
