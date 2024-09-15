# Climate Risks Analysis and Weather Derivative Modeling

## Summary	

The Climate Risks Analysis and Weather Derivative Modeling project provides a comprehensive framework for analyzing temperature data and pricing weather derivatives, essential for managing weather-related risks in a financial portfolio. It begins with the introduction and calculation of Heating Degree Days (HDD) and Cooling Degree Days (CDD), followed by a detailed statistical analysis of historical temperature data. The notebook then decomposes the temperature series into trend, seasonality, and residuals, and fits autoregressive models to the residuals. It models long-term trends and seasonal variations using Fourier series and analyzes temperature volatility through various methods, including polynomial regression and splines. The core of the notebook involves simulating temperature paths using a modified Ornstein-Uhlenbeck process and pricing temperature options under a risk-neutral measure, comparing results from Monte Carlo simulations and a modified Black-Scholes approach. This analytical approach ensures robust, data-driven decision-making for hedging temperature-related risks and diversifying a financial portfolio.
![image](https://github.com/user-attachments/assets/bf175a27-1225-4497-a4f8-964b811f4cb9)

<img src="https://github.com/user-attachments/assets/bf175a27-1225-4497-a4f8-964b811f4cb9" alt="Image" style="width: 70%;"/>

### Introduction to Temperature Options
- Concepts: Introduces Heating Degree Days (HDD) and Cooling Degree Days (CDD) as measures for estimating heating and cooling demands.
- Calculations: Uses numpy to simulate temperature data and calculate HDD and CDD values.
- DataFrame Creation: Constructs a DataFrame to store and summarize the simulated temperature data.

### Statistical Analysis of Temperature Data
- Data Import: Loads historical temperature data.
- Preprocessing: Cleans and merges maximum and minimum temperature datasets.
- Exploratory Data Analysis: Visualizes temperature trends, seasonal patterns, and distributions using time series plots and histograms.

### Time Series Decomposition and Modelling
- Decomposition: Decomposes the temperature series into trend, seasonality, and residual components using classical decomposition.
- Stationarity Testing: Applies the Augmented Dickey-Fuller test to check for stationarity in the residuals.
- Autoregressive Modelling: Fits an AR model to the residuals to capture any remaining autocorrelation.

### De-trending and Modelling Seasonal Variation with Fourier Series
- Denoising: Uses convolution to smooth the temperature series.
- Trend and Seasonality Modelling: Models long-term trends and seasonal variations using Fourier series.
- Model Comparison: Compares different Fourier series models to identify the best fit for seasonal variation.


### Temperature Volatility Models
- Volatility Analysis: Analyzes temperature volatility using various methods:
  - Piece-wise constant functions
  - Polynomial regression
  - Splines
  - Fourier series
- Model Fitting: Fits these models to the data and evaluates their performance.

### Monte Carlo Simulation of Temperature for Weather Derivative Pricing
- Simulation: Implements a modified Ornstein-Uhlenbeck process to simulate temperature paths.
- Visualization: Plots simulated temperature paths and compares summer and winter simulations.
- Euler Scheme: Uses the Euler scheme for numerical approximation in the simulation.

### Risk-Neutral Pricing of Weather Derivatives
- Risk-Neutral Measure: Transforms the temperature process to a risk-neutral measure for pricing.
- Option Pricing: Calculates the mean and variance under the risk-neutral measure to price temperature options.
- Black-Scholes Approach: Compares option prices using a modified Black-Scholes approach.

### Monte Carlo Valuation
- Simulation-Based Pricing: Uses Monte Carlo simulation to price temperature options.
- Error Estimation: Calculates standard errors for the option prices to assess the accuracy of the simulation.



