See 
* Python: [[Py - Introduction to Python]]
* Pandas: [[Py - Pandas (Data Structures)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Pandas Behind the Scenes
* When Pandas reads data from a text file, it automatically converts the raw column data into Pandas data types
* Typically straightforward
	* If a column contains ONLY numbers, it will be read into a `float` or `int` data type
	* If a column contains ONLY words, it will be read into an `object` data type
	* If a column contains a mix words and numbers it will become an an `object` data type

