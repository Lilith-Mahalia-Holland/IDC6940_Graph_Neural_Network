# Predictive Modeling of Weather Station Data

**Linear Regression vs. Graph Neural Network**

**Authors:** Colby Fenters & Lilith Holland

**Advisor:** Dr. Cohen

**Published:** August 4, 2025

**Project Website:** **(https://lilith-mahalia-holland.github.io/IDC6940_Graph_Neural_Network/)**

---

## Overview

This project investigates whether a **Graph Neural Network (GNN)** can outperform a **univariate time-series regression model** for short-term weather forecasting. Using real-world weather station data from southwestern Kansas, we compare a spatiotemporal GNN against a traditional regression baseline for next-step temperature prediction.

Despite the expressive power of GNNs, our results show that **a well-engineered linear model outperformed the GNN** on this small, spatially dense weather network, highlighting the importance of model selection, data scale, and feature engineering.

---

## Goals

* Build a **spatiotemporal GNN** capable of leveraging spatial relationships between weather stations
* Establish a **linear regression baseline** using identical temporal context
* Compare forecasting performance using real-world, noisy weather data
* Evaluate when graph-based deep learning adds value over simpler models

---

## Data

* **Source:** Iowa Environmental Mesonet (ASOS weather stations)
* **Region:** Southwestern Kansas
* **Time Range:** 2018–2020
* **Stations:** 7
* **Resolution:** 6-hour intervals
* **Final Features:**

  * Temperature (`tmpf`)
  * Relative Humidity (`relh`)
  * Wind Speed (`sknt`)
  * Wind Direction (sine & cosine encoding)

Extensive preprocessing was performed, including:

* Temporal alignment and downsampling
* Feature pruning and correlation analysis to prevent leakage
* Spatial + temporal imputation of missing values
* Robust feature scaling

---

## Models

### Graph Neural Network (GNN)

* **Architecture:** Diffusion Convolutional Recurrent Neural Network (DCRNN-inspired)
* **Framework:** PyTorch + torch-geometric-temporal
* **Graph:** Dense adjacency matrix weighted by inverse geodesic distance
* **Input:** Previous 28 time steps (7 days)
* **Target:** Next-step temperature prediction per station

**Test MSE:** `0.0562`

---

### Linear Regression Baseline

* **Approach:** Flattened multivariate time-series regression
* **Input:** Same 28 time-step history, aggregated across stations

**Test MSE:** `0.0147`

---

## Key Findings

* **Linear regression outperformed the GNN** across all stations
* **Spatial information provided limited benefit** at this small geographic scale
* **Temporal context was the dominant predictive signal**
* GNNs are **highly sensitive to graph size, structure, and tuning**
* Advanced models do not guarantee better performance without sufficient scale

---

## Repository Structure

* `slides.html`, `slides.qmd` – Final presentation
* `index.html`, `index.qmd` – Paper and GitHub Pages source
* `Final Presentation.html/qmd` – Final project presentation
* `best_model.pt` – Trained GNN model
* `kansas.asos_reduced_2018_2020.csv` – Cleaned dataset
* `references.bib` – Academic references
* `STA6257_Project.Rproj` – R project (used for writing & visualization)

> **Note:** Modeling and training were performed in Python; R was used for markdown, visualization, and paper composition.

---

## Takeaways

This project demonstrates that:

* **Strong baselines matter**
* **Data scale and structure** dictate whether deep learning is appropriate
* Graph-based models may excel in **larger, more spatially complex systems**
* Careful preprocessing and feature engineering can outweigh architectural complexity

---

## Future Work

* Larger geographic coverage
* Encoder–decoder GNN architectures
* More advanced graph variants
* Alternative imputation strategies
* Multivariate forecasting targets

---

**Slides:** **(https://lilith-mahalia-holland.github.io/IDC6940_Graph_Neural_Network/Final%20Presentation.html#/title-slide)**

**Website:** **(https://lilith-mahalia-holland.github.io/IDC6940_Graph_Neural_Network/)**
