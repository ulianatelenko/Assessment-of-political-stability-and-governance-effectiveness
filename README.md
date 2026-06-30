## Table of Contents

- [Project Title](#assessment-of-political-stability-and-governance-effectiveness)
- [Problem Description](#problem-description)
- [Tools Used](#tools-used)
- [Methodology](#methodology)
- [Results](#results)
- [Data Source](#data-source)
- [Project Structure](#project-structure)
- [How to Run (for Windows)](#how-to-run-for-windows)

# Assessment of Political Stability and Governance Effectiveness

A data analysis project focused on evaluating political stability and governance effectiveness across countries using international indicators from multiple sources.


## Problem Description

Political stability and governance effectiveness are complex topics that cannot be evaluated using only one indicator. Different international datasets measure related aspects such as governance quality, political freedoms, human rights, fragility, and state stability.

However, these datasets often come from different sources, use different scales, and have different formats. This makes direct comparison difficult without proper data preparation and standardization.

The main goal of this project was to combine several governance-related datasets into one structured dataset, transform the indicators into comparable units, and calculate a composite score that helps compare countries based on political stability and governance effectiveness.

The project answers questions such as:

- Which countries demonstrate stronger governance and political stability?
- Which countries show weaker governance performance?
- How can multiple political and governance indicators be combined into one composite index?
- How can countries be grouped based on similar governance profiles?

The project combines data preparation in **Microsoft Excel** with statistical analysis and visualization in **Python**.


## Tools Used

 **Microsoft Excel**
  - Initial data review and preparation
  - Manual inspection of source files
  - Organizing datasets before transformation
  - Prepared the initial `raw_data.xlsx` file for further analysis

 **Power Query**
  - Imported multiple datasets
  - Merged separate files into one structured table
  - Removed unnecessary columns
  - Filtered irrelevant rows
  - Converted data types
  - Transformed selected indicators into the same measurement direction
  - Standardized variables to comparable units of measurement

 **Python**
  - Cleaned and processed the dataset
  - Handled missing values using interpolation
  - Scaled indicators before PCA
  - Performed Principal Component Analysis
  - Calculated a composite governance indicator
  - Generated output files and visualizations

 **Pandas**
  - Data cleaning, transformation, aggregation, and export
  - Creating a correlation matrix between indicators

 **Scikit-learn**
  - Feature scaling and outliers removal with `StandardScaler`
  - PCA modeling

 **Matplotlib / Plotly**
  - Data visualization and world map creation

 **Jupyter Notebook**
  - Step-by-step analysis and documentation


## Methodology

### 1) Cleaning & preprocessing

- Collected propper data from the sources.
- Combined the data to one file, using Power Query.
- Removed unnecessary data.
- Result: [**raw_data.xlsx**](data/raw/raw_data.xlsx)

### 2) Missing Values

- Computed missing counts per country.
- Applied linear interpolation.
- Result: [**filled_missing_data.csv**](data/processed/filled_missing_data.csv)

### 3) Correlation Analysis and Outlier Detection

Before calculating indicator weights and applying PCA, an exploratory data quality check was performed to better understand relationships between variables and identify potential data issues.

The following steps were completed:

- Built a correlation matrix to analyze relationships between governance and stability indicators.
- Checked whether selected variables were meaningfully related and suitable for dimensionality reduction.
- Identified highly correlated indicators that could influence PCA results.
- Reviewed potential outliers that could distort the composite indicator calculation.
- Examined unusual country-year observations before proceeding with normalization and PCA.

### 4) Feature Scaling

Because PCA is sensitive to differences in scale, all indicators were **normalized** before dimensionality reduction using:

- scaler: `StandardScaler()`.
- output: zero mean, unit variance features.
- Result: [**normalized_indicators.csv**](data/processed/normalized_indicators.csv)

### 5) PCA

Principal Component Analysis helped to:

- Reduce dimensionality.
- Reveal latent structure in correlated indicators.
- Produce component scores per record (PC1, PC2).
- Result: [**weights_table.csv**](data/processed/weights_table.csv)

### 6) Composite Indicator Calculation

The PCA output was used to calculate a composite governance indicator. The process included:

- Extracting weights from PCA results.
- Combining normalized indicators using a weighted sum.
- Calculating a composite score for each country-year.
- Aggregating results to produce a final score per country.
- Ranking countries by the final composite indicator.
- Result: [**composite_index_ranked.csv**](data/processed/composite_index_ranked.csv)

### 7) Country Clustering and Visualization

- Countries were grouped based on their composite indicator scores.
- The final result was visualized as a clustered world map.
- Results:
  - [**clustered_countries.png**](clustered_countries/clustered_countries.png) - clustered world map visualization  
  - [**clustered_countries.csv**](clustered_countries/clustered_countries.csv) — country with cluster mapping


## Results

The project produced:

- A cleaned and interpolated country-level dataset.
- Normalized governance indicators.
- PCA-based indicator weights.
- A composite governance effectiveness score.
- A ranked table of countries.
- A clustered world map showing groups of countries with similar governance profiles.


## Data Source
- [**Governance Effectiveness:**](https://www.worldbank.org/en/publication/worldwide-governance-indicators/documentation#4)
- [**Human Rights And Freedoms:**](https://freedomhouse.org/reports/freedom-world/freedom-world-research-methodology)
- [**The Fragillity Of States:**](https://fragilestatesindex.org/excel/)


## Project Structure

```text
.
├── main.ipynb
├── README.md
├── data/
│   ├── raw/
│   │   └── raw_data.xlsx
│   └── processed/
│       ├── filled_missing_data.csv
│       ├── normalized_indicators.csv
│       ├── weights_table.csv
│       └── composite_index_ranked.csv
└── clustered_countries/
    ├── clustered_countries.csv
    └── clustered_countries.png
```
## How to Run (for Windows)

Open Command Prompt or PowerShell, clone the repository, create a virtual environment, install dependencies, and start Jupyter Notebook. Then open `main.ipynb` and run all cells from top to bottom.

```bash
git clone https://github.com/ulianatelenko/Assessment-of-political-stability-and-governance-effectiveness
cd Assessment-of-political-stability-and-governance-effectiveness

python -m venv .venv
.venv\Scripts\activate

pip install -U pip
pip install pandas numpy scikit-learn matplotlib openpyxl jupyter

jupyter notebook
```
