# Olist E-commerce Analysis

Exploratory data analysis of Olist's Brazilian e-commerce data, focusing on product prices, payment methods, delivery performance, and customer satisfaction.

This team project uses Python to turn transactional data into business insights through data preparation, visualization, correlation analysis, and statistical hypothesis testing.

## Business questions

- How are product prices and payment amounts distributed?
- Which product categories appear most frequently in order items?
- How do delivery times and spending relate to customer review scores?
- Do average item prices differ across major product categories?
- Is payment method associated with order completion?

## Tools

Python, Pandas, NumPy, Plotly, Matplotlib, Seaborn, SciPy, and Google Colab.

## Data

The analysis uses seven Olist CSV tables: orders, order items, products, customers, sellers, payments, and reviews. The orders table contains 99,441 records.

Dataset: **Brazilian E-Commerce Public Dataset by Olist**, available on Kaggle under `olistbr/brazilian-ecommerce`.

Raw CSV files are obtained separately. The notebook reads them from Google Drive.

## Analysis workflow

1. Inspect missing values, duplicate records, and data types.
2. Fill selected missing product attributes and review text fields; convert date columns for delivery analysis.
3. Explore item prices, payment amounts, freight costs, category frequencies, payment methods, and review scores.
4. Join relevant tables and examine relationships between spending, delivery time, and satisfaction.
5. Apply a t-test, one-way ANOVA, and a chi-square test to the business questions.
6. Summarize findings and propose operational actions.

## Key findings

Values below summarize the saved notebook outputs and project presentation.

| Metric or comparison | Result | Interpretation |
| --- | --- | --- |
| Average customer review score | 4.09 / 5 | Reviews are generally positive. |
| Median customer review score | 5.00 / 5 | The median review receives the highest rating. |
| Mean / median item price | 120.65 / 74.99 | Higher-priced items pull the mean above the median. These are item prices, not order-level basket values. |
| Delivery time vs. review score | Correlation approximately -0.33 | Longer delivery times are associated with lower ratings. |
| Spending vs. review score | Correlation approximately -0.05 | The observed linear relationship is weak. |
| Average review score: on-time / late delivery | 4.29 / 2.57 | Late deliveries receive substantially lower average ratings in the analyzed sample. |
| Completion rate: credit card / boleto | 97.12% / 97.00% | The observed rates are close in the tested payment records. |

## Hypothesis tests

The analysis uses a significance threshold of 0.05.

| Question | Test | Saved result | Conclusion |
| --- | --- | --- | --- |
| Do on-time and late deliveries have different average review scores? | Independent-samples t-test | t = 89.55; p reported as 0.0 | The test output indicates a statistically significant difference. |
| Do average item prices differ across the 10 most frequent product categories? | One-way ANOVA | F = 310.30; p reported as 0.0 | At least one tested category has a different mean item price. |
| Is credit card vs. boleto payment associated with completion? | Chi-square test | Chi-square = 0.774; p = 0.379 | Insufficient evidence to reject independence in the tested sample. |

P-values displayed as `0.0` reflect numerical precision and should not be interpreted as an exact zero probability. Completion is defined as an order with status `delivered`. The payment test includes credit card and boleto records only.

## Business recommendations

- Prioritize investigation of delivery delays, tracking late-delivery rates alongside review scores by seller or region.
- Provide proactive updates when an order is likely to miss its estimated delivery date.
- Compare prices within product categories rather than relying on one overall average.
- Investigate product quality and service factors alongside spending, given the weak spending–satisfaction correlation.
- Gather further evidence before changing payment options to improve completion; this test does not establish a meaningful difference between credit card and boleto.

These are proposed actions based on the analysis, not measured outcomes of implemented changes.

## Notebook

[View the analysis notebook](olistteam1.ipynb)

The original notebook contains Turkish explanations and saved analysis outputs.

### Run in Google Colab

1. Download `olistteam1.ipynb` or open it from GitHub in Google Colab.
2. Obtain the seven CSV files from the Olist dataset:
   - `olist_orders_dataset.csv`
   - `olist_order_items_dataset.csv`
   - `olist_products_dataset.csv`
   - `olist_customers_dataset.csv`
   - `olist_sellers_dataset.csv`
   - `olist_order_payments_dataset.csv`
   - `olist_order_reviews_dataset.csv`
3. Place the files in `MyDrive/olistteam1/`, or update the file paths used throughout the notebook.
4. Mount Google Drive and run the cells in sequence.

## Interpretation and reproducibility notes

- Findings describe associations in observational data; they do not establish causation.
- Tables have different levels of detail. Orders may have multiple items, payments, or reviews, so join cardinality matters when interpreting counts and averages.
- The original notebook reuses `p_value` across tests. A later delivery interpretation therefore displays the payment test's p-value of 0.379. The delivery result above comes from the original t-test output. The ANOVA interpretation should reference `anova_p_value`.
- This README documents the saved analysis; the notebook has been preserved as submitted and has not been rerun against the raw CSV files for this documentation update.

## Acknowledgements

Completed as a team data analysis project. Dataset credit belongs to Olist and its dataset contributors.
