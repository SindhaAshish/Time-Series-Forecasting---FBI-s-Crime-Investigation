# Time-Series-Forecasting---FBI-s-Crime-Investigation

# 🚔 Vancouver Crime Time Series Forecasting

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-0.24+-orange.svg)
![Pandas](https://img.shields.io/badge/Pandas-1.2+-green.svg)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Time%20Series-red.svg)

## 📌 Project Overview
This project aims to transition law enforcement from a **reactive** response model to a **proactive**, data-driven deployment strategy. Using historical crime investigation data from Vancouver, this machine learning architecture forecasts future monthly crime incident volumes based on the specific year, cyclical seasonality, and crime category.

By accurately predicting "crime waves" and baseline incident counts, police departments can optimize operational budgeting, authorize targeted overtime, and deploy specialized task forces efficiently.

## 📊 Dataset
* **Source:** Historical Crime Investigation Data (Vancouver/FBI structure).
* **Format:** Tabular Time Series data (`Train.xlsx` for historical training, `Test.csv` for future forecasting).
* **Target Variable:** `Incident_Counts` (Continuous numerical integer).
* **Key Features:** `YEAR`, `MONTH`, `TYPE` (Crime Category), `NEIGHBOURHOOD`, `HOUR`.

## ⚙️ Methodology & Architecture

### 1. Data Wrangling & Preprocessing
* **Macro-Aggregation:** Granular, incident-by-incident data was aggregated into a macro-level Time Series dataset using `.groupby()` to match the forecasting objective.
* **Feature Engineering:** Implemented **Cyclical Encoding** using Sine and Cosine transformations on the `MONTH` variable to allow the models to mathematically understand continuous annual seasonality (connecting December back to January).
* **Encoding:** Applied `LabelEncoder` to the categorical `TYPE` feature for tree-based algorithm compatibility.

### 2. Exploratory Data Analysis (EDA) & Statistical Testing
* Conducted extensive EDA using `Seaborn` and `Matplotlib` (15+ visualizations).
* **Hypothesis Testing (Welch's T-Test):** Statistically validated key patterns:
  1. Significant variance in crime volumes between Summer and Winter months.
  2. Significant spikes in crime during weekend nightlife hours compared to weekdays.
  3. Significant differences between daytime and nighttime crime frequencies.

### 3. Machine Learning Modeling
To prevent Data Leakage (peeking into the future), data was split chronologically (`shuffle=False`). Three primary models were evaluated:
1. **Random Forest Regressor** (Bagging Ensemble)
2. **Gradient Boosting Regressor** (Boosting Ensemble)
3. **K-Nearest Neighbors Regressor** (Distance-based Baseline)

### 4. Hyperparameter Tuning & Cross-Validation
* Utilized `RandomizedSearchCV` and `GridSearchCV`.
* **Critical Step:** Applied `TimeSeriesSplit` for cross-validation to ensure all optimization folds strictly rolled forward chronologically, maintaining the integrity of the time series.

### 5. Model Explainability
* Integrated **SHAP (SHapley Additive exPlanations)** to interpret the "black box" ensemble models. SHAP summary plots confirmed that the encoded Crime Type dictates the baseline volume, the Year establishes the macro-trend, and the Cyclical Month features provde precise seasonal variance.

## 🏆 Results & Conclusion
The **Tuned Gradient Boosting Regressor** emerged as the best-performing model. 

* **Evaluation Metrics:** Evaluated using Root Mean Squared Error (**RMSE**), Mean Absolute Error (**MAE**), and **R-Squared**.
* **Business Impact:** The Gradient Boosting model successfully minimized RMSE (proving it is highly resistant to catastrophic forecasting misses like failing to predict a massive summer crime wave) while capturing the highest variance in the historical trends.
* The final model was exported via `joblib` (`best_crime_forecasting_model.pkl`) and is ready for live deployment.

## 🚀 How to Run the Project

1. Clone the repository:
   ```bash
   git clone [https://github.com/yourusername/crime-time-series-forecasting.git](https://github.com/yourusername/crime-time-series-forecasting.git)

  
