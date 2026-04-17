Gini: 0.25056827550934905 at first test Evaluation.

# 🚀 Credit Risk Prediction using Machine Learning

## 📌 Overview

This project builds an end-to-end Credit Risk Prediction system using real-world banking data to identify high-risk (default) customers.

---

## 🎯 Highlights

* Built full ML pipeline from raw data to model evaluation
* Engineered financial behavioral features (utilization, DPD, enquiries)
* Parsed complex payment history strings (`STD`, `XXX`, numeric patterns)
* Implemented XGBoost classifier
* Evaluated using **Gini Score and Decile Analysis (industry standard)**

---

## 📊 Results

* **Gini Score:** ~0.20
* **Model Insight:** Limited but meaningful predictive power
* **Decile Analysis:** Shows need for advanced feature engineering

---

## 🧠 Challenges Solved

* Data type inconsistencies (string → numeric)
* Handling messy payment history data
* Fixing XGBoost errors (NaN, inf, dtype issues)
* Removing noisy features

---

## ⚙️ Tech Stack

* Python
* Pandas, NumPy
* XGBoost
* Matplotlib

---

## 📂 Project Structure

```
credit-risk-model/
│
├── notebooks/
│   └── credit_risk_model.ipynb
├── README.md
├── requirements.txt
```

---

## ⚠️ Note

Database connection is not public. Model can be run using exported datasets (CSV).

---

## 🚀 Future Improvements

* Time-based behavioral features
* Feature selection & tuning
* Model deployment (Streamlit)

---

## 👨‍💻 Author

Aditya Motghare


-----------------------------------------------------------------------------------------------------------------------------------------------
## ⚠️ Challenges Faced & Solutions

### 1. Data Type Issues (String vs Numeric)

* Many numerical columns such as `creditlimit` and `cur_balance_amt` were stored as strings.
* This caused failures during mathematical operations and model training.

**Solution:**

* Converted all relevant columns using `pd.to_numeric()`
* Ensured all model input features were numeric

---

### 2. Complex Payment History Format

* Payment history columns (`paymenthistory1`, `paymenthistory2`) contained mixed values like:

  * `STD`, `XXX`, and numeric sequences
* Direct parsing caused errors and incorrect feature extraction.

**Solution:**

* Used regex (`re.findall`) to extract only numeric values
* Engineered meaningful features like:

  * `dpd_count` (number of delayed payments)
  * `max_dpd` (maximum delay)

---

### 3. Model Training Failures (XGBoost Errors)

* Encountered multiple errors such as:

  * Invalid data types (`object`)
  * Presence of `inf` (infinity) values
  * Extremely large values causing crashes

**Solution:**

* Converted all features to numeric format
* Replaced `inf` and `-inf` values
* Applied clipping to limit extreme values
* Ensured clean and stable input data before training

---

### 4. Feature Noise & Low Model Performance

* Initial model performance (Gini ~0.29) degraded after including noisy features.
* Hidden encoded features (`feature_1` to `feature_79`) did not provide meaningful signal.

**Solution:**

* Removed noisy/uninterpretable features
* Focused on domain-driven features:

  * Credit utilization
  * Past due behavior
  * Enquiry patterns
  * Payment history-based features

---

### 5. Weak Risk Segmentation (Decile Analysis)

* Decile analysis showed poor separation between high-risk and low-risk customers.
* Model struggled to rank customers effectively.

**Solution:**

* Identified limitation of current feature set
* Concluded need for advanced features:

  * Time-based payment behavior
  * Trend analysis
  * Recent activity indicators

---

### 6. Handling Real-World Data Complexity

* Data contained inconsistencies, missing patterns, and non-standard formats.
* Required multiple iterations of debugging and validation.

**Outcome:**

* Built a robust data preprocessing pipeline capable of handling real-world financial datasets

---

Built by Aditya Motghare
