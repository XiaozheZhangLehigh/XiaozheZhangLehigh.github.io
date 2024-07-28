# Evaluating the Role of Equity and High-Yield Bonds in Portfolio Performance and Risk Management


## Research Intuition

**Argument 1: High-Yield Bonds vs. Stocks**
1. Risk and Return Characteristics:
- High-yield bonds and stocks share traits such as higher risk, higher return, and volatility.
- Stocks might generate similar returns (high-yield) with similar characteristics.
2. Market Behavior:
- High-yield bonds have credit risk.
- When the market declines, high-yield bond prices tend to fall, similar to stocks.
- During market upswings, both stocks and high-yield bonds rise.
- The question is whether it is better to hold high-yield bonds continuously or to increase equity allocation while keeping bonds as the portfolio’s insurance component.


**Argument 2: High-Yield Bonds in Taxable Accounts - Inefficiency of High-Yield Bond**
- High-yield bonds are inefficient for generating returns in taxable accounts.
- Holding more stocks than high-yield bonds would be better.
- Income from high-yield bonds is heavily taxed, resulting in a significant portion of the coupon income being paid to the federal government.
- Bondholders bear the risks but are not fully compensated, as the federal government benefits from the risk premium without taking any risks.

## Data Description	

### Data Sources (Bloomberg)

**Equity: Standard & Poor's 500 Index (S&P 500)**
= Description: The S&P 500 Index is a market-capitalization-weighted index that measures the stock performance of 500 of the largest companies listed on stock exchanges in the United States. It is considered a leading indicator of the overall performance of the U.S. stock market and economy.

**High-yield bond: Bloomberg Barclays US High-Yield Index**
- Description: This index measures the market of USD-denominated, non-investment grade, fixed-rate, taxable corporate bonds.

**Investment Grade Bond: Bloomberg Barclays US Aggregate Bond Index**
- Description: This index includes investment-grade bonds traded in the United States, including government, corporate, mortgage-backed, and asset-backed securities.


### Exploratory Analysis

#### Index Growth (1983-2024)
<img src="https://github.com/user-attachments/assets/ef4453fd-4a6e-4a24-993c-51e08319a15a" alt="Index Growth" style="width:70%;">

#### Annualized Volatility
<img src="https://github.com/user-attachments/assets/aff6f67b-a49d-458b-ab81-f79532f8e581" alt="Annualized Volatility" style="width:70%;">

#### Drawdown
<img src="https://github.com/user-attachments/assets/8355199c-45ee-41c7-8a49-10878fd94209" alt="Drawdown" style="width:70%;">

## Allocation Strategies
Testing Period: 1983-08-01 - 2024-06-25
The following Table shows the backtesting result for semi-annual rebalance because it has the best result:

| Portfolios  | Equity | HighYield Bonds | InvGrade Bonds | Total Return | Annualized Return | Annualized Volatility | Sharpe Ratio | Max Drawdown | Max Drawdown Date |
|-------------|--------|-----------------|----------------|--------------|-------------------|-----------------------|--------------|--------------|--------------------|
| Baseline    | 0.50   | 0.00            | 0.50           | **24.016**   | 0.057             | 0.076                 | 0.752        | -0.316       | 2009-03-09         |
| JS_Strategy | 0.40   | 0.10            | 0.50           | **23.655**   | 0.056             | 0.061                 | 0.918        | -0.281       | 2009-03-09         |
| JB_Strategy | 0.50   | 0.10            | 0.40           | **26.381**   | 0.059             | 0.073                 | 0.799        | -0.338       | 2009-03-09         |
| JE_Strategy | 0.45   | 0.10            | 0.45           | **25.031**   | 0.057             | 0.067                 | 0.854        | -0.310       | 2009-03-09         |


## Backtesting Result
#### Growth Plot Comparison: semi-annual rebalance 

