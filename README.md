Customer Churn Analysis & Retention Strategy
Project Overview
This project analyzes 4,200 subscription records for a subscription-based fitness service to identify customer segments with elevated observed churn, evaluate associated factors, and recommend retention experiments.
Business Problem
High customer churn reduces recurring revenue and increases customer acquisition costs. The goal is to identify which subscriber groups have the highest recorded churn and provide evidence-based recommendations for further testing.
Tools & Methods
Python-based data analysis through PlotStudio
Data cleaning and quality checks
Exploratory data analysis and segment comparisons
Logistic regression and stratified 5-fold cross-validation
Confidence intervals and adjusted comparisons
Business recommendations and retention experiment design
Key Findings
Overall observed churn: 42.1% (1,768 of 4,200 subscriptions)
Monthly promo-offer subscribers: 63.3% observed churn
Other monthly subscribers: 47.7% observed churn
Annual promo-offer subscribers: 30.3% observed churn
The monthly promo-offer segment remained the highest-churn group after adjustment for observed characteristics.
Model Evaluation
ROC-AUC: 0.751
Precision: 0.637
Recall: 0.502
F1-score: 0.562
These metrics evaluate classification of recorded churn in this dataset. They do not establish performance for predicting future churn in a real deployment.
Business Recommendations
Test targeted onboarding and early-renewal support for monthly promo-offer subscribers.
Experiment with promotion framing or eligibility while holding plan price constant.
Compare acquisition approaches using a controlled test and measure renewal or churn outcomes.
Limitations
The dataset does not provide a defined observation cutoff or customer engagement history. Findings describe observed associations, not causal effects. Further time-based validation is required before deploying a future-churn prediction model.
Files
subscriptions_cleaned.csv — cleaned dataset
overview customer churn.pdf — executive report
Chart files — segment comparisons and model evaluation
Author
Data Science Portfolio Project

