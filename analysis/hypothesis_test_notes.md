# Hypothesis Test Notes — Onboarding Campaign Experiment

## Metric Being Tested

**Paid Conversion Rate** — the share of users in each group who converted to a paid subscription within 30 days of signup.

This was selected as the primary test metric because it is the North Star metric for this experiment. Improving top-of-funnel metrics like landing page visits or trial starts only matters if those users eventually convert and generate revenue. Leadership's core question is whether the new onboarding experience drives more paying customers, not just more activity.

---

## Hypotheses

**Null Hypothesis (H₀):**  
The paid conversion rate in the Treatment group is less than or equal to the paid conversion rate in the Control group.  
H₀: p_treatment ≤ p_control

**Alternative Hypothesis (H₁):**  
The paid conversion rate in the Treatment group is greater than the paid conversion rate in the Control group.  
H₁: p_treatment > p_control

---

## Test Setup

| Parameter | Value |
|-----------|-------|
| Test type | One-tailed Two-Proportion Z-Test |
| Direction | Right-tailed (testing if Treatment > Control) |
| Significance level (α) | 0.05 |
| Primary metric | Paid Conversion Rate |

A one-tailed test was chosen because the business question is directional — leadership wants to know if the new campaign *improves* conversion, not simply whether it changes it. A two-tailed test would also be valid here, and the result would still be significant either way given the p-value.

---

## Observed Data

|  | Converted | Not Converted | Total | Conversion Rate |
|--|-----------|---------------|-------|-----------------|
| Control | 22 | 671 | 693 | 3.17% |
| Treatment | 50 | 665 | 715 | 6.99% |
| Total | 72 | 1,336 | 1,408 | 5.11% |

---

## Test Output

| Metric | Value |
|--------|-------|
| Z-statistic | 3.2519 |
| P-value (one-tailed) | 0.000573 |
| Chi-squared statistic (cross-check) | 9.8024 |
| Chi-squared p-value | 0.001743 |
| Decision rule | Reject H₀ if p < 0.05 |
| Decision | **Reject H₀** |

---

## Interpretation

The p-value of 0.000573 is well below the 0.05 threshold. The result is statistically significant. The treatment group converted at 6.99% compared to 3.17% in the control group — roughly a 2.2x lift.

The chi-squared cross-check (p = 0.0017) confirms the finding using a different approach.

In practical terms, this means the improvement in conversion is very unlikely to be due to random variation. The new onboarding experience genuinely moves more users to paid status faster.

However, the hypothesis test only confirms the conversion lift. The final launch decision also depends on guardrail metrics — specifically the support ticket rate increase and the lower average revenue per converted user — which are evaluated separately in the recommendation memo.

---

## Assumptions and Limitations

- Users were assigned to groups independently; no contamination between groups was detected.
- The test assumes approximate normality for proportions, which holds given sample sizes above 30 in each group.
- Days-to-convert data was only available for the 72 converting users; no statistical test was run on this metric.
- Engagement score differences were not formally tested but are directionally favorable for Treatment.
