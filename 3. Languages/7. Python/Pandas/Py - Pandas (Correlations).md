See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

----
#### Calculating the Correlation Coefficient 
* `corr()` -> calculates the correlation coefficient 
	* Called on a column or entire DataFrame. 
		* When called on DataFrame it returns a Correlation Matrix (DataFrame with the correlation coefficients for each pair of variables)
* Arguments
	* `variable` -> the second variable to be used in the correlation analysis
* Example
```python
import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

# Calling corr() method on the height column of the DataFrame & passing in the weight column as an arg
df['height'].corr(df['weight']) # 0.9165261045538688
```

```Python
# Calling a corr() method on a DataFrame
import pandas as pd
df = pd.read_csv('/datasets/height_weight.csv')
df.corr()
```
``
```
          height    weight       age      male
height  1.000000  0.916526  0.010042  0.760690
weight  0.916526  1.000000  0.228538  0.785218
age     0.010042  0.228538  1.000000  0.004750
male    0.760690  0.785218  0.004750  1.000000
```