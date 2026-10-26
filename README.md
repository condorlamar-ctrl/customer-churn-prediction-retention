Customer Churn Analysis & Retention Strategy

**Analyzing 4,200 fitness subscriptions to identify retention priorities and recommend experiments.**

Monthly subscribers acquired through promotional offers had the highest observed churn among the three segments compared in the report: **63.3%**, versus **47.7%** for other monthly subscribers. This project uses customer segmentation, statistical comparisons, and logistic regression to turn that finding into practical retention recommendations.

**[Read the executive report](overview%20customer%20churn.pdf)** | **[Explore the cleaned dataset](subscriptions_cleaned.csv)**

## Business Problem

Customer churn reduces recurring revenue and increases the cost of replacing lost subscribers. For a subscription-based fitness service, the key business question is:

> Which subscriber groups should the business prioritize for retention efforts, and what should it test to improve retention?

The analysis focuses on how monthly promo-offer subscribers compare with other monthly subscribers and annual promo-offer subscribers.

## Results at a Glance

| Metric | Result |
| --- | ---: |
| Total subscriptions analyzed | 4,200 |
| Churned subscriptions | 1,768 |
| Overall observed churn rate | 42.1% |

### Churn by Subscriber Segment

| Segment | Subscriptions | Observed churn rate | Adjusted churn probability |
| --- | ---: | ---: | ---: |
| **Monthly promo-offer** | **589** | **63.3%** | **63.0%** |
| Other monthly | 2,072 | 47.7% | 47.5% |
| Annual promo-offer | 360 | 30.3% | 30.0% |

These are the three comparison groups featured in the report, rather than all 4,200 subscriptions. "Other monthly" includes monthly subscribers acquired through channels other than promo offers. Adjusted probabilities account for observed differences in demographics, device, plan tier, and signup cohort; the report includes 95% confidence intervals.

**Business takeaway:** Monthly promo-offer churn was **15.6 percentage points higher** than other monthly churn and **33.0 percentage points higher** than annual promo-offer churn. The same ordering remained after adjustment, making this group a priority for retention testing. These associations do not prove that promotions or monthly billing cause churn.

## Approach & Tools

**Analysis platform:** PlotStudio AI.

1. **Prepare the data:** Clean subscription records and perform data quality checks.
2. **Explore churn patterns:** Compare recorded churn across subscription plans and acquisition channels.
3. **Assess segment differences:** Use statistical comparisons, confidence intervals, and adjusted logistic regression analysis.
4. **Evaluate classification:** Assess a logistic regression classifier using stratified 5-fold cross-validation.
5. **Recommend business tests:** Translate the findings into targeted retention experiments.

The analysis excluded `churn_date` and `cancel_reason` from predictors to avoid using information that reveals a customer's churn outcome.

## Model Evaluation

| Reported metric | Score | What it measures |
| --- | ---: | --- |
| ROC-AUC | 0.751 | Ability to distinguish churned from non-churned subscriptions across thresholds |
| Precision | 0.637 | Share of subscriptions flagged as churned that actually churned |
| Recall | 0.502 | Share of churned subscriptions correctly identified |
| F1-score | 0.562 | Balance between precision and recall |

At the evaluated classification threshold, the model identified about half of recorded churn cases. These results describe classification of recorded churn in this dataset; **future-churn prediction has not been validated**.

## Recommended Retention Experiments

| Business priority | Proposed test | Outcome to measure |
| --- | --- | --- |
| Support monthly promo-offer subscribers early | Randomize targeted onboarding and early-renewal support within this segment | Renewal and churn rates versus a control group |
| Understand how promotions affect retention | Test promotion framing or eligibility while holding plan price constant where possible | Retention differences between test groups |
| Evaluate acquisition approaches | Run controlled comparisons of promo and non-promo acquisition approaches for comparable monthly plans | Renewal and churn outcomes by acquisition approach |

These are proposed experiments. The project does not report implemented interventions, retention improvements, or realized revenue savings.

## Limitations & Next Steps

- **Observation window:** No clear observation cutoff is defined, so subscribers may have different amounts of time in which to churn.
- **Association versus causation:** Adjusting for observed characteristics does not establish the causes of churn.
- **Missing engagement data:** Customer activity and engagement history are unavailable.
- **Future validation:** Define a prediction date and outcome window, then use time-based validation before deploying a future-churn model.
- **Reproducibility:** This repository contains the cleaned data, report, and chart exports. Analysis code and a runnable model pipeline are not included.

## Project Files

| File | Contents |
| --- | --- |
| [Executive report](overview%20customer%20churn.pdf) | Findings, confidence intervals, interpretation, and recommended experiments |
| [Cleaned dataset](subscriptions_cleaned.csv) | Subscription records used in the analysis |
| [Segment churn comparisons](Churn_rates_and_adjusted_probabilities_by_segment.pdf) | Observed rates and adjusted probabilities; PDF chart |
| [Observed versus adjusted segment churn](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf) | Side-by-side segment comparison; PDF chart |
| [Acquisition channel comparison](acquisition-channel-comparison.pdf) | Raw and adjusted churn probabilities by channel; PDF chart |
| [Classifier evaluation](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf) | Precision, recall, and F1 comparison with a majority-rule baseline; PDF chart |
