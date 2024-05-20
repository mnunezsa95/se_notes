See [[Py - Introduction to Python]], [[Py - Matplotlib (Installing and Importing)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], 
Documentation:
* [Matplotlib Official Documentation](https://matplotlib.org/stable/)

---

#### Simple Plotting
* Pandas and Matplotlib can be combined to create simple figures for plotting
	* `plot()` -> creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
		* Indices are on the x-axis 
		* Column values are on the y-axis
* Matplotlib
	* `show()` -> displays a figure created using pandas
	* `savefig()` -> saves figures as image files
		* File is saved in the directory where Python script or Jupyter Notebook is in
		* The extension used is what the file will be saved as
* Example
```python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.DataFrame({'a':[2, 3, 4, 5], 'b':[4, 9, 16, 25]})
df.plot() # calling plot on an entire DataFrame
plt.show()

df['b'].plot() # calling plot on a single column
plt.show()
plt.savefig('myplot.png') # saving the plot figure as a .png file
```


#### `plot()` 
* Creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
* Arguments
	* `title=` -> string to specify the title name
	* `style=` -> a string specifying the style of the plot marker; see options [here](https://matplotlib.org/stable/api/markers_api.html)
	* `x=` -> a string specifying the data to plot on x-axis
	* `y=` -> a string specifying the data to plot on y-axis
	* `xlabel=` -> a string specifying the label of the x-axis
	* `ylabel=` -> a string specifying the label of the y-axis
	* `legend=` -> a boolean to display the legend or not (`True` by default)
	* `xlim=` -> a number or list of two numbers specifying either the max (or min and max) value(s) to display on x-axis
	* `ylim=` -> a number or list of two numbers specifying either the max (or min and max) value(s) to display on y-axis
	* `grid=` -> a boolean that specifies whether to add grid-lines to the plot (`False` by default)
	* `figsize=` -> a list specifying the `[width and height]` of the figure
	* `color=` -> a string to specify the marker color
* Example
```Python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.DataFrame({'a':[2, 3, 4, 5], 'b':[4, 9, 16, 25]})

df.plot(
    title='A vs C',
    x="c",
    y="a",
    style="*",
    color="hotpink",
    figsize=[5, 5],
    xlim=[0, 12],
    ylim=[1, 6],
    xlabel="C",
    ylabel="A"
    grid=True
    legend=False
)
plt.show()
```

