# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## Business Context

This project analyzes a controlled experiment run by a subscription-based digital product company. The company introduced a new onboarding and activation campaign with the goal of improving user conversion and early engagement. New signups were split into two groups:

- **Control:** Existing onboarding experience
- **Treatment:** New campaign experience

Leadership needs to decide whether to roll out the treatment to all users.

---

## Dataset Description

**File:** `data/campaign_experiment_data.xlsx`  
**Records (raw):** 1,408 rows | **After deduplication:** 1,400 usable records  
**Period:** January–May 2025

| Column | Description |
|--------|-------------|
| user_id | Unique user identifier |
| signup_date | Date user signed up |
| experiment_group | Control or Treatment |
| region | North / South / East / West |
| device_type | Mobile / Desktop / Tablet |
| traffic_source | Organic / Paid Search / Social / Referral / Email |
| plan_type | Free / Basic / Premium |
| visited_landing_page | 1 if user visited landing page, else 0 |
| started_trial | 1 if user started trial, else 0 |
| completed_onboarding | 1 if user completed onboarding, else 0 |
| converted_to_paid | 1 if user converted to paid plan, else 0 |
| revenue_30d | Revenue generated within 30 days (USD) |
| support_tickets_30d | Count of support tickets raised in 30 days |
| refund_requested | 1 if user requested a refund, else 0 |
| days_to_convert | Days from signup to paid conversion (null if not converted) |
| engagement_score | Engagement score (0–100) |

---

## Business Problem

The company needs to decide whether to replace the existing onboarding flow with the new campaign experience for all new users. The primary concern is whether the new experience meaningfully improves paid conversion without degrading user quality or satisfaction.

Decision needed: Launch, partial launch, or hold  
Who it affects: All future new users  
What must improve: Paid conversion rate  
What must not worsen: Refund rate, support ticket rate, engagement quality  
Evidence required: Statistical significance on the North Star metric + clean guardrail metrics

---

## North Star Metric

**Paid Conversion Rate** — the percentage of users who converted from free/trial to a paid plan within 30 days.

This metric was selected because it directly represents business revenue growth. Funnel metrics like trial starts and onboarding completions are useful for diagnosing problems but do not by themselves generate revenue. Paid conversion is the point where user interest translates to business value.

Blind optimization risk: If the campaign aggressively pushes users to convert before they understand the product, short-term conversion rises while refund rates, churn, and support costs also rise. That is why guardrail metrics are tracked alongside the North Star.

---

## KPI Tree Summary

```
Paid Conversion Rate (North Star)
├── Acquisition Quality
│   ├── Landing Page Visit Rate
│   ├── Traffic Source Mix
│   ├── Organic % vs Paid %
│   └── Device Type Distribution
├── Activation Effectiveness
│   ├── Trial Start Rate
│   ├── Onboarding Completion Rate
│   ├── Time-to-First-Action
│   └── Feature Adoption Rate
└── Revenue Quality
    ├── Average Revenue Per User (ARPU)
    ├── Revenue Per Converted User
    ├── Plan Type Upgrade Rate
    └── Days to Convert

Guardrail Metrics:
- Refund Rate (must stay < 2%)
- Support Ticket Rate (must not exceed 20%)
- Engagement Score (must stay > 55)
- Segment-Level Conversion Decline (no segment should regress)
```

Full KPI tree diagram: `outputs/kpi_tree.png`

---

## Data Quality & Preparation

Steps performed in `analysis/experiment_analysis.xlsx` (Data Quality sheet):

| Check | Finding | Action |
|-------|---------|--------|
| Duplicate user_id | 8 duplicates | Kept first occurrence |
| Missing: device_type | 18 nulls | Excluded from device segment analysis |
| Missing: traffic_source | 24 nulls | Excluded from traffic segment analysis |
| Missing: engagement_score | 14 nulls | Excluded from engagement averages |
| Missing: days_to_convert | 1,336 nulls | Expected — only 72 users converted |
| Invalid binary values | None | All 0/1 columns are clean |
| Revenue outliers (>$5,000) | 3 records | Retained — likely Premium plan users |
| Group balance | 693 vs 715 | Minor imbalance (~3%), acceptable |
| Segment distribution | Even across all segments | No skew detected |

---

## Experiment Analysis Approach

Metrics were computed for each group and compared across:
- Overall Control vs Treatment
- Segment breakdowns by Region, Device Type, Traffic Source, and Plan Type

Full details in:
- `analysis/experiment_analysis.xlsx`
- `outputs/experiment_summary.xlsx`

---

## Hypothesis Testing

**Test:** One-tailed Two-Proportion Z-Test  
**H₀:** p_treatment ≤ p_control  
**H₁:** p_treatment > p_control  
**α = 0.05**

**Result:**
- Z-statistic: 3.2519
- P-value: 0.000573
- **Decision: Reject H₀**

The treatment group converted at 6.99% vs 3.17% in control — a statistically significant improvement. Chi-squared cross-check confirmed (p = 0.0017).

Full notes: `analysis/hypothesis_test_notes.md`

---

## Guardrail Metrics

| Guardrail | Control | Treatment | Risk |
|-----------|---------|-----------|------|
| Refund Rate | 0.0% | 0.4% | Low — monitor post-launch |
| Support Ticket Rate | 14.7% | 24.8% | **Elevated — investigate before full launch** |
| Engagement Score | 57.0 | 62.9 | Clear — treatment is better |
| Avg Rev per Converted User | $1,630 | $770 | Watch — lower volume; check 60-day retention |

---

## Final Recommendation

**Phased launch** — begin with Mobile + Organic Traffic segments, investigate the support ticket increase, then proceed to full rollout if metrics hold.

Full reasoning and next steps: `outputs/recommendation_memo.md`

---

## Folder Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx
│   └── hypothesis_test_notes.md
├── outputs/
│   ├── kpi_tree.png
│   ├── experiment_summary.xlsx
│   └── recommendation_memo.md
├── screenshots/
│   ├── summary_metrics.png
│   ├── hypothesis_test_output.png
│   └── kpi_tree_preview.png
└── README.md
```

---

## Screenshots

| File | Contents |
|------|----------|
| `screenshots/summary_metrics.png` | Control vs Treatment summary table with all 11 metrics |
| `screenshots/hypothesis_test_output.png` | Contingency table, Z-test results, and funnel bar chart |
| `screenshots/kpi_tree_preview.png` | KPI tree diagram preview |

---

## Assumptions

- 8 duplicate user IDs were found; first occurrence was kept in each case.
- Revenue values above $5,000 were retained as valid Premium plan purchases.
- Days-to-convert is null for users who did not convert — this is expected behavior, not missing data.
- Support ticket rate was computed as: users with at least 1 ticket / total users in group.
- Refund rate was computed as: refund requests / total users in group.

---

## Limitations

- The experiment ran over a single season (Jan–May). Seasonal variation may affect generalizability.
- Revenue per converted user dropped significantly in treatment. Long-term retention data is not yet available to assess whether this is compensated by volume.
- The support ticket spike is unexplained. Root cause analysis is required before full launch.
- Group sizes are slightly unequal, which is acceptable for proportion tests but worth noting.
