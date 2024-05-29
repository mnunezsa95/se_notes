See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (DataFrame Object)]]
* [[Py - Pandas (Series Object)]]
* [[Py - Matplotlib (Methods)]]
* [[Py - Matplotlib (Graphing)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)


----
# Plotting 
- Pandas and Matplotlib can be used together to create simple plots:
    - **Pandas**:
        - `plot()` -- generates a figure where all numeric columns in a DataFrame are plotted on the same axes.
            - Indices are on the x-axis.
            - Column values are on the y-axis.
    - **Matplotlib**:
        - `show()` -- displays a figure created with pandas.
        - `savefig()` -- saves figures as image files.
            - The file is saved in the directory of the Python script or Jupyter Notebook.
            - The file format is determined by the extension used.
```python
# Example -- Simple Plotting

import pandas as pd
from matplotlib import pyplot as plt

df = pd.DataFrame({'a':[2, 3, 4, 5], 'b':[4, 9, 16, 25]})
df.plot() # calling plot on an entire DataFrame
plt.show()

df['b'].plot() # calling plot on a single column
plt.show()
plt.savefig('myplot.png') # saving the plot figure as a .png file
```


----

## Bar Plot
* `df.plot()` -- creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes 
	* Arguments (most relevant to Scatterplots)
		- `kind=` -- a string that specifies the type of plot to be used.
		    - `'bar'` - uses a bar chart to plot information.
		- `y=` -- a string that specifies the data to plot on the y-axis.
		    - If not specified, Pandas will automatically create a bar for each column in the DataFrame.
```Python
# Example -- Plotting a Bar Plot

import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/west_coast_pop.csv')
df.plot(x='year', kind='bar', title='West coast USA population growth', 
		xlabel='Year', ylabel='Population (millions)')

plt.legend(['CA', 'OR', 'WA'])
plt.show()
```


---
## Scatterplot
* `df.plot()`  -- creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
	* Arguments (most relevant to Scatterplots)
		- `kind=` -- a string used to determine the type of plot.
		    - `'scatter'` -- employs a scatterplot to represent data.
		- `alpha=` -- a float ranging from 0 (full transparency) to 1 (no transparency) that governs the opacity of the points (default is `1`)
```python
# Example -- Plotting a scatterplot

import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/height_weight.csv')
# plotting 'height' against 'age'
df.plot( 
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

## Line Plot
* `plot()` -- creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes 
	* Arguments (most relevant to Line plots)
		* `rot=` -- rotates the x-axis tick labels by a specified degree
```Python
# Example -- Plotting a line graph

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('sbux.csv')

df.plot(x='date',
        y='open',
        legend=False,
        title='Starbucks market open',
        xlabel='Date',
        ylabel='Share price / USD',
        rot=45)
plt.show()
```

* Multiple Lines on a Line Plot
	- To plot multiple lines on a single plot:
	    - Provide a list as the y-value in the `y` argument of the `plot()` method.
```python
# Example -- plotting a line graph with multiple lines

import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/sbux.csv')
cols = ['open', 'close']

df.plot(
    title='Historic SBUX price',
    x='date',
    y=cols,
    xlabel='Date',
    ylabel="Share price / USD",
    rot=50
)

plt.show()
```

## Histograms
- Pandas offers two methods for plotting histograms:
    - Contrast between `hist()` and `plot(kind=hist)`:
        - When applied to a DataFrame, `hist()` generates distinct graphs for each variable; meanwhile, `plot()` consolidates all distributions into a single graph.
        - Unlike the `plot()` method, `hist()` lacks keyword arguments for `title=`, `xlabel=`, or `ylabel=`
        
* `plot()` -- creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
	* Arguments (most relevant to histograms)
		- `kind=` -- a string indicating the type of plot to generate.
		    - `hist` -- utilizes a histogram to represent frequency.
		- `bins=` -- accepts a number or list of numbers that dictates the number of bins to incorporate in the histogram (default is 10).
- `hist()` -- Constructs histograms for the columns of the DataFrame.
	- When `hist()` is invoked on a DataFrame without any arguments, it generates an individual graph for each numerical column.
	- Arguments
	    - `column=` -- designates the column for which to plot the distribution.
	    - `bins=` -- accepts a number or list of numbers that determines the number of bins to incorporate in the histogram (defaults to 10).
```Python
# Example -- calling plot(kind=hist) on an entire DataFrame

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.plot(kind='hist')
plt.show()
```

```Python
# Example -- calling plot(kind=hist) on a column

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df['height'].plot(kind='hist', bins=30)
plt.show()
```

```python
# Example -- calling plot() on the height column twice to show the distribution of male and female on the same plot

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
# Example -- Using a list to specify the bins of the histogram

import pandas as pd
pur_time = pd.Series([36, 44, 73, 32, 44, 29, 63, 60, 55, 74, 61, 26, 76, 40, 39, 28, 69, 61, 54, 58, 47, 41, 70, 51, 58, 36, 71, 47, 74, 59, 50, 78, 59, 48, 67, 53, 67, 52, 38, 55, 53, 53, 43, 77, 44, 63, 63, 54])

pur_time.plot(kind='hist', alpha=0.5, bins=[15, 35, 55, 75, 90])
pur_time.plot(kind='hist', alpha=0.5, bins=[15, 45, 55, 90])
```

```python
# Example 
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/height_weight.csv')

df_20s = df[df['age'] < 30]
df_30s = df[(df['age'] >= 30) & (df['age'] < 40)]
df_40s = df[df['age'] >= 40]

df_20s['weight'].plot(kind='hist', bins=20, title='Wt/lbs', ylabel='Frequency')
df_30s['weight'].plot(kind='hist', bins=20, alpha=0.6)
df_40s['weight'].plot(kind='hist', bins=20, alpha=0.3)

plt.legend(['20s', '30s', '40s'])
plt.show()
```

```Python
# Example -- Calling hist() on an entire DataFrame

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.hist()
plt.show()
```

```Python
# Example -- Calling hist() on an entire DataFrame

import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('/datasets/height_weight.csv')

df.hist(column='height', bins=30)
plt.show()
```

## Scatter Matrix
* `plotting.scatter_matrix()` -- builds a scatter matrix
	* Arguments
		* 
```python
import pandas as pd
from matplotlib import pyplot as plt
df = pd.read_csv('height_weight.csv')

pd.plotting.scatter_matrix(df, figsize=(9, 9))
plt.show()
```