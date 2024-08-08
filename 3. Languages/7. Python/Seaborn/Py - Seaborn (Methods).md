See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Seaborn (Basics)]]
Resources:
* Documentation: [seaborn](https://seaborn.pydata.org/)


---

# Classes
##### `PairGrid()`
* Subplot grid for plotting pairwise relationships in a dataset.
	* Parameters (see complete list of parameters [here](https://seaborn.pydata.org/generated/seaborn.PairGrid.html))
		* `data` (df) -- A DataFrame where each column is a variable and each row is an observation.
		* `hue=`(str) -- Variable in `data` to map plot aspects to different colors.
		* `vars=` (list) -- Variables within `data` to use, otherwise use every column with a numeric datatype.
```Python
import seaborn as sns

g = sns.PairGrid(penguins)
```

```Python
import seaborn as sns

g = sns.PairGrid(penguins)
g.map_diag(sns.histplot)
g.map_offdiag(sns.scatterplot)
```

# Methods

##### `sns.pairplot()`
* Plot pairwise relationships in a dataset
* Parameters (see full list of parameters [here](https://seaborn.pydata.org/generated/seaborn.pairplot.html#seaborn-pairplot))
	* `data` (df) -- A DataFrame where each column is a variable and each row is an observation.
	* `diag_kind=` (str) -- Kind of plot for the diagonal subplots. If ‘auto’, choose based on whether or not `hue` is used.
		* `'auto'`
		* `'hist'`
		* `'kde'`
		* `None`
	* `hue=`(str) -- Variable in `data` to map plot aspects to different colors.

```Python
import seaborn as sns
sns.pairplot(data, diag_kind='hist')
```

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


##### `PairGrid.map_offdiag()`
* Plot with a bivariate function on the off-diagonal subplots.
	* Parameters
		* `func=` -- defines the graph type
			* `sns.scatterplot`
		* `s=` (int) -- sets the size of the marker
		* `marker=` (str) -- determines the shape of the points
		* `color=` (str) -- sets the marker color
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

# Constructs data from pairgrid.data on projections outside of the diagonals.
pairgrid.map_offdiag(func=sns.scatterplot, s=200, marker='*', color='red')

```
