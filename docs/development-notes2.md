## Housing Market Basic Model 1.py
This model is the first basic model created using a stochastic differential equation dPt/Pt = (alpha -beta r +gamma C)dt +sigma DWt
The housing price change = baseline growth - interest rate pressure + credit expansion + random market shocks
AT THE MOMENT THIS IS A FAKE HOUSING MARKET WITH FAKE VALUES
Completed in Python
P0 = starting market value
alpha = baseline housing growth rate aka +/- x % growth per year
beta & r is the interest effect and this model subtracts beta x r = interest pressure. The higher rates the more prices fall
Gamma and C are the credit expansion effect. More lending leads to prices rising
sig,a is the market randomness and volatility. bigger means a more chaotic housing market and smaller is the smoother prices. This controls the Brownian Motion
T and dt is the simulation length of time
steps = int(T / dt) time = np.linspace(0, T, steps + 1) creates a time grid and basically goes from 0 to x years in tiny steps
P = np.zeros(steps + 1) P[0] = P0 is the price storage, it creates an empty list of prices, we set the first prices and the rest is generated.
for t in range(steps): Runs the model step by step through time with each step = a small market update
drift = (alpha - beta*r + gamma*C) * dt This is the drift term which computes the baseline growth - interest pressure + credit expansion (predictable part of the housing market)
shock = sigma * np.sqrt(dt) * np.random.randn() This is the Brownian Shock (random market behaviour) this adds in the random economic shock
σ dW this is what the unpredictable shock mathemtically. 

Examples of "shocks"
- Policy surprise
- crisis
- inverstor sentiment
- speculation
- panic
P[t + 1] = P[t] * no.exp(drift + shock) this is the update housing price rule it essentially says new price = old price × growth factor
The exponemtial of the update ensures
- prices never go negative
- continuous compounding
- realistic financial behaviour
That is the geometic brownian motion

plt.plot(time, P) this is the plot of housing prices vs time.
We see: stochastic housing path, rises + falls and volatility.
AT THE MOMENT EACH RUN LOOKS DIFFERENT

This program at the moment:
- grows over time
- reacts to interest rates
- reacts to credit conditions
- fluctuates randomly
- never goes negatively
- looks like a financial time series
- it's a mock housing market economy

This program does not:
- learn from real data
- preditc real house prices
- include time varying interest rates
- model craches explicitly
- includes mean reversion
- include supply and demand ecomnomics

  Next Steps Might be:
  - Adding mean reversion
  - time-varying interest rates
  - real data calibration
 

WE HAVE PIVOTED TO MAKE A WEBSITE OR APP TO HELP OTHER PEOPLE OF HOUSE BUYING AFFORDABILITY

Version 2 – Enhanced Decision Model (Notebook-Based)

Version 2 builds on the initial housing model by transforming it from a simple price estimator into a multi-factor decision engine.

Key Improvements

The model now incorporates three core components:

1. Market Valuation
Uses county-level data
Estimates:
median price
interquartile range (25th–75th percentile)
Classifies properties as:
cheap
typical
overpriced

Buyer Affordability
Calculates monthly mortgage payments
Introduces payment-to-income ratio
Categorises financial pressure:
comfortable
moderate
high

Financing Structure (NEW in V2)

Adds Loan-to-Value (LTV):

LTV=LoanProperty Price
LTV=
Property Price
Loan
	​

Interprets leverage:
low
moderate
high

This is important because:

high LTV = higher risk exposure
aligns model more closely with real mortgage assessment

Market Trend Analysis
Uses yearly median prices
Estimates:
market growth
direction (rising / flat / falling)

Decision + Scoring System
Combines:
price vs market
affordability
financing risk
Outputs:
decision label (e.g. “reasonable”, “high risk”)
buyer score (0–100)

Human-Readable Output 
Converts raw numbers into natural language explanations

Version 3 – User-Facing Application (App / Interface Layer)

Version 3 takes the Version 2 model and wraps it in a simple interactive interface, turning it into a usable product.

User Inputs

The app allows users to enter:

County
Property price
Income
Deposit
Mortgage rate
(optionally term)

Backend Logic

The app directly calls:

analyse_house which is the coding in version 2

Outputs (User Experience)

The app presents:

1. Clear Assessment
“Reasonable purchase”
“Caution”
“High risk”
2. Financial Breakdown
Monthly payment
Income ratio
LTV
3. Buyer Score
Simple 0–100 score
Easy to interpret
4. Human Explanation
Instead of technical output, users see something like this:

