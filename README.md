# semiconductor-ai-demand-forecasting
PySpark-based demand forecasting for semiconductor and AI markets using machine learning and GCP Dataproc.
# Semiconductor & AI Product Demand Forecasting

## Project Overview

This project explores **product demand forecasting in the semiconductor and AI market** using machine learning and big-data analytics.

The objective was to predict `Product_Demand` using historical and market-related factors including historical demand, price, marketing spend, seasonality, economic conditions, supply-chain factors, competitive landscape, product lifecycle stage, and customer preferences.

The project was designed around a practical business use case: improving demand visibility to support **revenue forecasting, FP&A, inventory management, production planning, and supply-chain decisions**.

The solution was first developed and tested on a **50,000-row synthetic dataset** and was then scaled to a **1-million-row dataset using PySpark and GCP Dataproc**.

---

## ML Pipeline & Workflow

The project followed an end-to-end machine learning workflow:

**Data Generation → EDA → Data Cleaning → Feature Selection → Feature Engineering → Train/Validation Split → Model Training → Model Evaluation → Big Data Scaling**

### 1. Exploratory Data Analysis

The 50K-row dataset was initially analyzed in Google Colab to understand the data before modeling.

EDA included:

- Reviewing dataset structure and descriptive statistics
- Examining numerical feature distributions and ranges
- Identifying missing values and outliers
- Analyzing product demand patterns
- Examining average demand across seasonal factors

### 2. Data Cleaning & Feature Selection

Missing values in variables such as `Price`, `Marketing_Spend`, and `Economic_Conditions` were handled using mean imputation.

Nine predictors were selected for modeling:

`Historical_Demand`, `Price`, `Marketing_Spend`, `Seasonal_Factors`, `Economic_Conditions`, `Supply_Chain_Factors`, `Competitive_Landscape`, `Product_Lifecycle_Stage`, and `Customer_Preferences`.

### 3. Feature Engineering

The selected predictors were combined into a single feature vector using PySpark's `VectorAssembler`, preparing the dataset for Spark ML models.

### 4. Training & Validation

The processed dataset was split into:

- **80% training data**
- **20% validation data**

The training set was used to fit the models, while the validation set was used to evaluate performance on unseen observations.

### 5. Model Training & Evaluation

Two regression models were trained using Spark MLlib:

- **Linear Regression** — used as the baseline model
- **Random Forest Regressor** — used to capture nonlinear relationships and feature interactions

The models were evaluated using **RMSE (Root Mean Squared Error)** and **MAE (Mean Absolute Error)**, where lower values represent lower prediction error.

---

## Approach

The project followed a **develop-small, scale-large** approach.

The machine learning workflow was first developed and debugged using the 50K-row dataset in **Google Colab**. This made it easier to perform EDA, clean the data, engineer features, train models, and validate the complete pipeline.

Once the pipeline was working successfully, the same workflow was moved to **Google Cloud Dataproc**.

The full **1-million-row synthetic dataset** was stored in **Google Cloud Storage** and processed using PySpark on the Dataproc Spark cluster.

This allowed the project to demonstrate not only model development, but also how the same ML workflow can be transferred from a smaller development environment to a distributed big-data environment.

---

## Results

### Small Dataset — 50K Rows

| Model | RMSE | MAE |
|---|---:|---:|
| **Linear Regression** | **5,016.74** | **3,985.24** |
| Random Forest Regressor | 6,133.43 | 4,853.22 |

### Big Dataset — 1M Rows

| Model | RMSE | MAE |
|---|---:|---:|
| **Linear Regression** | **8,324.71** | **4,030.86** |
| Random Forest Regressor | 9,085.62 | 4,941.12 |

Linear Regression produced lower RMSE and MAE than Random Forest on both dataset sizes.

An important takeaway from the modeling process was that **greater model complexity did not automatically lead to better predictive performance**. For this synthetic dataset, the simpler Linear Regression model captured the underlying relationships more effectively than the tested Random Forest configuration.

---

## Tools & Technologies

- **Python & Pandas** — exploratory data analysis
- **PySpark** — scalable data processing and ML pipeline development
- **Spark MLlib** — feature engineering, model training, and evaluation
- **Google Colab** — small-data development and testing
- **Google Cloud Storage** — cloud dataset storage
- **GCP Dataproc** — distributed processing of the 1M-row dataset
- **Jupyter Notebook** — notebook-based development

---

## Repository Notes

The **50K-row synthetic dataset** and small-data notebooks are included in this repository.

The full **1-million-row dataset could not be uploaded to GitHub because of its large file size** and was originally stored in Google Cloud Storage.

The original **GCP Dataproc cluster is no longer active**, so the repository preserves the code, methodology, and results from the completed project rather than a live cloud environment.

> **Note:** All data used in this project is synthetic and was created for educational and analytical purposes.
