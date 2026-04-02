# Residual Value Risk Modelling — Automotive Lease Portfolios

**Author:** Nisrina Walyadin  
**Stack:** Python · statsmodels · Scikit-learn · Monte Carlo · R · ggplot2

📊 **[View Live Report](https://nicherina.github.io/rv-risk-analysis/r_replication/06_rv_risk_report.html)**

---

## Business Context

BMW Financial Services guarantees a buyback price when a customer leases a vehicle.  
If the **market value at end-of-lease falls below the guaranteed price**, the portfolio absorbs the loss.

This project models:
1. How cars depreciate (OLS log-linear model)
2. Which contracts carry residual value risk
3. Total portfolio exposure under market uncertainty (Monte Carlo simulation)
4. EV vs ICE risk differential

---

## Key Findings

- EV vehicles trade at a **~30% discount** to equivalent ICE vehicles, amplifying RV shortfalls
- Vehicles aged **7+ years are at risk in >90% of scenarios**
- **Monte Carlo simulation (10,000 runs)** quantifies portfolio loss distribution under market uncertainty
- Scenario analysis covers Base, Stress, and Severe (EV market drop −20%) shocks

---

## Project Structure

```
rv_risk_project/
├── data/
│   ├── vehicles.csv                  # Raw download (not committed)
│   ├── vehicles_clean.csv            # After notebook 01
│   ├── vehicles_with_predictions.csv # After notebook 02
│   └── vehicles_risk_scored.csv      # After notebook 03
├── notebooks/
│   ├── 01_data_and_eda.ipynb         # Data pull, cleaning, EDA
│   ├── 02_depreciation_model.ipynb   # OLS depreciation model
│   ├── 03_risk_classification.ipynb  # Contract-level risk scoring
│   └── 04_monte_carlo.ipynb          # Fleet portfolio simulation
├── r_replication/
│   └── 05_r_replication.Rmd          # R replication (ggplot2, broom)
├── outputs/
│   └── *.png                         # All charts saved here
└── README.md
```

---

## How to Run

### Python (recommended order)

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels kagglehub openpyxl

# Run notebooks in order:
jupyter notebook notebooks/01_data_and_eda.ipynb
jupyter notebook notebooks/02_depreciation_model.ipynb
jupyter notebook notebooks/03_risk_classification.ipynb
jupyter notebook notebooks/04_monte_carlo.ipynb
```

### Data download

The project uses the [Vehicle Sales Dataset](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data) from Kaggle.

**Option A (automatic):** Set up your Kaggle API token at `~/.kaggle/kaggle.json` and run notebook 01.  
**Option B (manual):** Download `car_prices.csv` from the link above and place it at `data/vehicles.csv`.

### R replication

```r
# In RStudio: open r_replication/05_r_replication.Rmd → Knit
# Requires: tidyverse, broom, scales, viridis
install.packages(c("tidyverse", "broom", "scales", "viridis"))
```

---

## Methods

| Step | Method | Library |
|------|--------|---------|
| Depreciation modelling | OLS log-linear regression | statsmodels (Python) / lm (R) |
| Risk classification | Rule-based + threshold scoring | pandas |
| Uncertainty quantification | Monte Carlo simulation (10,000 runs) | NumPy |
| Scenario analysis | Base / Stress / Severe market shocks | NumPy |
| Visualisation | Matplotlib, Seaborn | Python |
| R replication | ggplot2, broom | R |

---

## Outputs

| File | Description |
|------|-------------|
| `01_price_distribution.png` | Raw vs log-transformed price |
| `02_depreciation_curve.png` | Median market value by age |
| `03_ev_vs_ice_depreciation.png` | EV vs ICE comparison |
| `04_predicted_vs_actual.png` | Model fit |
| `05_rv_with_confidence_band.png` | OLS prediction + 95% CI |
| `06_risk_heatmap.png` | % at risk by age band & fuel type |
| `07_risk_by_brand.png` | Exposure breakdown by brand |
| `08_monte_carlo_distribution.png` | Loss distribution with VaR |
| `09_scenario_comparison.png` | Base vs Stress vs Severe |
| `R_01_depreciation_curve.png` | ggplot2 replication |
| `R_02_predicted_vs_actual.png` | ggplot2 replication |
| `R_03_risk_by_age_band.png` | ggplot2 replication |