![image](https://github.com/user-attachments/assets/11e20988-a0d7-4032-873e-4b3111aa98f1)


#### Bar Plot Comparison of Return and Risk Metrics
![image_return](https://github.com/user-attachments/assets/b6f5b789-044d-42eb-96ba-75cbbcd6dec8)

#### Key Insight from bar plot comparison:
- JB Strategy: Ideal for aggressive investors focused on maximizing returns and willing to accept higher drawdown and volatility.
- JS Strategy: Best for those prioritizing risk-adjusted returns, offering a good Sharpe ratio and moderate risk.
- JE Strategy: Suitable for investors seeking a balanced approach with moderate performance across all metrics.
- Baseline Strategy: Provides a reference point, showing moderate returns and risk, and can be considered a conservative choice.


#### Comparision between Baseline and Strategy Returns
![image](https://github.com/user-attachments/assets/2dd646cd-0ac6-4006-9ee0-60b55ad210a0)


##### JS Strategy
Significant Points on JS Strategy (over 1% difference)
| Background              | Date       | Baseline Daily Return | Strategy Daily Return | Strategy Performance |
|-------------------------|------------|-----------------------|-----------------------|-----------------------|
| Black Monday            | 1987-10-19 | -9.92%                | -7.33%                | <span style="color:green">Outperform</span>            |
| Black Monday            | 1987-10-21 | 4.41%                 | 3.26%                 | <span style="color:red">Underperform</span>          |
| Black Monday            | 1987-10-26 | -4.01%                | -2.96%                | <span style="color:green">Outperform</span>            |
| Black Monday            | 1987-10-30 | 3.23%                 | 2.18%                 | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-08-31 | 0.67%                 | -0.47%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-09-28 | 1.11%                 | -0.39%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1991-02-28 | -0.09%                | 1.91%                 | <span style="color:green">Outperform</span>            |
| Early 1990s recession   | 1991-03-28 | 0.12%                 | 1.17%                 | <span style="color:green">Outperform</span>            |
| 2007–2008 financial crisis | 2008-10-13 | 6.06%                 | 4.63%                 | <span style="color:red">Underperform</span>          |
| 2007–2008 financial crisis | 2008-10-28 | 5.44%                 | 4.16%                 | <span style="color:red">Underperform</span>          |
| 2007–2008 financial crisis | 2008-11-21 | 3.32%                 | 2.31%                 | <span style="color:red">Underperform</span>          |
| 2007–2008 financial crisis | 2008-12-01 | -4.43%                | -3.36%                | <span style="color:green">Outperform</span>            |


##### JB Strategy
![image](https://github.com/user-attachments/assets/8b03651f-fce1-4b77-9fbd-13c296b30e0b)
Significant Points on JB Strategy (over 1% difference)
| Background              | Date       | Baseline Daily Return | Strategy Daily Return | Strategy Performance |
|-------------------------|------------|-----------------------|-----------------------|-----------------------|
| Black Monday            | 1987-10-30 | 3.23%                 | 2.11%                 | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-08-31 | 0.67%                 | -0.34%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-09-28 | 1.11%                 | -0.24%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1991-02-28 | -0.09%                | 1.85%                 | <span style="color:green">Outperform</span>            |
| Early 1990s recession   | 1991-03-28 | 0.12%                 | 1.13%                 | <span style="color:green">Outperform</span>            |


##### JE Strategy
![image](https://github.com/user-attachments/assets/d3688641-2106-4011-b71b-65f77732681e)
Significant Points on JE Strategy (over 1% difference)
| Background              | Date       | Baseline Daily Return | Strategy Daily Return | Strategy Performance |
|-------------------------|------------|-----------------------|-----------------------|-----------------------|
| Black Monday            | 1987-10-19 | -9.92%                | -8.27%                | <span style="color:green">Outperform</span>            |
| Black Monday            | 1987-10-30 | 3.23%                 | 2.14%                 | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-08-31 | 0.67%                 | -0.40%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-09-28 | 1.11%                 | -0.31%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1991-02-28 | -0.09%                | 1.88%                 | <span style="color:green">Outperform</span>            |
| Early 1990s recession   | 1991-03-28 | 0.12%                 | 1.15%                 | <span style="color:green">Outperform</span>            |


#### Annual Returns and Monthly Return Distributions Strategy Comparison
<img width="624" alt="image" src="https://github.com/user-attachments/assets/f8ec3555-5c1a-45c4-b00e-2152fb9cd881">

#### Tax Consideration:
<img width="901" alt="image" src="https://github.com/user-attachments/assets/73098a1c-46e4-4f12-a459-6d5cf423936a">

The above plot only illustrates how different tax rates affect the return, but it does not incorporate the capital-gain and income tax brackets. Bonds spin off regular income payments that are taxed at ordinary tax rates, while the dividend payments from equities and equity funds are taxed at the same lower rates that apply to long-term capital gains, provided the dividends are qualified. From that perspective, fixed-income securities make the most sense in tax sheltered accounts, where their regular distributions can be reinvested and compounded without taxation until withdrawal time, while equities are better suited for taxable accounts. 
