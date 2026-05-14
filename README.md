# Coffee Futures Price Forecasting — Master's Thesis

**HEC Lausanne, University of Lausanne (UNIL) | 2026**  
**Author:** Mohamed Hussein  
**Supervisor:** M. Vialfont  

## Overview

This repository contains the full analysis for my Master's thesis in Management 
(Business Analytics orientation). The study compares six forecasting models — 
ARIMAX, Multiple Linear Regression, Random Forest, XGBoost, SVM and ANN — 
applied to monthly Arabica and Robusta coffee futures prices over 2000–2023, 
using macroeconomic, climatic, and speculative determinants.

## View the Analysis

👉 [Click here to view the full analysis](https://mohamedhussein2304.github.io/coffee-thesis/Mémoire_de_Master_Quarto.html)

## Requirements

- R >= 4.2.0
- RStudio >= 2023.x
- Quarto >= 1.4

## R Packages Required

```r
packages <- c(
  "readxl", "dplyr", "tidyr", "lubridate", "zoo", "readr",
  "ggplot2", "corrplot", "tseries", "urca", "forecast",
  "scales", "gridExtra", "knitr", "kableExtra", "moments",
  "ggrepel", "randomForest", "xgboost", "e1071", "nnet",
  "Metrics", "tibble"
)
install.packages(packages)
```

## Data Sources

- Refinitiv / CEDIF (UNIL) — Coffee futures prices (Arabica & Robusta)
- FRED (Federal Reserve) — Macroeconomic variables (WTI, CPI, Fed Funds Rate)
- Investing.com — US Dollar Index (DXY)
- USDA FAS PSD Online — Supply and demand fundamentals
- OECD Data Explorer — Quarterly GDP growth
- CFTC Disaggregated COT — Speculative positioning (Managed Money)
- World Bank CCKP (ERA5 0.25°) — Climate data (14 producer countries, ADM1)
- NOAA — Oceanic Niño Index (ENSO)

## Repository Structure

    coffee-thesis/
    ├── Mémoire_de_Master_Quarto.qmd         # Full Quarto source code
    ├── Mémoire_de_Master_Quarto.html        # Rendered HTML analysis
    ├── styles.css                           # Custom CSS styling
    └── Mémoire_de_Master_Quarto_files/      # Figures and libraries
        ├── figure-html/                     # ggplot2 figures
        ├── figure-pdf/                      # PDF figures
        └── libs/                            # JavaScript libraries

## How to Reproduce

1. Clone this repository
2. Place your data files in `Datasets mémoire de master/`
3. Open `Mémoire de Master.Rproj` in RStudio
4. Run the following in the terminal:

```bash
quarto render Mémoire_de_Master_Quarto.qmd
```

## Models Estimated

| Model | Arabica R² | Robusta R² |
|-------|-----------|-----------|
| ARIMAX | 0.821 | 0.929 |
| MLR | 0.784 | 0.276 |
| Random Forest | 0.802 | 0.701 |
| XGBoost | 0.818 | 0.796 |
| SVM | 0.696 | 0.624 |
| ANN | 0.762 | 0.775 |

## License

This project is for academic purposes only. Data sources are subject to their 
respective licenses and terms of use.
