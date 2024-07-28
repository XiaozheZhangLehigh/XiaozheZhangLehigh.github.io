# Home Credit - Credit Risk Model Stability


## Competition Description
Source: [Kaggle](https://www.kaggle.com/competitions/home-credit-credit-risk-model-stability)

The absence of a credit history might mean a lot of things, including young age or a preference for cash. Without traditional data, someone with little to no credit history is likely to be denied. Consumer finance providers must accurately determine which clients can repay a loan and which cannot and data is key. If data science could help better predict one’s repayment capabilities, loans might become more accessible to those who may benefit from them the most.
Currently, consumer finance providers use various statistical and machine learning methods to predict loan risk. These models are generally called scorecards. In the real world, clients' behaviors change constantly, so every scorecard must be updated regularly, which takes time. The scorecard's stability in the future is critical, as a sudden drop in performance means that loans will be issued to worse clients on average. The core of the issue is that loan providers aren't able to spot potential problems any sooner than the first due dates of those loans are observable. Given the time it takes to redevelop, validate, and implement the scorecard, stability is highly desirable. There is a trade-off between the stability of the model and its performance, and a balance must be reached before deployment.
Founded in 1997, competition host Home Credit is an international consumer finance provider focusing on responsible lending primarily to people with little or no credit history. Home Credit broadens financial inclusion for the unbanked population by creating a positive and safe borrowing experience. We previously ran a competition with Kaggle that you can see here.

Your work in helping to assess potential clients' default risks will enable consumer finance providers to accept more loan applications. This may improve the lives of people who have historically been denied due to lack of credit history.

## Competition Result: Silver Medal (35/3856)
<img src="https://github.com/user-attachments/assets/e313b6bb-5a9b-4bc9-8393-48d00e0b8308" alt="kaggle" style="width:70%;">

## Data Integration and Preprocessing

### Reading the File

Utilized `polars` and `pandas` libraries to efficiently load, transform, and reduce memory usage of large datasets from Parquet files. Implemented a customized function to scan Parquet files matching a given glob pattern and combine them into a LazyFrame.

### Customized Function for Data Transformation

Implemented custom functions to handle date transformations, filter columns based on null values and unique counts, and optimize data types. The key steps include:

- **Drop Columns with Excessive Null Values**: Removed columns with more than 95% null values.
- **Drop Columns Based on Unique Value Counts**: Eliminated columns with more than 200 unique values or only 1 unique value.
- **Convert Data Types for Optimization**: Employed the `reduce_memory_usage` function to downsize storage, ensuring efficient management of GPU power and storage. For example, data is stored in 16-bit when possible, avoiding 32-bit and 64-bit storage unless necessary.

## Feature Engineering

### Aggregate Features

Developed methods to aggregate features using statistical measures (max, min, mean, variance, mode) and handle categorical data. In real-world scenarios, data is often collected over time or across different groups. Aggregating features using statistical measures helps summarize this information effectively. Including these statistical measures can help models understand the underlying patterns and relationships in the data, leading to better predictions. Additionally, created a utility class to manage feature definitions and occurrences across multiple datasets.

## Model Training and Evaluation

### Voting Ensemble Model

Designed a voting ensemble model combining CatBoost and LightGBM classifiers, leveraging cross-validation to optimize model performance.

#### CatBoost

- **Handling Categorical Features**: Efficiently manages categorical data.
- **Robust to Overfitting**: Built-in mechanisms prevent overfitting, making it suitable for high-dimensional data.
- **Fast and Scalable**: Optimized for rapid training and prediction, even on large datasets.
- **High Accuracy**: Delivers high predictive accuracy.

#### LightGBM

- **Efficiency**: Notable for speed and memory usage efficiency.
- **Handling Large Datasets**: Capable of managing millions of instances and features.
- **Gradient-based One-Side Sampling (GOSS)**: Focuses on the most important data points, improving training efficiency.
- **Leaf-wise Tree Growth**: Grows trees leaf-wise rather than level-wise, leading to enhanced accuracy.

## Apache Parquet

Apache Parquet is an open-source, column-oriented data file format designed for efficient data storage and retrieval. It provides high-performance compression and encoding schemes to handle complex data in bulk and is supported in many programming languages and analytics tools.
