---
title: "Residual Return Prediction & Portfolio Optimization"
date: 2025-05-31
author: ["Ashish Mathew"]
tags: ["Finance","Time Series","R"]
summary: "Build a ML model to predict stock alpha and backtest the portfolio"
editPost:
    URL: "https://github.com/ashishmathew98/financial-ds-project"
    Text: "GitHub"
showToc: false
disableAnchoredHeadings: false
---
## Project Objective

The goal of this project is to develop a robust machine learning pipeline to predict **residual asset returns**—the portion of a stock's return that cannot be explained by common market and industry factors. By isolating these idiosyncratic returns ("Alpha"), the project implements a mean-variance optimization strategy to construct an automated trading portfolio that maximizes risk-adjusted returns.

## Methodology

### 1. Data Processing & Liquidity Filtering

* **Dataset:** Daily return and covariance data spanning the period from **2003 to 2010**.
* **Liquidity Filter:** To ensure the strategy remains tradeable, the universe was restricted to assets with a market capitalization of **$1B or greater**. This reduced the dataset from 23 million to approximately 5 million rows.
* **Normalization:** Daily returns were **winsorized** to mitigate the impact of extreme outliers and normalize the distribution.

### 2. Factor Modeling & Residual Extraction

* The model accounts for **59 industry factors** and **6 style factors** (Beta, Size, Momentum, Value, Leverage, and Liquidity).
* **Residuals ($Y$)** were calculated by regressing asset returns against these factors using a pseudo-inverse approach, effectively stripping away market and sector noise.

### 3. Model Selection & Training

* **Data Split:** A chronological **70:30 train/test split** was used to ensure the model was evaluated on "future" unseen data.
* **Comparison:** Two models were evaluated using `TimeSeriesSplit` cross-validation:
* **LASSO (Linear):** Best alpha of 0.0001.
* **XGBoost (Non-linear):** Optimized for depth and learning rate.


* **Final Selection:** **LASSO** was selected as the final model due to its superior computational efficiency and better Mean Squared Error (MSE) performance on the validation sets.

### 4. Efficient Portfolio Optimization

The project utilizes the **Woodbury Matrix Identity** to handle large-scale portfolio optimization efficiently.

* The covariance matrix ($\sum$) is decomposed into factor exposure ($X$), factor covariance ($F$), and specific variance ($D$):
$$\sum = D + XFX^T$$
* This allow for daily weight updates without the computational burden of inverting a massive full covariance matrix.

## Results

* **Performance:** Backtesting on the test set revealed a **consistent upward trend in P&L**, demonstrating that the strategy successfully captured positive alpha.
  <img width="986" height="528" alt="image" src="https://github.com/user-attachments/assets/bdd0e81c-93f9-4498-9cc3-02cbfbb09251" />
* **Dollar Value:** Our portfolio remains dollar neutral i.e. the long market value (LMV) is approximately the same as the short market value (SMV). This is indicated by the graph below where the two lines are mirror images.
  <img width="1006" height="528" alt="image" src="https://github.com/user-attachments/assets/90058cbb-3c63-44ea-be5c-53975f1fb68f" />
* **Risk Management:** The optimization process successfully balanced factor exposures while focusing on idiosyncratic risk to generate stable returns. This is indicated by the chart below analyzing idiosyncratic risk as a percentage of total risk which shows that idiosyncratic risk accounts for 99% of total risk, showing that our PnL is driven by alpha generation.
  <img width="1008" height="528" alt="image" src="https://github.com/user-attachments/assets/789534f2-b974-4b4c-beff-3964f061f5e6" />
## Tech Stack

* **Language:** Python
* **Key Libraries:** `pandas`, `numpy`, `scikit-learn`, `xgboost`, `statsmodels`, `patsy`, `matplotlib`

---
