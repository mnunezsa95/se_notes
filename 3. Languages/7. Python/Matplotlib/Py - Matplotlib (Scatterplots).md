See [[Py - Introduction to Python]], [[Py - Matplotlib (Installing and Importing)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Matplotlib (Plots)]]
Documentation:
* [Matplotlib Official Documentation](https://matplotlib.org/stable/)

---

#### What is a Scatterplot?
* A scatterplot is a graph where a single point is plotted for each set of variables, but the points are not connected by lines.
#### Scatterplots
* Helps us understand the relationships between variables (i.e. columns) in data
* Useful when each data point is a discrete independent measurement.

#### `plot()` 
* Creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
	* `kind=` -> a string to specify the kind of plot to be used
		* `scatter` -> uses a scatterplot to plot information
	* `alpha=` -> a float between 0 (full transparency) and 1 (no transparency) that controls the transparency of the points (default is `1`); helps when trying to find areas of high-density in the data
* Example
```python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/height_weight.csv')
df.plot( # plotting 'height' against 'age'
    y='height',
    x='age',
    title='Adult heights',
    kind='scatter',
    figsize=[8, 6],
    xlabel='Age / years',
    ylabel='Height / inches',
    alpha=0.36
)
plt.show()
```

