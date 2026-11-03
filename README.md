# The Effects of the Pitch Clock Rule on MLB Performance and Market Efficiency

Caitlyn Mahoney — Capstone project (MA-470), Worcester State University, Fall 2025

Major League Baseball introduced a pitch clock for the 2023 season. This project uses data from 2022–2024 to test what actually changed after the rule went into effect: whether games got higher scoring, whether pitchers got worse, which pitchers were affected most, and whether betting markets priced the change correctly.

## Research questions

- Did total scoring change after the pitch clock was introduced in 2023?
- Did pitcher performance change, and were slow tempo pitchers affected more than fast tempo pitchers?
- Did over/under betting markets remain efficient once scoring changed?

## Key findings

| Measure | 2022 (before) | 2023 (first year) | 2024 |
| --- | ---: | ---: | ---: |
| Mean total runs per game | 8.57 | 9.23 | 8.79 |

- Scoring rose sharply in the first pitch clock season. Mean total runs increased from 8.57 in 2022 to 9.23 in 2023 (p < 0.001), then eased back to 8.79 in 2024.
- Pitch strength declined after the clock. Using a composite pitch strength metric, pitchers performed worse after the clock was introduced, and slow tempo pitchers were hit hardest.
- Workload does not explain the drop. Total pitches per pitcher did not change in a way that accounts for the decline in pitch strength.
- Betting markets stayed efficient at season level. Over/under results were consistent with a fair 50/50 market over a full season, even though early series games showed imbalances.

## Files in this repository

Run the files in this order. Together they cover data preparation, scoring, pitching, a workload check, and market efficiency.

- **`2022-2024_matchups.rmd` — data preparation.** Joins Retrosheet game results to OddsShark over/under lines, maps OddsShark team names to Retrosheet team codes, and handles doubleheaders so each game matches the right betting line.

- **`Score_Compare_Means.rmd` — scoring analysis.** Compares mean total runs by season with plots, ANOVA, and pairwise t-tests, the analysis behind the scoring results above.

- **`pitching_tempo.rmd` — main pitching analysis.** Builds a composite pitch strength metric from scaled Statcast indicators for the 141 pitchers with 50+ innings pitched in all three seasons, classifies pitchers as fast or slow tempo from their 2022 tempo, and runs paired t-tests by group.

- **`pitching_totals.rmd` — supporting workload check.** Runs t-tests on total pitches per pitcher, with a boxplot, to test whether a change in workload explains the change in performance.

- **`Log_Likelihood.rmd` — market efficiency analysis.** Uses log-likelihood and chi-square tests to compare over/under results against a fair 50/50 market. This file contains two versions of the test — one for all series and one for 3 game series only.

Earlier drafts and side analyses (an ERA only version and an earlier scoring draft) are not included, so the files above are the complete, final version of the project.

## Methods and tools

  Language and environment: R and R Markdown, using tidyverse style data cleaning, joining, and plotting.
- Scoring: ANOVA and pairwise two-sample t-tests on total runs per game, by season.
- Pitching: a composite pitch strength metric built from scaled Statcast indicators, compared with paired t-tests within fast  and slow tempo groups.
- Market efficiency: log-likelihood and chi-square tests of over/under outcomes against a 50/50 fair market benchmark.
- Data work: multi source joins across Retrosheet, Statcast, and OddsShark, including team name mapping and doubleheader handling.

## Data

All analysis covers the 2022, 2023, and 2024 MLB seasons.

| Source | Data used |
| --- | --- |
| Retrosheet | Game logs and final scores, used for total runs per game |
| Statcast | Pitcher level pitching and tempo statistics, used for the pitch strength metric |
| OddsShark | Over/under lines and results, used for the market efficiency tests |

### Data files the code expects

The original code reads and writes files in a local folder. If you upload the datasets, put them in a `data/` folder in this repository and update the file paths at the top of each file to match — for example, `data/gl2022.txt` instead of the original local folder path.

Input files used by the code:

- Retrosheet game logs: `gl2022.txt`, `gl2023.txt`, `gl2024.txt`
- OddsShark workbooks: `Oddsshark - 2022.xlsx`, `Oddsshark - 2023.xlsx`, `Oddsshark - 2024.xlsx`
- Pitching data: `pitching .csv` and `pitching_stats_tempo.csv`
- Workload data: `total pitches 2022-2024.csv`

Main files created by the code:

- Season results: `mlb2022_results.csv`, `mlb2023_results.csv`, `mlb2024_results.csv`
- Over/under lines: `OU_Lines_2022.csv`, `OU_Lines_2023.csv`, `OU_Lines_2024.csv`
- Merged results with over/under outcomes, used by `Log_Likelihood.rmd`
- `consistent_pitchers_2022_2024.csv` — the 141 pitchers who appear in all three seasons

A note on uploading data: the smaller merged CSV files are the most useful ones to include, because they let a reader run the scoring and market analyses directly. If a raw file is very large, leave it out and rely on the source list above so readers can obtain the same data from Retrosheet, Statcast, and OddsShark themselves.

## How to run

1. Clone or download this repository.
2. Place the data files listed above in a `data/` folder, and update the file paths in each `.rmd` file if needed.
3. Open the project in RStudio.
4. Run `2022-2024_matchups.rmd` first — the later files use the merged files it creates.
5. Run the remaining files in the order listed above. Each file loads the packages it needs at the top.

## Suggested repository structure

```text
mlb-pitch-clock-capstone/
├── README.md
├── 2022-2024_matchups.rmd
├── Score_Compare_Means.rmd
├── pitching_tempo.rmd
├── pitching_totals.rmd
├── Log_Likelihood.rmd
└── data/
    ├── gl2022.txt
    ├── gl2023.txt
    ├── gl2024.txt
    ├── Oddsshark - 2022.xlsx
    ├── Oddsshark - 2023.xlsx
    ├── Oddsshark - 2024.xlsx
    ├── pitching .csv
    ├── pitching_stats_tempo.csv
    └── total pitches 2022-2024.csv
```

## About the author

Caitlyn Mahoney — B.S. in Mathematics with a concentration in Statistics & Modeling, Worcester State University, December 2025. This project was completed as a capstone in Fall 2025. Interests: data analysis, statistical modeling, and sports analytics.
