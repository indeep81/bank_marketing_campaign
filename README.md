# Machine Learning Classification: Bank Marketing Campaign Analysis

## Executive Summary

This project analyzes marketing campaign data from a Portuguese bank to predict whether a client will subscribe to a term deposit. By using machine learning classification techniques, we aim to help marketing teams improve their targeting strategies and optimize conversion rates through data-driven decision-making.

## Business Problem
Direct marketing campaigns are resource-intensive. A major Portuguese banking institution seeks to predict customer behavior to improve the effectiveness of their term deposit campaigns. The key challenge is to:

- Accurately identify clients who are likely to subscribe
- Allowing the bank to prioritize outreach and reduce costs.

## The Data

The dataset contains information on past marketing campaigns, including:
- **Customer demographics**: age, job, marital status, education
- **Economic indicators**: loan status, housing status
- **Campaign details**: number of contacts, previous outcomes
- **Communication attributes**: contact method, month, day of week
- **Target variable**: `y` (whether the client subscribed to a term deposit)

### Dataset Info:
- **Source**: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/bank+marketing)
- **Reference**: Moro et al., 2014 — Data mining for bank telemarketing using support vector machines.

## Initial Baseline Model Performance & Challenges

An initial baseline model was developed to predict term deposit subscriptions. While this model achieved a high overall accuracy of **89%**, this metric proved to be misleading due to a significant class imbalance in the dataset (7,310 instances of Class 0 - no subscription, versus 928 instances of Class 1 - subscription).

As a majority-class predictor, the baseline model:
-   Correctly classified all Class 0 instances (Recall: 1.00 for Class 0).
-   **Failed entirely to identify any Class 1 instances (subscribers)**, resulting in **0.00 precision, recall, and F1-score for Class 1**.
-   Misclassified all 928 positive (Class 1) cases as negative (Class 0).

Despite the seemingly high accuracy, this model was ineffective for the business objective, which critically relies on identifying potential subscribers (Class 1). This highlighted the need for models that can effectively handle class imbalance and prioritize the accurate identification of the minority class.

## Findings

Exploratory Data Analysis revealed several key insights influencing customer subscription behavior:

| Feature | Insight |
|--------|---------|
| Job | Students and retirees are more likely to subscribe. |
| Contact Method | Calls made via cellular had higher success rates. |
| Previous Outcome | A successful previous campaign strongly predicts subscription. |
| Duration | Longer call durations correlate positively with conversion — though not usable for prediction. |
| Poutcome | Prior success in campaigns significantly increases odds of subscription. |

## Model Comparison

| Model               | Train Time (s) | Train Accuracy | Test Accuracy |
|---------------------|----------------|----------------|---------------|
| Logistic Regression | 0.199          | 0.851          | 0.856         |
| KNN                 | 0.006          | 0.951          | 0.840         |
| Decision Tree       | 0.762          | 1.000          | 0.873         |
| SVM                 | **40.368**     | **0.950**      | **0.903**     |

SVM achieved the highest Test Accuracy among the evaluated models.


## Confusion Matrix (SVM)

Based on the Support Vector Machine (SVM) Classifier:

-   **True Negatives ([TN_SVM])**: Correctly predicted no subscription.
-   **True Positives ([TP_SVM])**: Correctly predicted subscription.
-   **False Positives ([FP_SVM])**: Predicted subscription when there was none.
-   **False Negatives ([FN_SVM])**: Missed potential subscribers.


## Improving the Model

Given the class imbalance (more "no" responses than "yes") and the limitations of the baseline model, we focused on improving performance for the minority class:

-   **Addressed class imbalance using SMOTE (Synthetic Minority Over-sampling Technique)**. SMOTE was applied to the training data to generate synthetic samples for the minority class, effectively balancing the dataset before model training.
    *   *For example, with SMOTE-balanced data, the logistic regression model showed improved recall (0.84) and F1-score (0.57) for the minority class (Class 1), highlighting the benefit of synthetic resampling for addressing severe class imbalance.*
-   Applied hyperparameter tuning techniques (e.g., `GridSearchCV`, `RandomizedSearchCV` if you used them for these models) to optimize model performance.
-   Evaluated various classification models including **Logistic Regression, K-Nearest Neighbors (KNN), Decision Tree, and Support Vector Machine (SVM)**.
-   Evaluated models using metrics appropriate for imbalanced datasets, such as **Precision, Recall, and F1 Score** for the minority class, in addition to overall accuracy.
-   Feature engineering (e.g., handling `pdays` to create a `was_contacted_before` indicator) and one-hot encoding improved prediction.


## 🚀 Next Steps & Recommendations

- 🎯 Focus campaigns on job groups with higher conversion rates (e.g., students, retirees)
- 🧪 Test model predictions in a live A/B marketing test
- ⏳ Exclude features like `duration` for real-world prediction use (only known after the call)
- 🔁 Regularly retrain model as market behavior shifts
- 🧠 Explore alternate resampling strategies or more complex models like Random Forest or XGBoost for further gains.

---

## 🗂️ Outline of Project

1.  **Data Exploration & Cleaning**
2.  **EDA (Exploratory Data Analysis)**
3.  **Feature Engineering**
4.  **Model Building & Evaluation**
5.  **Model Comparison & Insights**
6.  **Final Recommendations**

---

## 📬 Contact Information

**Author:** Indeep Kaur
📧 Email: [YourEmail@example.com]
🔗 GitHub: [github.com/indeep81](https://github.com/indeep81)

---

> 🔖 _This project is part of a Machine Learning portfolio to demonstrate data science techniques in real-world business scenarios._