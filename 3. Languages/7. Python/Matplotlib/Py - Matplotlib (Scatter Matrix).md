See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Correlations)]], [[Py - Matplotlib (Scatterplots)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

----

#### What is a Scatter Matrix?
* A Scatter Matrix is a set of pairwise plots (or a scatterplot for every possible pair of parameters)

#### Building a Scatter Matrix
* `plotting.scatter_matrix()` -> builds a scatter matrix
* Arguments
	* 
```python
import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('height_weight.csv')

pd.plotting.scatter_matrix(df, figsize=(9, 9))
plt.show()
```
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_1_1656569039.png)