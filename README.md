# Assessment of political stability and governance effectiveness

 This project builds a cleaned, interpolated country-level dataset and uses PCA to explore underlying patterns across indicators, producing interpretable components (PC1/PC2) and visual summaries.


## Table of Contents
- [Overview](#overview)
- [What’s inside](#whats-inside)
- [Data source](#data-source)
- [Methodology](#methodology)
- [Results](#results)
- [Project structure](#project-structure)
- [How to run](#how-to-run)
- [License](#license)


## Overview
This repository contains a **data analysis** project focused on **political stability and governance effectiveness**.  
As a result, we can see a clustered world map based on the calculated composite indicator.

## What’s inside
A notebook that:
- loads and cleans the dataset  
- handles missing data using interpolation  
- scales features  
- performs PCA  
- calculates a composite indicator  
- visualizes country distributions and contributions


## Data source
- [**Governance Effectiveness:**](https://www.worldbank.org/en/publication/worldwide-governance-indicators/documentation#4)
- [**Human Rights And Freedoms:**](https://freedomhouse.org/reports/freedom-world/freedom-world-research-methodology)
- [**The Fragillity Of States:**](https://fragilestatesindex.org/excel/)


## Methodology
### 1) Cleaning & preprocessing
- Collect propper data from the sources.
- Combine the вшааукуте data to one file, using Excel.
- Remove unnecessary data.
- Result: [**raw_data.xlsx**](data/raw/raw_data.xlsx)

### 2) Missing values
- Compute missing counts per country.
- Apply linear interpolation.
- Result: [**filled_missing_data.csv**](data/processed/filled_missing_data.csv)

### 3) Scaling
PCA is sensitive to feature scale, so I used **normalization**:
- scaler: `StandardScaler()`.
- output: zero mean, unit variance features.
- Result: [**normalized_indicators.csv**](data/processed/normalized_indicators.csv)

### 4) PCA
Principal Component Analysis is used to:
- reduce dimensionality.
- reveal latent structure in correlated indicators.
- produce component scores per record (PC1, PC2).
- Result: [**weights_table.csv**](data/processed/weights_table.csv)

### 5) Composite indicator
- Used the PCA output to obtain **weights** for each indicator.
- Combined the normalized indicators into a **single composite score** for each country-year using a weighted sum.
- Aggregated the score to get a final value per country.
- Created a ranked table of countries by the composite indicator and saved it for the clustering step.
- Result: [**composite_index_ranked.csv**](data/processed/composite_index_ranked.csv)

## Results
- Built a clustered world map based on the composite indicator (higher score = stronger political stability and governance effectiveness).
- Grouped countries into clusters with similar composite scores and compared their distributions.
- Exported the cluster assignments and a visualization for easy interpretation.

**Outputs:**
- [**clustered_countries.png**](outputs/clustered_countries.png) - clustered world map visualization  
- [**clustered_countries.csv**](outputs/clustered_countries.csv) — country with cluster mapping

## Project structure

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
└── outputs/
    ├── clustered_countries.csv
    └── clustered_countries.png
```
## How to run (for Windows)

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