Your mortgage payments look comfortable relative to your income.

This property is priced in line with the local market.

Overall assessment: This looks like a strong overall purchase.

Testing and Validation of the Housing Model

To ensure the model produces reliable and sensible outputs, several forms of testing were carried out throughout development.
Data Loading and Integrity Checks

The first stage of testing focused on verifying that the dataset was correctly loaded and structured.
Methods:

Checked available county sheets to ensure all data was accessible
Displayed sample rows to inspect structure and values
Converted date columns into the correct format

Outcome:
This confirmed that the dataset was correctly loaded and that key variables such as price and date were usable for analysis.

Manual Checks on Statistics

Basic statistics were tested to ensure they matched realistic expectations.

Methods:

Calculated average price, median price, and quartiles
Compared results to typical UK housing price ranges

Outcome:
Values were confirmed to be realistic. This step also helped identify that averages could be distorted by extreme values.

Outlier and Aggregation Testing

An issue was identified where yearly averages produced unrealistic spikes due to outliers.

Methods:

Compared mean (average) and median calculations
Replaced mean with median for yearly price trends

Outcome:
Median-based aggregation produced more stable and realistic results, improving robustness against extreme values.

cenario Testing

The model was tested using multiple hypothetical scenarios by varying key inputs.

Tested variables:

Property price
Income
Deposit
Interest rate

Examples:

Lower price with high income resulted in strong affordability ratings
Higher price relative to the county resulted in “overpriced” classifications
High payment-to-income ratios triggered financial pressure warnings

Outcome:
The model responded logically to different inputs, confirming correct behaviour.

Boundary Testing

Edge cases were tested to ensure stability around key thresholds.

Examples:

Very high interest rates
Very low deposits (high loan-to-value ratios)
Income levels close to affordability thresholds (30% and 40%)

Outcome:
The model correctly classified affordability levels and handled edge cases without errors.

Logical Consistency Testing

The relationships between variables were tested to ensure financial logic was correct.

Checks included:

Higher property prices increased monthly payments
Higher income reduced payment-to-income ratios
Larger deposits reduced loan-to-value ratios

Outcome:
The model behaved consistently with expected financial principles.

Function Validation

After converting the model into a reusable function, additional testing was performed.

Methods:

Verified that the function returned consistent outputs
Tested with different counties and input values
Checked that all outputs (decision, score, summary) were correctly generated

Outcome:
The function operated reliably and could be reused across multiple scenarios.

Output Readability Testing

The model output was refined to ensure it was understandable for non-technical users.

Improvements:

Converted numerical outputs into clear explanations
Structured results into readable summaries
Removed raw technical formatting

Outcome:
The output became user-friendly and suitable for use in an application.

isual Validation

Graphs were used to validate market behaviour and identify anomalies.

Methods:

Plotted yearly house price trends
Reviewed trends for consistency and realism

Outcome:
This helped confirm general market direction and identify irregularities in the dataset.

NEXT STEPS:

Annual growth rate
For each county, calculate historical yearly growth.

Average growth
Then compute average growth over the sample

Volatility
tells you how unstable the county market is

5-year projected value

Build a “rise or fall” metric
expected 5-year trend: positive / neutral / negative
projected 5-year value range
probability value in 5 years is above today’s price

Add a “buying quality” model
should combine:
current price fairness
affordability
leverage
local trend
future downside risk

Website roadmap
Stage 1: Streamlit MVP
Stage 2: Make it pretty
Stage 3: Proper web app

Make it user friendly
Users should never see:

drift
volatility
stochastic process
return series

Instead show:

local market trend
market stability
expected 5-year outlook
downside risk
affordability pressure

Add sensitivity analysis

A very strong feature for buyers is:
“What happens if rates rise?”


