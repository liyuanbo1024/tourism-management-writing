# Quantitative Methods in Tourism Research

This reference covers the core quantitative methodologies used in top-tier tourism journals. Each method is presented with its specification, diagnostics, reporting standards, and common mistakes to avoid.

---

## 1. Tourism Demand Modeling

Tourism demand modeling is the backbone of quantitative tourism economics. The dominant approaches are time-series models and structural models.

### 1.1 Autoregressive Integrated Moving Average (ARIMA)

**Purpose**: Forecasting tourist arrivals, tourism receipts, or occupancy rates using only historical patterns of the series itself.

**Specification**:
```
ARIMA(p, d, q) where:
- p: autoregressive order (lags of the dependent variable)
- d: order of integration (number of differencing to achieve stationarity)
- q: moving average order (lags of forecast errors)
```

**Model Selection Protocol**:

1. **Unit Root Testing**: Apply ADF (Augmented Dickey-Fuller) test and KPSS test. The ADF null is "unit root present" (non-stationary); the KPSS null is "series is stationary." Use both — if ADF fails to reject and KPSS rejects, the series is non-stationary and requires differencing. Report both test statistics and their 5% critical values.

2. **Order Selection**: Use AIC, BIC, and AICc (corrected AIC for small samples). Never report only one criterion. The BIC penalizes complexity more heavily and tends to select more parsimonious models — this is usually preferred for forecasting. State: "Model selection was based on minimising the AICc, with the AIC and BIC reported for robustness."

3. **Seasonality**: Tourism data is almost always seasonal. Test for seasonal unit roots using the HEGY test before applying seasonal differencing. Specify SARIMA(p,d,q)(P,D,Q)s where s=12 for monthly data or s=4 for quarterly data.

**Diagnostics**:
- **Residual autocorrelation**: Ljung-Box Q-statistic on residuals at multiple lags (report lags 12, 24, 36 for monthly data). Null hypothesis: residuals are independently distributed.
- **Residual normality**: Jarque-Bera test. Not strictly required for ARIMA consistency but relevant for prediction intervals.
- **ARCH effects**: Engle's ARCH-LM test on squared residuals. If significant, consider ARIMA-GARCH models.
- **Parameter stability**: CUSUM and CUSUM-of-squares tests (Brown, Durbin, and Evans 1975).

**Reporting Standard**:
> We estimated an ARIMA(2,1,1)(1,0,1)[12] model for monthly international tourist arrivals to Thailand (January 2000–December 2023). The ADF test statistic of -2.14 (5% critical value: -2.86) confirmed non-stationarity in levels; first-differencing achieved stationarity (ADF = -8.76, p < 0.01). The Ljung-Box Q-statistic at lag 24 was 18.43 (p = 0.78), indicating no residual autocorrelation. The model achieved a MAPE of 4.2% in the hold-out sample (January 2022–December 2023).

**Common Mistakes**:
1. Applying seasonal differencing without testing for seasonal unit roots
2. Using only the ADF test without complementary KPSS test
3. Reporting only AIC without considering BIC for parsimony
4. Ignoring structural breaks (2008 financial crisis, COVID-19) — use Bai-Perron test for unknown breakpoints
5. Failing to report out-of-sample forecasting performance with multiple metrics (MAPE, RMSE, MAE)

### 1.2 Vector Autoregression (VAR)

**Purpose**: Modeling the dynamic interdependencies among multiple tourism-related variables (e.g., tourist arrivals, exchange rates, income, relative prices).

**Specification**:
```
Y_t = A_1 Y_{t-1} + A_2 Y_{t-2} + ... + A_p Y_{t-p} + C X_t + ε_t
where Y_t is a k-vector of endogenous variables, and X_t is a vector of exogenous variables.
```

**Pre-Estimation Protocol**:
1. **Order of integration**: Apply ADF and KPSS to each variable. If all variables are I(1), test for cointegration before proceeding.
2. **Cointegration testing**: Johansen trace and maximum eigenvalue tests. If cointegrated, use a VECM. If not, estimate VAR in first differences. Report both the trace and max-eigenvalue statistics with their 5% critical values.
3. **Lag length selection**: Report LR, FPE, AIC, SC (BIC), and HQ. Use majority rule when criteria disagree. For tourism data (often monthly), test up to lag 12 and include seasonality.

**Post-Estimation Diagnostics**:
- **Granger causality tests**: Report F-statistics and p-values for each block of equations. "A variable X Granger-causes Y if lagged values of X help predict Y beyond lagged values of Y alone."
- **Impulse response functions (IRFs)**: Report orthogonalized IRFs with Cholesky decomposition. **Critical**: Justify the ordering of variables. In tourism demand, order from most to least exogenous: world GDP → relative prices → exchange rate → tourism demand. Report IRFs with 95% confidence bands (bootstrap or analytical). Show both accumulated and non-accumulated responses.
- **Forecast error variance decomposition (FEVD)**: Report the proportion of forecast error variance in tourist arrivals attributable to each shock at horizons 1, 4, 8, and 12 quarters (or equivalent).
- **Inverse roots of AR characteristic polynomial**: All roots must lie inside the unit circle for stability.
- **Residual diagnostics**: LM test for serial correlation at the lag order; normality test (Doornik-Hansen).

