# 🌦️ Weather Analytics & Predictive Machine Learning

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.2%2B-orange.svg?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-yellow.svg?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

An end-to-end meteorological data analytics and machine learning system built on **96,453 hourly weather records** spanning a decade (2006–2016). This project covers **Exploratory Data Analysis (EDA)**, **Inferential Statistical Hypothesis Testing**, **Supervised & Unsupervised Machine Learning**, and **Interactive Power BI Business Intelligence Dashboards**.

---

## 📌 Table of Contents
- [Project Architecture](#-project-architecture)
- [Dataset Overview](#-dataset-overview)
- [Exploratory Data Analysis & Statistical Testing](#-exploratory-data-analysis--statistical-testing)
- [Machine Learning Models & Results](#-machine-learning-models--results)
  - [1. Linear Regression (Supervised Regression)](#1-linear-regression-supervised-regression)
  - [2. Logistic Regression (Supervised Classification)](#2-logistic-regression-supervised-classification)
  - [3. K-Means Clustering & PCA (Unsupervised Learning)](#3-k-means-clustering--pca-unsupervised-learning)
- [Model Performance Summary](#-model-performance-summary)
- [Power BI Dashboard](#-power-bi-dashboard)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)

---

## 🏗️ Project Architecture

```
Raw Weather History Dataset (96K+ Rows)
               │
               ▼
   Data Cleaning & Preprocessing
   ├── Handling Missing Values & Types
   ├── Feature Engineering (Seasons, Time Deltas)
   └── Outlier & Distribution Checks
               │
       ┌───────┴────────────────────────┐
       ▼                                ▼
Statistical Hypothesis Testing     Machine Learning Pipeline
├── Pearson Correlation (-0.66)     ├── Linear Regression (R² = 0.99)
├── Welch's Two-Sample t-test       ├── Logistic Regression (99.58% Acc)
└── One-Way Seasonal ANOVA          └── K-Means (K=4) + PCA Analysis
                                        │
                                        ▼
                        Interactive Power BI Dashboards
                        ├── Page 1: Overview & Seasonal Trends
                        ├── Page 2: Correlation Analysis
                        ├── Page 3: Predictive Analytics
                        └── Page 4: Unsupervised Clustering
```

---

## 📊 Dataset Overview

* **Source:** Historical Hourly Weather Data (`weatherHistory.csv`)
* **Observations:** 96,453 records across 10+ years
* **Key Features:**
  * `Temperature (C)` & `Apparent Temperature (C)` ("Feels Like")
  * `Humidity` (Relative humidity: 0.0 to 1.0)
  * `Wind Speed (km/h)` & `Wind Bearing (degrees)`
  * `Visibility (km)`
  * `Pressure (millibars)`
  * `Precip Type` (`rain`, `snow`, `none`)
  * `Summary` & `Daily Summary`

---

## 🔍 Exploratory Data Analysis & Statistical Testing

<p align="center">
  <img src="Project_Report_Figures/Figure%2019%20-%20Combined%20Weather%20Analysis%20Visualization.png" alt="Combined Weather Visualizations" width="850"/>
</p>

### Statistical Hypotheses & Tests:
1. **Temperature vs. Humidity Correlation:**
   * **Pearson Correlation:** $r = -0.6635$ ($p < 0.001$)
   * *Conclusion:* Strong statistically significant negative correlation — hotter air has a significantly higher capacity to hold vapor, resulting in lower relative humidity.
2. **Seasonal Humidity Disparity (Summer vs. Winter):**
   * **Welch's Two-Sample t-test:** $t = -74.74$ ($p < 0.001$)
   * *Conclusion:* Confirms statistically significant divergence in atmospheric humidity across seasons.
3. **Seasonal Wind Variations:**
   * **One-Way ANOVA:** $F = 157.64$ ($p = 2.11 \times 10^{-101}$)
   * *Conclusion:* Strong seasonal variance in wind patterns throughout the decade.

<p align="center">
  <img src="Project_Report_Figures/Figure%207%20-%20Correlation%20Heatmap.png" alt="Correlation Heatmap" width="600"/>
</p>

---

## 🤖 Machine Learning Models & Results

### 1. Linear Regression (Supervised Regression)
* **Goal:** Predict perceived **Apparent Temperature (°C)** given physical weather measurements.
* **Features:** Temperature, Humidity, Wind Speed, Wind Bearing, Visibility, Pressure (Standardized via `StandardScaler`).
* **Feature Weights (Coefficients):**
  * `Temperature (C)`: **+10.98** (Primary positive driver)
  * `Wind Speed (km/h)`: **-0.70** (Captures physical **Wind Chill**)
  * `Humidity`: **+0.24** (Captures discomfort index)
* **Metrics:**
  * **$R^2 = 0.98997$ (~99.0% variance explained)**
  * **$\text{RMSE} = 1.08^\circ\text{C}$**
  * **$\text{MAE} = 0.85^\circ\text{C}$**

<p align="center">
  <img src="Project_Report_Figures/Figure%2013%20-%20Linear%20Regression%20Actual%20vs%20Predicted%20Plot.png" alt="Actual vs Predicted" width="48%"/>
  <img src="Project_Report_Figures/Figure%2014%20-%20Linear%20Regression%20Residual%20Plot.png" alt="Residual Plot" width="48%"/>
</p>

---

### 2. Logistic Regression (Supervised Classification)
* **Goal:** Classify precipitation state as **Rain** ($1$) vs. **Snow** ($0$).
* **Features:** Temperature, Humidity, Wind Speed, Pressure.
* **Evaluation:**
  * **Accuracy:** **$99.58\%$**
  * **Precision:** **$99.72\%$**
  * **Recall:** **$99.80\%$**
  * **F1-Score:** **$99.76\%$**
* **Finding:** The physical freezing transition boundary around $0^\circ\text{C}$ provides clean, distinct separation for logistic classification.

<p align="center">
  <img src="Project_Report_Figures/Figure%2015%20-%20Logistic%20Regression%20Confusion%20Matrix.png" alt="Confusion Matrix" width="500"/>
</p>

---

### 3. K-Means Clustering & PCA (Unsupervised Learning)
* **Goal:** Discover atmospheric weather regimes without ground-truth labels.
* **Method:**
  * Tested clusters $K \in [2, 7]$ using the **Elbow Method**.
  * Optimal cluster count identified at **$K = 4$**.
* **Clustering Performance:**
  * **Silhouette Score:** **$0.2842$**
* **Principal Component Analysis (PCA):**
  * **PC1:** Explains **$46.90\%$** of variance.
  * **PC2:** Explains **$26.46\%$** of variance.
  * *Together, the top 2 components capture >73.3% of total variance.*

<p align="center">
  <img src="Project_Report_Figures/Figure%2016%20-%20K-Means%20Elbow%20Method.png" alt="Elbow Method" width="48%"/>
  <img src="Project_Report_Figures/Figure%2017%20-%20K-Means%20Cluster%20Visualization.png" alt="Cluster Visualization" width="48%"/>
</p>

---

## 📈 Model Performance Summary

| Metric | Model / Task | Score | Interpretation |
|---|---|---|---|
| **$R^2$ Score** | Linear Regression (Apparent Temp) | **0.98997** | 99% variance explained |
| **RMSE** | Linear Regression (Apparent Temp) | **1.0801 °C** | Average prediction error $\approx 1^\circ\text{C}$ |
| **Accuracy** | Logistic Regression (Rain vs Snow) | **99.58%** | Highly reliable state detection |
| **F1-Score** | Logistic Regression (Rain vs Snow) | **99.76%** | Excellent harmonic mean of Precision & Recall |
| **Silhouette Score** | K-Means ($K=4$) | **0.2842** | Distinct atmospheric cluster separation |

---

## 📊 Power BI Dashboard

The project includes an enterprise-ready Power BI project (`.pbip`) with TMDL semantic modeling:
* **Page 1: Overview & Seasonal Trends:** KPI cards, yearly temperature trajectories, and monthly humidity boxplots.
* **Page 2: Correlation Analysis:** Cross-variable interaction matrices and scatter plot distributions.
* **Page 3: Predictive Modeling:** Actual vs. Predicted apparent temperature and classification metrics.
* **Page 4: Weather Clustering:** Interactive cluster slicing by seasonal conditions and wind bearing.

---

## 📁 Project Structure

```
├── Weather_Analytics_and_ML.ipynb        # Main Jupyter Notebook (EDA, ML, Stats)
├── weatherHistory.csv                     # Historical Weather Dataset (96K+ rows)
├── requirements.txt                       # Python dependencies
├── .gitignore                             # Git ignore rules
├── README.md                              # Project documentation
├── FDS_Weather_Analytics.pbip             # Power BI Project File
├── FDS_Weather_Analytics.Report/          # Power BI Report visual definitions
├── FDS_Weather_Analytics.SemanticModel/   # Power BI TMDL data model
├── Project_Report_Figures/                # High-res exported charts and figures
└── FDS_Presentation_Final_Attractive.pptx # Project presentation slides
```

---

## 🚀 Getting Started

### Prerequisites
* Python 3.10+
* Jupyter Notebook or VS Code
* Power BI Desktop (optional, for viewing `.pbip` reports)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/MidnightMorgan2748/Weather_ML_Model.git
   cd Weather_ML_Model
   ```

2. Create and activate a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # macOS/Linux:
   source venv/bin/activate
   ```

3. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook Weather_Analytics_and_ML.ipynb
   ```

---

## 📜 License
This project is licensed under the [MIT License](LICENSE).
