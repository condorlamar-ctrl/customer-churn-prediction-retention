Customer Churn Analysis & Retention Strategy

**Analyzing 4,200 fitness subscriptions to identify retention priorities and recommend experiments.**

Monthly subscribers acquired through promotional offers had the highest observed churn among the three segments compared in the report: **63.3%**, versus **47.7%** for other monthly subscribers. This project uses customer segmentation, statistical comparisons, and logistic regression to turn that finding into practical retention recommendations.

**[Read the executive report](overview%20customer%20churn.pdf)** | **[Explore the cleaned dataset](subscriptions_cleaned.csv)** | **[View the segment comparison](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf)** | **[View classifier results](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf)** | **[View the visualizations](#visualizations)**

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

## Visualizations

### 1. Observed Versus Adjusted Churn by Segment

[View the full-size segment visualization (PDF)](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf)

![Observed churn rates and adjusted churn probabilities across the three featured subscriber segments](Observed_vs_Adjusted_Churn_Rate_by_Segment.png)

**Interpretation:** Monthly promo-offer subscribers have the highest observed churn (**63.3%**) among the featured groups, followed by other monthly subscribers (**47.7%**) and annual promo-offer subscribers (**30.3%**). The same ordering remains after adjustment.

### 2. Segment Churn Estimates and Confidence Intervals

[View the full-size confidence interval comparison (PDF)](Churn_rates_and_adjusted_probabilities_by_segment.pdf)

![Observed and adjusted churn estimates with confidence intervals for monthly promo-offer, other monthly, and annual promo-offer subscribers](Churn_rates_and_adjusted_probabilities_by_segment.png)

**Interpretation:** Reported adjusted churn probabilities are **63.0%**, **47.5%**, and **30.0%** for the three respective groups. The intervals show uncertainty around each estimate. This chart presents an alternative view of the same segment comparison.

### 3. Churn Probability by Acquisition Channel

[View the full-size acquisition channel visualization (PDF)](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.pdf)

![Original acquisition channel comparison, with the orange Raw series and a second blue series](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.png)

**Interpretation:** In the cleaned dataset, promo-offer subscribers across both plan types have **50.8%** observed churn, compared with **33.8%** for referral subscribers. These channel-wide groups differ from the monthly-only segment comparison.

The original chart labels the orange series Raw but does not identify the blue series in its legend. Adjusted channel values are therefore not interpreted from this export.

### 4. Classifier Evaluation Versus a Majority-Rule Baseline

[View the full-size classifier evaluation (PDF)](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf)

![Logistic classifier precision, recall, and F1 compared with an always-majority-class rule](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.png)

**Interpretation:** The classifier has reported precision of **0.637**, recall of **0.502**, and F1 of approximately **0.56**. It identifies about half of recorded churn cases. The majority-rule baseline makes no positive churn predictions, and the chart displays zero churn-class precision, recall, and F1.

The previews are **2,400 × 1,480-pixel** PNGs rendered from the four supplied PDFs. Keep the PNGs and PDFs beside this README so both previews and full-size links work on GitHub.

## Approach & Tools

**Analysis platform:** PlotStudio AI.

1. **Prepare the data:** Clean subscription records and perform data quality checks.
2. **Explore churn patterns:** Compare recorded churn across subscription plans and acquisition channels.
3. **Assess segment differences:** Use statistical comparisons, confidence intervals, and adjusted logistic regression analysis.
4. **Evaluate classification:** Assess a logistic regression classifier using stratified 5-fold cross-validation.
5. **Recommend business tests:** Translate the findings into targeted retention experiments.

The analysis excluded `churn_date` and `cancel_reason` from predictors to avoid using information that reveals a customer's churn outcome.

The reported classification results use stratified 5-fold cross-validation. The supplied files contain the report, cleaned data, and chart exports; a runnable model pipeline was not supplied, so the adjusted estimates and classification results were not independently refitted.

## Model Evaluation

| Reported metric | Score | What it measures |
| --- | ---: | --- |
| ROC-AUC | 0.751 | Ability to distinguish churned from non-churned subscriptions across thresholds |
| Precision | 0.637 | Share of subscriptions flagged as churned that actually churned |
| Recall | 0.502 | Share of churned subscriptions correctly identified |
| F1-score | 0.562 | Balance between precision and recall |

Scores above are reported in the project summary. The original classifier chart displays F1 as **0.561**, while the summary reports **0.562**; both are approximately **0.56**.

At the evaluated classification threshold, the model identified about half of recorded churn cases. These results describe classification of recorded churn in this dataset; **future-churn prediction has not been validated**.

## Data Validation

| Validation check | Result | What it establishes |
| --- | ---: | --- |
| Subscription records | 4,200 | Dataset size matches the executive report |
| Unique customer identifiers | 4,200 | No duplicate customer IDs |
| Recorded churn | 1,768 yes; 2,432 no | Overall observed churn is 42.1% |
| Missing core identifiers, predictors, and churn flag | 0 | All nine checked fields are populated |
| Featured segment sizes | 589; 2,072; 360 | Counts agree with the report's comparison groups |
| Featured observed churn rates | 63.3%; 47.7%; 30.3% | Rates calculated from the dataset agree with the report |
| Visualization files | 4 supplied PDFs and 4 rendered PNGs | Every chart link and preview resolves within the project folder |

The three featured groups contain **3,021 subscriptions**. The other **1,179** are annual subscribers acquired through non-promo channels. Overall churn covers all 4,200 records. Adjusted probabilities and confidence intervals are retained as reported rather than recalculated from the chart images.

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
| [Cleaned dataset](subscriptions_cleaned.csv) | 4,200 subscription records used in the analysis |
| [Observed versus adjusted segment churn — PDF](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf) | Original comparison of observed and adjusted churn by segment |
| [Segment confidence intervals — PDF](Churn_rates_and_adjusted_probabilities_by_segment.pdf) | Alternative segment comparison showing uncertainty |
| [Acquisition channel comparison — PDF](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.pdf) | Original channel export; the blue series is unlabeled |
| [Classifier evaluation — PDF](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf) | Precision, recall, and F1 comparison with a majority-rule baseline |
