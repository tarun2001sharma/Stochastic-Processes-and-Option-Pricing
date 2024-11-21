


# Financial Securities and Markets: Stochastic-Processes-and-Option-Pricing

Simulations and analysis of stochastic processes, option pricing, hedging strategies, and volatility estimation using Python for quantitative finance.

## Overview

This repository contains content learned in **MATH-GA 2791.001: Financial Securities and Markets** (Fall 2024). The assignment delves into the simulation and analysis of stochastic processes, pricing of financial derivatives, hedging strategies, and volatility estimation.

Instructor: Prof. Bernhard Hientzsch  
Author: Tarun Sharma  

---

## Objective

The primary goal of this homework is to explore and implement key concepts in financial mathematics using Python. By simulating stochastic processes and financial derivatives, students gain a hands-on understanding of the Black-Scholes model, option pricing mechanisms, hedging strategies, and volatility behavior.

---

## Problem Details and Solutions

### 1. Simulation of Brownian Motion Paths

#### Theory
Brownian Motion $W_t$, also called Wiener Process, is a key building block in stochastic calculus. It has the following properties:
1. $W_0 = 0$
2. Independent increments
3. Normally distributed increments, $W_t - W_s \sim \mathcal{N}(0, t-s)$ for $t > s$
4. Continuous sample paths

Discrete-time simulation uses:
$$
W_{t_{i+1}} = W_{t_i} + \sqrt{\delta t} Z_i, \quad Z_i \sim \mathcal{N}(0,1)
$$

#### Tasks
1. Implement a function `simulate_brownian_motion` to simulate multiple paths of $W_t$ over a given time horizon using a discrete approximation.
2. For $20,000$ paths:
   - Estimate $E(W_t)$, the expected value at each time step.
   - Compute $\sqrt{	ext{Var}(W_t)}$, the standard deviation.
3. Plot:
   - The estimated mean and standard deviation at each time step.
   - Overlay theoretical values: $E(W_t) = 0$ and $\sqrt{	ext{Var}(W_t)} = \sqrt{t}$.

#### Insights
- The simulated values validate the theoretical properties of Brownian Motion.
- Accuracy improves with more paths and finer time discretization.

---

### 2. Simulation of Black-Scholes Paths

#### Theory
The Black-Scholes model extends Brownian Motion to model the dynamics of an asset price $S_t$. Using the stochastic differential equation:
$$
rac{dS_t}{S_t} = \mu dt + \sigma dW_t
$$
The discretized solution for $S_t$ is:
$$
S_{t_{i+1}} = S_{t_i} \exp\left[\left(\mu - rac{1}{2} \sigma^2
ight)\delta t + \sigma\sqrt{\delta t} Z_i
ight]
$$

#### Tasks
1. Simulate multiple paths of $S_t$ for:
   - Initial price $S_0 = 100$
   - Drift $\mu = 5\%$, Volatility $\sigma = 30\%$, Risk-free rate $r = 3\%$
   - Daily time steps over one year ($T = 1$, $\delta t = 1/360$).
2. Analyze the simulated paths to verify the geometric Brownian motion properties.

#### Insights
- Asset prices exhibit exponential growth with added noise.
- Volatility and drift directly influence the dispersion and trend of the paths.

---

### 3. Pricing by Simulation

#### Theory
The price of a European call option is given by:
$$
C = e^{-rT} \mathbb{E}\left[\max(S_T - K, 0)
ight]
$$
Monte Carlo simulation is used to estimate this expectation by generating paths for $S_T$.

#### Tasks
1. Simulate $S_T$ for multiple paths and calculate the discounted payoff for a strike price $K = 100$.
2. Repeat the simulation for two additional strike prices and analyze:
   - Mean price
   - Standard deviation and standard error
3. Study the impact of increasing the number of paths on the price estimates and error bars.

