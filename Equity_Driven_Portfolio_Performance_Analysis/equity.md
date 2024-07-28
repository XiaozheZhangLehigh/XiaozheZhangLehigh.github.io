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
![image](https://github.com/user-attachments/assets/598852b1-d46f-4c56-88ed-d635917abf10)
![image](https://github.com/user-attachments/assets/1597cd1b-7177-4919-b328-ed681867ce33)
![image](https://github.com/user-attachments/assets/0edd97e1-6538-4bd2-afef-fbcbdd28fb1d)
![image](https://github.com/user-attachments/assets/7786b807-602a-4cb1-86fb-b534d8b2fe29)
![image](https://github.com/user-attachments/assets/768112d8-2103-4d81-ba6d-d4b8b64e2f79)

#### Key Insight from bar plot comparison:
- JB Strategy: Ideal for aggressive investors focused on maximizing returns and willing to accept higher drawdown and volatility.
- JS Strategy: Best for those prioritizing risk-adjusted returns, offering a good Sharpe ratio and moderate risk.
- JE Strategy: Suitable for investors seeking a balanced approach with moderate performance across all metrics.
- Baseline Strategy: Provides a reference point, showing moderate returns and risk, and can be considered a conservative choice.


#### Comparision between Baseline and Strategy Returns
![image](https://github.com/user-attachments/assets/2dd646cd-0ac6-4006-9ee0-60b55ad210a0)

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

![image](https://github.com/user-attachments/assets/8b03651f-fce1-4b77-9fbd-13c296b30e0b)
Significant Points on JB Strategy (over 1% difference)
| Background              | Date       | Baseline Daily Return | Strategy Daily Return | Strategy Performance |
|-------------------------|------------|-----------------------|-----------------------|-----------------------|
| Black Monday            | 1987-10-30 | 3.23%                 | 2.11%                 | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-08-31 | 0.67%                 | -0.34%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1990-09-28 | 1.11%                 | -0.24%                | <span style="color:red">Underperform</span>          |
| Early 1990s recession   | 1991-02-28 | -0.09%                | 1.85%                 | <span style="color:green">Outperform</span>            |
| Early 1990s recession   | 1991-03-28 | 0.12%                 | 1.13%                 | <span style="color:green">Outperform</span>            |


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


#### Classification Criteria
- Cosine Similarity: The similarity between models is based on the cosine of the angle between their sector composition vectors.
- Linkage Criteria: The clusters are formed based on the Ward's method criterion, which considers the increase in within-cluster variance.

- linkage function: This function from the scipy.cluster.hierarchy module performs **hierarchical clustering**.

#### Input:
- 1 - similarity_matrix: The cosine similarity matrix is converted to a distance matrix by subtracting the similarity values from 1. This is because the linkage function expects a distance matrix, where lower values indicate more similarity.
- method='ward': Ward's method is used for clustering. This method minimizes the total within-cluster variance. At each step, it merges the pair of clusters that leads to the smallest increase in total within-cluster variance.


## Consolidation Result	
#### Dendrogram for Model Clustering
![image](https://github.com/user-attachments/assets/c3a880df-5835-44a0-ae04-3bcc39d0fe14)


#### Clustering Result and Representative Models

| Cluster | Representative Model Name                              | # of linked Portfolios | Cluster Size |
|---------|--------------------------------------------------------|------------------------|--------------|
| 1       | TIAA CREF University 1 Aggressive                      | 15                     | 5            |
| 2       | TIAA CREF NQ 3 Moderate Fix                            | 1                      | 2            |
| 3       | Hafkin-TIAA                                            | 1                      | 2            |
| 4       | TIAA BROOKHAVEN 1 Aggressive                           | 1                      | 1            |
| 5       | Schwab - NQ NTF 3 Moderate - National                  | 2                      | 12           |
| 6       | Schwab - NQ NTF 4 ConservativePlus - OH                | 1                      | 3            |
| 7       | Schwab - ESG - NQ Instl - 5 Conservative - National    | 1                      | 1            |
| 8       | Schwab - NQ NTF 1 Aggressive - OH                      | 2                      | 6            |
| 9       | Schwab - NQ NTF 2 ModeratePlus - OH                    | 23                     | 11           |
| 10      | Schwab - ESG - Qualified NTF - 3 Moderate CCVA         | 5                      | 5            |
| 11      | Schwab Ultra-Low-Cost - 3 - Mod                        | 72                     | 10           |
| 12      | Schwab - Qualified CMP Institutional 5 Cons            | 2                      | 2            |
| 13      | Fidelity OSU 3 -New                                    | 4                      | 3            |
| 14      | Schwab - Qualified Institutional 5 Conservative        | 1                      | 9            |
| 15      | Fidelity UCP 2 ModAgg 403(B)                           | 2                      | 8            |
| 16      | Fidelity UC 2 ModAgg ARP_403b                          | 10                     | 6            |
| 17      | Schwab Ultra-Low-Cost - 2 - ModAgg                     | 110                    | 13           |
| 18      | TIAA CREF NW Childrens 403b_DC 1 Aggressive            | 2                      | 19           |
| 19      | Schwab - Allocation - 1 - DGEIX                        | 2                      | 5            |
| 20      | Schwab - Values - Sharia-Halal - Instl - 2 ModAgg      | 2                      | 1            |
| 21      | Lincoln InvestorAdvtg Annuity - 2 ModeratePlus         | 2                      | 1            |
