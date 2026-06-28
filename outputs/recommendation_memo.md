## Executive Summary

The company ran an A/B experiment to evaluate a new onboarding and activation campaign. Users were split into Control (existing experience) and Treatment (new campaign). The experiment ran across **1,408 users** (693 Control, 715 Treatment).

The hypothesis test shows the Treatment campaign **significantly improves paid conversion rate** (3.17% → 6.99%, p = 0.0006). However, two guardrail metrics raise important concerns about revenue quality and user experience that prevent me from recommending a full immediate launch.

**My Recommendation: Launch with conditions — prioritize high-performing segments and investigate guardrail issues before full rollout.**

---

## Business Problem Statement

The company is deciding whether to replace the existing onboarding experience with a new campaign-based flow for all users. The key question is: does the new campaign lead to meaningfully more paid conversions without causing harm to revenue quality or user satisfaction?

**Decision to be made:** Whether to launch the Treatment campaign to all users, selected segments, or not at all.

**Who it impacts:** All new users entering the onboarding funnel, the customer success team (support volume), and ultimately the revenue team.

**What needs to improve:** Paid conversion rate (North Star Metric).

**What risks must be monitored:** Refund rate, support ticket volume, and revenue per converted user.

**Evidence required:** Statistical significance on conversion rate improvement, plus acceptable guardrail metrics before full launch is recommended.

---

## North Star Metric: Paid Conversion Rate

**Definition:** Number of users who converted to paid / Total number of users in group

**Why this is the North Star:**  
Paid conversion rate is the single most direct measure of whether the campaign achieves its business goal. Unlike engagement score or trial start rate, it actually touches the revenue line. It captures the full funnel behavior — a user who visits the landing page, starts a trial, completes onboarding, *and* actually pays is the definition of a successful outcome.

**Why other metrics are supporting metrics:**
- *Landing page visit rate* only tells us if users showed up, not if they stayed
- *Trial start rate* measures intent, not commitment
- *Engagement score* shows product usage but doesn't guarantee payment
- *ARPU* is useful but noisy due to outliers — it's better as a supporting quality check

**Connection to business growth:** More paid conversions directly means more revenue. If the company can double its conversion rate on new users without degrading other metrics, that's a significant growth lever that compounds over time.

**Risk of optimizing blindly:** A campaign could artificially inflate conversion rate by attracting low-value users or creating pressure-based UX that converts users who later refund or churn. This is exactly why guardrail metrics like revenue per converter and refund rate need to be monitored alongside conversion rate.

---

## KPI Tree Summary

The KPI tree breaks down the North Star into 4 primary drivers:

| Level 1 Driver | Sub-drivers |
|----------------|-------------|
| **Funnel Engagement** | LP Visit Rate → Trial Start Rate → Onboarding Completion Rate |
| **Revenue Quality** | ARPU → Rev per Converted User → Revenue Growth Trend |
| **User Experience** | Engagement Score → Days to Convert → Feature Adoption Rate |
| **Guardrail Metrics** | Refund Rate → Support Ticket Rate → Segment-Level Decline Risk |

The full KPI tree is available at `outputs/kpi_tree.png`.

---

## Experiment Results Summary

| Metric | Control | Treatment | Change |
|--------|---------|-----------|--------|
| Total Users | 693 | 715 | +22 |
| Landing Page Visit Rate | 63.6% | 72.6% | **+9.0 ppt** |
| Trial Start Rate | 25.1% | 29.1% | **+4.0 ppt** |
| Onboarding Completion Rate | 15.6% | 21.3% | **+5.7 ppt** |
| **Paid Conversion Rate (NS)** | **3.17%** | **6.99%** | **+3.82 ppt ↑** |
| ARPU (all users) | $51.75 | $53.88 | +$2.13 |
| Revenue per Converter | $1,630.10 | $770.41 | **-$859.69 ↓** |
| Refund Rate | 0.00% | 0.42% | +0.42% |
| Support Ticket Rate | 14.7% | 24.8% | **+10.1 ppt ↑** |
| Avg Engagement Score | 57.0 | 62.9 | **+5.9 pts ↑** |
| Avg Days to Convert | 8.86 days | 6.40 days | **-2.46 days ↑** |

The funnel improved at every stage, and the Treatment group shows stronger engagement and faster conversion. However, support ticket rate and revenue per converter are concerning.

---

## Hypothesis Test Interpretation

**Test Used:** Two-proportion z-test for Paid Conversion Rate  
**H₀:** p_treatment ≤ p_control  
**H₁:** p_treatment > p_control  
**Significance Level:** α = 0.05 (one-tailed)

| Result | Value |
|--------|-------|
| Z-Statistic | 3.252 |
| P-Value | 0.0006 |
| Decision | **Reject H₀** |

The result is statistically significant at the 0.05 level (and even the 0.001 level). The Treatment campaign leads to a meaningfully higher conversion rate and it is very unlikely this result happened by chance.

---

## Guardrail Metric Analysis

### Guardrail 1: Refund Rate
- Control: 0.00% | Treatment: 0.42%
- Treatment has some refunds while Control had none. The absolute number is small (3 users), but the fact that refunds appeared at all is worth investigating. This could indicate users are converting without being fully satisfied — possibly due to a more persuasive onboarding flow that sets incorrect expectations.