**Reporting Standard**:
> A VAR(4) model was estimated on monthly data for tourist arrivals (TA), real effective exchange rate (REER), and GDP of major source markets (GDP). The Johansen trace test indicated one cointegrating vector (trace statistic = 35.42, 5% CV = 29.80), leading us to specify a VECM. Granger causality tests revealed that REER Granger-causes TA (F = 7.34, p < 0.01) but TA does not Granger-cause REER (F = 1.12, p = 0.34). The FEVD at the 12-month horizon showed that REER shocks account for 28% of the forecast error variance in tourist arrivals.

**Common Mistakes**:
1. Using Cholesky decomposition without justifying or testing alternative orderings
2. Reporting IRFs without confidence bands
3. Failing to test for cointegration before estimating VAR in levels
4. Including too many variables relative to sample size (rule: T ≥ 50 + kp, where k = variables, p = lags)
5. Interpreting Granger causality as economic causality (it is predictive causality only)

### 1.3 Autoregressive Distributed Lag Model (ARDL)

**Purpose**: Estimating long-run relationships between tourism demand and its determinants, especially with mixed I(0)/I(1) variables.

**Bounds Testing Approach (Pesaran, Shin, and Smith 2001)**:

**Specification**:
```
ΔTA_t = α_0 + Σ β_i ΔTA_{t-i} + Σ γ_j ΔX_{t-j} + θ_1 TA_{t-1} + θ_2 X_{t-1} + ε_t
```
where the long-run coefficients are recovered as -(θ_2/θ_1).

**Protocol**:
1. **Stationarity pre-test**: Confirm no variable is I(2) — the bounds test is invalid if any variable is I(2).
2. **Lag selection**: Use AIC or SBC with maximum lag determined by data frequency (max 12 for monthly, 4 for quarterly).
3. **Bounds F-test**: Compare F-statistic to Pesaran et al. (2001) critical value bounds (or Narayan 2005 for small samples, T < 80). If F > upper bound, cointegration exists. If F < lower bound, no cointegration. If F is between bounds, the test is inconclusive.
4. **Diagnostics** (all must pass for valid inference):
   - Serial correlation: Breusch-Godfrey LM test
   - Functional form: Ramsey RESET test
   - Normality: Jarque-Bera test
   - Heteroskedasticity: Breusch-Pagan-Godfrey test
   - Parameter stability: CUSUM and CUSUMSQ tests

**Reporting Standard**:
> We employed the ARDL bounds testing approach to examine the long-run relationship between tourism demand (TA) and its determinants. The unit root tests confirmed that TA and relative price (RP) are I(1), while income (GDP) is I(0), satisfying the bounds test requirement of no I(2) variables. The AIC selected an ARDL(3,2,4) specification. The computed F-statistic of 6.84 exceeds the upper bound critical value of 5.06 at the 1% level (Narayan 2005, Case III: unrestricted intercept, no trend, n=120), confirming a long-run relationship. The long-run income elasticity is 1.42 (t = 8.13, p < 0.01), indicating that tourism is a luxury good in this context.

**Common Mistakes**:
1. Applying the bounds test without confirming no variable is I(2)
2. Using asymptotic critical values (Pesaran et al. 2001) with small samples (< 80 obs) — use Narayan (2005)
3. Ignoring structural breaks — consider the augmented ARDL with a break dummy
4. Reporting long-run coefficients without reporting the bounds cointegration test first
5. Failing to conduct post-estimation diagnostics (serial correlation invalidates the bounds test)

### 1.4 Gravity Models for Tourism Flows

**Purpose**: Modeling bilateral tourism flows as a function of origin and destination characteristics, distance, and other bilateral factors.

**Specification**:
```
ln(TA_{ijt}) = α + β_1 ln(GDP_{it}) + β_2 ln(GDP_{jt}) + β_3 ln(DIST_{ij}) + β_4 ln(POP_{it}) + β_5 ln(POP_{jt})
               + γ_1 CONTIG_{ij} + γ_2 COMLANG_{ij} + γ_3 COLONY_{ij} + γ_4 COMMON_RELIGION_{ij}
               + γ_5 VISA_{ijt} + γ_6 DIRECT_FLIGHT_{ijt} + δ_i + δ_j + δ_t + ε_{ijt}
```

**Estimation Protocol**:

1. **Multilateral resistance terms (MRTs)** are non-negotiable in modern gravity estimation (Anderson and van Wincoop 2003). Three approaches:
   - **Origin-time and destination-time fixed effects** (recommended, PPML-compatible)
   - **Baier-Bergstrand (2009) approximation**: First-order Taylor series linearization of MRTs
   - **Bonus vetus** method: Include remoteness indices as explicit regressors (not recommended)

