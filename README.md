# Rumor Spread Modelling

A comprehensive mathematical and data-driven study of rumor propagation across News and Twitter platforms using extended Daley–Kendall / Maki–Thompson (DK/MT) rumor models, RK4 numerical integration, and LSTM neural networks.

---

## Overview

This project investigates how rumors spread in different information ecosystems using:

- Nonlinear differential equation models
- Real-world News and Twitter datasets (2020–2022)
- Numerical simulation using RK4
- Parameter estimation and error analysis
- LSTM-based time-series forecasting

The work combines interpretable dynamical systems with deep learning methods to analyze endogenous and exogenous rumor propagation dynamics.

---

# Mathematical Model

The project implements an extended DK/MT rumor-spreading framework with three compartments:

- **Ignorants (I)** — users unaware of the rumor
- **Spreaders (S)** — users actively spreading the rumor
- **Stiflers (R)** — users who stop spreading the rumor

The governing equations are:

\[
\frac{dI}{dt} = -\beta \frac{IS}{N}
\]

\[
\frac{dS}{dt}
=
\beta \frac{IS}{N}
-
\alpha \frac{S(S+R)}{N}
+
\kappa \lambda(t)
\]

\[
\frac{dR}{dt}
=
\alpha \frac{S(S+R)}{N}
\]

where:

- \(\beta\) = rumor transmission rate
- \(\alpha\) = stifling rate
- \(\kappa\) = external forcing strength
- \(\lambda(t)\) = real-world forcing signal from datasets

---

# Numerical Integration

The nonlinear ODE system is solved using a custom implementation of the classical fourth-order Runge–Kutta (RK4) method.

### Features
- RK4 solver built from scratch
- Interpolation for continuous forcing signals
- Non-negativity enforcement
- Population renormalization
- Daily timestep simulation

---

# Datasets

The project uses real rumor datasets from:

- News platforms
- Twitter activity

### Preprocessing includes:
- 7-day moving average smoothing
- interpolation
- normalization
- temporal alignment

---

# Parameter Estimation

Model parameters were estimated using:
- Ordinary Least Squares (OLS)
- Nonlinear Least Squares optimization
- RK4-based trajectory fitting

## Final Parameters

### News Dataset
- β = 0.0983
- α = 0.26829
- κ = 0.26892

### Twitter Dataset
- β = 0.1966
- α = 0.0468
- κ = 0.00974

---

# Error Analysis

Model accuracy was evaluated using RMSE.

## Results
- RMSE (News): 781.80
- RMSE (Twitter): 1349.06

### Observations
- News data is smoother and more predictable
- Twitter contains bursty high-frequency volatility
- ODE models fit News data significantly better

---

# Source-Structured Extension

The project also introduces separate spreader classes:
- Twitter-origin spreaders
- News-origin spreaders

This allows:
- platform-specific contagion analysis
- cross-platform interaction modeling
- source-specific forcing dynamics

---

# Neural Network Modeling

An LSTM-based forecasting framework was implemented for:
- total activity prediction
- rumor prediction
- non-rumor prediction

## Architecture
- LSTM (32 units)
- Dropout regularization
- Dense layers
- Adam optimizer
- Sliding window sequence modeling

## Findings
- LSTMs perform very well on smoother News data
- Twitter volatility is harder to predict
- Neural networks capture nonlinear fluctuations better than deterministic ODEs

---

# Tech Stack

- Python
- NumPy
- SciPy
- Pandas
- Matplotlib
- TensorFlow / Keras

---

# Project Structure

```bash
rumor_spread_modelling/
│
├── datasets/
│   ├── news_dataset_fixed.csv
│   └── twitter_dataset_fixed.csv
│
├── notebooks/
│   ├── rk4.ipynb
│   ├── model_news_dataset_fixed.ipynb
│   └── model_twitter_dataset_fixed.ipynb
│
├── report/
│   └── modelling_report_final.pdf
│
└── README.md
```

---

# Key Insights

- News rumor propagation is primarily forcing-driven
- Twitter rumor propagation is interaction-driven
- Deterministic ODEs provide interpretability
- LSTMs improve short-term forecasting
- Hybrid ODE + ML frameworks are effective for complex rumor ecosystems

---

# References

1. Daley & Kendall — *Epidemics and Rumours*
2. Maki & Thompson — *Mathematical Models and Applications*
3. LSTM forecasting literature
4. COVID-19 rumor datasets
