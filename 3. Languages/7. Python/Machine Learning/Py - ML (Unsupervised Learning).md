See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Classes and Methods)]]
* [[Py - Seaborn (Basics)]]
* [[Py - Seaborn (Methods)]]
* [[Py - Matplotlib (Methods)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [seaborn](https://seaborn.pydata.org/)

---
# Intro to Unsupervised Learning

## What is Unsupervised Learning?
* **Unsupervised Learning** -- a type of machine learning problem where the target feature is not provided.
	- **Objective**: The algorithms autonomously find relationships between observations.
	- **Key Points**:
	    - No labeled data or predefined categories.
	    - Algorithms detect patterns, structures, or groupings in the data.


# Cluster Analysis
## What is Cluster Analysis?
* **Cluster Analysis** (also known as 'Clustering') -- is the task of combining similar observations into groups, or clusters
	* **Objective:** Involve determining the similarity of difference between observations based on the distanced between them
		* Closer = more similar
		* Further = less similar
		![[clustering-visual-video.webm]]
* Popular Clustering Tasks
	* Segmenting users or products. This can be closely connected to recommendation systems.
	- Detect fraud by spotting non-typical behavior (for example, generating fake clicks or likes in social media).

## Various Clustering Algorithms
* The sklearn library has several algorithms for clustering analysis
	* `KMeans()`
		* Works best on well-defined data groups of similar size
	* `AffinityPropogation()`
	* `MeanShift()`
	* `SpectralClustering()`
	* `Ward()`
	* `AggolmerativeClustering()`
	* `DBSCAN()`
	* `OPTICS()`
	* `Birch()`
	* `GaussianMixture()`
	![[various-of-clustering-algorithms.png]]

# K-Means Clustering
### Understanding the K-Means Algorithm
* K-means clustering is a popular unsupervised machine learning algorithm that groups unlabeled data into clusters.
	* Main Concepts:
		* The algorithm's key concept is the centroid, the center of a cluster.
		- Closeness to a centroid determines an observation's cluster.
		- Each cluster has its own centroid.
		- A centroid is calculated as the arithmetic mean of the cluster's observations.
		
	- How it works:
		- The algorithm randomly assigns a cluster number to each observation, from 1 to $k$
		- The algorithm repeats a two-step iteration until the observation clusters stop changing:
			- The centroid of each cluster is calculated.
			- Each observation is assigned the number of a new cluster whose centroid is closest to the observation.
			
	- Calculating the Centroid Value ($mu$) $$mu=1/N sum^(N)_(j=1)x^j=1/N(sum^(N)_(j=1)x^j_1, sum^(N)_(j=1)x^j_2,...sum^(N)_(j=1)x^j_n)$$
## K-Means Clustering in Sklearn
* The `cluster` module in the sklearn library has a `KMeans()` class for k-means clustering
```Python
import pandas as pd
import numpy as np
from sklearn.cluster import KMeans

data = pd.read_csv('/datasets/segments.csv')
centers = np.array([[20, 80, 8], [50, 20, 5], [20, 30, 10]])

# Training the model without initial centroids
model = KMeans(n_clusters=3, random_state=12345)
model.fit(data)

print('Cluster centroids:')
print(model.cluster_centers_) # Print the centroid values of the resulting clusters

# Training a model with initial centroids
model = KMeans(n_clusters=3, random_state=12345, init=centers)
model.fit(data)

print('Cluster centroids of the model with initial centroids:')
print(model.cluster_centers_)
```

```
Cluster centroids:
[[40.14472236 15.00741697  8.56      ]
 [10.90357994 29.90244865 15.096     ]
 [10.68632155 98.90275017 10.856     ]]
 
Cluster centroids of the model with initial centroids:
[[10.68632155 98.90275017 10.856     ]
 [50.06201472 19.62701512  1.808     ]
 [20.56550497 20.14513373 15.204     ]]
```


## The Objective Function
### What is the Objective Function?
* **Objective Function** -- the sum of intra-cluster distances that assess the quality of the model in unsupervised learning
	* Similar to the loss function in supervised learning
	
* The goal of the training is to minimize the resulting sum of the Objective Function

### Formulas for the Objective Function
* Formula: **Calculation of Centroid of Each Cluster** $$μ_k = 1/abs(C_k) sum_(x^j ∈ C_k)x^j = 1/abs(C_k) (sum_(x^j ∈ C_k)x^j_1, sum_(x^j ∈ C_k)x^j_2,...sum_(x^j ∈ C_k)x^j_n)$$
	* $|C_k|$ -- the number of points in the cluster
	- $x$ -- defines observations, and in this case, it's vectors of size $n$
	- $∈$ -- signifies that the observation belongs to the cluster
	
- Formula: Objective Function $$min_kd_2(mu_k,x)=min_ksqrt(sum^n_(i=1)(mu_i^k-x_i)^2)$$
- Formula: Calculation of Intra-Cluster Distances $$D_k = sum_(x^j ∈ C_k)(d_2(mu_k,x^j))^2$$
- Formula: Final Objective Function (calculated as the sum of intra-cluster deviations) $$SD=sum_kD_k=sum_ksum_(x^j ∈ C_k)(d_2(mu_k,x^j))^2$$

### Objective Function is Sklearn
* The `inertia_` attribute on the `KMeans()` class is used to find the objective function
```Python
import pandas as pd
import numpy as np
from sklearn.cluster import KMeans

data = pd.read_csv('/datasets/segments.csv')
centers = np.array([[20, 80, 8], [50, 20, 5], [20, 30, 10]])

model = KMeans(n_clusters=3, random_state=12345)
model.fit(data)

print('Objective function:')
print(model.inertia_)

model = KMeans(n_clusters=3, init=centers, random_state=12345)
model.fit(data)

print('The objective function of the model with initial centroids:')
print(model.inertia_)
```

```
Objective function:
68431.50999400369

The objective function of the model with initial centroids:
74253.20363562094
```

## The Local Minimum
### What is the Local Minimum?
* A value obtained as a minimum for a specific initial set of observations in the cluster.
	- Starting with a different initial set of observations can lead to a different local minimum value.
	- Each different initial set of observations can result in a new local minimum.

### Understanding the local minimum
* The more algorithm launches (`n_init`) and more iterations (`max_iter`), the smaller the objective function value 
	* This will get the objective function closer to the local minimum


## Data Visualization
### Working with the seaborn library
* The seaborn library has a `pairplot()` method that plots pairwise relationships in a dataset.

```Python
import seaborn as sns
sns.pairplot(data, diag_kind='hist')
```
![[seaborn-pairplot-unsupervised-example-1.png]]

* Plotting the centroids
```Python
import pandas as pd
from sklearn.cluster import KMeans
import seaborn as sns

# Import data
data = pd.read_csv('segments.csv')

# Create K-cluster model
model = KMeans(n_clusters=3, random_state=12345)

# Train the data
model.fit(data)

# Create the centroids as DF
centroids = pd.DataFrame(model.cluster_centers_, columns=data.columns)

# Add a column with the cluster number
data['label'] = model.labels_.astype(str)

# Naming the centroids
centroids['label'] = ['0 centroid', '1 centroid', '2 centroid']

# Combine the dataframes and ignore the index
data_all = pd.concat([data, centroids], ignore_index=True)

# Plot the graph
sns.pairplot(data_all, hue='label', diag_kind='hist')
```

![[seaborn-pairplot-unsupervised-example-2.png]]

* Dealing with basic and advanced segments: Adding an additional layer of initial centroids to determine the clusters suitable for them.
	* Steps:
		* Save the instance corresponding to the graph
		* Pass the additional values needed for plotting the graph using the `data` attribute
		* Call the `map_offdiag()` method to construct data on projections outside of the diagonals
```Python
import pandas as pd
from sklearn.cluster import KMeans
import seaborn as sns

# Import data
data = pd.read_csv('segments.csv')

# Create K-cluster model
model = KMeans(n_clusters=3, random_state=12345)

# Train the data
model.fit(data)

# Create the centroids as DF
centroids = pd.DataFrame(model.cluster_centers_, columns=data.columns)

# Add a column with the cluster number
data['label'] = model.labels_.astype(str)

# Naming the centroids
centroids['label'] = ['0 centroid', '1 centroid', '2 centroid']

# Combine the dataframes and ignore the index
data_all = pd.concat([data, centroids], ignore_index=True)

# Save the instance corresponding to the graph, pairgrid
pairgrid = sns.pairplot(data_all, hue='label', diag_kind='hist')

# Pass additional values needed for plotting the graph using the `data` attribute
pairgrid.data = pd.DataFrame(
	[[20, 80, 8], [50, 20, 5], [20, 30, 10]], 
	\\ columns=data.drop(columns=['label']).columns
)

# Construct data from pairgrid.data on projections outside of the diagonals
pairgrid.map_offdiag(func=sns.scatterplot, s=200, marker='*', color='red')
```

![[seaborn-pairplot-unsupervised-example-3.png]]

* Example
```Python
import pandas as pd
import numpy as np
from sklearn.cluster import KMeans
import seaborn as sns
import warnings
warnings.filterwarnings("ignore")

data = pd.read_csv('/datasets/segments.csv')
centers = np.array([[20, 80, 8], [50, 20, 5], [20, 30, 10]])

model = KMeans(n_clusters=3, init=centers, random_state=12345)
model.fit(data)
centroids = pd.DataFrame(model.cluster_centers_, columns=data.columns)

data['label'] = model.labels_.astype(str)
centroids['label'] = ['0 centroid', '1 centroid', '2 centroid']

# An index reset is required to create pairgrid.data
data_all = pd.concat([data, centroids], ignore_index=True)

pairgrid = sns.pairplot(data_all, hue='label', diag_kind='hist')
centroids_init = pd.DataFrame(
	centers, 
	columns=data.drop(columns=['label']).columns
)

centroids_init['label'] = 4

# An additional layer for the centroids
pairgrid.data = centroids_init
pairgrid.map_offdiag(func=sns.scatterplot, s=200, marker='*', palette='flag')
```


## Optimal Number of Clusters
### Determining the Optimal Number of Clusters
* The **Elbow Method** -- a way of finding the optimal number of clusters.
	* It's graph resembles an arm bent at the elbow

### Performing the Elbow Method
* Steps:
	* Train the model several times and save the objective function values for each model in the **distortion** list.
	* Display the resulting list on the graph
	* Determine the number of optimal clusters visually
```Python
# Find Number of optimal clusters

import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

distortion = [] # Distortion list to store objective functions
K = range(1, 8) # Indictor to train the model 7 times
for k in K:
    model = KMeans(n_clusters=k, random_state=12345)
    model.fit(data)
	print('Number of clusters:', k) 
    print('Objective function value', model.inertia_)
    distortion.append(model.inertia_)

plt.figure(figsize=(12, 8))
plt.plot(K, distortion, 'bx-')
plt.xlabel('Number of clusters')
plt.ylabel('Objective function value')
plt.show()
```

```
Number of clusters: 1
Objective function value 782222.4354730697

Number of clusters: 2
Objective function value 161733.64953602126

Number of clusters: 3
Objective function value 68431.50999400369

Number of clusters: 4
Objective function value 27110.79024796993

Number of clusters: 5
Objective function value 22468.766585439167

Number of clusters: 6
Objective function value 19960.565605742842

Number of clusters: 7
Objective function value 18257.632605610874
```

### Reading the Elbow Method Graph
* The moment of transition (into a plateau) signifies the **optimal number of clusters**
![[elbow-method-example-1.png]]


### Using the Optimal Number of Clusters
* Once the optimal number is determined, it can be used to create and train a model with the optimal number of clusters
```Python
# Use the number of optimal clusters (from above) to create and train the model

import pandas as pd
import seaborn as sns
from sklearn.cluster import KMeans

data = pd.read_csv('/datasets/segments.csv')

# Training a model for 4 clusters

model = KMeans(n_clusters=4, random_state=12345)
model.fit(data)

centroids = pd.DataFrame(model.cluster_centers_, columns=data.columns)
data['label'] = model.labels_.astype(str)

centroids['label'] = ['0 centroid', '1 centroid', '2 centroid', '3 centroid']
data_all = pd.concat([data, centroids], ignore_index=True)

# Plot the graph
sns.pairplot(data_all, hue='label', diag_kind='hist')

# Print the rounded centroids of the resulting model
print('Typical user segments for 4 clusters:')
print(model.cluster_centers_.round())
```

```
Typical user segments for 4 clusters:
[[30. 10. 15.]
 [11. 99. 11.]
 [50. 20.  2.]
 [11. 30. 15.]]
```

* Example
```Python
# Finding Optimal Number of Clusters

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

data = pd.read_csv('/datasets/cars.csv')

K = range(1, 11)
distortion = []

for k in K:
    model = KMeans(n_clusters=k, random_state=12345)
    model.fit(data)
    distortion.append(model.inertia_)

plt.figure(figsize=(12, 8))
plt.plot(K, distortion, 'bx-')
plt.xlabel('Number of clusters')
plt.ylabel('Objective function value')
plt.show()
```

```Python
import pandas as pd
from sklearn.cluster import KMeans
import seaborn as sns

data_full = pd.read_csv('/datasets/cars_label.csv')

data = data_full.drop(columns=['brand'])

# Train the model
model = KMeans(n_clusters=3, random_state=12345)
model.fit(data)

# Create centroids and concatenate them to the dataset
centroids = pd.DataFrame(model.cluster_centers_, columns=data.columns)
centroids['brand'] = ['US centroid', 'Europe centroid', 'Japan centroid']
data_all = pd.concat([data_full, centroids], ignore_index=True)

# Plot the results
pairgrid = sns.pairplot(data_all, hue='brand', diag_kind='hist')
pairgrid.map_offdiag(func=sns.scatterplot, s=200, marker='*', color='red')
```

# Anomalies
## What are Anomalies?
* Anomalies, or outliers, are observations with abnormal properties (i.e. those that deviate from the normal trend).
* Outliers indicate a problem in the data or that something is out of the ordinary.
* Example:
	* John, from St. Louis, only uses his card 2x per week (on restaurants)
	* Suddenly, his card is used on a very expensive smartphone in Hanoi

## Anomalies in One-Dimensional Data
* Boxplots can be used to detect outliers in one-dimensional data
### Boxplots (Review)
- **Box Boundaries**:
    - **Upper Boundary (Top of the Box)** -- this marks the third quartile (Q3), or the 75th percentile of the data. 
	    - 75% of the data values are below this point.
    - **Lower Boundary (Bottom of the Box)** -- this marks the first quartile (Q1), or the 25th percentile of the data. 
	    - 25% of the data values are below this point.
    - **Median** -- The line within the box represents the median, which is the 50th percentile. 
	    - 50% of the data values are below this line.
- **Whiskers**:
	- **Whiskers** -- The whiskers show the spread of the data outside the box. They reach out to the smallest and largest values that are still within 1.5 times the IQR from the quartiles
		- **Interquartile Range (IQR)** -- This is the range of the middle 50% of the data $$IQR=Q_3−Q_1$$
		- Lower Inner Fence of the Boxplot 
			- $k$ -- coefficient for interquartiles ranges (usually 1.5) $$L = Q_1 - k * IQR$$
		- Upper Outer Fence of the Boxplot 
			- $k$ -- coefficient for interquartiles ranges (usually 1.5)$$R = Q_3 + k * IQR$$
- **Outliers**:
    - Outliers are data points that fall outside the whiskers (plotted as individual circles) and represent values that are unusually high or low compared to the rest of the data.
	![[boxplot-description.png]]

### Boxplots in Matplotlib
* The `boxplot()` method creates a boxplot
```Python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('/datasets/sales.csv')

# Create boxplot
boxplot = plt.boxplot(df['Sales'].values)
plt.ylabel('Total sales')
plt.title('Outliers in total sales')

# Show the boxplot
plt.show()

# Find outliers
outliers = list(boxplot['fliers'][0].get_data()[1])
print('Outliers in total sales: ', len(outliers))
```

```
Outliers in total sales:  1167
```

```Python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('/datasets/sales.csv')

boxplot = plt.boxplot(df['Profit'].values)
outliers = list(boxplot['fliers'][0].get_data()[1])

df_outliers = df[df["Profit"].isin(outliers)]

print('Number of anomalies: ', len(df_outliers))
```


## Anomalies in Multi-Dimensional Data
## Isolation Forests
* Isolation Forests can be used to detect outliers in multi-dimensional data

### The Isolation Forest Algorithm
* **Isolation Forest** -- an ensemble method that uses multiple decision trees to make predictions.
- **Tree Nodes** -- Each node in the trees contains decision rules that classify observations.
- **Anomaly Detection** -- Relies on the principle that anomalies can be separated from normal data using fewer decision rules.
	![[isolation-forest.png]]

### Isolation Forest in Sklearn
* The `ensemble` module has an `IsolationForest()` class that can be used to train an isolation forest
	* Finds anomalies based on several features
* Steps:
	* Import the required `IsolationForest` class
	* Create the model
		* The more estimators (number of tree), the more accurate the results
	* Convert the data into 2D array 
		* Using the `reshape()` method
	* Select the features that will be checked for anomalies
	* Train the data
	* Call the `decision_function()` function on the isolation forest model to get the anomaly scores
	* Calculate the number of anomalies using the `predict()` method
		* This classifies observations and distinguishes the normal ones from the outliers. 
			* If the observation class is 1, the observation is normal
			* If the observation class is -1, it's an outlier.
```python
# Performing Isolation Forest Algorithm

# Import the class
from sklearn.ensemble import IsolationForest

# Create the model
isolation_forest = IsolationForest(n_estimators=100)

# Reshape the data
sales = df['Sales'].values.reshape(-1, 1)

# Select features to be checked for anomalies
data = df[['Sales', 'Profit']]

# Train the data
isolation_forest.fit(data)

# Get anomaly scores
anomaly_scores = isolation_forest.decision_function(data)

# Determine if features are anomalies or not
estimator = isolation_forest.predict(data)

# fit_predict() can be used if anomaly estimates aren't necessary
# estimator = isolation_forest.fit_predict(data)
```

```Python
# Performing Isolation Forest Algorithm

import pandas as pd
from sklearn.ensemble import IsolationForest

df = pd.read_csv('/datasets/sales.csv')

isolation_forest = IsolationForest(n_estimators=100)
data = df[['Sales', 'Profit']]
estimator = isolation_forest.fit_predict(data)

outliers = []
for e in estimator:
    if e == -1:
        outliers.append(e)

print('Number of anomalies: ', len(outliers))
# Number of anomalies:  1029
```


## KNN-Based Detection 
### K-nearest Neighbors Algorithm (KNN)
- **Observation as Vector** -- KNN treats each observation as a vector in multidimensional space.
- **Anomaly Detection** -- The algorithm identifies anomalies based on the distance between observations; those further from their neighbors are more likely to be outliers.

### KNN in PyOD
* The `models.knn` module of the PyOD (Python toolkit for detecting outlying objects) library has a `KNN()` class for detecting multi-dimensional anomalies
* Steps
	* Import the class
	* Create the model
	* Train the model using the `fit()` method
	* Search for anomalies in the dataset using `predict()` method
		* Returns a list where,
			* "1" indicates an anomaly
			* "0" means the observation is part of the general trend
```Python
from pyod.models.knn import KNN

model = KNN()
model.fit(data)

predictions = model.predict(data)
```

* Example: Comparing KNN and IsolationForest Algorithms
```Python
import pandas as pd
from pyod.models.knn import KNN
from sklearn.ensemble import IsolationForest

df = pd.read_csv('/datasets/sales.csv')
data = df[['Sales', 'Profit']]

model = KNN()
estimation_knn = model.fit_predict(data) == 1
outliers_knn = estimation_knn.sum()
print('Number of anomalies (KNN): ', outliers_knn)

model = IsolationForest(n_estimators=100)
estimation_iforest = model.fit_predict(data) == -1
outliers_iforest = estimation_iforest.sum()
print('Number of anomalies (isolation forest): ', outliers_iforest)

print('Matched: ', (estimation_knn & estimation_iforest).sum())
```

```
Number of anomalies (KNN):  1000
Number of anomalies (isolation forest):  1106
Matched:  897
```