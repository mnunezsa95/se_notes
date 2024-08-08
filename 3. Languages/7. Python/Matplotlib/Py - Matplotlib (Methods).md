See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Methods)]]
* [[Py - NumPy (Methods)]]
* [[Py - SciPy (Methods)]]

Resources
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

---


##### `pyplot.boxplot()`
* Draws a box and whisker plot.
	* Parameters (see complete list [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html))
		* `x` (array or sequence) -- The input data
			* If sequence, boxplot draw for each column in `x`
		* `whis=` (float) -- The position of the whiskers.
			* If a float, the lower whisker is at the lowest datum above `Q1 - whis*(Q3-Q1)`, and the upper whisker at the highest datum below `Q3 + whis*(Q3-Q1)`, where Q1 and Q3 are the first and third quartiles. 
		* `vert=` (bool) -- the position of the whiskers
			* If `True`, draws vertical boxes. 
			* If `False`, draw horizontal boxes.
	* Methods
		* `get_data()` -- returns the data from a boxplot
```python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('/datasets/sales.csv')

plt.boxplot(df['Sales'].values)
plt.ylabel('Total sales')
plt.title('Outliers in total sales')
plt.show()
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

##### `pyplot.figure()`
* Creates a new figure, or activate an existing figure
	* Parameters
		* `num=` -- an int or str serving as unique identifier for the figure
		* `figsize=` -- Width and height in inches
		* `facecolor=` -- A str identifying the background color
		* `layout=` -- A str describing the layout mechanism for positioning of plot elements to avoid overlapping Axes decorations
			* Options: `'constrained'`, `'compressed'`, `'tight'`, `'none'`
```Python

```

##### `pyplot.legend()`
* Places a legend on the Axes
	* Parameters
		* `legend_names` -> a list of label names; the order of the legend labels in the list will correspond to the order of the columns in the DataFrame
```python
matplotlib.pyplot.legend(*args, **kwargs)
```

```Python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('/datasets/west_coast_pop.csv')
df.plot(x='year', kind='bar', title='West coast USA population growth', 
		xlabel='Year', ylabel='Population (millions)')

plt.legend(['CA', 'OR', 'WA'])
plt.show()
```

##### `pyplot.arrow()`
* Adds an arrow to the axes; draws an arrow from `(x, y)` to `(x + dx, y + dy)`
	* Parameters
		* `x, y` -- The x and y coordinates of the arrow base
		* `dx, dy` -- The length of the arrow along x and y direction
		* `**kwargs` (see documentation)
```Python
matplotlib.pyplot.arrow(x, y, dx, dy, **kwargs
```

```Python
import numpy as np
import matplotlib.pyplot as plt

vector = np.array([75, 15])
plt.figure(figsize=(3.5,3.5))
plt.axis([0, 100, 0, 100]) 
plt.arrow(0, 0, vector[0], vector[1], head_width=4, length_includes_head="True")
plt.xlabel('Price')
plt.ylabel('Quality')
plt.grid(True)
plt.show()
```


##### `pyplot.imshow()`
* Display data as an image, i.e., on a 2D regular raster.
	* Parameters (see complete list of parameters [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.imshow.html))
		* `X` -- An array-like or PIL image 
		* `cmap=` -- A string or color map, representing the Colormap instance or registered colormap name used to map scalar data to colors.
		* `norm=` -- A string specifying the normalization method used to scale scalar data to the (0, 1) range before mapping to colors using `cmap`.
```Python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

image = Image.open('/datasets/ds_cv_images/face.png')
array = np.array(image)

plt.imshow(array, cmap='gray')
plt.colorbar()
```

##### `pyplot.colorbar()`
* Adds a colorbar to a plot.
	* Parameters
		* `mappable=` -- The `matplotlib.cm.ScalarMappable` (i.e., `AxesImage`, `ContourSet`, etc.) described by this colorbar. 
		* `cax=` -- Specifies the Axes into which the colorbar will be drawn. 
			* If `None`, then a new Axes is created and the space for it will be stolen from the Axes(s) specified in `ax`.
		* `ax=` -- An iterable the represents one or more parent Axes from which space for a new colorbar Axes will be stolen. 
			* This parameter is only used if `cax` is not set.
		* `use_gridspec=` -- an optional boolean representing the grid spec
			* If `cax` is `None`, a new `cax` is created as an instance of Axes. 
			* If `ax` is positioned with a subplotspec and `use_gridspec` is `True`, then `cax` is also positioned with a subplotspec.
```Python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

image = Image.open('/datasets/ds_cv_images/face.png')
array = np.array(image)

plt.imshow(array, cmap='gray')
plt.colorbar()
```