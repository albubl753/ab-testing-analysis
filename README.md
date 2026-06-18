# A/B Testing Analysis & Statistical Validation

## Business Goal
Evaluate the impact of four different UI/UX hypotheses (A/B tests) on user conversion funnels. The objective is to determine statistical significance using a Two-Proportion Z-Test to identify winning variations for scaling and filter out changes that negatively affect user behavior.

## Tech Stack
* **Languages & Libraries:** Python (Pandas, NumPy, Statsmodels)
* **Database:** Google BigQuery (SQL)
* **BI Tool:** Tableau Public

## Methodology
* **Statistical Test:** Two-Proportion Z-Test (calculated via Python `statsmodels`).
* **Parameters:** 95% Confidence Level (Alpha = 0.05).
* **Evaluation:** If the p-value < 0.05, the metric change is marked as statistically significant (driven by the test, not random chance).

## Interactive Dashboards
*[View Calculation Metrics Dashboard on Tableau Public](https://public.tableau.com/views/A_BTestingTool_17781304401450/CalculationMetrics?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)*

*[View Sample Distribution Dashboard on Tableau Public](https://public.tableau.com/views/ABTestingTool_17762612381770/ABTest?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)*

## Key Analytical Findings & Recommendations

* **Test 1 (The Winner):** Demonstrated a statistically significant uplift across multiple lower-funnel metrics. 
  * `begin_checkout` conversion rose from 8.3% to 8.8% (p-value: 0.002).
  * `add_payment_info` increased from 4.3% to 4.9% (p-value: 0.00008).
  * `add_shipping_info` grew from 6.6% to 7.1% (p-value: 0.009).
  * **Actionable Recommendation:** Scale these changes to 100% of users, as they conclusively improve the final steps before purchase.

* **Test 2 (The Bottleneck):** Showed a significant increase in the `add_to_cart` metric (from 5.5% to 6.0%, p-value: 0.0002). However, this did not translate into higher sales—checkout and payment metrics showed no significant changes (p-values > 0.05). 
  * **Actionable Recommendation:** Investigate the user journey post-cart addition. Users are motivated to add items to the cart, but experience friction during checkout (cart abandonment).

* **Test 3 & Test 4 (The Losers):** 
  * **Test 3:** Caused a significant drop in `begin_checkout` (13.6% to 13.1%, p-value: 0.012) and `add_to_cart` (25.2% to 24.4%, p-value: 0.0008).
  * **Test 4:** Significantly reduced `new_accounts` registrations (8.5% to 8.2%, p-value: 0.017) and `begin_checkout` transitions (11.9% to 11.6%, p-value: 0.045).
  * **Actionable Recommendation:** Reject both hypotheses and immediately roll back any related changes, as they negatively disrupt the conversion funnel.
