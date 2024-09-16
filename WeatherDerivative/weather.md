# Climate Risks Analysis and Weather Derivative Modeling

## Summary	

The Climate Risks Analysis and Weather Derivative Modeling project provides a comprehensive framework for analyzing temperature data and pricing weather derivatives, essential for managing weather-related risks in a financial portfolio. It begins with the introduction and calculation of Heating Degree Days (HDD) and Cooling Degree Days (CDD), followed by a detailed statistical analysis of historical temperature data. The notebook then decomposes the temperature series into trend, seasonality, and residuals, and fits autoregressive models to the residuals. It models long-term trends and seasonal variations using Fourier series and analyzes temperature volatility through various methods, including polynomial regression and splines. The core of the notebook involves simulating temperature paths using a modified Ornstein-Uhlenbeck process and pricing temperature options under a risk-neutral measure, comparing results from Monte Carlo simulations and a modified Black-Scholes approach. This analytical approach ensures robust, data-driven decision-making for hedging temperature-related risks and diversifying a financial portfolio.

### Introduction to Temperature Options
- Concepts: Introduces Heating Degree Days (HDD) and Cooling Degree Days (CDD) as measures for estimating heating and cooling demands.
- Calculations: Uses numpy to simulate temperature data and calculate HDD and CDD values.
- DataFrame Creation: Constructs a DataFrame to store and summarize the simulated temperature data.
<img src="https://github.com/user-attachments/assets/7c120755-48fc-40ab-96fe-96b3a38cc200" alt="Image" style="width: 70%;"/>


### Statistical Analysis of Temperature Data
- Data Import: Loads historical temperature data.
- Preprocessing: Cleans and merges maximum and minimum temperature datasets.
- Exploratory Data Analysis: Visualizes temperature trends, seasonal patterns, and distributions using time series plots and histograms.

<div style="position: relative; width: 500px; height: 500px;">
  <!-- Top-left corner -->
  <img src="https://github.com/user-attachments/assets/ea3df274-b08b-40c1-ae2f-cb71d1c96548" style="position: absolute; top: 0; left: 0; width: 45%;"/>

  <!-- Top-right corner -->
  <img src="https://github.com/user-attachments/assets/cda262f5-02bf-40da-b725-25ecb544edc1" style="position: absolute; top: 0; right: 0; width: 45%;"/>

  <!-- Bottom-left corner -->
  <img src="https://github.com/user-attachments/assets/48540d47-8647-45c2-b31e-d3ff4844aab2" style="position: absolute; bottom: 0; left: 0; width: 45%;"/>

  <!-- Bottom-right corner -->
  <img src="https://github.com/user-attachments/assets/50ff4343-8f99-409f-8b3e-82cf658ef687" style="position: absolute; bottom: 0; right: 0; width: 45%;"/>
</div>

### Time Series Decomposition and Modelling
- Decomposition: Decomposes the temperature series into trend, seasonality, and residual components using classical decomposition.
- Stationarity Testing: Applies the Augmented Dickey-Fuller test to check for stationarity in the residuals.
- Autoregressive Modelling: Fits an AR model to the residuals to capture any remaining autocorrelation.
<img src="https://github.com/user-attachments/assets/957b9fbf-e0ff-4a81-86b8-867f42fb3175" alt="Image" style="width: 70%;"/>

### De-trending and Modelling Seasonal Variation with Fourier Series
- Denoising: Uses convolution to smooth the temperature series.
- Trend and Seasonality Modelling: Models long-term trends and seasonal variations using Fourier series.
- Model Comparison: Compares different Fourier series models to identify the best fit for seasonal variation.
<img src="https://github.com/user-attachments/assets/7e5a7d1a-dce6-40c9-a880-983a8165d6d1" alt="Image" style="width: 70%;"/>

### Modelling Temperature with a Modified Ornstein-Uhlenbeck (OU) Process

- **Using Modified OU Process**  
  The standard Ornstein-Uhlenbeck (OU) process assumes a constant mean, but when modeling temperature, the expectation deviates from the long-run average temperature due to seasonal and long-term trends.

- **Mean Reversion Level (θ):**  
  In this model, the drift term includes both the mean reversion component and the rate of change of the seasonal mean. This allows the model to capture the changing trends in temperature over time, rather than assuming a constant mean.

- **Estimating Speed of Mean Reversion:**  
  The temperature dynamics can be modeled by the following stochastic differential equation:

$$
dT_t = \left( \frac{d\bar{T}_t}{dt} + \kappa(\bar{T}_t - T_t) \right) dt + \sigma_t dW_t
$$

Where:
- \(T_t\): The temperature at time \(t\)
- \(\bar{T}_t\): The dynamic mean temperature
- \(\kappa\): The mean reversion speed
- \(\sigma_t\): The time-varying volatility
- \(dW_t\): The Wiener process (random noise)

- **Mean Reversion Speed (κ):**  
  The mean reversion speed κ is determined through statistical analysis of historical temperature data. It can be estimated using an autoregressive model (AR(1)), from which κ is extracted as a key parameter.

- **Volatility (Dynamic):**  
  Unlike traditional models where volatility is constant, the volatility \( \sigma_t \) in the temperature process is dynamic. This captures the changing variability in temperature over time, which may depend on seasonal factors or other environmental influences.

### Temperature Volatility Models
- Volatility Analysis: Analyzes temperature volatility using various methods:
  - Piece-wise constant functions
  - Polynomial regression
  - Splines (Best)
  - Fourier series
- Model Fitting: Fits these models to the data and evaluates their performance.
<img src="https://github.com/user-attachments/assets/11a758b8-3104-4bb5-89f6-f565bd1a1a29" alt="Image" style="width: 70%;"/>

### Monte Carlo Simulation of Temperature for Weather Derivative Pricing
- Simulation: Implements a modified Ornstein-Uhlenbeck process to simulate temperature paths.
- Visualization: Plots simulated temperature paths and compares summer and winter simulations.
- Euler Scheme: Uses the Euler scheme for numerical approximation in the simulation.  
  With Euler scheme of approximation:

  $$ T_{i+1} = T_i + \bar{T}'_i + \kappa (\bar{T}_i - T_i) + \sigma_i z_i $$ 
<img src="https://github.com/user-attachments/assets/95a1222e-702e-489d-87e7-44b3f40e6230" alt="Image" style="width: 70%;"/>
<img src="https://github.com/user-attachments/assets/02253297-0920-4378-a390-9c8b491c46cf" alt="Image" style="width: 70%;"/>
<img src="https://github.com/user-attachments/assets/0462c1cb-25a7-4b2d-8244-f4fb415af7d6" alt="Image" style="width: 70%;"/>



### Risk-Neutral Pricing of Weather Derivatives
- Risk-Neutral Measure: Transforms the temperature process to a risk-neutral measure for pricing.
- Option Pricing: Calculates the mean and variance under the risk-neutral measure to price temperature options.
- Black-Scholes Approach: Compares option prices using a modified Black-Scholes approach.
<img src="https://github.com/user-attachments/assets/cc51041d-370b-4b59-afc1-14054cfb7e1f" alt="Image" style="width: 70%;"/>


### Compare the result
<img src="https://github.com/user-attachments/assets/5071d074-11d3-4b65-9868-b94a612d93de" alt="Image" style="width: 70%;"/>