#### Insights
- Option price decreases as the strike price increases, reflecting reduced payoff probability.
- Increasing paths reduces standard error, demonstrating the convergence property of Monte Carlo simulations.

---

### 4. Simulation of Hedging

#### Theory
Delta hedging replicates the option payoff using a portfolio:
$$
P_t = \Delta_t S_t + \phi_t B_t
$$
where:
- $\Delta_t = rac{\partial C}{\partial S}$ adjusts for price sensitivity.
- $B_t$ represents a bond component to balance the portfolio.

#### Tasks
1. Simulate daily portfolio values $P_t$ and compare with the theoretical option price $C_{BS}$ for various paths.
2. Plot:
   - $P_t$ vs. $C_{BS}$
   - Histogram of hedging errors $arepsilon_T = P_T - 	ext{Payoff}$
   - Include mean $E(arepsilon_T)$ and variance $	ext{Var}(arepsilon_T)$ on plots.

#### Insights
- Hedging errors arise from discretization and model assumptions.
- Errors decrease with finer time steps and accurate volatility estimates.

---

### 5. Behavior of Hedging Error

#### Theory
Hedging errors depend on parameters like:
- Drift $\mu$
- Volatility $\sigma$
- Time step $\delta t$

#### Tasks
1. Analyze the impact of:
   - Increasing $\mu$ from $5\%$ to $20\%$.
   - Increasing $\sigma$ up to $80\%$.
   - Reducing time steps ($\delta t = 1/60$, $1/30$).
2. Plot histograms of hedging errors under varying conditions.

#### Insights
- Hedging errors increase with higher volatility.
- Larger time steps exacerbate discrepancies, highlighting the importance of frequent rebalancing.

---

### 6. Estimation of Volatility

#### Theory
Volatility can be estimated via:
1. **Historical Volatility**:
   $$
   	ext{Historical Volatility} = rac{360}{n} \sum_{i=1}^{n} (X_{t_i} - X_{t_{i-1}})^2
   $$
2. **Break-Even Volatility**: The volatility that perfectly hedges an at-the-money call.

#### Tasks
1. Plot historical volatility for paths of $S_t$ as $n$ increases.
2. Compute the break-even volatility over 10,000 paths and plot its distribution.

#### Insights
- Historical volatility converges with finer time discretization.
- Break-even volatility highlights sensitivity to model calibration.

---

### 7. Holding Value by Simulation

#### Theory
The holding value at $t = 0.5Y$ depends on:
- The value of the underlying $S_t$.
- The expected discounted payoff from $t$ to $T$.

#### Tasks
1. Simulate paths for $S_t$, evaluate payoffs, and collect data.
2. Use Ordinary Least Squares (OLS) to approximate the conditional expectation of the payoff as a function of $S_t$ using basis functions.
3. Compare approximations with the Black-Scholes formula.

#### Insights
- OLS regression provides a data-driven alternative to closed-form solutions.
- Increasing the number of basis functions improves the approximation.

---

## Implementation

### Requirements
The simulations are implemented in Python using:
- `numpy`, `scipy` for numerical operations
- `matplotlib`, `seaborn` for visualizations
- `pandas` for data handling

### How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/tarunsharma-financial-models/homework1.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Execute the Jupyter Notebook:
   ```bash
   jupyter notebook Homework1.ipynb
   ```

---

## Results and Observations

1. **Brownian Motion**: Simulations validate theoretical properties.
2. **Black-Scholes Model**: Reflects the dynamic nature of asset prices.
3. **Option Pricing**: Monte Carlo estimates converge with increased paths.
4. **Hedging**: Errors depend on discretization and volatility assumptions.
5. **Volatility Analysis**: Provides insights into model calibration and risk management.

---

## References

1. Black, F., & Scholes, M. (1973). The Pricing of Options and Corporate Liabilities. *Journal of Political Economy*.
2. Hull, J. C. (2006). *Options, Futures, and Other Derivatives*. Prentice Hall.

--- 