**Verdict: WATCH — Not a blocking issue, but monitor closely post-launch.**

### Guardrail 2: Support Ticket Rate
- Control: 14.7% | Treatment: 24.8% (almost 70% relative increase)
- This is the most significant guardrail concern. Nearly 1 in 4 Treatment users raised a support ticket within 30 days, compared to roughly 1 in 7 in Control. This suggests the new onboarding experience may be creating confusion — possibly introducing too many steps, unclear messaging, or a UX issue that frustrates users.

**Verdict: FLAG — This is a blocking concern for a full launch. Investigate root cause before scaling.**

### Guardrail 3: Revenue Per Converted User
- Control: $1,630.10 | Treatment: $770.41 (53% lower)
- While the conversion rate doubled, the revenue per converter dropped by more than half. This is the most financially significant guardrail concern. Treatment is converting more users but those users are spending less on average. It's possible the campaign is converting users who would have been better suited for a lower-tier or free plan.

*A note here: part of this gap may be driven by outliers in the Control group (USR-100106 had $8,610 in revenue, USR-100303 had $6,789). After removing the top 2 outliers, Control rev/converter drops to around $1,023 vs Treatment's $770 — still lower, but the gap narrows. This doesn't eliminate the concern but softens it.*

**Verdict: FLAG — Revenue quality needs investigation. The campaign may be converting price-sensitive users.**

### Guardrail 4: Engagement Score
- Control: 57.0 | Treatment: 62.9 (positive)
- Higher engagement in Treatment is a good sign. Users are more engaged under the new campaign, suggesting better product adoption.

**Verdict: OK**

### Guardrail 5: Days to Convert
- Control: 8.86 days | Treatment: 6.40 days (Treatment converts faster)
- Faster conversion is generally good and suggests the new campaign creates clearer urgency or simpler friction points.

**Verdict: OK**

---

## Segment-Level Insights

**By Region:**
- Treatment performs best in **North region** (8.89% conv vs 3.45% Control — largest lift)
- **West region** shows the weakest lift (5.03% vs 3.38%), though still positive
- All 4 regions show positive lift — no regional decline detected

**By Device Type:**
- **Tablet users** in Treatment show the biggest relative lift (7.14% vs 1.79% in Control)
- **Mobile** and **Desktop** both show strong improvement
- Treatment improves conversion across all device segments — good sign

**By Traffic Source:**
- **Referral** users in Treatment show the highest conversion (10.99%) — these users already have social proof and the new campaign amplifies it
- **Paid Search** and **Organic** both show strong improvement
- No traffic source shows a decline in conversion under Treatment

**By Plan Type:**
- **Free plan** users show the highest lift in Treatment (9.24% vs 3.05% in Control)
- **Premium users** also improve (6.25% vs 2.75%)
- **Basic plan** shows minimal lift (3.83% vs 3.59%) — the campaign seems to work better for non-Basic segments

---

## Final Recommendation

**Decision: Launch for selected segments, with guardrail investigation before full rollout**

Based on the evidence:

✅ Conversion rate improvement is statistically significant (p = 0.0006) — the campaign works  
✅ All segments show positive lift — no obvious subgroup harmed  
✅ Engagement and speed-to-convert both improved  
⚠️ Support ticket rate jumped significantly — needs UX investigation  
⚠️ Revenue per converter is lower — needs further analysis of user quality  

**Recommended phased approach:**
1. **Immediate:** Launch Treatment for North region and Referral traffic users — these show the strongest lift with relatively lower guardrail risk
2. **30-day review:** Monitor refund rate and support ticket volume closely. If support tickets remain elevated, conduct a UX audit of the onboarding flow to find the confusion points
3. **Investigate revenue quality:** Review whether lower rev/converter is due to plan tier selection or user LTV (Lifetime Value) — the 30-day window may not capture full revenue potential
4. **Full launch only if:** Support ticket rate drops below 18% and revenue per converter improves

---

## Risks and Limitations

- **Short observation window:** Revenue data is captured over 30 days. It's possible Treatment converters generate more revenue over 90+ days (LTV analysis needed).
- **Revenue outliers in Control:** Two outlier users inflate Control's avg rev/converter. After adjustment, the gap narrows — the concern is real but smaller than raw numbers suggest.
- **Sample size for converters:** Only 22 Control converters and 50 Treatment converters — the revenue per converter calculation is based on small samples and could vary significantly with more data.
- **Group imbalance:** Control has 693 users, Treatment has 715. Minor imbalance, but not enough to meaningfully affect results.
- **Missing values:** 18 device_type missing, 24 traffic_source missing, 14 engagement_score missing — these were excluded from segment analyses. Small enough to not be a concern.
- **No causal analysis of support tickets:** We know the rate is higher but don't know *why*. Could be an onboarding UX bug, unclear pricing, or simply a more engaged user base that asks more questions.

---

## Next Steps

1. Run UX analysis on the Treatment onboarding flow to identify the source of increased support tickets
2. Pull 90-day revenue data for both cohorts to check if revenue gap narrows over time
3. Launch Treatment for North + Referral segments immediately (lowest risk, highest lift)
4. Set up monitoring dashboard tracking: conversion rate, support ticket rate, refund rate, and ARPU — weekly reviews
5. Plan a follow-up experiment that addresses identified UX issues in the current Treatment flow

---
