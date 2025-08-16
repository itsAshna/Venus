---
layout: page
title: Loan Approval Prediction
description: A machine learning project that predicts loan approval decisions using applicant data.
img: assets/img/5.png
importance: 5
---

**GitHub Repository:** [View on GitHub](https://github.com/itsAshna/Loan-approval-prediction)

#### 📖 Introduction

This project focuses on predicting whether a loan application will be approved based on applicant demographic, financial, and credit history data. Loan approval prediction is a critical task for financial institutions, as it helps minimize default risk while ensuring eligible applicants are not overlooked. By leveraging machine learning, the process becomes faster, more consistent, and more data-driven.

---

#### 🎯 Problem

Financial institutions must evaluate loan applications efficiently while balancing risk and fairness. The main challenges include:

- **Imbalanced datasets** – far more denied than approved applications.
- **Mixed data types** – numerical, categorical, and binary variables.
- **Precision–Recall trade-off** – balancing false approvals and false denials.
- **Model interpretability** – avoiding bias in decision-making.

---

#### 🛠 Approach

##### 1. Data Preprocessing

- Removed unrealistic outliers (e.g., employment length > 100 years).
- Standardized numerical features for model stability.
- Encoded categorical features using label encoding.
- Applied **SMOTE** to address class imbalance.
- Used **PCA** for dimensionality reduction (retained 95% variance).

##### 2. Exploratory Data Analysis

- Examined distributions and correlations between features.
- Identified that **credit history length** and **loan percent income** are strong predictors.
- Visualized approval trends by demographic and loan characteristics.

##### 3. Modeling

Trained and evaluated multiple models:

- Logistic Regression (baseline)
- Random Forest (best balanced performance)
- XGBoost (best minority class recall)
- Neural Network (high recall with deep learning)

##### 4. Evaluation

- Metrics: Accuracy, Precision, Recall, F1-score, ROC-AUC, Confusion Matrix.
- Performed hyperparameter tuning for Random Forest and XGBoost.

---

#### 📊 Results

| Model               | Accuracy | Recall (Class 1) | ROC-AUC |
| ------------------- | -------- | ---------------- | ------- |
| Logistic Regression | 0.90     | 0.42             | 0.87    |
| Random Forest       | 0.89     | 0.76             | 0.90    |
| XGBoost             | 0.84     | 0.81             | 0.89    |
| Neural Network      | 0.73     | 0.76             | 0.91    |

- **Best Overall**: Random Forest – balanced accuracy and recall.
- **Best Minority Recall**: XGBoost & Neural Network.

---

#### 🚧 Challenges

- Severe **class imbalance** reducing minority class recall.
- Avoiding overfitting with a relatively small dataset.
- Ensuring interpretability for decision-making transparency.

---

#### ✅ What I Solved

- Built a complete preprocessing and modeling pipeline.
- Improved minority class recall using **SMOTE** and hyperparameter tuning.
- Used SHAP values for explainable AI, ensuring transparency in predictions.

---

#### 📌 Conclusion

The project successfully developed a loan approval prediction model that balances accuracy and fairness. Random Forest emerged as the most reliable choice for production deployment, while XGBoost and Neural Networks offered stronger minority class recall when high-risk detection is prioritized.

---

#### 🔮 Future Improvements

- Incorporating behavioral and transactional data for richer insights.
- Deploying the model as a **web app** for real-time decision support.
- Experimenting with ensemble stacking to improve accuracy.
- Implementing bias detection and fairness checks across demographic groups.

---
