# Assignment 04 Interpretation Memo

**Student Name:** Joshua Keoshkerian
**Date:** 2/13/2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): 0.1082 (SE: 0.0060, p-value: 0.000)
- Slope (β₁): -0.0687 (SE: 0.0325, p-value: 0.035)
- R²: 0.002 | N: 2527

**Model 2: ret ~ prime_rate**
- Intercept (β₀): 0.1974 (SE: 0.0230, p-value: 0.000)
- Slope (β₁): -0.0155 (SE: 0.0036, p-value: 0.000)
- R²: 0.007 | N: 2527

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): 0.0973 (SE: 0.0092, p-value: 0.000)
- Slope (β₁): 0.5770 (SE: 0.5675, p-value: 0.309)
- R²: 0.000 | N: 2518

*Note: Model 3 may have fewer observations if ffo_at_reit has missing values; statsmodels drops those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a -0.000687 change in annual return (about -0.07 percentage points).
- The slope is negative, so higher dividend yield is linked to slightly lower annual returns in this sample, which could reflect yield rising when prices fall or higher-yield firms being viewed as riskier.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a -0.000155 change in annual return (about -0.02 percentage points).
- The relationship is negative and statistically meaningful, which fits the idea that higher interest rates raise financing costs and pressure REIT valuations.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets is associated with a 0.5770 change in annual return; a 0.01 increase is about +0.0058 (roughly +0.58 percentage points).
- The sign is positive, but the estimate is not statistically significant, so I do not find strong evidence that more profitable REITs earn higher annual returns in this simple model.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant — dividend yield has a small but statistically meaningful negative relationship with annual returns.
- **prime_rate:** Significant — higher interest rates are associated with lower annual REIT returns.
- **ffo_at_reit:** Not significant — the slope is imprecise and could be near zero.

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** prime_rate, since it has the smallest p-value and the largest absolute t-stat.

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- prime_rate has the highest R² (0.007), but all three are very low, which implies these single predictors explain only a tiny share of annual return variation. Most variation likely comes from firm-specific risk, macro shocks, and sector dynamics not captured here.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- REIT size (lnmcap or market_equity): larger firms may have lower risk and different return profiles.
- Leverage or balance-sheet risk (btm or debt proxies): financing structure can affect sensitivity to rates and returns.
- Momentum or prior returns (ret1 or ret_6_1): recent performance often predicts short-term returns.

**Potential bias:** If higher dividend yield or higher rates are correlated with riskier or distressed firms, the negative slopes could partly capture risk effects rather than a clean causal impact of yield or rates.

---

## 7. Summary and Next Steps

**Key Takeaway:**
Prime rate has the clearest and most statistically robust relationship with annual REIT returns, and the sign is negative as theory would suggest. Dividend yield also shows a small negative association, while FFO/Assets is positive but not statistically different from zero. Overall, the low R² values mean these single-variable models explain very little of the return variation.

**What we would do next:**
- Extend to multiple regression (include two or more predictors)
- Test for heteroskedasticity and other OLS assumption violations
- Examine whether relationships vary by time period or REIT sector

---

## Reproducibility Checklist
- [x] Script runs end-to-end without errors
- [x] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [x] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [x] Report accurately reflects regression results
- [x] All interpretations are in economic units (not just statistical jargon)

