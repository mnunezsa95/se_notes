See: [[Py - Introduction to Python]], [[Py - Jupyter (Intro to Jupyter Notebooks)]]

---

## Writing and Running Code in Jupyter Notebook

#### Navigating Jupyter Notebook
* Opening Jupyter Notebook will start a server session, opening a window in your web browser. 
	* The server will be created on the local machine (no internet needed)
		* The address should say` localhost:xxxx/tree`, where `xxxx` is port 8888 by default, but may be another port if multiple Jupyter Notebook sessions launched at the same time. 

#### Creating a Jupyter Notebook
* Jupyter Notebooks are of the filetype `.ipynb`.
	* The `.ipynb` file extension stands for "iPython notebook" because Jupyter is derived from the older [iPython](https://ipython.org/) project. `.ipynb` files are just plain text files with a [JSON](https://www.json.org/json-en.html) format, which Jupyter interprets and turns into visually beautiful notebooks!
* The cells are used to portray information as either
	* python code
	* markdown language

#### Working in a Jupyter Notebook
* Jupyter Notebooks allow for  work in the command line within a notebook itself by using the special `!` symbol. 
```Python
# Code in cpus.py
import os
cpu_num = os.cpu_count()
print(f"My computer has {cpu_num} CPUs")
```

* Variables are assigned to the environment in Jupyter Notebooks
```python
# running the code above
!python cpus.py
```
