# 🚗 Waze User Churn Prediction Project
### Google Advanced Data Analytics Professional Certificate | Project

<p align="left">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Machine_Learning-FF6F00?style=for-the-badge" alt="ML">
  <img src="https://img.shields.io/badge/XGBoost-orange?style=for-the-badge" alt="XGBoost">
</p>

---

## 📌 Project Background
Waze’s data team is working to optimize user retention. The goal of this project was to analyze user data and build a machine learning model to predict **user churn** (defined as users who uninstalled or stopped using the app during the month).

Identifying churn factors allows Waze to implement proactive retention strategies, such as targeted notifications or specialized incentives for **"at-risk"** users.

---

## 🛠️ Data Science Pipeline (PACE)

### 1. Plan & Analyze (EDA)
I performed a thorough investigation of **14,999 user profiles**.
* **Missing Data:** Identified 700 missing values in the `label` column. Analysis confirmed they were **Missing Completely at Random (MCAR)**, allowing for safe removal.
* **Device Distribution:** ~64.5% iPhone users vs. ~35.5% Android users.
* **Key Finding:** Churned users drove **~200km more** and **~2.5 hours more** per month than retained users, but used the app on **fewer days**. This suggests a "power user" or "commercial driver" profile that is churning.

### 2. Statistical Hypothesis Testing
I conducted a **Welch’s t-test** to determine if there was a statistically significant difference in the mean number of drives between iPhone and Android users.
* **Null Hypothesis ($H_0$):** No difference in mean drives between device types.
* **Result:** $p\text{-value} \approx 0.143$.
* **Conclusion:** **Failed to reject the null hypothesis.** Usage behavior is statistically consistent across different devices.

### 3. Feature Engineering
Created several high-signal features to boost model performance:
* **`km_per_driving_day`**: Identified as a major churn indicator.
* **`professional_driver`**: Binary indicator for high-volume drivers (60+ drives & 15+ days).
* **`percent_sessions_in_last_month`**: Captured recent engagement spikes.
* **`km_per_hour`**: Calculated average speed as a proxy for traffic/driving type.

### 4. Modeling & Evaluation
I tested three different modeling approaches to find the best predictor:

| Model | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: |
| Logistic Regression | 0.53 | 0.11 | 0.18 |
| Random Forest | 0.49 | 0.11 | 0.18 |
| **XGBoost (Champion)** | **0.41** | **0.17** | **0.23** |

> **Note on Champion Model:** XGBoost was selected as the champion. While recall is low (17%), it provided a **50% improvement** over the baseline Logistic Regression model. **Feature Engineering** proved vital, as engineered features were among the top predictors.

---

## 📈 Key Insights & Business Recommendations

* **The "Super Driver" Discrepancy:** Users who drive extremely long distances on fewer days (likely long-haul or commercial drivers) have a higher churn rate. 
    * *Recommendation:* Investigate if the app lacks features for larger vehicles or professional routing.
* **Engagement Decay:** The strongest predictor of churn was `activity_days`. A drop in the frequency of app openings is a more reliable churn signal than total distance driven.
* **Retention Strategy:** Marketing efforts should target users whose `activity_days` decrease by more than **20% week-over-week**, regardless of their total mileage.

---
*This project was completed as part of the Google Advanced Data Analytics Professional Certificate.*
