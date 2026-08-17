# Lab 1: Data Preprocessing & Exploratory Data Analysis (Part 1)

## Aim
To perform data loading, cleaning, missing-value treatment, dataset merging, and outlier detection/treatment on real-world datasets using pandas.

## Datasets
| Dataset | File | Description |
|---|---|---|
| Air Quality | `city_day.csv` | Day-wise air quality readings (PM2.5, PM10, NO, NO2, NOx, NH3, CO, SO2, O3, Benzene, Toluene, AQI, AQI_Bucket) across Indian cities |
| Crop Production | `crop_production.csv` | State/district-wise crop production records (Crop, Season, State, Production, etc.) |

## Notebook
- `Lab1.ipynb`

## Steps / Tasks Covered

| Task | Description |
|---|---|
| **Setup** | Load both datasets into pandas DataFrames using `pd.read_csv()`; preview the first 5 rows of each |
| **Task 1: Dataset Exploration** | Inspect shape, columns, dtypes, summary statistics (`.describe()`), and count/percentage of missing values and duplicates for both datasets |
| **Task 2: Missing Value Treatment** | - City dataset: drop `Xylene` and `AQI_Bucket` (excessive missing values); fill pollutant columns (`PM2.5`, `PM10`, `NO`, `NO2`, `NOx`, `NH3`, `CO`, `SO2`, `O3`, `Benzene`, `Toluene`, `AQI`) with the **median grouped by City**, falling back to the overall median where needed<br>- Crop dataset: fill `Production` with the **median grouped by Crop and Season** |
| **Task 3: Dataset Merging & Consistency** | Clean inconsistent state names in the crop dataset (strip whitespace, title-case, map old names like `Orissa` → `Odisha`, `Uttaranchal` → `Uttarakhand`, `Pondicherry` → `Puducherry`); map each city to its state; cross-check state-name consistency between the two datasets before merging |
| **Task 4: Distribution Analysis** | Plot a histogram and box plot of `AQI` to visualize its distribution and spot extreme outliers |
| **Task 5: Outlier Treatment (IQR Method)** | Compute Q1, Q3, and IQR for `AQI`; flag values outside `[Q1 − 1.5×IQR, Q3 + 1.5×IQR]` as outliers; cap (clip) `AQI` to these bounds and compare box plots before vs. after treatment |

## Key Techniques Used
- `pandas` for data loading, cleaning, and grouped aggregation (`groupby().transform()`)
- Missing value imputation using **group-wise median**
- String cleaning (`.str.strip()`, `.str.title()`) and value mapping (`.replace()`) for merge-key consistency
- IQR method for outlier detection and capping
- `matplotlib` for histograms and box plots

## Key Findings
- The City dataset has **29,531 observations and 16 attributes**, with several pollutant columns missing up to ~38% of values (`NH3`); the Crop dataset has **246,091 observations and 7 attributes**, missing only ~1.5% of `Production` values.
- A direct merge on state names would silently drop rows due to trailing whitespace and naming mismatches (e.g., `'Tamil Nadu'` vs `'Tamil Nadu '`), so state names were cleaned before merging.
- AQI is heavily right-skewed with extreme outliers (values exceeding 2000); after IQR-based capping, the maximum AQI dropped to **391**.

## How to Run
1. Place `city_day.csv` and `crop_production.csv` in the same directory as the notebook.
2. Install dependencies:
   ```bash
   pip install pandas matplotlib
   ```
3. Open `Lab1.ipynb` and run all cells in order.

## Continuation
This lab is continued in **Lab2** (branch `Lab2`), which builds on the cleaned datasets here to perform trend analysis, seasonal analysis, state-wise aggregation, and final insights.
