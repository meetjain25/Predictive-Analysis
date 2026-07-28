# Predictive Analytics Capstone Project

This project focuses on optimizing store formats for existing retail locations, classifying newly planned stores into appropriate store formats based on demographic features, and forecasting future produce sales using time-series modeling.

---

## 📌 Project Summary

* **Task 1: Store Segmentation (Clustering)** – Identified optimal store formats for existing stores using K-Means clustering.
* **Task 2: Classification Modeling** – Trained classification algorithms on demographic data to assign 10 new stores into store segments.
* **Task 3: Time Series Forecasting** – Evaluated ETS and ARIMA models to predict future produce sales for both existing and new store locations.

---

## 🏬 Task 1: Determine Store Formats for Existing Stores

### 1. Optimal Number of Clusters
Using the **K-Centroid Diagnostic Tool** and **K-Means Clustering**, the analysis determined that **3 store formats** is optimal.
* **Evaluation Metrics:** Both the **Adjusted Rand Indices** and **Calinski-Harabasz Indices** peaked at 3 clusters.

### 2. Store Distribution
* **Cluster 1:** 23 stores
* **Cluster 2:** 29 stores
* **Cluster 3:** 33 stores

### 3. Cluster Characteristics
* **Cluster 1:** Highest median total sales and largest sales variance; higher proportion of **General Merchandise** sales.
* **Cluster 2:** Higher proportion of **Produce** sales.
* **Cluster 3:** Most consistent and compact sales distributions across locations.

### 🔗 Visualizations
* [Task 1 Store Location & Sales Dashboard](https://public.tableau.com/profile/aljoscha.grunwald#!/vizhome/Task1_4_2/Task4_1)

---

## 🎯 Task 2: Formats for New Stores

### 1. Predictive Model Selection
To assign new store locations to a store format, a 20% validation sample with a **Random Seed = 3** was evaluated across three models:
* **Decision Tree**
* **Random Forest**
* **Boosted Model**

**Selected Model:** **Boosted Model**
* **Overall Accuracy:** 82.35% (0.8235)
* **F1 Score:** 0.8889 (outperformed Random Forest's 0.8426 and Decision Tree's 0.7685)

### 2. Top Demographic Indicators
The three most influential variables for determining store segment are:
1. `Ave0to9` (Average population aged 0 to 9)
2. `HVal750KPlus` (Home values $750K+)
3. `EdHSGrad` (High school graduation rate)

### 3. New Store Segment Predictions

| Store ID | Assigned Segment |
| :--- | :--- |
| **S0086** | Cluster 3 |
| **S0087** | Cluster 2 |
| **S0088** | Cluster 1 |
| **S0089** | Cluster 2 |
| **S0090** | Cluster 2 |
| **S0091** | Cluster 1 |
| **S0092** | Cluster 2 |
| **S0093** | Cluster 1 |
| **S0094** | Cluster 2 |
| **S0095** | Cluster 2 |

**New Store Distribution Summary:** 3 stores in Cluster 1, 6 stores in Cluster 2, and 1 store in Cluster 3.

---

## 📈 Task 3: Predicting Produce Sales

### 1. Model Selection & Comparison
Time-series forecasting models were evaluated on a 6-month holdout sample to forecast future produce sales:
* **ETS Model:** `ETS(M,N,M)` — Multiplicative Error, No Trend, Multiplicative Seasonality (No dampening).
* **ARIMA Model:** `ARIMA(0,1,2)(0,1,0)`

| Model Metric | ETS(M,N,M) | ARIMA(0,1,2)(0,1,0) | Selected |
| :--- | :--- | :--- | :--- |
| **RMSE** | **1,020,597** | 1,429,296 | ✅ **ETS** |
| **MASE** | **0.45** | 0.53 | ✅ **ETS** |
| **AIC** | 1,283 | 859 | — |

**Decision:** The **ETS(M,N,M)** model was selected due to significantly lower error rates (RMSE and MASE).

### 2. Sales Aggregation Strategy
* **Existing Store Forecasts:** Directly calculated using the ETS model.
* **New Store Forecasts:** Calculated by taking the average sales per store for each cluster using `ETS(M,N,M)` and weighting them according to the new store segment distribution (3× Cluster 1 + 6× Cluster 2 + 1× Cluster 3).

### 🔗 Visualizations
* [Task 3 Produce Sales Forecast Dashboard](https://public.tableau.com/profile/aljoscha.grunwald#!/vizhome/Task3_283/Task3)

---

## 🛠️ Software & Tools Used

* **Alteryx Designer:** Data cleansing, K-Means clustering, machine learning classification workflows, and time-series forecasting modules.
* **Tableau Public:** Geospatial and metric visualizations.