2. **Zero flows**: Tourism bilateral flows often contain zeros (no tourism from origin i to destination j). The log-linear OLS model drops zeros, creating selection bias. Solutions:
   - **PPML (Poisson Pseudo Maximum Likelihood)**: Santos Silva and Tenreyro (2006). Estimates the model in multiplicative form, naturally handles zeros, and is robust to heteroskedasticity. This is the current gold standard.
   - **Negative binomial**: Alternative when overdispersion is severe.
   - **Heckman two-stage**: Selection equation + outcome equation (used before PPML became standard).
   - **Tobit**: Not recommended; inconsistent under heteroskedasticity.

3. **Distance measures**: Report which distance measure is used. Great-circle distance between capitals is standard but increasingly replaced by:
   - Population-weighted distances
   - Travel time (driving, flight hours)
   - Cultural distance (Hofstede, GLOBE, or Kogut-Singh index)
   - Psychic distance

**Diagnostics**:
- **RESET test**: Applied to PPML models — a significant RESET indicates misspecification.
- **Overdispersion test**: For count models, test α in negative binomial against Poisson (α=0).
- **Heteroskedasticity-robust standard errors**: Always report. For PPML, use robust/clustered SEs.
- **Clustered standard errors**: Cluster by country pair (ij) as a minimum; consider multi-way clustering (origin-year, destination-year, pair).

**Reporting Standard**:
> We estimate a structural gravity model of bilateral tourism flows for 189 origin countries and 156 destination countries over 2000-2023 using PPML with origin-year and destination-year fixed effects. The model includes 1.2 million observations, of which 34% are zero flows. The GDP elasticity at origin is 0.87 (SE = 0.04, p < 0.01), consistent with tourism as a normal good. The distance elasticity is -1.43 (SE = 0.03, p < 0.01). A common language increases tourism flows by 42% [exp(0.35)-1], while a visa requirement reduces flows by 25% [exp(-0.29)-1].

**Common Mistakes**:
1. Estimating log-linear OLS without addressing zeros (biased and inconsistent)
2. Omitting multilateral resistance terms (biased estimates of distance and border effects)
3. Using cross-sectional gravity without time fixed effects
4. Interpreting coefficients on GDP as elasticities in a PPML without noting the semi-elasticity interpretation for dummy variables
5. Failing to cluster standard errors by country pair

### 1.5 Panel Data Methods

Tourism research increasingly uses panel data — repeated observations on the same cross-sectional units (countries, regions, hotels, destinations). Panel data enables controlling for unobserved heterogeneity.

#### 1.5.1 Pooled OLS

**When appropriate**: When there is no unobserved heterogeneity across units (unlikely in tourism applications). Always test against fixed effects.

**Check**: "If unobserved time-invariant heterogeneity is present, pooled OLS is biased and inconsistent."

#### 1.5.2 Fixed Effects (FE) Estimator

**Purpose**: Controls for time-invariant unobserved heterogeneity at the unit level (e.g., destination-specific cultural appeal, hotel-specific location quality). Also controls for time fixed effects (e.g., global macroeconomic shocks, COVID-19).

**Specification**:
```
Y_{it} = α_i + β X_{it} + δ_t + ε_{it}
```
where α_i is the unit-specific effect (correlated with X_{it}) and δ_t is the time effect.

**Key Diagnostics**:
1. **F-test for individual effects**: H0: all α_i = 0 (i.e., pooled OLS is appropriate). Report F-statistic and p-value.
2. **F-test for time effects**: H0: all δ_t = 0. Report both tests.
3. **Hausman test**: H0: RE is consistent and efficient (i.e., α_i uncorrelated with X_{it}). If p < 0.05, reject RE in favor of FE. Report χ² statistic, df, and p-value.
4. **Modified Wald test for groupwise heteroskedasticity**: FE assumes homoskedasticity. In tourism panels (large N, small T), heteroskedasticity is common. Use cluster-robust standard errors clustered at the unit level.
5. **Wooldridge test for serial correlation**: In panels with T > 10, test for AR(1) errors. If present, use cluster-robust SEs or Newey-West standard errors.

**Reporting Standard**:
> We estimated a two-way fixed effects model of hotel occupancy rates across 250 hotels over 60 months (T=60, N=250). The F-test strongly rejected the null of no individual effects (F(249, 14720) = 34.2, p < 0.01) and no time effects (F(59, 14720) = 12.8, p < 0.01). The Hausman test rejected the random effects estimator (χ²(8) = 156.3, p < 0.01). Standard errors are clustered at the hotel level to account for heteroskedasticity and serial correlation (Wooldridge test: F(1, 249) = 87.4, p < 0.01). The coefficient on the online review score is 0.042 (SE = 0.008, p < 0.01), indicating that a one-unit increase in review score is associated with a 4.2% increase in the occupancy rate.

#### 1.5.3 Random Effects (RE) Estimator

