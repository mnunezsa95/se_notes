See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Renaming Columns
* Column headers are sometimes a bit messy and do not represent the data in their column and oftentimes include unnecessary spaces
* snake_case is preferred when naming data columns

* Example: Renaming columns
```Python
import pandas as pd

# measurements are stored in a list of lists 
measurements = [['Sun', 146, 152], ['Moon', 0.36, 0.41], ['Mercury', 82, 217],['Venus', 38, 261], ['Mars', 56, 401], ['Jupiter', 588, 968], ['Saturn', 1195, 1660], ['Uranus', 2750, 3150], ['Neptune', 4300, 4700], ['Halley\'s comet', 6, 5400]]

# column names are stored in the header variable
header = ['Celestial bodies ', 'MIN', 'MAX'] 

# converting the data above into 'celestial' DataFrame
celestial = pd.DataFrame(data=measurements, columns=header)

celestial = celestial.rename(
  columns={
    'Celestial bodies ': 'celestial_bodies',
    'MIN': 'min_distance',
    'MAX': 'max_distance'
  }
)
```