Customer Churn Analysis & Retention Strategy
Project Overview
This project analyzes 4,200 subscription records for a subscription-based fitness service to identify high-churn customer segments and recommend retention strategies.
Business Problem
High customer churn reduces recurring revenue and increases customer acquisition costs. This analysis identifies subscriber groups with elevated observed churn.
Tools and Methods
PlotStudio AI
Data cleaning and quality checks
Exploratory data analysis
Logistic regression
Stratified 5-fold cross-validation
Statistical comparisons and confidence intervals
Key Findings
Total subscriptions: 4,200
Churned subscriptions: 1,768
Overall observed churn: 42.1%
Monthly promo-offer churn: 63.3%
Other monthly churn: 47.7%
Annual promo-offer churn: 30.3%
Key insight: Monthly promo-offer subscribers had the highest observed churn, even after adjusting for observed customer characteristics.
Model Evaluation
ROC-AUC: 0.751
Precision: 0.637
Recall: 0.502
F1-score: 0.562
These metrics classify recorded churn in this dataset. They do not establish performance for predicting future churn.
Business Recommendations
Test targeted onboarding and early-renewal support for monthly promo-offer subscribers.
Test promotion framing or eligibility while holding plan price constant.
Compare acquisition approaches using controlled experiments and measure renewal or churn outcomes.
Limitations
No defined observation cutoff.
Findings describe associations, not proven causes.
Customer engagement history is unavailable.
Further time-based validation is needed before deploying a future-churn model.
Project Files
subscriptions_cleaned.csv — cleaned dataset
overview customer churn.pdf — executive report
Chart ZIP files — segment comparisons and model evaluation
Author
Data Science Portfolio Project

