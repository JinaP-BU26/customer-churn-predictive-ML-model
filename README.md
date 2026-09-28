Customer Churn Prediction
Predicting which telecom customers are likely to leave, and identifying why, so retention teams can intervene before revenue is lost.

 Business Problem
About 1 in 4 customers (26.6%) in this dataset churned. Keeping a customer costs far less than acquiring a new one, so the goal was to build models that flag at-risk customers and reveal the behaviors driving churn.

📊 Dataset
5,986 telecom customers with 21 attributes (5,976 after cleaning)
Demographics, account details (tenure, contract, payment method, charges) and services (internet type, online security, tech support, streaming)
Target: Churn (Yes/No), imbalanced at 73.4% stayed vs 26.6% churned
Source: Slightly modified sample of the IBM Telco Customer Churn dataset, publicly available on Kaggle.

** Approach for this project:
Data cleaning: converted TotalCharges from text to numeric and removed rows with missing values
Exploratory analysis: churn rates by contract, internet service, payment method, and tenure
Feature engineering: one-hot encoded 15 categorical variables into 45 model features
Random Forest: built a baseline, then tuned it with GridSearchCV (5-fold CV across 192 combinations)
Feature selection: used Random Forest importances to choose inputs for a second model
Multicollinearity check: removed highly correlated and duplicate inputs (e.g. tenure ↔ TotalCharges, r = 0.83)
Logistic Regression: built a standardized, interpretable model to explain the direction of each churn driver
Evaluation: 60/40 train-test split; accuracy, precision, recall, specificity, balanced accuracy, and a train-vs-test overfitting check

✅ Results
Model	Accuracy	Precision (Churn)	Recall (Churn)	Specificity	Balanced Acc.
Random Forest (tuned)	80%	0.67	0.46	92%	69%
Logistic Regression	80%	0.65	0.51	90%	70%
Train vs. test accuracy differed by under 2 points for both models, so neither is overfitting
Logistic Regression caught more actual churners (higher recall) while staying easy to explain

** Key Insights
Churn Driver	Effect	Business Interpretation
Month-to-month contract	⬆️ Higher churn	No commitment makes switching easy
One- and two-year contracts	⬇️ Lower churn	Long-term commitment builds loyalty
No Online Security / Tech Support	⬆️ Higher churn	Customers without support feel less valued
Fiber optic internet	⬆️ Higher churn	The premium price may not meet expectations
Electronic check payment	⬆️ Higher churn	Manual payers are less "locked in" than auto-pay users
Longer tenure	⬇️ Lower churn	Established customers are more satisfied

** Business Recommendations
Convert month-to-month customers to annual plans with incentives (e.g. 2 months free)
Bundle Tech Support and Online Security into plans for at-risk segments
Promote auto-pay enrollment for electronic check users
Invest in onboarding, since churn risk peaks in the first months of tenure
Rank customers by churn probability and prioritize proactive outreach to the highest-risk ones

** Limitations & Next Steps
Churn recall of ~50% means about half of churners are still missed. Next: class weighting, SMOTE, and decision-threshold tuning
Try gradient boosting (XGBoost / LightGBM) and evaluate with ROC-AUC
Add SHAP values for customer-level explanations
Deploy as a Streamlit app so business users can score customers themselves

Tech Stack : Python · pandas · NumPy · scikit-learn · Matplotlib · Seaborn · Jupyter Notebook

**Project Done by**  
Jinal Patel · MS Applied Business Analytics, Boston University 
*Completed as part of graduate coursework in Marketing Analytics*
