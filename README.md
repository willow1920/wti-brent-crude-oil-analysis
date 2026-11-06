# WTI–Brent Crude Oil Spot Price Spread Analysis

## Project overview
This project explores the historical relationship between West Texas Intermediate (WTI) and Europe Brent crude oil spot prices. It calculates the WTI–Brent spread, examines its long-term behavior, identifies statistical outliers and persistent outlier episodes, and presents results in an interactive Plotly dashboard.

**Core definition**

`Spread = WTI - Brent`

A negative spread means WTI is priced below Brent; a positive spread means WTI is priced above Brent.

## Data
- **WTI:** Cushing, Oklahoma WTI Spot Price FOB
- **Brent:** Europe Brent Spot Price FOB
- **Unit:** USD per barrel
- **Frequency:** Daily
- **Provider/source lineage:** DataHub / DataPressr compilation of U.S. Energy Information Administration (EIA) data
- **Dataset page:** https://datahub.io/datapressr/oil-prices
- **WTI CSV:** https://datahub.io/datapressr/oil-prices/_r/-/data/wti-daily.csv
- **Brent CSV:** https://datahub.io/datapressr/oil-prices/_r/-/data/brent-daily.csv
- **License stated by dataset:** Open Data Commons Public Domain Dedication and License (PDDL-1.0)

The notebook merges the two daily series using an inner join on `Date`, so only dates with observations in both series are retained.

## Methods
1. Load and inspect the source datasets.
2. Convert dates to datetime and check missing values, duplicate records, and date ordering.
3. Merge WTI and Brent prices by date.
4. Calculate the daily spread.
5. Summarize spread statistics and positive/negative observations.
6. Detect outliers using the 1.5×IQR rule.
7. Examine the concentration and duration of lower-outlier episodes.
8. Aggregate monthly and annual averages and calculate rolling averages and annual changes.
9. Build an interactive Plotly dashboard.
10. Examine the April 2020 negative WTI spot-price observation.

## Selected results from the saved notebook
- Merged observations: **9,790**
- Mean daily spread: **-1.71 USD/bbl**
- Median daily spread: **0.63 USD/bbl**
- Standard deviation: **5.39 USD/bbl**
- Minimum spread: **-54.34 USD/bbl**
- Maximum spread: **22.18 USD/bbl**
- IQR lower bound: approximately **-11.81 USD/bbl**
- IQR upper bound: approximately **9.66 USD/bbl**
- Lower outliers: **559**
- Upper outliers: **4**
- Lower outliers during 2011–2013: **496**, or **88.7%** of all lower outliers
- Lower outliers in 2011–2013 as a share of all observations in that period: **66.2%**

## Key interpretation
The most pronounced period of negative WTI–Brent spreads occurred during 2011–2013. Lower outliers were concentrated in three prolonged episodes rather than being evenly distributed. Annual price changes show that the spread movement reflects the relative change in the two benchmarks:

`ΔSpread = ΔWTI - ΔBrent`

The April 20, 2020 observation in this dataset records WTI at -36.98 USD/bbl and Brent at 17.36 USD/bbl. These are the spot-price series values in the dataset; they should not be confused with the official settlement price of the May 2020 WTI futures contract.

## Repository structure
```text
.
├── 003_oil_price_analysis_final_review.ipynb
├── wti-daily.csv
├── brent-daily.csv
└── README.md
```

## How to run
1. Install Python 3.10+.
2. Install dependencies:
   ```bash
   pip install pandas numpy plotly jupyter
   ```
3. Place both CSV files beside the notebook.
4. Open Jupyter Notebook or JupyterLab and run the notebook from top to bottom.

The notebook's source cells expect the exact filenames `wti-daily.csv` and `brent-daily.csv`.

## Limitations and reproducibility
- The merged dataset includes only dates present in both input series.
- IQR outliers are statistical flags, not automatic data errors.
- The analysis is descriptive and does not establish causality.
- The notebook snapshot ends on 2026-09-01; 2026 is a partial year.
- A fresh full execution was not performed during this review because the WTI CSV was not supplied as a local file. Existing saved outputs are retained, and the corrected outlier-run cells have had their outputs cleared for regeneration.
- DataHub/EIA snapshots and subsequent revisions may differ in historical coverage.

## Author note
This is an exploratory energy-data analytics portfolio project demonstrating data preparation, quality checks, statistical analysis, time-series analysis, outlier episode detection, and interactive visualization. It is not investment advice.
