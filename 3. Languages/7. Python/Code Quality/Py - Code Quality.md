See: [[Py - Introduction to Python]], [[Py - Installing Packages, Modules, and Libraries]]
Resources:
* Documentation: [pylint](https://pylint.pycqa.org/en/latest/)
	* [List of pylint checkers](https://pylint.pycqa.org/en/latest/user_guide/checkers/features.html)
* Documentation: [PEP 8 Style Guide](https://peps.python.org/pep-0008/)

----
# Linters
* Linters -- check for different aspects of code styles, some are more restrictive, some are more suitable for large projects.
* Popular linters are easily integrated with IDEs

## Pylint
* `Pylint` -- a well-established, reputable linter for Python
* `Pylint` will output where the code does not follow the code-style (PEP8 by default)
#### Installing `pylint`
* `pylint` can be installed with `pip` or `conda`
```bash
pip install pylint
```

```bash
conda install pylint
```

#### Running `pylint`
1) Run pylint to check code based on the checkers listed ([see complete list](https://pylint.pycqa.org/en/latest/user_guide/checkers/features.html))
```bash
# SYNTAX
pylint script_name.py
```
`
```Example
- ************ Module my_script
my_script.py:6:8: C0303: Trailing whitespace (trailing-whitespace)
my_script.py:8:0: C0305: Trailing newlines (trailing-newlines)
my_script.py:1:0: C0114: Missing module docstring (missing-module-docstring)
my_script.py:3:0: C0103: Constant name "a" doesn't conform to UPPER_CASE naming style (invalid-name)

---
Your code has been rated at 0.00/10 (previous run: 0.00/10, +0.00)
```

* Certain checkers can be disabled as needed
```bash
pylint --disable=C0114 my_script.py
```