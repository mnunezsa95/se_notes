See: [[Py - Introduction to Python]], [[Py - Creating a Virtual Environment]], [[Py - Modules, Packages and Libraries]], 

---

## Installing Packages, Modules and Libraries

#### The Python Package Index: pypi
* [Python Package Index](https://pypi.org/)) = a database of python packages


#### What is `pip`?
* PIP (pip install packages) = a built in pip package manager for Python

#### Installing with `pip`
1) Ensure the virtual environment (venv) is activated
2) Run the pip install for the specific package
```shell
# Syntax
python pip install package_name
```

* Example
```bash
# Example
python -m pip install -U prettytable
```

#### Installing with `conda`
1) Ensure you are the virtual conda (base) environment is activated
2) Run the `conda install` command
	* `-c` -- stands for channel
```shell
# Syntax
conda install -c channel_name package_name
```

* Example
```shell
# Acitvating base environment
conda activate

# running the conda install command
conda install -c plotly plotly
```


## Updating Packages, Modules, and Libraries

#### Updating with `pip`
1) 
```bash
# Syntax 

```

#### Updating with `conda`
1) Run the `conda update` command
```bash
# Syntax 
conda update package_name
```
 