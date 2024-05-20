See: [[Py - Introduction to Python]], [[Py - Environmental Variables]]
Documentation:
* Official: [dotenv](https://pypi.org/project/python-dotenv/)

---

####  Installing the `.env` Module
```bash
pip install python-dotenv
```

#### Using `.env` Module to Retrieve Variables
```Python
from dotenv import dotenv_values # importing the dotenv_values fn from dotenv

config = dotenv_values(".env") # create a dict of the variables
API_KEY = config["API_KEY_OWM"] # get API_KEY variable
```