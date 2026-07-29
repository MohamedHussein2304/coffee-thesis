# Predicting Arabica and Robusta Coffee Futures Prices

Master's thesis project, HEC Lausanne (University of Lausanne)
Author: Mohamed Hussein · Supervisor: M. Vialfont

## What this is

This is my Master's thesis in Management (Business Analytics), where I compare six different models for forecasting monthly Arabica and Robusta coffee futures prices between 2000 and 2023. The idea is to see how two classic econometric approaches (Multiple Linear Regression and ARIMAX) stack up against four machine learning models (Random Forest, XGBoost, SVM, and a neural network), using a mix of macroeconomic data, USDA supply/demand fundamentals, climate variables, the ENSO/ONI index, and speculative positioning data from the CFTC.

Models are evaluated out-of-sample with a walk-forward expanding window, so at every step the model only ever sees data it would have had access to at the time.

## What's in this repo

- `Mémoire_de_Master_Quarto.qmd` — the whole analysis, from data cleaning to the final discussion. This is the main file.
- `Mémoire_de_Master_Quarto.html` — the rendered version, if you just want to read the results without running anything.
- `Mémoire_de_Master_Quarto_files/` — figures and assets Quarto generates when it renders the document.
- `styles.css` — some custom styling for the HTML output.

The full thesis submitted to the faculty, including the literature review, is maintained separately as a PDF and is not part of this repository.

## About the data

I can't include the raw data here. Some of it (mainly the Refinitiv/CEDIF futures prices) is licensed and I'm not allowed to redistribute it, and the rest is just excluded to keep things clean. If you want to reproduce the analysis, here's where everything comes from:

| Data | Source |
|---|---|
| Arabica, Robusta, Sugar No.1, Cocoa futures prices | Refinitiv (institutional access via CEDIF) |
| CPI, WTI, Federal Funds Rate | FRED |
| DXY (US Dollar Index) | Investing.com |
| Production, Consumption, Exports, Ending Stocks | USDA FAS PSD Online |
| Real GDP growth | OECD Data Explorer |
| ONI / ENSO index | NOAA |
| Temperature, Precipitation (ERA5, 0.25°, ADM1-level) | World Bank Climate Knowledge Portal |
| Managed Money net positioning (COT) | CFTC Disaggregated Futures-Only reports |

## Running this yourself

You'll need R with these packages:

- **Data import & wrangling**: `readxl`, `readr`, `dplyr`, `tidyr`, `tibble`, `lubridate`, `zoo`
- **Visualization**: `ggplot2`, `corrplot`, `scales`, `gridExtra`, `ggrepel`, `ggh4x`
- **Stationarity & diagnostics**: `tseries`, `urca`, `car`, `moments`, `broom`
- **Models**: `forecast` (ARIMAX), `randomForest`, `xgboost`, `e1071` (SVM), `nnet`, `neuralnet`, `RSNNS`, `rpart` (CART), `glmnet` (LASSO/Ridge)
- **Model evaluation**: `Metrics`
- **Reporting**: `knitr`, `kableExtra`
- **Text processing**: `tidytext`
- **Python bridge**: `reticulate`, `keras3`

Two parts of the analysis step outside base R:

- The **ANN activation function comparison** uses `keras3` (via `reticulate`) to compare against `neuralnet`'s default optimiser.
- The **Random Forest cost-complexity pruning** robustness check calls **scikit-learn** directly through `reticulate`, since R's `randomForest` has no direct `cp`-style parameter.

Both require a working Python environment with the relevant packages (TensorFlow/Keras backend, scikit-learn) installed and accessible to `reticulate`.

## How it's set up

- Walk-forward validation with an 80/20 split, re-estimated at every step as the window expands.
- ARIMAX's (p,d,q) order is chosen once on the initial training window and then held fixed for the rest of the loop, rather than re-selected at every step.
- The ML models are trained on Min-Max scaled price levels, not first differences (differencing killed almost all predictive signal, see the discussion in the thesis for why).

## Results

Out-of-sample R² for each model:

| Model | Arabica | Robusta |
|---|---|---|
| ARIMAX | 0.955 | 0.926 |
| XGBoost | 0.812 | 0.797 |
| SVM | 0.813 | 0.761 |
| Random Forest | 0.815 | 0.676 |
| MLR | 0.784 | 0.276 |
| ANN | 0.728 | 0.456 |

There's a lot more in the actual document: four robustness checks (disaggregated climate data, variety-specific predictors, GDP growth, lagged COT positioning), plus extra digging into ARIMAX order selection, Random Forest tuning and pruning, ANN depth and activation functions, and MLR regularisation.

## Read the analysis online

The full analysis is available at: https://mohamedhussein2304.github.io/coffee-thesis/Mémoire_de_Master_Quarto.html

## Reproducibility

*(CI badge once GitHub Actions is set up — checks the code runs on Windows, macOS and Ubuntu)*

## Citing this

> Hussein, M. (2026). *Predicting Arabica and Robusta Coffee Futures Prices: A Machine Learning Approach with Macroeconomic, Climatic, and Speculative Determinants* [Master's thesis, HEC Lausanne, University of Lausanne].

## Questions

Feel free to open an issue or reach out directly.

## AI Assistance Declaration

Claude (Anthropic) was used as an AI assistant during the development of this project, including support for writing and structuring the thesis text and for the design and debugging of the R data processing and modelling pipeline implemented in Quarto. All analytical decisions, interpretations, and written content remain the sole responsibility of the author.
