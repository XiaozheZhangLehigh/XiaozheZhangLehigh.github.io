# Model Consolidation for Investment Models via Hierarchical Clustering

## Summary

Summary
- Hierarchical Clustering: A method of cluster analysis that groups similar objects into groups called clusters. The endpoint is a set of clusters, where each cluster is distinct from each other cluster, and the objects within each cluster are broadly similar to each other.
- Ward's Method: A variance-minimizing approach that merges clusters to minimize the increase in total within-cluster variance.
- Cosine Similarity: Used to measure the similarity between models based on their sector allocations.
- Dendrogram: A visual representation of the hierarchical clustering process, helping to decide the number of clusters.
- Threshold: A cut-off value to determine the number of clusters from the dendrogram.

This process groups similar models together based on their sector allocations, allowing for a more organized and interpretable analysis of the models.

## Data Description

### Data Sources and Samples

Model samples in this analysis come from the investment models based on different risk-return profiles from a financial advisory company.

### Model Preparation and Cleaning

Investment models are constructed based on sector allocations of:
      'U.S. Large Cap Growth', 'U.S. Large Cap Value', 'U.S. Large Cap Blend',
       'U.S. Mid Cap Growth', 'U.S. Mid Cap Value', 'U.S. Mid Cap Blend',
       'U.S. Small Cap Growth', 'U.S. Small Cap Value', 'U.S. Small Cap Blend',
       'Non-US Dev Stock', 'Non-US Emrg Stock', 'U.S. Txbl Long Term Bonds',
       'U.S. Txbl Int Term Bonds', 'U.S. Txbl Short Term Bonds',
       'U.S. Infl Protected Bonds', 'U.S. Tax-Exempt Bonds',
       'U.S. High Yield Bonds', 'Non-US Dev Bonds', 'Non-US Emrg Bonds',
       'U.S. Bonds', 'Cash', 'U.S. Real Estate', 'Commodities', 'Alternatives',
       'Other',

As each allocation has different market exposure and growth potentials.

Cleaning is needed as there are personalized models for specific client and niche models for cryptos, 401k, 529 accounts. 


### Sentiment Analysis

#### What is Sentiment?

The core of the whole analysis is to answer the question, "Do 10-K filings contain value-relevant information in the sentiment of the text?"
The word "Sentiment" in our context is: "Does the word have a positive or negative tone (e.g., "confident" vs. "against")."

What we want to know: **Is the positive or negative sentiment in a 10-K associated with better/worse stock returns?**

**Sentiment Score**: To analyze the sentiment in a 10-K report, we need to obtain word lists of positive/negative words and calculate the corresponding sentiment scores in the 10-K report text.
The equation is as follows:

The equation is as followed: 
$$\text{Sentiment Score} = \frac{\text{Positive/Negative Word Count in Report}}{\text{Total Word Count in Report}}$$



#### Sentiment Variables Selection and Description