**When appropriate**: When α_i is uncorrelated with regressors (Hausman test not rejected), or when time-invariant variables are of substantive interest (e.g., country location, cultural distance).

**Key Diagnostic**: Breusch-Pagan LM test: H0: σ²_α = 0 (no panel-level variance component). Rejection justifies RE over pooled OLS.

#### 1.5.4 Dynamic Panel GMM (Arellano-Bond / Arellano-Bover / Blundell-Bond)

**Purpose**: When the dependent variable depends on its own past values (e.g., tourism arrivals exhibit persistence due to habit formation, word-of-mouth, and repeat visitation) AND the panel has small T relative to N.

**Specification** (Arellano-Bond Difference GMM):
```
Y_{it} = γ Y_{i,t-1} + β X_{it} + α_i + ε_{it}
```
First-differenced to eliminate α_i:
```
ΔY_{it} = γ ΔY_{i,t-1} + β ΔX_{it} + Δε_{it}
```
Lagged levels (Y_{i,t-2}, Y_{i,t-3}, ...) serve as instruments for ΔY_{i,t-1}.

**Specification (System GMM, Blundell-Bond)**:
Adds the levels equation instrumented with lagged differences, improving efficiency when Y is persistent.

**Diagnostics (non-negotiable)**:
1. **AR(2) test** (Arellano-Bond): H0: no second-order serial correlation in first-differenced errors. The estimator allows AR(1) but NOT AR(2). Report z-statistic and p-value.
2. **Hansen J-test of overidentifying restrictions**: H0: instruments are valid (exogenous). Report χ² statistic, df, and p-value. CRITICAL: p > 0.05 but NOT p > 0.25 (too many instruments inflate the Hansen p-value). Report the instrument count.
3. **Difference-in-Hansen test**: Tests the validity of the additional moment conditions in System GMM relative to Difference GMM.
4. **Instrument count**: Must be less than N. If instrument count > N, the Hansen test is unreliable. Use the `collapse` option in Stata or limit lag depth.

**Reporting Standard**:
> We employ the system GMM estimator to examine the persistence of tourism demand. The dependent variable (tourist arrivals) is strongly persistent (the lagged dependent variable coefficient in OLS is 0.82), motivating a dynamic specification. The two-step system GMM estimator with Windmeijer-corrected standard errors is reported. The AR(2) test fails to reject the null of no second-order serial correlation (z = -1.12, p = 0.26). The Hansen J-test does not reject instrument validity (χ²(38) = 42.3, p = 0.29). The instrument count (44) is well below the number of cross-sectional units (N=150). The coefficient on lagged tourist arrivals is 0.61 (SE = 0.09, p < 0.01), confirming substantial persistence.

