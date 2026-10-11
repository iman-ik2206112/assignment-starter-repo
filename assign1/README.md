# Assignment 1

**Global AI Jobs 2026** dataset (5,000 job postings, 37 columns). Everything is in one notebook, `assign1.ipynb`.
Gold is a star schema, and four analytical questions are answered from Gold tables only.

- **URL:** https://www.kaggle.com/datasets/datascikhan/global-ai-jobs-2026

## Setup

1. Install Python 3.10 or newer, then the packages:
```bash
   pip install duckdb pandas matplotlib jupyter
```
   A recent DuckDB (1.4 or newer) is needed for DuckLake and `MERGE INTO`. The first run needs an internet
   connection once, so DuckDB can install the `ducklake` extension.
2. Download `global_ai_jobs_2026.csv` from the Kaggle URL above and place it in the same folder as `assign1.ipynb`
   (the notebook reads it with the relative path `global_ai_jobs_2026.csv`).
3. Open `assign1.ipynb` in Jupyter or VS Code.

The setup cell uses DuckLake (`USE_DUCKLAKE = True`). Setting it to `False` uses a plain DuckDB file with the same
schemas and the same SQL.

## Execution order

Run **all cells from top to bottom** (Restart kernel -> Run All). The first code cell deletes and recreates `lakehouse/` and `landing_zone/`, so every run starts clean. Do not run later cells on their own after restarting the kernel, because they need the setup cell and the tables created before them.

## Known limitations

- `Posted_Date` runs from 2026 to 2039, and 4,760 of the 5,000 rows have `Posted_Date` after `Record_Created`, so no time-trend question is asked. The problem is reported in the quality report and the rows are not removed.
- `Record_Created` has only one value, so it cannot be a watermark. `Posted_Date` is used only to split the file into three simulated daily deliveries.
- The source passed every validation rule, so the quarantine table is empty.
- The pay period of `Salary_USD` is not stated in the source, so salary results describe this dataset only.
- The source has no change date, so `QUALIFY` keeps the latest copy of a duplicate by ingestion time.

# Acknowledgements

I understood and played with code examples the doctor provided to us, especially the 01_meddalion_ducklake. This helped me to build this assignment. I used AI tool wisely to help me configure any data issues that I might not discover it by myself. Also, I used it to help me plot the star schema and visuals when answering the 4 questions as the doctor example I followed did not plot that.