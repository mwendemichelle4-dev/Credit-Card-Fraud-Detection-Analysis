# CREDIT CARD FRAUD DETECTION ANALYSIS
![Credit card security and fraud prevention illustration depicting biometric authentication and identity theft prevention Stock Illustration _ Adobe Stock](https://github.com/user-attachments/assets/4a9daf5e-a371-456b-9c99-4cdc24922e39)
# BACKGROUND
Credit card fraud is a persistent financial risk for banks and payment providers, leading to direct monetary losses, increased operational costs, and erosion of customer trust. Although fraudulent transactions represent a very small fraction of total transaction volume, their financial impact is significant and disproportionate.

Fraud detection systems must balance two competing risks: failing to detect fraudulent transactions (false negatives), which results in direct financial loss, and incorrectly blocking legitimate transactions (false positives), which causes customer frustration, lost revenue, and higher customer support costs. Many existing systems rely on static rules or legacy models that struggle to adapt to evolving fraud patterns, resulting in suboptimal outcomes.

From an actuarial and data science perspective, this problem can be framed as a risk classification and expected loss minimization task. Rather than maximizing accuracy alone, the objective is to build a predictive model that balances the cost of false positives and false negatives to minimize overall business impact.
This is the guiding question:

How can transaction data be used to accurately detect credit card fraud while minimizing financial loss and customer disruption?
# PROBLEM STATEMENT
Financial institutions face significant losses from credit card fraud while also incurring costs from incorrectly blocking legitimate transactions. Existing fraud detection approaches often struggle to balance these competing risks, resulting in either missed fraud or unnecessary customer disruption. This project aims to develop a data-driven classification model that identifies fraudulent transactions and minimizes overall expected loss by balancing false positives and false negatives.
# OBJECTIVES
General Objective: To develop a data-driven fraud detection model that accurately identifies fraudulent credit card transactions while minimizing overall financial loss and customer disruption.

# Specific Objectives:

To explore and understand transaction patterns associated with fraudulent and non-fraudulent behavior using exploratory data analysis (EDA).

To address class imbalance and assess its impact on fraud detection performance.

To build and compare classification models for identifying fraudulent transactions.

To evaluate model performance using appropriate metrics for imbalanced data, such as precision, recall, F1-score, and ROC-AUC.

To assess the trade-off between false positives and false negatives in order to select a model that minimizes expected loss.
# Data Understanding & Challenges
The credit card fraud dataset provides a snapshot of credit card transactions made by European cardholders over two days in September 2013.
# Key Characteristics:
* Number of transactions: 284,807 (after initial cleaning).
* Fraudulent transactions: 492 ($\approx 0.17\%$ of total), highlighting extreme class imbalance.
* Features: 31 numerical features (V1 to V28, Time, Amount). V1–V28 are PCA-transformed features to anonymize sensitive data.
# Dataset Challenges:
*Extreme Class Imbalance: Fraudulent transactions are very rare, making standard accuracy metrics unreliable.
*Anonymized Features: Feature interpretability is limited, requiring reliance on model-derived feature importance scores.
*Skewed Data: Features like Amount and Time require careful normalization or scaling.

Methodology & Technical Approach
The entire analysis is contained within the Notebook.

# Preprocessing & Imbalance Handling
Data Splitting: Stratified train-test split performed before any scaling or resampling to prevent data leakage.

Scaling: Time and Amount features were standardized (using StandardScaler).

Imbalance Techniques Compared:

* Class Weights (Logistic Regression)

* SMOTE (Random Forest, XGBoost, LightGBM)

* Random Undersampling (Random Forest)

# Model Comparison
 The following models were trained and benchmarked across different resampling techniques:
 * Logistic Regression
 * Random Forest Classifier
 * XGBoost Classifier
 * LightGBM Classifier (The typically best performer)
# Optimization Goal
* Primary Metric: The final model selection and tuning was optimized to maximize the Area Under the ROC Curve (ROC-AUC).
* Tuning Method: $\text{RandomizedSearchCV}$ was applied to the best model to find optimal hyperparameters (e.g., n_estimators, num_leaves, learning_rate).
