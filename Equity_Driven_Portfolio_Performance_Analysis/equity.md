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
Cumulative Return

**Data Cleaning:**

The data cleaning process is essential due to the presence of personalized models tailored for specific clients and niche models, including those focused on cryptocurrencies, 401k plans, and 529 college savings accounts. Ensuring the consistency and accuracy of these models is crucial for reliable analysis and interpretation.

## Method

#### Cluster Analysis

**Cosine similarity** is easily interpretable since it is bounded between zero and one. Thus, two insurers with identical portfolios will have a cosine similarity equal to one; two insurers whose portfolios are completely different will have a cosine similarity equal to zero.

##### Step 1: Calculate Similarity
- Calculate the similarity between models based on their sector allocations.
- We'll use cosine similarity to measure the similarity between models.
- Identify Similar Models if the similarity score is between 0.95 - 0.99999

##### Step 2: Cluster Models
- Use clustering techniques to group similar models together.
- We'll use hierarchical clustering to group similar models.

##### Explanation of Ward's Method
- Ward's Method: This method minimizes the total within-cluster variance. At each step, it merges the pair of clusters that leads to the smallest increase in total within-cluster variance.
- Advantages: Ward's method is effective in producing clusters of similar size and compactness, making it suitable for identifying distinct groups in the data.

##### Classification Criteria
- Cosine Similarity: The similarity between models is based on the cosine of the angle between their sector composition vectors.
- Linkage Criteria: The clusters are formed based on the Ward's method criterion, which considers the increase in within-cluster variance.

- linkage function: This function from the scipy.cluster.hierarchy module performs **hierarchical clustering**.

##### Input:
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
