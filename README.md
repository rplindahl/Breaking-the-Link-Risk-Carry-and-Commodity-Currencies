# Breaking-the-Link-Risk-Carry-and-Commodity-Currencies

This repository contains the data pipeline and econometric analysis for a project investigating the relationship between country-specific commodity price shocks and exchange rate movements. 

We construct custom, daily commodity export and import price indices for various countries and evaluate their impact on currencies using panel data econometrics.

Link to working paper: [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6392120)

## 📋 Project Overview
1. **Index Construction:** We built unique daily export and import commodity price indices for individual countries. We did this by downloading annual trade data, calculating the percentage share of specific commodities in a country's total trade portfolio, and multiplying those weights by daily global commodity prices.
2. **Currency Data:** We track currency performance using both bilateral exchange rates against the USD and Nominal Effective Exchange Rates (NEER).
3. **Econometric Analysis:** We use time-series methodologies to test how commodity price shocks impact currencies over time, and how global uncertainty or market states alter that relationship.

## File Structure & Workflow

The project is divided into four main Jupyter Notebooks:

### 1. `trade_api.ipynb` (Trade Data & Weights)
* Connects to the UN Comtrade API to download annual export and import data.
* Maps over 60 specific commodities using their Harmonized System (HS) codes.
* Calculates the percentage share of each commodity relative to a country's total commodity trade, establishing the weights for our indices.
* Aggregates data for individual countries.

### 2. `com_price_index_construction.ipynb` (Index Creation)
* Loads daily global commodity prices (e.g., Brent Crude, Copper, Wheat).
* Merges the daily prices with the annual country-specific trade weights calculated in the previous step.
* Computes the final daily Export and Import Commodity Price Indices for each country and normalizes them to a base year.
* Generates descriptive statistics and visualizations for the newly created indices.

### 3. `currency_calc.ipynb` (Exchange Rate Processing)
* Standardizes daily bilateral exchange rates (vs. USD) ensuring consistent naming and base-currency formatting.
* Calculates daily log returns for the currency pairs.

### 4. `regressions_currency.ipynb` (Econometric Analysis)
This notebook includes the core econometric analysis, utilizing panel data to test the impact of our custom indices on exchange rates. 
* **Baseline Local Projections (LP):** Estimates the impulse response of currencies to commodity export/import shocks over time.
* **Panel Local Projections:** Runs LP across groups of countries (e.g., Commodity Exporters).
* **Threshold Panel LP:** Tests for state-dependence (e.g., how do currencies react to commodity shocks when global uncertainty/VIX is exceptionally high vs. low?).
* **Rolling Regressions:** Evaluates how the sensitivity of exchange rates to commodity prices evolves over time using rolling windows.
* **Bayesian Model Averaging (BMA):** Plots the  Posterior Inclusion Probabilities (PIP) extracted from seperate code in R.
