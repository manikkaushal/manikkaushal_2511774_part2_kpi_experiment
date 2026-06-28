# Hypothesis Test Notes — Onboarding & Activation Campaign
**A/B Experiment

---

## Task 6: Framing the Hypotheses

### Metric Being Tested
**Paid Conversion Rate** — the proportion of users in each group who converted to a paid subscription within 30 days.

This is the North Star Metric for the experiment. It directly reflects the core business question: did the new onboarding campaign actually get more users to pay?

### Why This Metric?
I chose Paid Conversion Rate because it's the most direct measure of whether the campaign does what leadership wants it to do — get more people to become paying customers. Other metrics like engagement score or trial start rate are good supporting indicators, but they don't tell us if users are actually spending money. There's a risk that a campaign can increase engagement without increasing real revenue, which would look good on paper but not help the business. So using the North Star ensures we test what actually matters to the company's growth.

*Note: An argument could be made that revenue per user (ARPU) is a better metric since it captures revenue magnitude, not just conversion count. However, ARPU is noisier due to outliers and is harder to test statistically, so I stayed with conversion rate for the formal hypothesis test.*

---

### Null Hypothesis (H₀)
> H₀: The paid conversion rate of the Treatment group is **equal to or less than** the Control group.
>
> H₀: p_treatment ≤ p_control

### Alternate Hypothesis (H₁)
> H₁: The paid conversion rate of the Treatment group is **greater than** the Control group.
>
> H₁: p_treatment > p_control

---

### Test Type
**One-Tailed Test (Right-Tailed)**

I chose a one-tailed test here because the business question is directional — leadership wants to know if the treatment *improves* conversion, not whether it could go either way. We're not looking to see if the treatment makes things worse (we'll check that via guardrail metrics separately). This is the standard approach for A/B tests where the hypothesis is framed as "new experience is better."

*I initially started thinking this should be two-tailed because I wanted to catch any negative effect, but after thinking more carefully, one-tailed is right for this specific business decision. The guardrail metrics serve the purpose of catching negative effects.*

---

### Significance Level
**α = 0.05**

This is the standard significance level used in most business A/B testing. It means we're willing to accept a 5% chance of being wrong and saying the treatment works when it actually doesn't (Type I error). Some companies use α = 0.01 for very expensive rollouts, but 0.05 feels right for an onboarding campaign decision.

---

### Interpretation Logic
- If the p-value is **less than 0.05** → reject H₀ → there is statistically significant evidence that the treatment improves conversion rate
- If the p-value is **greater than or equal to 0.05** → fail to reject H₀ → we cannot conclude the treatment improves conversion rate

**Important note:** Statistical significance alone should not drive the launch decision. We also need to review guardrail metrics before making a final recommendation (see Task 8).

---

## Task 7: A/B Test Analysis Results

### Test Method: Two-Proportion Z-Test

I used a **two-proportion z-test** to compare the conversion rates between Control and Treatment groups. This test is appropriate when:
- The outcome is binary (converted = 1, not converted = 0)
- Sample sizes are large enough for the normal approximation to hold
- The two groups are independent (users are randomly assigned)

The formula for the z-statistic is:

```
z = (p̂_treatment - p̂_control) / sqrt(p̂_pool × (1 - p̂_pool) × (1/n_c + 1/n_t))
```

Where `p̂_pool = (conv_c + conv_t) / (n_c + n_t)`

---

### Test Inputs

| Parameter | Control | Treatment |
|-----------|---------|-----------|
| Total Users (n) | 693 | 715 |
| Conversions | 22 | 50 |
| Conversion Rate (p̂) | 0.0317 (3.17%) | 0.0699 (6.99%) |
| Pooled p̂ | 0.0513 | — |
| Standard Error | 0.0104 | — |

---

### Test Output

| Result | Value |
|--------|-------|
| Z-Statistic | **3.252** |
| P-Value (one-tailed) | **0.0006** |
| Critical Value (α=0.05, one-tail) | 1.645 |
| Decision | **Reject H₀** |

---

### Interpretation

The z-statistic of **3.252** is well above the critical value of 1.645, and the p-value of **0.0006** is far below the significance level of 0.05. This means:

> **We reject the null hypothesis.** There is strong statistical evidence that the Treatment group has a significantly higher paid conversion rate than the Control group.

The treatment increased the conversion rate from **3.17%** to **6.99%**, which is approximately a **2.2x improvement** (or +3.82 percentage points absolute lift). This is a practically meaningful difference — not just statistically significant.

---

### Connecting to the Business Decision

The hypothesis test supports moving forward with the treatment. However, the decision to actually launch cannot be based on this test alone. As explained in Task 8 and the recommendation memo, we found two important guardrail issues:

1. **Support ticket rate** in the Treatment group is nearly 70% higher than Control (24.8% vs 14.7%), which suggests users are more confused or frustrated under the new experience
2. **Revenue per converted user** is significantly lower in Treatment ($770 vs $1,630 in Control), which means we're converting more users but at a lower average spend

These guardrail concerns suggest the treatment should **not be launched universally yet**, even though the hypothesis test shows a significant improvement in conversion rate. A **phased rollout or further investigation** is recommended before full launch.

