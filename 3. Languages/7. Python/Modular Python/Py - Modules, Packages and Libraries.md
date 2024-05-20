See: [[Py - Introduction to Python]]

---

## Modules, Packages, and Libraries 
* Modules, packages, and libraries are a hierarchical way to organize Python code that is meant to be used by other people.
* These three words are often used interchangeably 
* Python comes installed with some built-in modules, packages and libraries
#### Modules
* A `module` -- a Python script (a text file with a `.py` extension) that contains definitions of functions, classes, and/or variables that all help to solve some particular problem.
#### Package
* A `package` -- a collection of related modules. So a package will contain multiple scripts.
#### Library
* A `library` -- a collection of Python packages and modules.

## Checking Module, Package and Library Versions 
* These modules, packages and libraries get regular updates to stay up-to-date
* When not working properly, check the version and documentation
	* Refer to the documentation for support 
```python
# Examples: Checking Sersions

## Checking module version 
import sys
sys.version # '3.8.10 (default, May 19 2021, 13:12:57)[MSC v.1916 64 bit (AMD64)]

## Checking the package version
import pandas as pd
print(pd.__version__) # 1.2.5

## Checking the library version
from matplotlib
print(matplotlib.__version__) # 3.3.4
```