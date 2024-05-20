See [[Py - Introduction to Python]], [[Py - Importing Modules]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Looping over a dictionary (review)
```python
student_dict = {"student": ["Angela", "James", "Lily"], "score": [56, 76, 98]}

# Looping through dictionaries
for key, value in student_dict.items():
  print(value)
```

#### Looping through a DataFrame
* Pandas has a built-in method called `iterrows()` that iterates over the rows of particular DataFrame
```Python
# Looping through DataFrame
import pandas

for index, row in student_data_frame.iterrows():
  print(row.student)
print(row.score)
```