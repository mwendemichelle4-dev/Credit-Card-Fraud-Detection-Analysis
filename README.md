# CREDIT CARD FRAUD DETECTION ANALYSIS
![Credit card security and fraud prevention illustration depicting biometric authentication and identity theft prevention Stock Illustration _ Adobe Stock](https://github.com/user-attachments/assets/4a9daf5e-a371-456b-9c99-4cdc24922e39)
# BUSINESS UNDERSTANDING
Fraud is a dynamic, adversarial problem. Traditional rule-based systems often fail to keep pace with evolving criminal tactics, resulting in two primary business pains:

* **Direct Loss:** Uncaptured fraud leads to immediate capital drain and merchant chargebacks.

* **Customer Insult:** Overly aggressive security filters block legitimate transactions, leading to "cart abandonment" and long-term brand damage.

This is the guiding question:

**How can transaction data be used to accurately detect credit card fraud while minimizing financial loss and customer disruption?**

# STAKEHOLDERS
The beneficiaries of this project are:

* Financial Institutions (Banks & Card issuers)
* Cardholders (Customers)
* Payment Networks (e.g., Visa, Mastercard)
* Fraud Operations & Risk Management Teams
* Customer Support & Call Centers
* Regulators & Compliance Bodies
* Merchants
* Data Scientists & Analysts
* Executive Management
At the center of these stakeholders are everyday cardholders and merchants, whose trust, financial security, and ability to transact smoothly depend on effective and balanced fraud detection systems.

# OBJECTIVES
# General Objective:
To develop a data-driven fraud detection model that accurately identifies fraudulent credit card transactions while minimizing overall financial loss and customer disruption.

# Specific Objectives:

* To explore and understand transaction patterns associated with fraudulent and non-fraudulent behavior using exploratory data analysis (EDA).

* To address class imbalance and assess its impact on fraud detection performance.

* To build and compare classification models for identifying fraudulent transactions.

* To evaluate model performance using appropriate metrics for imbalanced data, such as precision, recall, F1-score, and ROC-AUC.

* To assess the trade-off between false positives and false negatives in order to select a model that minimizes expected loss.
# DATA UNDERSTANDING AND CHALLENGES
**Data Source & Suitability**

The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/isaikumar/creditcardfraud), it represents 48 hours of European credit card transactions. It is uniquely suitable because it captures the Extremely Imbalanced Class Distribution inherent in financial crime, providing a realistic testing ground for anomaly detection.
# Key Characteristics:
* Number of transactions: 284,807 (after initial cleaning).
* Fraudulent transactions: 492 ($\approx 0.17\%$ of total), highlighting extreme class imbalance.
* Features: 31 numerical features (V1 to V28, Time, Amount). V1–V28 are PCA-transformed features to anonymize sensitive data.
# DATASET CHALLENGES
* **Extreme Class Imbalance:** Fraudulent transactions are very rare, making standard accuracy metrics unreliable.
* The **PCA transformation**, while excellent for privacy, masks the semantic meaning of the features. This prevents us from identifying if fraud is linked to specific locations or merchant categories, restricting our ability to build "human-readable" rules.
* **Skewed Data**: Features like Amount and Time require careful normalization or scaling.



# DATA PREPARATION AND PREPROCESSING
* **Data Splitting:** Stratified train-test split performed before any scaling or resampling to prevent data leakage.

* **Scaling:** Time and Amount features were standardized (using StandardScaler).
* **Synthetic Balancing (SMOTE):** To address the 578:1 class ratio, we implemented SMOTE.

The Justification: Simple oversampling leads to overfitting; simple undersampling throws away 99% of our data. SMOTE creates "interpolated" fraud cases, forcing the model to learn the boundaries of fraud rather than just memorizing existing cases.

* **Reproducibility:** All preparation steps were wrapped in functions with fixed random_state seeds to ensure consistent results across different environments

# ITERATIVE MODELING
 The following models were trained and benchmarked across different resampling techniques:
 * Logistic Regression with class weight
 * Random Forest Classifier (SMOTE) (The typically best performer)
 * XGBoost Classifier(SMOTE) 
 * LightGBM Classifier(SMOTE) 

The results were as follows: 

### MODEL COMPARISON - RANKED BY ROC-AUC

              Model     Technique   PR-AUC  ROC-AUC  Precision   Recall  F1-Score
      Random Forest         SMOTE 0.874731 0.973103   0.845361 0.836735  0.841026
            XGBoost         SMOTE 0.827005 0.975970   0.345528 0.867347  0.494186
           LightGBM         SMOTE 0.799299 0.977294   0.326772 0.846939  0.471591
     Logistic Regression Class Weights 0.715912 0.972169   0.060976 0.918367  0.114358


<img width="989" height="605" alt="image" src="https://github.com/user-attachments/assets/03f4ffb4-8c42-4a30-971a-01d9747a1fad" />

**Final Choice (Random Forest)**
**Justification:** Random Forest’s "Bagging" nature naturally reduces variance. It proved more resilient to the noise in the synthetic fraud data, maintaining a cleaner separation between classes.
# EVALUATION AND IMPLICATIONS
**Metric Selection: The F2-Score**
In a $100 transaction, missing a fraud case costs the bank $100. A false alarm costs the bank ~$5 in operational review. Therefore, **Recall is significantly more valuable than Precision**.
* The **F2-Score** was chosen as it mathematically weights Recall twice as heavily as Precision.

<img width="1489" height="490" alt="image" src="https://github.com/user-attachments/assets/21e7f538-f1d1-45c3-ae91-11f8fea154cd" />

**Final Model Performance**
**Model:** Random Forest + SMOTE
**Optimal Threshold:** $0.35$
**Test Performance:** 89.8% Recall and 76.5% Precision.

**Implications**

By deploying this model at the $0.35$ threshold, the bank can expect to capture 11% more fraud than a standard $0.50$ threshold. The operational team will find that ~8 out of 10 alerts they investigate are genuine fraud, representing a massive increase in labor efficiency.
# RECOMMENDATIONS
* **Deploy a Tiered Response System:** Use the 0.35 threshold to trigger real-time MFA for suspicious cases and a 0.75 threshold to auto-block high-confidence fraud.

* **Monitor Top Fraud Signals:** Track features V14, V10, and V4 for "data drift" to detect changes in criminal behavior as they happen.

* **Establish a Feedback Loop:** Automatically feed verified fraud outcomes back into the training pipeline to keep the model updated.

* **Schedule Monthly Retraining**: Update the model every 30 days using SMOTE on the latest data to ensure it remains resilient against evolving tactics.
# CONCLUSION
This project demonstrates that in highly imbalanced environments like fraud detection, Accuracy is a vanity metric. By shifting the focus to PR-AUC and optimizing the F2-Score, we created a model that is mathematically tuned to the bank's actual risk appetite. The final Random Forest model provides a robust defense that catches nearly 90% of fraudulent activity while ensuring that the vast majority of legitimate customers never experience a false decline.

# FOR MORE INFORMATION
contact me at mwendemichelle4@gmail.com
