See [[Py - Introduction to Python]], [[Py - Matplotlib (Installing and Importing)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Matplotlib (Plots)]]
Documentation:
* [Matplotlib Official Documentation](https://matplotlib.org/stable/)

---

#### What is a Histogram?
* A histogram shows how frequently different values appear for a variable in your dataset
	* Essentially they are useful for plotting the distribution of a single variable

#### Differences Between Bar Charts and Histograms
* Difference 1:
	* Bar charts are used to compare values for discrete variables
	* Histograms are used to plot distributions of _continuous numeric_ variables.
* Difference 2:
	* The order of bars in bar charts can be modified for style or communication
	* The order of bars in histograms cannot be changed.

#### Understanding the Histogram
* The X-axis represents the variable and has the range of values that the variable can take. 
* The Y-axis represents the frequency with which each value occurs
* A histogram partitions the range of values into sections called **bins**
	* The data will look different depending on the number of bins
* Example(s):
	* Here is a data set with 10, 25 and 100 bins.

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_8_1656570138.png)
 ![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_7_1656570121.png)

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_9_1656570153.png)


#### Plotting a Histogram (using `hist()`)
* `hist()` -> Make a histogram of the DataFrame’s columns.
	* If `hist()` is called on a DataFrame without any args, it creates a separate graph for each numerical column
	* Arguments
		* `column=` -> specifies the column to for which to plot distribution
		* `bins=` -> takes a number or list of numbers that specifies the number of bins to use on histogram (defaults to 10)
* Example:
```Python
# Calling hist() on an entire DataFrame

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.hist()
plt.show()
```

```Python
# Calling hist() on a particular column

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.hist(
	column='height',
	bins=30,
	
	)
plt.show()
```


#### Plotting a Histogram (using `plot()`)
* `plot()` -> creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
* Arguments
	* `kind=` -> a string to specify the kind of plot to be used
		* `hist` -> uses a histogram to plot frequency
	* `bins=`-> takes a number or list of numbers that specifies the number of bins to use on histogram (defaults to 10)
* Examples:
```Python
# calling plot(kind=hist) on an entire DataFrame

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.plot(kind='hist')
plt.show()
```

```Python
# calling plot(kind=hist) on a column

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df['height'].plot(kind='hist', bins=30)
plt.show()
```

```python
# calling plot() on the height column twice to show the distribution of male and female on the same plot

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df[df['male'] == 1]['height'].plot(kind='hist', bins=30)
# Include an alpha value so we can fully see both histograms
df[df['male'] == 0]['height'].plot(kind='hist', bins=30, alpha=0.8)

plt.legend(['Male', 'Female'])
plt.show()
```

```Python
# Using a list to specify the bins of the histogram

import pandas as pd
pur_time = pd.Series([36, 44, 73, 32, 44, 29, 63, 60, 55, 74, 61, 26, 76, 40, 39, 28, 69, 61, 54, 58, 47, 41, 70, 51, 58, 36, 71, 47, 74, 59, 50, 78, 59, 48, 67, 53, 67, 52, 38, 55, 53, 53, 43, 77, 44, 63, 63, 54])

pur_time.plot(kind='hist', alpha=0.5, bins=[15, 35, 55, 75, 90])
pur_time.plot(kind='hist', alpha=0.5, bins=[15, 45, 55, 90])
```


#### Difference between `hist()` and `plot(kind=hist)`?
* When called on a DataFrame `hist()` creates a different graph for each variable; `plot()` puts all distributions on one graph
* The `hist()` method does not have kwargs for `title=`, `xlabel=`, or `ylabel=`.


#### Example from Exercise
```python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/height_weight.csv')

df_20s = df[df['age'] < 30]
df_30s = df[(df['age'] >= 30) & (df['age'] < 40)]
df_40s = df[df['age'] >= 40]

df_20s['weight'].plot(kind='hist', bins=20, title='Weight / lbs', ylabel='Frequency')
df_30s['weight'].plot(kind='hist', bins=20, alpha=0.6)
df_40s['weight'].plot(kind='hist', bins=20, alpha=0.3)

plt.legend(['20s', '30s', '40s'])
plt.show()
```
