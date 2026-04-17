
# Hull-White Calibration & Swaption Pricing

> Calibration of the Hull-White one-factor short-rate model on €STR data, and multi-method swaption pricing under three equivalent measures.

## Overview

This project implements the full pipeline from model calibration to derivative pricing within the Hull-White (HW) framework:

1. **Calibration** of the HW parameters $(a, \sigma)$ from historical €STR data under the real-world measure $\mathbb{P}$, using two methods: AR(1) regression and Maximum Likelihood Estimation (MLE).
2. **Yield curve fitting** via a Nelson-Siegel parametrization to extract the initial term structure $\theta(t)$.
3. **Swaption pricing** under three equivalent measures — risk-neutral $\mathbb{Q}$, forward measure, and annuity measure — using Monte Carlo simulations and a Trinomial Tree.
4. **Convergence & sensitivity analysis** of both numerical methods.

## Model

The Hull-White one-factor model under the risk-neutral measure $\mathbb{Q}$:

$$dr_t = (\theta(t) - a r_t)\,dt + \sigma\,dW_t$$

- $a$ : mean-reversion speed (constant)
- $\sigma$ : volatility (constant)
- $\theta(t)$ : time-dependent drift calibrated to fit the initial yield curve

## Results

| Method | Swaption Price |
|---|---|
| Monte Carlo — Risk-neutral $\mathbb{Q}$ | 9.887 % |
| Monte Carlo — Forward measure | 9.887 % |
| Monte Carlo — Annuity measure | 9.886 % |
| Trinomial Tree | 9.888 % |

All four methods converge to ~9.89%, confirming the consistency of the implementation across measures and numerical schemes.

## Repository Structure

```
rates-models/
├── notebooks/
│   └── hull_white_swaption_pricing.ipynb   # Full pipeline: calibration → pricing
├── data/
│   └── ESTR.csv                            # ECB Euro Short-Term Rate (daily)
└── README.md
```

## Getting Started

**Prerequisites**
```bash
pip install numpy pandas scipy matplotlib
```

**Run the notebook**
```bash
jupyter notebook notebooks/hull_white_swaption_pricing.ipynb
```

> The notebook reads data from `../data/ESTR.csv` — keep the folder structure intact.

## References

- Hull, J. & White, A. (1990). *Pricing Interest-Rate Derivative Securities*. The Review of Financial Studies.
- Brigo, D. & Mercurio, F. (2006). *Interest Rate Models — Theory and Practice*. Springer.
- ECB Statistical Data Warehouse — Euro Short-Term Rate (€STR): `EST.B.EU000A2X2A25.WT`
  