The first 4 out of 10 sentiment variables come from published academic papers, studying the textual analysis for finance. 
The **Loughran-McDonald Master Dictionary w/ Sentiment Word Lists (LM word list)** come from [When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks](https://onlinelibrary.wiley.com/doi/10.1111/j.1540-6261.2010.01625.x), and word list from **machine learning (ML) algorithm (ML word lists)** come from [The colour of finance words](https://www.sciencedirect.com/science/article/abs/pii/S0304405X22002422). Researchers in both papers improved the positive and negative word lists based on previous studies and created their own lists based on their textual analysis studies.
The corresponding word list can be found in the ```/input``` folder of the project repo:

1. ```LM_MasterDictionary_1993-2021.csv``` Loughran-McDonald Master Dictionary w/ Sentiment Word Lists
2. ```ML_negative_unigram.txt```
3. ```ML_positive_unigram.txt```

#### Processing Sentiment Variables

Before using the word lists to extract the sentiment from the report, we need to turn text into usable datasets by natural language processing (NLP).

“Anchor phrase” is a simple yet powerful technique we utilize here, and it allows python to look for a word (or words) near another word (or words) to see if (and how much) a document is discussing some topic. 

Professor Donald Bowen provides us with the following function in this project:

[NEAR_regax](https://github.com/LeDataSciFi/ledatascifi-2023/blob/main/community_codebook/near_regex.py) is a key function employed to modify word lists and enable python to parse through 10-K reports. This function conducts anchor phrase searches and leverages the power of regex while mostly keeping us away from the necessary work of writing a dang regex.

I downloaded the NEAR_regas function python file from the above link and saved it to my project folder. 
To use the function, I imported the function from the project folder by:
    
```python
from NEAR_regex import NEAR_regex
```
Then, we would load the word list and ensure the words are in list form. Then, we want to build a regex that looks for “hey” OR “hi” or “sup”, we need to implement these three things:
1. In regex, OR is “|”.

2. No spaces between terms

3. **Important: Put the parentheses around the whole set of terms!**

So, “hey” OR “hi” or “sup” becomes '(hey|hi|sup)'.
Here is the sample code: 
```python
LM_positive_for_regex = ['('+'|'.join(LM_positive)+')'] 
```

#### Cleaning 10-K files from SEC htmls

Next, we need to load and clean the context from 10-K reports in ```10k_files.zip``` in ```10k-file``` folder, and the specific method is located in the ```build_sample-ipynb```. 
After cleaning, we can extract the document's length and count the word occurrence from word lists, calculating sentiment scores by the equation provided above.
Sample code provided here:
```python
htmldf['LM_positive_score'] = htmldf['cleaned_html'].apply(lambda x:
    len(re.findall(NEAR_regex(LM_positive_for_regex), x))/len(x.split()))
```

#### Original Contextual Sentiment Selection

The rest of the 6 out of 10 sentiment variables are contextual sentiment variables that fit the overall analysis's purpose.
Here, I picked three topics for “Contextual” sentiment, which refers to the (positive and negative) sentiment of the text in a 10-K around discussions of a particular topic. Each topic gets a positive and negative sentiment score.

**Topic 1: Asset Return**

The topic of Asset Return comes from an academic paper on [Predicting Returns with Text Data](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3389884). 
Researchers introduce a new text-mining methodology that extracts sentiment information from news articles to predict asset returns. The paper presents a supervised learning framework that constructs a sentiment score that is specifically adapted to the problem of return prediction. In their study, I found word lists they use called "TableA.2: List of Top 50 Positive/Negative Sentiment Words" which fit the purpose of my sentiment analysis.

**Topic 2: Climate**

The topic of climate is chosen because 10-K reports provide important information about a company's financial performance and risks, including climate-related risks. Therefore, the topic of climate in 10-K reports matters for stock returns because investors are increasingly concerned about climate-related risks and the importance of ESG factors in investment decision-making. Failure to adequately disclose these risks or address sustainable practices can lead to a decline in stock price.

In recent years, there has been growing interest in understanding climate change's impact on businesses and its financial risks. However, there is a lack of research on how the sentiment of company reports on climate relates to their financial performance. To fill this gap, I used ChatGPT with GPT4 to analyze climate-related words in company reports and generate a list of 50 positive and 50 negative words. This approach allows insights into how companies communicate their stance on climate and whether it affects their stock returns. By leveraging GPT4's natural language processing capabilities, we can better understand how companies view climate change and sustainability and their impact on financial performance.

**Topic 3: Financial Constraint**

The topic of Condition for Financial Constraint comes from an academic paper on [Using 10-K Text to Gauge Financial Constraints](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2331544). 
The paper uses 10-K Text to Gauge Financial Constraints. The paper discusses how measuring the extent to which a firm is financially constrained is critical in assessing capital structure. The paper proposes a unique lexicon based on constraining words to parse 10-K disclosures filed with the SEC. The paper finds that the frequency of constraining words exhibits a very low correlation with traditional measures of financial constraints and predicts subsequent liquidity events—like dividend omissions or increases, equity recycling, and underfunded pensions—better than widely-used financial constraint indexes

As this paper presents a negative word list to measure a company's financial constraints, this approach can help identify potential financial struggles. Developing a positive word list that highlights companies that do not experience financial constraints or show signs of financial struggles may also be possible. On the other hand, this paper refers to constraining words only, which highlighted words indicative of a company's financial constraints or struggles. However, it did not provide a positive word list indicating whether companies do not experience financial constraints or show signs of financial struggles. I prompted ChatGPT, powered by GPT4, to create a 50 positive words list that could be used to measure whether a company was doing well financially.

The negative words from TABLE 3 are the Fifty Most Frequently Occurring Constraining Words in 10-Ks based on the study.

#### Original Contextual Sentiment Measurement

After selecting words and creating the word list for contextual sentiment for different topics, I adopt the same modification from ```Processing Sentiment Variables``` section to use NEAR_regex and calculate the sentiment scores for each S&P 500 company.

Whether the contextual sentiment measures pass basic smell tests, it can be concluded that the measures are appropriate and trustworthy. Three topics of *Asset Return, Climate, and Financial Constraints* are associated with the stock return performance of s&p 500 companies. Besides, half of the word lists used are from academic papers published in creditworthy financial journals, ensuring that the measures are grounded in established financial research. The approach researchers take to develop the measures in their papers is rigorous and well-thought-out, so using those word lists would be one of the best ways to perform the sentiment analysis for selected topics. 


Additionally, I utilized an AI language model, ChatGPT, powered by GPT4, to generate the other half of the word lists. It is an innovative approach to sentiment analysis, and it shows the future role of emerging new technology in improving the measures based on human beings' needs. The AI-generated word lists are diversified and contain no overlapping words, which is crucial to achieving a comprehensive and accurate understanding of the sentiment expressed in the texts. 

Regarding the question of whether the industries of the S & P 500 companies are talking positively or negatively about the selected topics, the sentiment expressed by these industries is mixed. This is not unexpected, as the sentiment expressed in language can be complex and nuanced. However, further analysis, such as sentiment clustering or topic modeling, may reveal more insights into the sentiment expressed by these industries. Overall, the approach in this analysis to developing and testing the contextual sentiment measures appears rigorous and thoughtful, and the measures pass basic smell tests.