V4 Model Now Does
I have developed a housing analysis model that acts as a structured decision-making tool rather than just a simple price estimator.
The model evaluates the property’s price relative to the local market by calculating:
median price
interquartile range
classification as cheap, typical, or overpriced
It assesses affordability by calculating:
mortgage loan amount
monthly repayment
payment-to-income ratio
affordability category (comfortable, moderate, high pressure)
It incorporates financing risk using:
loan-to-value (LTV) ratio
leverage classification
interest rate stress testing (e.g. +1%, +2%)
It includes market dynamics by analysing:
yearly median house prices
annual growth rates
log returns
volatility
compound annual growth rate (CAGR)
It produces a 5-year outlook by:
calculating a trend-based projected value
running a Monte Carlo simulation
estimating a range of possible future values
calculating the probability that the property value will rise or fall
It combines all components into:
a buyer score (0–100)
a final recommendation (e.g. strong buy, caution, high risk)
a clear, human-readable summary
Overall, the model evaluates:
price fairness
affordability
financial risk
market conditions
future outlook
It therefore answers a broader question:
whether the property is a sensible financial decision over the medium term, not just whether it is affordable today
Testing and Validation
I verified data integrity by:
loading all sheets correctly
checking county names
inspecting sample rows
converting date fields into proper datetime format
I carried out statistical realism checks by:
calculating median prices and ranges
comparing outputs with realistic housing values
identifying issues with mean values being affected by outliers
I improved robustness by:
replacing mean-based calculations with median-based calculations
ensuring more stable and realistic market trends
I performed scenario testing by varying:
property price
income
deposit
interest rate
county
I confirmed that:
higher prices increased affordability pressure
higher income reduced financial strain
larger deposits reduced loan-to-value ratios
different counties produced different market outcomes
I conducted boundary testing by checking behaviour at:
30% and 40% payment-to-income thresholds
high loan-to-value levels (e.g. above 75% and 90%)
I tested logical consistency by verifying that:
higher interest rates increase monthly payments
higher deposits reduce borrowing
higher income improves affordability
higher volatility increases forecast uncertainty
I validated the forecasting component by:
inspecting yearly price trends
checking growth rate calculations
confirming that volatility and projections were reasonable
ensuring simulation outputs produced realistic value ranges
I tested output clarity by:
converting numerical outputs into clear explanations
structuring results into readable summaries
ensuring outputs are understandable for non-technical users
Overall, I tested the model for:
data integrity
statistical realism
robustness to outliers
sensitivity to input changes
logical consistency
clarity of user output
This gives confidence that the model provides a realistic and useful framework for analysing housing decisions, even though it does not attempt to perfectly predict future prices

Next Steps
Phase 1 – Prepare the model for the app
Move the main function (analyse_house_advanced) into a separate file called model.py
Keep the notebook for testing, debugging, and experimenting with new maths
Remove unnecessary working cells and keep the notebook clean
Ensure all logic is contained inside functions (no hardcoding)
Phase 2 – Build the first version of the app
Create a new file called app.py
Use Streamlit to build a simple interface
Add input fields for:
county
asking price
income
deposit
interest rate
Call the model function using these inputs
Display:
summary
score
decision
Phase 3 – Improve the user interface
Structure the app into sections:
inputs (top or left)
results (main area)
Add key output cards:
buyer score
monthly payment
5-year outlook
risk level
Format output using headings, spacing, and icons
Improve readability of the summary text
Phase 4 – Add visualisations
Add charts to the app:
county price trend (by year)
annual growth rate
5-year simulation distribution
Label charts clearly and make them easy to interpret
Use charts to support decision-making, not just display data
Phase 5 – Improve the maths
Use weighted averages for growth (give more weight to recent years)
Filter out unreliable data (e.g. years with low transaction counts)
Refine volatility calculation for stability
Improve 5-year projection accuracy
Ensure outputs remain realistic and interpretable
Phase 6 – Add risk analysis features
Add probability of price increase/decrease (already calculated)
Highlight downside risk (e.g. 10th percentile outcome)
Categorise risks:
affordability risk
pricing risk
market risk
leverage risk
Add a “market outlook” label (e.g. favourable, neutral, unfavourable)
Phase 7 – Add scenario analysis
Allow users to test different situations:
higher interest rates
different deposit amounts
different incomes
Show how outputs change dynamically
Highlight sensitivity to interest rate increases
Phase 8 – Finalise as a project
Organise files into a clean structure:
model.py
app.py
data/ folder
notebooks/ folder
Create a README explaining:
what the model does
how it works
how to run the app
Save screenshots of the app
Prepare it for portfolio or submission
Overall Goal
Turn the model into a full decision tool that evaluates:
price fairness
affordability
financial risk
market conditions
future outlook
Deliver a user-friendly app that answers:
“Should I buy this house?”
“What are the risks?”
“What might happen over the next 5 years?”
