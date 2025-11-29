## comp5511 assignment2 
## LINEAR REGRESSION FOR HOUSING PRICE PREDICTION

### 1. Project Overview
This project aims to gain a deeper understanding of supervised learning, unsupervised learning (K-means clustering), and the impact of different data segmentation strategies on model performance through practical application.
### 2. Setup and Dependencies
The project code is implemented in Google Colab (LINEAR_REGRESSION_FOR_HOUSING_PRICE_PREDICTION.ipynb), and Python 3.8+ is recommended.
```bash
pip install numpy==1.26.0 pandas==2.1.0 scikit-learn==1.3.0 matplotlib==3.7.2
```
### Necessary Python Libraries
- Python 3.8+：Core Programming Language
- NumPy 1.26.0：Scientific Computing and Array Manipulation
- Pandas 2.1.0：Data Reading and Processing
- Scikit-learn 1.3.0：Linear Regression, K-means, Data Preprocessing, Performance Evaluation
- Matplotlib 3.7.2：Data Visualization and Plotting

### 3.Linear Regression and Housing Price Prediction
Based on the ParisHousing.csv dataset, we compared the performance differences of three different linear regression modeling strategies in house price prediction:

- Baseline Model：Train a standard linear regression model on the complete training set.
- Segmentation Model：Divide the data into 10 subsets based on the discrete values ​​of 'numPrevOwners' (1-10), and train an independent linear model for each subset.
- K-Means Clustering Model：Use the K-means algorithm to cluster features, partition the data according to the clustering results, and train an independent linear model for each cluster.

#### Data Preprocessing

Data Loading and Splitting: Load the data using pandas and separate the features $X$ (all columns except 'price') and labels $y$ (the 'price' column). The data is then split into training and test sets.

#### Feature Engineering (Pipeline):

- Numerical Feature Standardization: Standardize continuous numerical features (e.g., 'squareMeters') using StandardScaler.

- One-Hot Encoding of Categorical Features: One-hot encode categorical features (e.g., 'cityPartRange') using OneHotEncoder.

- Use ColumnTransformer to integrate the preprocessing steps, ensuring the efficiency and consistency of the data pipeline.

### Segmentation Strategy and Training

#### All models are implemented using sklearn.linear_model.LinearRegression:

- Baseline Model: Fit the model directly to the fully preprocessed training set.

- Feature Segmentation:

Iterate through all possible values ​​of 'numPrevOwners' ($g=1$ to $10$).

In each iteration, extract subsets of the training and test sets corresponding to the $g$ values.

Train a separate LinearRegression model on each subset and use it to predict the test data for that subset.

- K-means Clustering Segmentation:

Cluster the features of the training set using KMeans (e.g., K=5) and assign cluster labels to all samples.

Iterate through each cluster label $k$ and train a separate LinearRegression model on the training subset corresponding to $k$.

Use the corresponding local model to predict the subset of $k$ in the test set.

#### Performance Evaluation

The performance of all models is evaluated on the test set.

- Evaluation metrics: The primary metrics used are Mean Absolute Error (MAE), Root Mean Square Error (RMSE), and R² Score.

- Segmented Model Summary: The overall performance of the segmented model is calculated by combining the predicted results $\hat{y}$ and the actual values ​​y of all subsets, and then calculating the total MAE and RMSE.
  
