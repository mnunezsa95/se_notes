See: [[Py - Introduction to Python]], [[Py - Code Quality]], [[Py - Errors and Exceptions]]
Resources:

----

# Testing Code

## Unit Tests
* Unit tests are used to test individual parts of code. 

#### The `pytest` Library
* `pytest` -- one of the best libraries for running unit tests in Python and provides functionality like:
	* running tests explicitly
	* filtering which test cases to run
	* rerunning only failed tests
	* reporting test results

#### Installing `pytest`
* `pytest` can be installed with `pip` or `conda`
```bash
pip install pytest
```

```bash
conda install pytest
```

#### How `pytest` Works
1) `pytest` looks for functions with names starting with `test_` in the code and runs them.
2) If no `AssertionException` is raised, then the function is considered to have passed
```Python
def sign(x):
    """Returns the sign of number."""
    if x is None:
        return None
    if x < 0:
        return -1
    return 1

# it tests the sign function
def test_sign():
    assert sign(-10) == -1
    assert sign(10) == 1
    assert sign(0) == 1
    assert sign(None) is None
```

#### What is an Assertion?
* `AssertionException` -- a type of exception raised with assertion statements, which are logical sanity check statements embedded in the code. 
* Assertions are always meant to be `True`, unless there is an issue then it would be `False`
	* If `False`, an `AssertionError` is raised with the `assertion_message`
```Python
# SYNTAX

# The expression should yield True if there are no issues, otherwise False.
assert expression[, assertion_message]
```

#### Running `pytest`
* Use the following command
```bash
# SYNTAX

pytest script_name.py
```

* `pytest` provides a report that looks something like this:
```Example

$ pytest sign.py
========================== test session starts ================================
platform linux -- Python 3.9.12, pytest-6.2.5, py-1.10.0, pluggy-1.0.0
rootdir: /home/dpdonetskov/projects/dxp
plugins: anyio-3.3.4
collected 1 item

sign.py F                                                                [100%]

=========================== FAILURES ==========================================
___________________________ test_sign _________________________________________

    def test_sign():
        assert sign(-10) == -1
>       assert sign(10) == 1
E       assert None == 1
E        +  where None = sign(10)

sign.py:11: AssertionError
========================= short test summary info =============================
FAILED sign.py::test_sign - assert None == 1
========================== 1 failed in 0.28s ===================================
```

