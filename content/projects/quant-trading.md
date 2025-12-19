---
title: "Quant Trading"
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

## Residual Return Prediction & Portfolio Optimization
**Objective:**The goal of this project is to develop a robust machine learning pipeline to predict residual asset returns—the portion of a stock's return that cannot be explained by common market and industry factors. By isolating these idiosyncratic returns ("Alpha"), the project implements a mean-variance optimization strategy to construct an automated trading portfolio that maximizes risk-adjusted returns.

### Methodology
1. Data Processing & Liquidity Filtering 
- Dataset: Daily return and covariance data spanning the period from 2003 to 2010.
- Liquidity Filter: To ensure the strategy remains tradeable, the universe was restricted to assets with a market capitalization of $1B or greater. This reduced the dataset from 23 million to approximately 5 million rows.
- Normalization: Daily returns were winsorized to mitigate the impact of extreme outliers and normalize the distribution.
2. Factor Modeling & Residual Extraction
The model accounts for 59 industry factors and 6 style factors (Beta, Size, Momentum, Value, Leverage, and Liquidity).Residuals ($Y$) were calculated by regressing asset returns against these factors using a pseudo-inverse approach, effectively stripping away market and sector noise.
3. Model Selection & Training
- Data Split: A chronological 70:30 train/test split was used to ensure the model was evaluated on "future" unseen data.
- Comparison: Two models were evaluated using TimeSeriesSplit cross-validation:
    - LASSO (Linear): Best alpha of 0.0001.
    - XGBoost (Non-linear): Optimized for depth and learning rate.
- Final Selection: LASSO was selected as the final model due to its superior computational efficiency and better Mean Squared Error (MSE) performance on the validation sets.
4. Efficient Portfolio Optimization
The project utilizes the Woodbury Matrix Identity to handle large-scale portfolio optimization efficiently.
- The covariance matrix ($\Sigma$) is decomposed into factor exposure ($X$), factor covariance ($F$), and specific variance ($D$):
$$\Sigma = D + XFX^T$$
This allow for daily weight updates without the computational burden of inverting a massive full covariance matrix.

Results
Performance: Backtesting on the test set revealed a consistent upward trend in P&L, demonstrating that the strategy successfully captured positive alpha.

Risk Management: The optimization process successfully balanced factor exposures while focusing on idiosyncratic risk to generate stable returns.

Tech Stack
Language: Python

Key Libraries: pandas, numpy, scikit-learn, xgboost, statsmodels, patsy, matplotlib