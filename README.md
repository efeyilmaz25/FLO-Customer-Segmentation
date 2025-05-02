# FLO-Customer-Segmentation
This repository applies simple segmentation processes on the FLO customer dataset.

# Business Problem
FLO wants to divide its customers into segments and determine marketing strategies according to these segments. To this end, customer behaviors will be defined and groups will be created according to clusters in these behaviors.

# Dataset Story
The dataset consists of information obtained from the past shopping behavior of customers who made their last purchases from Flo as OmniChannel (both online and offline shopping) in 2020 - 2021.

# Customer Segmentation Analysis

This repository contains two implementations of customer segmentation analysis:
1. A Pandas-based implementation using scikit-learn (original code)
2. A PySpark implementation for large-scale data processing

Both implementations perform clustering analysis on customer data to identify meaningful customer segments based on purchasing behavior.

## Dataset

The analysis uses the "flo_data_20k.csv" dataset which contains customer purchase behavior data. The key features used for segmentation include:

- **Recency**: Days since the customer's last purchase
- **Tenure**: Days since the customer's first purchase
- **Order Frequency**: Total number of orders made by the customer
- **Monetary Value**: Total amount spent by the customer

## Pandas Implementation

### Dependencies
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- yellowbrick
- scipy

### Key Steps
1. **Data Loading and Preprocessing**:
   - Load data from CSV
   - Convert date columns to datetime format
   - Calculate recency, tenure, total order number, and total customer value

2. **K-Means Clustering**:
   - Scale features using MinMaxScaler
   - Determine optimal number of clusters using the Elbow method
   - Apply K-means clustering with the optimal number of clusters (k=4)
   - Analyze segment characteristics

3. **Hierarchical Clustering**:
   - Perform hierarchical clustering using Ward's method
   - Visualize the dendrogram
   - Cut the dendrogram to create 4 clusters
   - Compare segment characteristics

### Key Features
- Uses scikit-learn's KMeans implementation
- Uses scipy's hierarchical clustering implementation
- Suitable for small to medium-sized datasets that fit in memory

## PySpark Implementation

### Dependencies
- pyspark
- findspark
- matplotlib
- seaborn
- scipy
- scikit-learn

### Key Steps
1. **SparkSession Initialization**:
   - Create a SparkSession with appropriate configurations

2. **Data Loading and Preprocessing**:
   - Load data into a Spark DataFrame
   - Convert date columns to date type
   - Calculate recency, tenure, total order number, and total customer value

3. **Feature Engineering Pipeline**:
   - Use VectorAssembler to combine features into a feature vector
   - Apply MinMaxScaler to scale features to [0,1] range

4. **K-Means Clustering**:
   - Determine optimal number of clusters by calculating SSE for different k values
   - Apply K-means clustering with the optimal number of clusters (k=4)
   - Convert results to Pandas for analysis and visualization

5. **Hierarchical Clustering**:
   - Convert scaled data to Pandas/NumPy for hierarchical clustering
   - Perform hierarchical clustering using Ward's method
   - Visualize the dendrogram
   - Create clusters and analyze segment characteristics

6. **Alternative: BisectingKMeans**:
   - Implement PySpark's BisectingKMeans as an approximation to hierarchical clustering
   - Compare results with traditional hierarchical clustering

### Key Features
- Uses PySpark's DataFrame API for data processing
- Implements a machine learning pipeline with VectorAssembler and MinMaxScaler
- Uses PySpark ML's KMeans and BisectingKMeans implementations
- Suitable for large datasets that may not fit in single-machine memory
- Combines Spark processing with Pandas/SciPy for specific operations not available in Spark

## Implementation Differences

### Data Processing
- **Pandas**: Processes data in-memory on a single machine
- **PySpark**: Distributes data processing across a cluster (or simulates distribution on a single machine)

### Feature Scaling
- **Pandas**: Uses scikit-learn's MinMaxScaler
- **PySpark**: Uses PySpark ML's MinMaxScaler with a pipeline approach

### K-Means Clustering
- **Pandas**: Uses scikit-learn's KMeans implementation
- **PySpark**: Uses PySpark ML's KMeans implementation with distributed computation

### Hierarchical Clustering
- **Pandas**: Directly uses scipy's linkage and dendrogram functions
- **PySpark**: Converts to Pandas/NumPy for hierarchical clustering (since PySpark doesn't have built-in hierarchical clustering)
- **PySpark Alternative**: Uses BisectingKMeans as an approximation of hierarchical clustering

### Visualization
- **Pandas**: Directly visualizes from Pandas DataFrames
- **PySpark**: Converts Spark DataFrames to Pandas for visualization

## When to Use Which Implementation

### Use Pandas Implementation When:
- Working with small to medium-sized datasets (fits in memory)
- Running analysis on a single machine
- Need for quick prototyping and exploration
- Need for hierarchical clustering specifically

### Use PySpark Implementation When:
- Working with large datasets that don't fit in memory
- Need for distributed processing across a cluster
- Processing speed for large data is a priority
- Integrating with a larger Spark-based data pipeline

## Results

Both implementations produce:
1. Optimum cluster number determination using the elbow method
2. K-means clustering with 4 segments
3. Hierarchical clustering with 4 segments
4. Segment analysis and visualization showing the characteristics of each customer segment

The results allow for identifying distinct customer groups based on their purchase behavior, which can inform targeted marketing strategies and customer relationship management.

## Execution Instructions

### Pandas Implementation
```
python pandas_customer_segmentation.py
```

### PySpark Implementation
```
python pyspark_customer_segmentation.py
```

For running in a Jupyter or Colab environment, simply execute the cells in order.
