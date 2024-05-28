See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Methods)]]
* [[Py - Numpy (Methods)]]

Resources
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)

---

##### `matplotlib.pyplot.figure()`
* Creates a new figure, or activate an existing figure
* Arguments
	* `num=` -- an int or str serving as unique identifier for the figure
	* `figsize=` -- Width and height in inches
	* `facecolor=` -- A str identifying the background color
	* `layout=` -- A str describing the layout mechanism for positioning of plot elements to avoid overlapping Axes decorations
		* Options: `'constrained'`, `'compressed'`, `'tight'`, `'none'`
```Python

```

##### `matplotlib.pyplot.legend()`
* Places a legend on the Axes
* Arguments
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

##### `matplotlib.pyplot.arrow()`
* Adds an arrow to the axes; draws an arrow from `(x, y)` to `(x + dx, y + dy)`
* Arguments
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