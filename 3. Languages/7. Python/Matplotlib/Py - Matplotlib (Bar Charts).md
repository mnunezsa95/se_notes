See [[Py - Introduction to Python]], [[Py - Matplotlib (Installing and Importing)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Matplotlib (Plots)]]
Documentation:
* [Matplotlib Official Documentation](https://matplotlib.org/stable/)

---

#### What is a Bar Chart?
* Bar charts allow us to compare numeric properties between categorical properties.
* Levels are plotted on one chart axis, and values are plotted on the other axis. 
* Each categorical value claims one bar, and the length of each bar corresponds to the bar’s value.

#### Plotting a Line Plot
* `plot()` -> creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes 
	* `kind=` -> a string to specify the kind of plot to be used
		* `bar` -> uses a bar chart to plot information
	* `y=` -> a string specifying the data to plot on y-axis
		* If not specified, Pandas will will automatically create a bar for every column in the DataFrame
* Example
```Python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/west_coast_pop.csv')

df.plot(x='year',
        kind='bar',
        title='West coast USA population growth',
        xlabel='Year',
        ylabel='Population (millions)')

plt.legend(['CA', 'OR', 'WA'])
plt.show()
```

#### Editing the Legend
* `legend()` -> Allows for manual specification of the legend labels rather than the default behavior of using the column names from the DataFrame.
* Arguments
	* `legend_names` -> a list of label names; the order of the legend labels in the list will correspond to the order of the columns in the DataFrame
* Example
```Python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/west_coast_pop.csv')

df.plot(x='year',
        kind='bar',
        title='West coast USA population growth',
        xlabel='Year',
        ylabel='Population (millions)')

plt.legend(['CA', 'OR', 'WA'])
plt.show()

```