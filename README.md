# ⚽ Player Performance Analysis 

This repository contains **Exploratory Data Analysis (EDA)** and a suite of **machine learning models** built on a player-performance dataset.  

---

## 🎯 Project Description
- **Profile data quality** and **understand feature distributions/relationships**.
- Train and compare a range of ML models for:
  - **Classification** (predicting player labels/outcomes)
  - **Regression** (predicting a continuous outcome)
  - **Clustering** (grouping similar players)
- Report **transparent metrics** and **model settings** for reproducibility.

---

## 🧾 Dataset 
A structured dataset of player records with performance and trait features.  
Examples of columns observed across notebooks include:

- **Performance:** `appearance`, `goals`, `assists`, `minutes played`, `goals conceded`
- **Attributes:** `height`, `award` (binary/flag), **position** features (e.g., `position_Attack`)
- (Plus additional engineered/encoded columns used per model)

> EDA covers data reliability, timeliness, consistency, uniqueness, completeness, and accuracy — along with univariate and multivariate analyses.

---

## 🧹 Data Preparation (high level)
- Column standardization & type fixes  
- Handling missing values (median for numeric where relevant)  
- Train/test split, scaling where required (e.g., SVM/KNN)  
- Feature selection subsets for specific experiments (e.g., **K-Means with 3 features** vs **all features**)

---

## 🤖 Models — Purpose, Parameters, and Results

Below, each model is documented **individually** with its **purpose**, **key parameters**, and **results pulled from the notebooks**.

---

### 1) Logistic Regression (`LogisticR.ipynb`)
**Purpose:** Classification (binary)

**Results (test)**  
- **Accuracy:** `0.843`  

---

### 2) Support Vector Machine — SVM (`SVM.ipynb`)
**Purpose:** Classification (binary)

**Typical parameters used**  
- `kernel='rbf'`, `C=5`, `gamma='0.1'`  

**Results**  
- **Accuracy:** `0.871`
- 
---

### 3) K-Nearest Neighbors — KNN (`knn.ipynb`)
**Purpose:** Classification

**Key parameters (defaults unless specified)**  
- `n_neighbors = 6` 

**Results**  
- **Accuracy:** `0.829` 


---

### 4) Decision Tree (`DT+RF.ipynb`)
**Purpose:** Classification

**Key parameters (common defaults)**  
- `'max_depth': 8, 'n_estimators': 35`


**Results**  
- **Accuracy:** `0.836`  
---

### 5) Random Forest (`DT+RF.ipynb`)
**Purpose:** Classification

**Key parameters**  
- Baseline: `n_estimators=100`, `criterion='gini'`  
- **Best model**: depth/trees tuned to reduce overfitting (as per notebook section *“Random Forest best model”*)

**Results**   
- **Test metrics (best model, macro):** `0.897`

---

### 6) Linear Regression (`LinearR.ipynb`)
**Purpose:** Regression (predict a continuous target)

**Key parameters**  
- `LinearRegression()` (ordinary least squares)

**Results**  
- **R² (train):** `0.726`  
- **R² (test):** `0.719`  
---

### 7) K-Means — Clustering (`k-means-3-features.ipynb`)
**Purpose:** Clustering (unsupervised) on a **3-feature** subset

**Key parameters**  
- `KMeans(n_clusters=5)`  

**Observations**  
- **Cluster counts (k=5):** 1630, 1359, 1274, 786, 686
- As illustrated below
![Player Clustering Results](images/kmeans3.png)

---

### 8) K-Means — Clustering (`k-means-all-features.ipynb`)
**Purpose:** Clustering on **all features**

**Key parameters**  
- `KMeans(n_clusters=5)`
- 
**Observations**  
- **Cluster counts (k=5):** 2183, 1240, 920, 788, 604
-  As illustrated below
![Player Clustering Results](images/kmeansall.png)

---

### 9) DBSCAN — Density-based Clustering (`DBSCAN.ipynb`)
**Purpose:** Clustering (density-based), automatically finds arbitrary shapes/outliers

**Key parameters**  
- `DBSCAN(eps=chosen_eps, min_samples=min_samples)` (tuned interactively)  

**Results**  
- **Silhouette score:** `-0.554` (indicates poor global cluster structure for tested params)  
- Produced many small clusters
- As illustrated below
![Player Clustering Results](images/kmeansall.png)

---

## 📊 Side-by-Side Comparison

### Classification (Test Set)
| Model               | Accuracy |
|---------------------|----------|
| Logistic Regression | 0.843  | 
| **SVM (RBF)**       | 0.871 |
| KNN                 | 0.829   | 
| Decision Tree       | 0.836   | 
| Random Forest (best)| **0.897** |
> **Note:** Random Forest (tuned) and SVM delivered the strongest classification performance.
---

### Regression
| Model            | R² (Train) | R² (Test) | Notes |
|------------------|------------|-----------|-------|
| Linear Regression| 0.726     | **0.719** | MSE also computed |

---

### Clustering
| Model                 | k / Params                     | Notable Outcome |
|-----------------------|--------------------------------|-----------------|
| K-Means (3 features)  | k = 5                          | Cluster sizes: 1630 / 1359 / 1274 / 786 / 686 |
| K-Means (all features)| k = 5                          | Cluster sizes: 2183 / 1240 / 920 / 788 / 604 |
| DBSCAN                | `eps`, `min_samples` (tuned)   | Silhouette = **−0.554** |

---

## 🚀 Deployment
[![Streamlit](https://img.shields.io/badge/Streamlit-App-red?logo=streamlit)](https://clustring-players.streamlit.app/)

