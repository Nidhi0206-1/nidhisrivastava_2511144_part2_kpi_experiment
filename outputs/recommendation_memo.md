# Recommendation Memo
**To:** Product Leadership  
**From:** Business Analytics  
**Date:** June 2025  
**Subject:** Onboarding Campaign Experiment — Launch Recommendation

---

## Executive Summary

The new onboarding and activation campaign shows a statistically significant improvement in paid conversion rate (3.2% → 7.0%, p = 0.0006). Every funnel metric improved. Engagement scores are higher in the treatment group and users are converting faster.

One guardrail metric is elevated: the support ticket rate nearly doubled (14.7% → 24.8%). This needs attention before a full launch. The lower average revenue per converted user ($770 vs $1,630) is partly explained by the higher volume of conversions skewing toward lower-spend users on entry plans.

**Recommendation: Launch with phased rollout, beginning with Mobile and Organic traffic segments, while investigating the support ticket increase in parallel.**

---

## Business Problem

The company is deciding whether to replace the existing onboarding experience with a new campaign-driven flow for all new users. The decision affects every user who signs up going forward.

The key question is whether the conversion improvement is large enough, stable enough, and clean enough across segments to justify a full rollout — or whether the support ticket spike and revenue per user drop create risks that require investigation first.

Success requires: (1) a meaningful and statistically significant conversion lift, (2) no serious degradation in guardrail metrics, and (3) reasonable consistency across user segments.

---

## North Star Metric

**Paid Conversion Rate** is the primary success metric for this experiment.

This metric matters most because it directly connects user behavior to revenue. High trial start rates or engagement scores are positive signs, but they do not pay the bills. A user who engages heavily but never converts is still a cost center. Paid Conversion Rate captures the outcome that drives subscription revenue growth.

Risks of optimizing only this metric: pushing users toward conversion with friction-heavy prompts or aggressive discounting can inflate short-term conversion while hurting retention, engagement quality, and long-term LTV. That is why refund rate and revenue per converted user are tracked as guardrails.

---

## KPI Tree Summary

The KPI tree breaks the North Star metric into three primary driver groups:

**1. Acquisition Quality** — whether users arriving at the product are the right fit. Sub-drivers: landing page visit rate, traffic source mix, device distribution.

**2. Activation Effectiveness** — whether users complete the early product experience. Sub-drivers: trial start rate, onboarding completion rate, feature adoption, time to first action.

**3. Revenue Quality** — whether converting users generate durable revenue. Sub-drivers: ARPU, revenue per converted user, plan upgrade rate, days to convert.

Guardrail metrics: Refund Rate, Support Ticket Rate, and Engagement Score set the boundaries within which conversion improvements are acceptable.

---

## Experiment Results Summary

| Metric | Control | Treatment | Change |
|--------|---------|-----------|--------|
| Users | 693 | 715 | — |
| Landing Page Visit Rate | 63.6% | 72.6% | +9.0pp |
| Trial Start Rate | 25.1% | 29.1% | +4.0pp |
| Onboarding Completion | 15.6% | 21.3% | +5.7pp |
| **Paid Conversion Rate** | **3.2%** | **7.0%** | **+3.8pp** |
| ARPU | $51.75 | $53.88 | +$2.13 |
| Avg Revenue per Converted User | $1,630 | $770 | -$860 |
| Refund Rate | 0.0% | 0.4% | +0.4pp |
| Support Ticket Rate | 14.7% | 24.8% | +10.1pp |
| Avg Engagement Score | 57.0 | 62.9 | +5.9 |
| Avg Days to Convert | 8.9 days | 6.4 days | -2.5 days |

All funnel and activation metrics improved. Engagement scores are meaningfully higher. Users convert faster in the treatment group. ARPU improved slightly despite lower revenue per converter, because conversion volume is significantly higher.

---

## Hypothesis Test Interpretation

**Test:** One-tailed Two-Proportion Z-Test  
**H₀:** Treatment conversion rate ≤ Control conversion rate  
**H₁:** Treatment conversion rate > Control conversion rate  
**Result:** Z = 3.25, p = 0.0006  
**Decision:** Reject H₀ at α = 0.05

The conversion improvement is statistically significant and not attributable to random noise. A chi-squared cross-check returned p = 0.0017, confirming the result. The effect size (3.8 percentage points, roughly 120% relative lift) is also commercially meaningful — not just a marginal technical result.

---

## Guardrail Analysis

**1. Refund Rate**  
Control: 0.0% | Treatment: 0.4%. The treatment group had 3 refund requests vs zero in control. The rate is low and not alarming, but it warrants monitoring. If refund rate climbs above 2% post-launch, that would signal that users are converting before they fully understand the product.

**2. Support Ticket Rate**  
Control: 14.7% | Treatment: 24.8%. This is the most significant guardrail concern. Nearly 1 in 4 treatment users raised a support ticket, compared to roughly 1 in 7 in control. This 10 percentage point increase suggests the new onboarding flow may leave some users confused about certain product features. It does not block launch, but it needs investigation before full rollout. If support load increases by this magnitude at full scale, it adds operational cost and may affect user experience.

**3. Engagement Score**  
Control: 57.0 | Treatment: 62.9. The engagement score is better in treatment, which is reassuring. Higher engagement typically predicts lower churn and better retention. This guardrail is clear.

**4. Revenue per Converted User**  
Control: $1,630 | Treatment: $770. This is worth understanding before launch. The drop may reflect that the treatment campaign is bringing in more entry-level plan users who generate lower initial revenue. If these users upgrade over time, this is fine. If they churn at higher rates, the lower revenue per user will compound. Recommend a 60-day cohort retention check post-launch.

---

## Segment-Level Insights

The conversion improvement appears across all regions and device types. Some observations:

- **Mobile users** show a stronger treatment effect than desktop users, likely because the new onboarding experience is better optimized for mobile screens.
- **Organic traffic users** respond better to the new experience than Paid Search users, possibly because organic users arrive with higher intent.
- **Free plan users** benefit the most from the new campaign, which makes sense since the campaign focuses on activation.
- No major segment showed a conversion decline in treatment vs control.

---

## Final Recommendation

**Launch with a phased rollout.**

Start with Mobile + Organic Traffic users, who showed the clearest benefit and no guardrail concerns. Simultaneously, run a root cause analysis on the support ticket increase to identify which part of the onboarding flow is generating the most tickets. Fix those points before extending to the full user base.

Set a 30-day monitoring window post-initial rollout with the following thresholds:
- Refund rate must stay below 2%
- Support ticket rate must trend back toward 18% or below
- Conversion rate must sustain above 5.5%

If those conditions hold at 30 days, proceed with full rollout.

---

## Risks and Limitations

- The support ticket increase is unexplained. Until we know which step in the new flow is causing confusion, we are operating with incomplete information.
- Revenue per converted user is significantly lower in treatment. If early cohort retention is also lower, the revenue impact could be negative net of support costs.
- The experiment ran from January to May 2025. Seasonal factors could influence conversion patterns; a post-launch check in Q3 is warranted.
- Group sizes are slightly imbalanced (693 vs 715), though this does not materially affect the test validity.
- 8 duplicate user IDs were found in the raw data and removed. Their origin is unknown.

---

## Next Steps

1. Root cause analysis of support ticket spike — identify which onboarding screen or step is generating tickets.
2. Begin phased rollout to Mobile + Organic segments.
3. Track 30-day and 60-day retention for converted users in the treatment group.
4. Revisit revenue per converted user at 60 days to determine whether plan upgrades close the gap.
5. Schedule a formal readout at 30 days post-rollout to decide on full launch.
