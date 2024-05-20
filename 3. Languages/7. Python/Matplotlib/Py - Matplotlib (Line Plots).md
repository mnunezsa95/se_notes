See [[Py - Introduction to Python]], [[Py - Matplotlib (Installing and Importing)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Matplotlib (Plots)]]
Documentation:
* [Matplotlib Official Documentation](https://matplotlib.org/stable/)

---

#### What is a Line Plot?
* A line plot represents data that is connected chronologically and each time point of data has some dependence on the previous point
	* Temperature Data
	* Traffic Data
	* Stock Market Data

#### Plotting a Line Plot
* `plot()` -> creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes 
	* `rot=` -> rotates the x-axis tick labels by a specified degree

```Python
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

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_3_1656569226.png)
#### Multiple Lines on a Line Plot
* Plotting more than one line on the same plot
	* Pass an list as the y value in the `y` argument of the `plot()` method
* Example
```python
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