**Common Mistakes in Dynamic Panel**:
1. Reporting only one-step results (two-step with Windmeijer correction is standard)
2. Instrument proliferation: using all available lags without restricting them. Always report the instrument count relative to N.
3. Hansen p-value approaching 1.0 (p > 0.50 is suspicious — likely due to instrument proliferation)
4. Not reporting the AR(2) test
5. Using system GMM when difference GMM is appropriate (check if the dependent variable is close to a random walk — then system GMM's extra moment conditions are weak)
6. Failing to use forward orthogonal deviations (preferable to first differencing in unbalanced panels with gaps)

---

## 2. Structural Equation Modeling (SEM)

SEM is one of the most widely used methods in top tourism journals for testing relationships among latent constructs (e.g., destination image → satisfaction → loyalty).

### 2.1 Covariance-Based SEM (CB-SEM)

**Software**: AMOS, LISREL, Mplus, lavaan (R)

**Purpose**: Theory testing — confirmatory. CB-SEM aims to reproduce the observed covariance matrix with a theoretical model. It is a "hard" test of theory.

**Specification Components**:

1. **Measurement Model**: The relationship between latent constructs and their observed indicators.
   ```
   x = Λ_x ξ + δ    (exogenous indicators)
   y = Λ_y η + ε    (endogenous indicators)
   ```
   where Λ are loading matrices, ξ are exogenous latent constructs, η are endogenous latent constructs, and δ and ε are measurement errors.

2. **Structural Model**: The relationship among latent constructs.
   ```
   η = B η + Γ ξ + ζ
   ```
   where B are structural coefficients among endogenous constructs, Γ are coefficients from exogenous to endogenous constructs.

**Fit Indices and Their Thresholds**:

| Fit Index | Abbreviation | Good Fit | Acceptable Fit | Notes |
|-----------|-------------|----------|----------------|-------|
| Chi-square / df | χ²/df | < 2.0 | < 3.0 | Sensitive to sample size. In large samples (N > 400), almost always significant. Report but do not rely solely on this. |
| Comparative Fit Index | CFI | ≥ 0.95 | ≥ 0.90 | Incremental fit. Compares to null model. Preferred to GFI in small samples. |
| Tucker-Lewis Index | TLI (NNFI) | ≥ 0.95 | ≥ 0.90 | Rewards parsimony. Can exceed 1.0. |
| Root Mean Square Error of Approximation | RMSEA | < 0.05 | < 0.08 | Absolute fit. Report 90% CI. Upper bound of 90% CI should be ≤ 0.08. |
| Standardized Root Mean Square Residual | SRMR | < 0.05 | < 0.08 | Absolute fit. Less affected by sample size. |
| Goodness of Fit Index | GFI | ≥ 0.95 | ≥ 0.90 | Similar to R² in regression but for the measurement model. |
| Adjusted Goodness of Fit | AGFI | ≥ 0.90 | ≥ 0.85 | GFI adjusted for df. |

**Reporting Protocol**:
> The measurement model demonstrated adequate fit: χ²(142) = 315.64, p < 0.01; χ²/df = 2.22; CFI = 0.96; TLI = 0.95; RMSEA = 0.052 (90% CI: 0.044–0.060); SRMR = 0.041. Although the chi-square was significant (expected with N=582), all other indices met or exceeded recommended thresholds (Hu and Bentler 1999).

**Validity Assessment**:
1. **Convergent validity**: AVE > 0.50 for each construct; CR (composite reliability) > 0.70; all standardized loadings > 0.50 and significant (p < 0.05).
2. **Discriminant validity**: (a) Fornell-Larcker criterion: AVE for each construct > squared correlation with any other construct. (b) HTMT (Heterotrait-Monotrait ratio) < 0.85 (or < 0.90 for conceptually similar constructs).
3. **Construct reliability**: Cronbach's alpha > 0.70 (traditional) but CR (composite reliability) > 0.70 is preferred as it does not assume equal loadings.

**Common Mistakes in CB-SEM**:
1. Reporting a non-significant chi-square as the primary evidence of good fit (it's sample-size dependent)
2. Cherry-picking fit indices — report at minimum: χ², df, χ²/df, CFI, TLI, RMSEA (with 90% CI), SRMR
3. Modifying the model based on modification indices without theoretical justification (capitalization on chance)
4. Using single-indicator latent variables without fixing measurement error (set error variance to (1-α)×σ²)
5. Reporting standardized estimates without reporting unstandardized estimates and SEs
6. Ignoring Heywood cases (negative variance estimates or standardized loadings > 1.0)

### 2.2 Partial Least Squares SEM (PLS-SEM)

**Software**: SmartPLS, WarpPLS, plspm (R), SEMinR (R)

**Purpose**: Prediction-oriented — maximizing explained variance (R²) in endogenous constructs. PLS-SEM is a "soft" modeling approach that is more forgiving of non-normal data, small samples, and formative indicators.

**When to Use PLS-SEM vs. CB-SEM** (Hair et al. 2019 decision criteria):

| Criterion | Prefer PLS-SEM | Prefer CB-SEM |
|-----------|---------------|---------------|
| Research objective | Prediction and theory development | Theory testing and confirmation |
| Measurement model | Includes formative constructs | All constructs are reflective |
| Structural model | Complex (many constructs, many paths) | Simple to moderate complexity |
| Sample size | Small relative to model complexity | Large (N > 200 minimum) |
| Data distribution | Non-normal | Multivariate normal |
| Model fit assessment | Limited (no global GoF index) | Comprehensive fit indices |

**PLS-SEM Reporting Standards**:

1. **Measurement Model Assessment** (reflective):
   - Loadings > 0.708 (or > 0.70 for established scales, > 0.40 acceptable for exploratory research)
   - Internal consistency: CR (ρc) 0.70–0.95; Cronbach's alpha as a lower bound
   - Convergent validity: AVE > 0.50
   - Discriminant validity: HTMT < 0.85 (strict) or < 0.90 (liberal). Report HTMT confidence intervals (bias-corrected bootstrap).

2. **Measurement Model Assessment** (formative):
   - Indicator weights and their significance (not loadings)
   - Collinearity assessment: VIF < 5.0 (ideally < 3.3) for all indicators
   - Indicator relevance: if weight is non-significant but loading > 0.50, retain the indicator (it has absolute importance)

3. **Structural Model Assessment**:
   - Collinearity among predictor constructs: VIF < 5.0
   - Path coefficients (β): report unstandardized AND standardized
   - Significance: bootstrap percentile and bias-corrected CIs (report both)
   - R²: 0.75 (substantial), 0.50 (moderate), 0.25 (weak) — Hair et al. 2011 thresholds
   - f² effect size: 0.02 (small), 0.15 (medium), 0.35 (large)
   - Q² predict (Stone-Geisser): > 0 (predictive relevance), > 0.25 (medium), > 0.50 (large)
   - PLSpredict: Compare RMSE/MAE from PLS to naive benchmark (LM). Lower PLS prediction errors indicate predictive power.

**Common Mistakes in PLS-SEM**:
1. Using the Fornell-Larcker criterion (not robust — always use HTMT)
2. Reporting GoF (Tenenhaus et al. 2005) — it has been shown to be conceptually flawed
3. Failing to distinguish between formative and reflective measurement — a critical conceptual error
4. Using PLS-SEM "because the sample is small" without justifying why CB-SEM is infeasible (PLS-SEM also has minimum sample size requirements: the "10 times rule" — max(indicators per construct, structural paths to a construct) × 10)
5. Reporting only p-values without bootstrap CIs and effect sizes

---

## 3. Discrete Choice Experiments (DCE) for Destination Choice

**Purpose**: Eliciting tourist preferences for destination attributes by observing choices in hypothetical scenarios. Grounded in random utility theory (McFadden 1974).

**Design Protocol**:

1. **Attribute and Level Selection**: Identify 4-7 attributes through qualitative pre-testing (focus groups, literature review). Each attribute has 2-4 levels. Example:
   - Beach quality (low, medium, high)
   - Accommodation type (hotel, resort, Airbnb)
   - Price per night ($100, $200, $350, $500)
   - Distance to attractions (< 30 min, 30-60 min, > 60 min)
   - Crowdedness (low, moderate, high)

2. **Experimental Design**:
   - **Full factorial**: k attributes × L_k levels = product of all combinations. With 5 attributes at 3 levels: 3⁵ = 243 profiles — impractical.
   - **Fractional factorial**: Orthogonal or efficient designs. D-efficient designs minimize the D-error (determinant of the asymptotic variance-covariance matrix). Report the design efficiency (D-error).
   - **Blocking**: Assign choice sets to blocks to reduce respondent burden (typically 8-12 choice sets per respondent).
   - **Opt-out option**: Always include a "neither" or "I would not travel to either destination" alternative to avoid forced-choice bias.

3. **Choice Set Construction**: Each choice set presents 2-3 alternatives (unlabeled or labeled) + opt-out. Example format:
   ```
   | Attribute | Destination A | Destination B | Neither |
   |-----------|---------------|---------------|---------|
   | Beach     | High quality  | Medium quality|    ○    |
   | Price     | $200/night    | $350/night    |         |
   | Distance  | 30-60 min     | < 30 min      |         |
   ```

**Estimation**:
1. **Multinomial Logit (MNL)**: Baseline model. Assumes IIA (independence of irrelevant alternatives). Report log-likelihood, McFadden's pseudo-R², and AIC/BIC.
2. **Mixed Logit (MXL) / Random Parameters Logit**: Relaxes IIA by allowing preference heterogeneity. Parameters are assumed to follow a distribution (normal, lognormal, triangular). Report means and standard deviations of random parameters. Use Halton draws (≥ 500) for simulation.
3. **Latent Class Model (LCM)**: Identifies unobserved segments with homogeneous preferences. Report: number of classes (determined by BIC, CAIC, and interpretation), class membership probabilities, and class-specific utility parameters.
4. **Hybrid Choice Models**: Integrate latent variables (e.g., environmental attitudes, destination image) into the choice model.

**Key Outputs to Report**:
- **Willingness to Pay (WTP)**: Marginal WTP for each attribute = -(β_attribute / β_price). Report mean WTP with Delta method or Krinsky-Robb confidence intervals.
- **Relative importance**: Share of each attribute in total utility variation.
- **Choice probabilities**: Predicted market shares for different destination profiles.

**Reporting Standard**:
> A D-efficient design with 24 choice sets blocked into 3 survey versions (8 choice sets per respondent) was generated using Ngene. Each choice set comprised two unlabeled destination profiles and an opt-out alternative. A mixed logit model with 1000 Halton draws was estimated. All price coefficients were specified as fixed; non-price attributes were specified as normally distributed. The mean WTP for high beach quality was $78.50/night (95% CI: $62.30–$94.70). The estimated standard deviation of the beach quality coefficient was significant (SD = 1.23, p < 0.01), indicating substantial preference heterogeneity. McFadden's pseudo-R² was 0.24, indicating good model fit for choice data.

**Common Mistakes**:
1. Omitting the opt-out alternative (forces choice, inflates WTP estimates)
2. Using orthogonal designs when priors are available (D-efficient designs are more efficient)
3. Failing to test for scale heterogeneity (Hess and Rose 2012)
4. Reporting WTP without confidence intervals (the Delta method underestimates; use Krinsky-Robb or bootstrap)
5. Using only MNL without testing for IIA violation (Hausman-McFadden test)

---

## 4. Conjoint Analysis for Tourism Attributes

**Purpose**: Decomposing overall preference for a tourism product/service into part-worth utilities of its attributes. Used for destination positioning, hotel service design, and event feature optimization.

**Types**:
1. **Traditional (Full-Profile) Conjoint**: Respondents rank or rate full profiles. Less common now.
2. **Choice-Based Conjoint (CBC)**: Respondents choose among profiles — most common in tourism. (Closely related to DCE; see Section 3.)
3. **Adaptive Conjoint Analysis (ACA)**: Computer-administered, adapts to respondent preferences.
4. **Menu-Based Choice (MBC)**: Respondents choose combinations of attributes (e.g., selecting multiple activities from a menu).

**Analysis Outputs**:
- **Part-worth utilities**: Attribute-level contributions to total utility
- **Importance scores**: Relative importance of each attribute (% of total utility range)
- **Market simulations**: First-choice, share of preference, or randomized first-choice rules
- **Segmentation**: Interaction effects or latent class analysis to identify preference segments

---

## 5. Importance-Performance Analysis (IPA)

**Purpose**: Identifying which destination attributes should be prioritized for management attention based on their importance to tourists and perceived performance.

**Basic IPA Framework (Martilla and James 1977)**:

| | Low Performance | High Performance |
|---|---|---|
| **High Importance** | Concentrate Here (Quadrant I) | Keep Up the Good Work (Quadrant II) |
| **Low Importance** | Low Priority (Quadrant III) | Possible Overkill (Quadrant IV) |

**Extensions**:

1. **IPA with Gap Analysis**: Compute importance-performance gaps: Gap = P − I. Negative gaps in Quadrant I are high priority. Report using paired t-tests for statistical significance.

2. **Revised IPA (Deng 2007)**: Uses partial correlation coefficients between attribute performance and overall satisfaction as derived importance (instead of stated importance). This addresses social desirability bias in stated importance ratings.

3. **IPA-Kano Integration**: Classify attributes into Kano categories (basic, performance, excitement) before placing on IPA grid. Basic attributes with low performance require immediate attention (they cause dissatisfaction), while excitement attributes with high performance are differentiators.

4. **Fuzzy IPA**: Incorporates uncertainty in importance and performance ratings using fuzzy set theory. Each attribute is represented by a fuzzy number rather than a single point.

5. **IPA with Competitor Benchmarking**: Overlay competitor performance on the IPA grid to identify competitive advantages and disadvantages.

**Reporting Standard**:
> We conducted an Importance-Performance Analysis of 22 destination attributes among 487 visitors to the destination. The grand means of importance (M=4.21) and performance (M=3.78) were used as crosshair coordinates following the data-centered quadrant approach. Paired t-tests revealed significant negative gaps (p < 0.01) for three attributes in the "Concentrate Here" quadrant: cleanliness of public spaces (gap = -0.94), value for money (gap = -0.87), and visitor information availability (gap = -0.72). These three attributes represent the highest management priority.

**Common Mistakes**:
1. Using the scale midpoint as the crosshair instead of the data-centered mean (the scale midpoint is arbitrary; most tourism ratings are positively skewed)
2. Treating importance as static — importance may change after performance improvements
3. Ignoring the statistical significance of the gap between importance and performance
4. Over-interpreting small differences in attribute positions
5. Failing to acknowledge the ceiling effect: attributes with very high importance have limited room for improvement

---

## 6. Big Data Methods in Tourism

### 6.1 GPS Tracking and Spatial Analysis

**Applications**: Tourist movement patterns, attraction visitation sequences, spatial behavior segmentation.

**Methods**:
- **Kernel density estimation**: Identify hotspots of tourist activity
- **Sequence alignment (optimal matching)**: Cluster tourists by movement sequences
- **Markov chain models**: Transition probabilities between attractions
- **Space-time prisms**: Temporal and spatial constraints on tourist movement
- **Multilevel models**: Nesting GPS tracks within tourists

**Reporting**: Report sampling frequency (temporal resolution), spatial accuracy of GPS device, and participation rate (selection bias concerns — tech-savvy tourists overrepresented).

### 6.2 Social Media Sentiment Analysis

**Applications**: Destination image from UGC, tourist satisfaction from online reviews, crisis communication effectiveness.

**Pipeline**:
1. **Data collection**: API scraping of TripAdvisor, Yelp, Twitter/X, Weibo, Instagram (respect API terms)
2. **Preprocessing**: Tokenization, stemming/lemmatization, stop-word removal, negation handling ("not good" ≠ "good")
3. **Sentiment classification**: Lexicon-based (LIWC, VADER, SentiStrength) vs. ML-based (SVM, Naive Bayes, BERT). Report accuracy, precision, recall, F1-score from a manually labeled validation set (min 500-1000 reviews).
4. **Topic modeling**: LDA (Latent Dirichlet Allocation) to identify latent themes. Report perplexity and coherence scores for topic number selection. Structural Topic Model (STM) allows covariates to influence topic prevalence.
5. **Aspect-based sentiment analysis**: Extracts sentiment toward specific attributes (e.g., "room was clean" but "breakfast was terrible").

**Common Mistakes**:
1. Failing to validate the sentiment classifier on manually labeled data (lexicon-based methods have low accuracy in tourism contexts with domain-specific language)
2. Reporting word clouds as substantive analysis (they are descriptive, not inferential)
3. Ignoring selection bias: online reviewers are not a random sample of tourists
4. Using only positive/negative without neutral classification (tourism reviews are often mixed)

### 6.3 Online Review Analysis (Econometric)

**Methods**:
- **Hedonic pricing models**: Decompose hotel room price into attribute implicit prices, including review scores
- **Panel regressions**: Review characteristics → hotel performance (RevPAR, occupancy)
- **Difference-in-differences**: Causal effect of management responses to reviews on subsequent ratings
- **Regression discontinuity**: Causal effect of crossing rating thresholds (e.g., 3.5→4.0 stars on TripAdvisor)

### 6.4 Machine Learning in Tourism

**Common Applications**:
- **Tourism demand forecasting**: LSTM, GRU neural networks; gradient boosting (XGBoost, LightGBM); random forests. Compare against benchmark ARIMA.
- **Tourist segmentation**: K-means, hierarchical clustering, latent class analysis, self-organizing maps (SOM)
- **Image analytics**: Convolutional neural networks (CNNs) to classify destination image from tourist photos (Flickr, Instagram)
- **Recommendation systems**: Collaborative filtering and content-based filtering for personalized destination/hotel/activity recommendations

**Reporting Standards for ML in Tourism**:
1. Always compare against a non-ML benchmark (ARIMA, linear regression, MNL)
2. Report training/validation/test split (e.g., 70/15/15) — never test on training data
3. Report multiple performance metrics (accuracy alone is insufficient for imbalanced data)
4. For forecasting: use time-series cross-validation (expanding or rolling window), not random k-fold
5. Report hyperparameter tuning procedure (grid search, Bayesian optimization)
6. Discuss interpretability: SHAP values, LIME, partial dependence plots (tourism journals value explanation over pure prediction)

---

## 7. Cross-Cutting Methodological Issues

### 7.1 Common Method Bias (CMB)

Tourism research relies heavily on self-report surveys collected at a single point in time — a classic recipe for CMB.

**Procedural Remedies** (ex ante):
1. Temporal separation of predictor and criterion measurement (collect IVs and DVs at different times)
2. Psychological separation: use different cover stories or sections
3. Different response formats for different constructs (semantic differential vs. Likert)
4. Protect respondent anonymity and reduce evaluation apprehension
5. Counterbalance question order

**Statistical Remedies** (ex post):
1. **Harman's single-factor test**: All items loaded onto a single factor in EFA. If the single factor explains > 50% of variance, CMB is a concern. (Note: this is a diagnostic, not a remedy. It is widely criticized but still requested by reviewers.)
2. **Common latent factor (CLF) in CFA**: Compare the model with and without a CLF. If standardized regression weights change by < 0.20, CMB is not a major concern.
3. **Marker variable technique** (Lindell and Whitney 2001): Include a theoretically unrelated variable. Partial out the marker's correlation from all substantive correlations.
4. **CFA marker technique** (Williams et al. 2010): More sophisticated, uses a marker latent variable to model method variance.

### 7.2 Endogeneity

Tourism models are plagued by endogeneity from simultaneity, omitted variables, and measurement error.

**Common Sources in Tourism**:
- Tourist satisfaction and loyalty are jointly determined
- Destination image both influences and is influenced by visit intention
- Hotel price and quality (star rating) are simultaneously determined

**Solutions**:
1. **Instrumental variables (2SLS)**: Requires valid instrument (relevant AND exogenous). Report first-stage F-statistic > 10 (Stock-Yogo). Report the Sargan/Hansen J-test for overidentifying restrictions.
2. **Control function approach**: For non-linear models (probit/logit), include first-stage residuals as additional regressors.
3. **Propensity score matching (PSM)**: For selection on observables. Report balance tests after matching (standardized mean differences < 0.25).
4. **Regression discontinuity design (RDD)**: For treatment assignment based on a threshold (e.g., marketing campaign for destinations above a certain revenue level). Report McCrary density test for manipulation of the running variable.

### 7.3 Mediation and Moderation

**Mediation Analysis**:
- **Baron and Kenny (1986) causal steps**: Largely superseded but still requested by reviewers.
- **Bootstrapped indirect effect** (Preacher and Hayes 2004, 2008): Preferred. Report the indirect effect (a×b) with bias-corrected bootstrap CI (5000 resamples). If CI excludes zero, mediation is supported. Report the completely standardized indirect effect for comparability.
- **Reporting**: "The indirect effect of destination image on behavioral intention through satisfaction was significant (a×b = 0.24, 95% bias-corrected bootstrap CI: 0.15–0.34). The direct effect remained significant (c' = 0.31, p < 0.01), indicating complementary partial mediation."

**Moderation Analysis**:
- **Interaction terms**: Mean-center continuous variables before creating interaction terms to reduce multicollinearity (though it does not affect the coefficient on the interaction).
- **Simple slopes**: Report the effect of X on Y at −1 SD, mean, and +1 SD of the moderator.
- **Johnson-Neyman technique**: Identifies the range of the moderator where the effect of X on Y is significant.

**Moderated Mediation (Conditional Process Analysis)**:
- Use Hayes' PROCESS macro or structural equation modeling
- Report the index of moderated mediation with bootstrap CI
