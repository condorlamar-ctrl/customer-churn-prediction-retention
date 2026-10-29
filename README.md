Customer Churn Analysis & Retention Strategy

**Analyzing 4,200 fitness subscriptions to identify retention priorities and recommend experiments.**

Monthly subscribers acquired through promotional offers had the highest observed churn among the three segments compared in the report: **63.3%**, versus **47.7%** for other monthly subscribers. This project uses customer segmentation, statistical comparisons, and logistic regression to turn that finding into practical retention recommendations.

**[Read the executive report](overview%20customer%20churn.pdf)** | **[Explore the cleaned dataset](subscriptions_cleaned.csv)** | **[View the visualizations](#visualizations)**

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

[View the PDF](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf) | [View the PNG preview](Observed_vs_Adjusted_Churn_Rate_by_Segment.png)

![Observed churn rates and adjusted probabilities for annual promo-offer, other monthly, and monthly promo-offer subscriptions](Observed_vs_Adjusted_Churn_Rate_by_Segment.png)

**Interpretation:** Monthly promo-offer subscribers have the highest observed churn (**63.3%**) among the three featured groups. The adjusted estimate (**63.0%**) preserves the ordering. Annual promo-offer subscribers have the lowest observed and adjusted estimates.

### 2. Segment Estimates and Confidence Intervals

[View the PDF](Churn_rates_and_adjusted_probabilities_by_segment.pdf) | [View the PNG preview](Churn_rates_and_adjusted_probabilities_by_segment.png)

![Observed and adjusted churn estimates with confidence intervals for the three subscriber segments](Churn_rates_and_adjusted_probabilities_by_segment.png)

**Interpretation:** This is an alternative view of the same three-group comparison. The report gives adjusted probabilities of **63.0%**, **47.5%**, and **30.0%** for monthly promo-offer, other monthly, and annual promo-offer subscribers, respectively. Confidence intervals show the uncertainty around these estimates.

### 3. Churn by Acquisition Channel

[View the PDF](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.pdf) | [View the PNG preview](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.png)

![Original acquisition-channel export showing raw and a second unlabeled churn-probability series](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.png)

**Interpretation:** Across both plan types, the cleaned dataset records **50.8%** observed churn for promo-offer acquisition and **33.8%** for referral acquisition. These channel-wide populations differ from the monthly-only segment comparison.

**Export note:** Although the filename describes raw and adjusted probabilities, the original legend labels only the orange Raw series. The blue series is not identified in the legend. Its exact values and adjustment procedure are not supplied in a separate table, so adjusted channel differences are not interpreted here.

### 4. Classifier Evaluation Versus a Majority-Rule Baseline

[View the PDF](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf) | [View the PNG preview](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.png)

![Logistic classifier precision, recall, and F1 compared with an always-majority-class rule](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.png)

**Interpretation:** The chart reports precision of **0.637**, recall of **0.502**, and F1 of approximately **0.56**. The majority-rule baseline identifies no churn cases and is displayed with zero churn-class precision, recall, and F1. Zero precision here is the export's convention for a rule that makes no positive churn predictions.

The four linked PDFs are the supplied source charts. The **2,400 × 1,480-pixel** PNG previews were rendered directly from those PDFs for GitHub display. Keep the images, PDFs, report, and dataset beside this README for the relative links to resolve.

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
| F1-score | ≈0.56 | Balance between precision and recall |

The scores above are reported in the supplied project summary rather than independently reproduced here. The chart labels F1 as **0.561**, its filename uses **0.5615**, and the original summary rounds it to **0.562**. The README uses approximately **0.56** to avoid implying a reconciled final decimal. ROC-AUC is reported in the summary and is not plotted in the classifier export.

At the evaluated classification threshold, the model identified about half of recorded churn cases. These results describe classification of recorded churn in this dataset; **future-churn prediction has not been validated**.

## Data Validation

| Validation check | Result | What it establishes |
| --- | ---: | --- |
| Subscription records | 4,200 | Dataset size agrees with the executive report |
| Unique customer identifiers | 4,200 | No duplicate customer IDs |
| Recorded churn | 1,768 yes; 2,432 no | Overall observed churn is 42.1% |
| Missing core identifiers, predictors, and churn flag | 0 | The nine checked fields are populated |
| Featured segment sizes | 589; 2,072; 360 | Counts agree with the report's three comparison groups |
| Featured observed churn rates | 63.3%; 47.7%; 30.3% | Rates recalculated from the cleaned data agree with the report |
| Chart exports | 4 supplied PDFs and 4 PNG previews | PDFs copied directly from the supplied files; previews rendered from those PDFs |

The three featured groups contain **3,021 subscriptions**. The remaining **1,179** are annual subscribers acquired through channels other than promo offers. Reported overall churn covers all 4,200 records.

Missing churn dates for non-churned subscriptions are distinct from missing predictors. Adjusted probabilities, confidence intervals, and classification scores are retained as reported; a runnable estimation pipeline was not supplied and these models were not refitted.

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
| [Observed versus adjusted segment churn — PDF](Observed_vs_Adjusted_Churn_Rate_by_Segment.pdf) / [PNG preview](Observed_vs_Adjusted_Churn_Rate_by_Segment.png) | Observed and adjusted estimates for the three featured segments |
| [Segment estimates and confidence intervals — PDF](Churn_rates_and_adjusted_probabilities_by_segment.pdf) / [PNG preview](Churn_rates_and_adjusted_probabilities_by_segment.png) | Alternative view of the three-segment comparison |
| [Acquisition channel comparison — PDF](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.pdf) / [PNG preview](Raw_vs_Adjusted_Churn_Probability_by_Acquisition_Channel.png) | Original channel export; the second series is unlabeled in the legend |
| [Classifier evaluation — PDF](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.pdf) / [PNG preview](Classifier_F1_0.5615_on_4_200_subscriptions_Precision_Recall_F1_vs_Majority_Rule.png) | Precision, recall, and F1 comparison with a majority-rule baseline |
