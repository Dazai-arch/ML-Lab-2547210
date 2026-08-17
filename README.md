# Lab 2: Data Preprocessing & Exploratory Data Analysis (Part 2)

## Aim
To continue the EDA started in Lab 1 by performing time-based trend analysis, seasonal analysis, state-level aggregation, and cross-dataset correlation between air quality and crop yield.

## Datasets
| Dataset | File | Description |
|---|---|---|
| Air Quality | `city_day.csv` | Day-wise air quality readings (PM2.5, PM10, NO, NO2, NOx, NH3, CO, SO2, O3, Benzene, Toluene, AQI) across Indian cities |
| Crop Production | `crop_production.csv` | State/district-wise crop production records (Crop, Season, State, Production, Area, etc.) |

## Notebook
- `Lab2.ipynb`

## Steps / Tasks Covered

**Tasks 1–5** repeat the same preprocessing pipeline as Lab 1 (dataset exploration, missing-value imputation via group-wise median, state-name cleanup for merging, AQI distribution plots, IQR-based outlier capping) to rebuild the cleaned datasets used in the rest of the notebook.

| Task | Description |
|---|---|
| **Task 6: Yearly Trend Analysis** | Extract `Year` from `Date`; compute mean AQI per year; identify the most and least polluted years; visualize the trend with a line plot |
| **Task 7: Seasonal Analysis** | Extract `Month` from `Date`; compute mean AQI per month; group months into 4 seasons (Winter, Pre-Monsoon, Monsoon, Post-Monsoon); visualize monthly and seasonal AQI with color-coded bar charts |
| **Task 8: State-Wise Aggregation & Correlation** | Map cities to states; aggregate mean AQI, PM2.5, NO2, SO2, PM10 by state; aggregate crop production/area by state and compute `Yield = Production / Area`; merge air-quality and crop data at state level; visualize correlations with a heatmap and yield bar chart |
| **Task 9: Insights & Conclusions** | Summarize national-level findings (e.g., AQI trend from 2016–2020) and combined conclusions from Lab 1 + Lab 2 |
| **Optional Task A** | Rank states by pollution and compare crop yield between the top-5 most polluted and top-5 least polluted states |
| **Optional Task B** | Compute Pearson correlation between state-level Mean AQI and Crop Yield; visualize with a scatter plot and regression line |
| **Optional Task C** | Full correlation heatmap combining all air-quality and crop variables at the state level |

## Key Techniques Used
- `pandas` `.dt` accessor for extracting Year/Month from dates
- `groupby().agg()` for state-level aggregation of multiple metrics
- `pandas.merge()` to combine air-quality and crop datasets at the state level
- `scipy.stats.pearsonr` and `scipy.stats.linregress` for correlation and trend-line analysis
- `seaborn` heatmaps and `matplotlib` bar/line/scatter plots for visualization

## Key Findings
- National average AQI **fell ~45%, from 191 (2016) to 111 (2020)**, roughly 17 AQI points/year of improvement, though a spike occurred between 2015–2016.
- Pollution peaks in **October–November** (harvest/stubble-burning season) and remains high through December–January; the claim that pollution is worst only during harvest season is **partly true**.
- Mean AQI and Mean NO2 show a **strong positive correlation (r ≈ 0.73)** at the state level, consistent with vehicular/industrial sources.
- Mean AQI vs. Crop Yield shows a **weak negative correlation (r ≈ -0.20)** — high-pollution states don't consistently have lower yields, so the "pollution reduces crop yield" hypothesis is only partially supported.

## How to Run
1. Place `city_day.csv` and `crop_production.csv` in the same directory as the notebook.
2. Install dependencies:
   ```bash
   pip install pandas matplotlib seaborn scipy numpy
   ```
3. Open `Lab2.ipynb` and run all cells in order.

## Relation to Lab 1
This lab builds directly on the cleaning pipeline established in **Lab1** (branch `Lab1`) — Tasks 1–5 are repeated here to regenerate the cleaned DataFrames before the new analysis in Tasks 6–9 and the optional tasks.