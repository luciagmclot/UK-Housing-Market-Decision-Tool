# UK Housing Market Decision Tool

> **University of Aberdeen | Mathematics Group Project | 2026**

**This project was developed collaboratively as a three-person university group project.**  
This repository has been organised as a portfolio version of the project and preserves the different stages of development to demonstrate how the mathematical model and user-facing application evolved over time.

---

## Overview

The **UK Housing Market Decision Tool** is a quantitative decision-support project designed to help explore whether a residential property purchase appears financially reasonable given:

- the property's asking price,
- local housing-market conditions,
- the buyer's income,
- available deposit,
- mortgage interest rate,
- loan term,
- financial leverage,
- and historical market behaviour.

The project began as a mathematical housing-price model based on stochastic processes and progressively evolved into a broader property decision tool combining **market valuation, mortgage affordability, risk analysis and probabilistic forecasting**.

The final version presents the model through an interactive browser-based interface designed to make the outputs understandable to non-technical users.

---

## Project Objective

The project evolved around three practical questions:

> **Is this property reasonably priced relative to its local market?**

> **Can the buyer realistically afford the mortgage?**

> **What risks might affect the property over the next five years?**

Rather than attempting to perfectly predict future house prices, the model provides a structured framework for analysing a potential property purchase from several different perspectives.

---

## Final Model

The final V4 model combines five main areas of analysis.

### 1. Local Market Valuation

The asking price is compared with county-level housing statistics including:

- median property price,
- lower quartile (Q1 / 25th percentile),
- upper quartile (Q3 / 75th percentile),
- transaction count,
- historical yearly median prices.

The property is then classified as broadly:

- **Cheap**
- **Typical**
- **Overpriced**

relative to the local market distribution.

---

### 2. Mortgage Affordability

The model calculates:

- required mortgage amount,
- monthly mortgage payment,
- payment-to-income ratio,
- total repayment,
- total interest cost.

The affordability assessment considers how much of the buyer's monthly income would be required to service the mortgage.

The model distinguishes between:

- comfortable affordability,
- moderate financial pressure,
- high financial pressure.

---

### 3. Loan-to-Value and Financing Risk

The model calculates the **Loan-to-Value ratio (LTV)**:

\[
LTV = \frac{\text{Mortgage Loan}}{\text{Property Price}}
\]

This provides an indication of the amount of leverage used in the purchase.

Higher LTV values imply greater dependence on borrowed capital and therefore potentially greater financial exposure.

---

### 4. Market Trend and Risk Analysis

Historical county-level data are used to calculate and analyse:

- yearly median house prices,
- annual growth,
- log returns,
- Compound Annual Growth Rate (CAGR),
- market volatility,
- market direction.

These metrics allow the property assessment to consider the wider behaviour of the local housing market rather than evaluating affordability alone.

---

### 5. Five-Year Monte Carlo Forecast

The final model introduces a probabilistic five-year outlook using **Geometric Brownian Motion**.

The simulation uses historical county-level:

- average log return,
- volatility,
- current property value.

The general structure is:

\[
P_T =
P_0
\exp
\left[
(\mu-\frac{1}{2}\sigma^2)T
+
\sigma\sqrt{T}Z
\right]
\]

where:

- \(P_0\) = current property value
- \(\mu\) = estimated historical log return
- \(\sigma\) = historical volatility
- \(T\) = forecast horizon
- \(Z\) = standard normally distributed random variable

The application runs **5,000 simulated paths** and estimates:

- median future value,
- forecast distribution,
- downside and upside ranges,
- probability of the property increasing in value,
- probability of the property decreasing in value.

This should be interpreted as a **scenario model rather than a prediction of future house prices**.

---

## Interest Rate Stress Testing

Mortgage affordability is also tested under changing interest-rate environments.

The application compares the current mortgage payment with scenarios where rates increase by:

- **+1 percentage point**
- **+2 percentage points**

This allows the user to see how sensitive their monthly payments and payment-to-income ratio are to changes in borrowing costs.

---

## Composite Buyer Score

The final model combines several indicators into a score between **0 and 100**.

The score considers:

- property price relative to the local market,
- affordability,
- payment-to-income ratio,
- Loan-to-Value,
- historical market growth,
- volatility,
- probability of future appreciation.

The model then converts the score into a simple assessment such as:

- **Strong Buy**
- **Reasonable Buy**
- **Caution**
- **High Risk**

These classifications are model outputs and should not be interpreted as financial advice.

---

# Interactive Application

The final browser application contains four main sections.

