Customer Churn Analysis & Retention Strategy
1. Project Overview
This project analyzes 4,200 subscription records for a subscription-based fitness service to identify high-churn customer segments, evaluate associated factors, and recommend retention strategies.
2. Business Problem
High customer churn reduces recurring revenue and increases customer acquisition costs. This analysis identifies subscriber groups with elevated observed churn and recommends evidence-based experiments to improve retention.
3. Tools & Methods
PlotStudio AI for data analysis and reporting
Data cleaning and quality assurance
Exploratory data analysis and segment comparisons
Logistic regression
Stratified 5-fold cross-validation
Confidence intervals and adjusted statistical comparisons
4. Key Findings
Metric
Result
Total subscriptions
4,200
Churned subscriptions
1,768
Overall observed churn
42.1%
Monthly promo-offer churn
63.3%
Other monthly churn
47.7%
Annual promo-offer churn
30.3%

Key insight: Monthly promo-offer subscribers had the highest observed churn, and the difference remained after adjustment for observed customer characteristics.
5. Model Evaluation
Metric
Result
ROC-AUC
0.751
Precision
0.637
Recall
0.502
F1-score
0.562

These metrics evaluate classification of recorded churn in this dataset. They do not establish performance for predicting future churn in a real-world deployment.
6. Business Recommendations
Test targeted onboarding and early-renewal support for monthly promo-offer subscribers.
Test promotion framing or eligibility while holding plan price constant.
Compare acquisition approaches using controlled experiments and measure renewal or churn outcomes.
7. Limitations
The dataset does not provide a defined observation cutoff.
Findings describe observed associations, not causal effects.
Customer engagement history is unavailable.
Further time-based validation is required before deploying a future-churn prediction model.
8. Project Files
subscriptions_cleaned.csv — cleaned dataset
overview customer churn.pdf — executive report
Chart files — segment comparisons and model evaluation
9. Author
Data Science Portfolio Project