## Area Explorer

Allows the user to select a UK county and examine:

- median property price,
- interquartile price range,
- number of recorded transactions,
- historical trend,
- estimated CAGR,
- comparison with other areas.

## Property Assessment

The main decision tool.

The user enters:

- county,
- property price,
- annual gross income,
- deposit,
- mortgage interest rate,
- mortgage term.

The model then evaluates:

- local price fairness,
- monthly mortgage cost,
- affordability,
- LTV,
- market trend,
- volatility,
- five-year forecast,
- rate sensitivity,
- automatic risk warnings,
- overall buyer score.

## Mortgage Planner

Provides a more focused view of:

- mortgage amount,
- monthly repayment,
- total interest,
- affordability,
- LTV,
- interest-rate stress scenarios.

## Region Compare

Allows multiple UK regions or counties to be compared using metrics such as:

- price growth,
- relative price index,
- absolute property prices,
- regional market indicators.

---

# Development Process

One purpose of this repository is to preserve the development process rather than displaying only the final result.

The model went through several distinct iterations.

## V1 — Stochastic Housing Model

The first version explored housing prices through a stochastic differential equation.

The conceptual model was:

\[
\frac{dP_t}{P_t}
=
(\alpha-\beta r+\gamma C)dt+\sigma dW_t
\]

where housing-price movements were influenced by:

- baseline growth,
- interest-rate pressure,
- credit expansion,
- random market shocks.

At this stage the model used simulated values rather than real housing data.

The purpose of V1 was primarily to explore the mathematical behaviour of a stochastic housing market.

---

## V2 — Housing Decision Model

The project then changed direction.

Instead of modelling an abstract housing market, the objective became to build a tool capable of helping a potential buyer assess a real property.

V2 introduced:

- county-level market statistics,
- median and quartile analysis,
- asking-price classification,
- mortgage calculations,
- payment-to-income ratios,
- Loan-to-Value,
- market trend analysis,
- buyer scoring,
- human-readable outputs.

This represented the transition from a mathematical simulation to a **decision-support model**.

---

## V3 — User-Facing Model

V3 began transforming the quantitative model into something that could be used by a non-technical user.

Inputs included:

- county,
- property price,
- income,
- deposit,
- mortgage rate,
- mortgage term.

The interface translated mathematical outputs into clearer assessments covering:

- purchase assessment,
- monthly mortgage cost,
- affordability,
- LTV,
- buyer score,
- explanatory text.

---

## V4 — Advanced Decision Model

V4 expanded the model substantially.

It incorporated:

- improved market statistics,
- CAGR,
- log returns,
- volatility,
- mortgage stress testing,
- five-year projections,
- Monte Carlo simulation,
- probability of price appreciation/depreciation,
- risk warnings,
- composite scoring,
- human-readable explanations.

This became the basis for the final browser application included in this repository.

---

# Testing and Validation

Testing was carried out throughout development.

### Data Integrity

Checks included:

- inspecting the available county data,
- reviewing sample observations,
- checking county names,
- validating date formats,
- confirming that required variables were available.

### Statistical Checks

The project compared mean and median housing prices and identified cases where extreme values could distort averages.

Median-based aggregation was therefore used extensively to create more robust local-market measures.

### Scenario Testing

Model behaviour was tested by changing:

- asking price,
- income,
- deposit,
- interest rate,
- county.

The expected financial relationships were checked, including:

- higher property prices increasing mortgage pressure,
- higher income improving affordability,
- larger deposits reducing LTV,
- higher interest rates increasing monthly payments.

### Boundary Testing

Important thresholds were tested around:

- payment-to-income ratios,
- high Loan-to-Value values,
- affordability classifications.

### Forecast Validation

Forecasting outputs were checked by reviewing:

- historical trends,
- growth calculations,
- volatility,
- simulated future-value distributions.

The objective was not to prove that future values could be predicted accurately, but to ensure that the model behaved consistently with its mathematical assumptions.

---

# Repository Structure

```text
UK-Housing-Market-Decision-Tool/
│
├── README.md
│
├── docs/
│   └── development-notes.md
│
├── notebooks/
│   ├── 01_housing_model_v1_county_prices.ipynb
│   ├── 02_housing_model_v2.ipynb
│   ├── 03_housing_model_v3.ipynb
│   └── 04_housing_market_v4.ipynb
│
└── web/
    ├── 01_home_guide_prototype.html
    ├── 02_home_guide_v4_prototype.html
    ├── index.html
    ├── county_stats.js
    └── reit_data.js
