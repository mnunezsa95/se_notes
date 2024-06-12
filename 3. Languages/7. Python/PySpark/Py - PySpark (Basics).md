See: 
* [[Py - Introduction to Python]]
Resources:
* Documentation: [PySpark](https://spark.apache.org/docs/1.1.0/programming-guide.html)
* Article: [SparkSession vs SparkContext in Apache Spark](https://data-flair.training/forums/topic/sparksession-vs-sparkcontext-in-apache-spark/)

---
# Distributed Systems

## What is a Distributed System?
* **Distributed Systems**: Systems that give access to files stored on different machines
	* These systems are useful when data grows and one computer is not enough to perform calculations 
	* Files are divided into segments, and each segment can be saved multiple times, in a few different locations

## Spark: A Distributed System
* **Spark** is a type of distributed system, which allows it to quickly access tons of data to perform calculations.
* Spark’s distributed file system consists of multiple **nodes** (a computer with the ability to computer and process data)
	* Types of Nodes
		1) **NameNode** -- manages the assignment of files to different machine clusters
		2) **DataNode** -- stores and processes data. 
			* Each file will be replicated in multiple data nodes to avoid data loss
		![[pyspark-nodes.png]]

## Improving Data Storage and Processing
* There are two ways to improve a computer's ability to store and process more data
	1) Scaling Up -- increasing the efficiency of every node or replacing the nodes with more powerful one 
	2) Scaling out -- Increasing the _number_ of nodes in a cluster
	![[scaling-types.png]]


# Resilient Distributed Datasets

## What is the Resilient Distributed Datasets?
* **Resilient Distributed Dataset (RDD)** -- the basic building block of the Spark Library
	* **RDD** -- a distributed data structure located across multiple nodes in a cluster

## What is Apache Spark?
* **Apache Spark** -- an open-source distributed computing framework used to store and process data on several computers
	* Originally written in **Scala**

## What is PySpark?
* **PySpark** -- a newer version of **Apache Spark** written in Python

## What are RDDS used for?
* **RDDs** -- used for transforming unstructured data and are part of more complex data types


---
---
# Working with PySpark: Basics
## Creating a SparkContext in PySpark

#### `SparkContext()`
* `SparkContext()` -- an object responsible for cluster operations
	* Arguments
		1) `appName=` -- the name of the object
```Python
from pyspark import SparkContext

# sc is short for Spark Context
sc = SparkContext(appName='IntroToSpark')
```

#### `parallelize()`
* Converts a list into an Resilient Distributed Database
	* Arguments
		1) `list` -- the list to be converted into an RDD
```Python
from pyspark import SparkContext

# sc is short for Spark Context
sc = SparkContext(appName='TaxiTracker')
taxi_entry = sc.parallelize(['2009-01-01', 0, 0, 24])
print(taxi_entry) 
```

```
ParallelCollectionRDD[0] at parallelize at PythonRDD.scala:195
```

## Creating a SparkSession in PySpark
* A **DataFrame API** is required to work with a distributed file system
* PySpark has a DataFrame API called **Spark SQL** 
#### `SparkSession`
* Used to create an object to create and use DataFrames
```python
from pyspark.sql import SparkSession

APP_NAME = 'sampleApp'
spark = SparkSession.builder.appName(APP_NAME)
```

#### `getOrCreate()`
* Returns the SparkSession object created with `SparkSession` or creates it if it does not exist
	* Arguments:
		1) none
```Python
# Creating a SparkSession 
from pyspark.sql import SparkSession

APP_NAME = 'sampleApp'
spark = SparkSession.builder.appName(APP_NAME).getOrCreate()
```

```Python
# Creating a SparkSession without the status being displayed
from pyspark.sql import SparkSession

APP_NAME = 'sampleApp'
spark = SparkSession.builder.appName(APP_NAME) \ 
	.config('spark.ui.showConsoleProgress', 'false') \ 
	.getOrCreate()
```

---
---
# DataFrames in PySpark
* PySpark DataFrames:
	* Stores its rows in RDDS
	* Are immutable
		* Any change produces a new copy
	* Are lazily evaluated
		* The calculations are delayed until the user requests the results

### Differences between Pandas and PySpark DataFrames
* Pandas DataFrames consist of rows
* PySpark DataFrames contain column names and column values in each row of the table


# Working with DataFrames in PySpark
### Converting a Pandas DataFrame into PySpark DataFrame
#### `createDataFrame()`
* Converts a pandas DataFrame into a Spark DataFrame
	* Arguments
		* 1) `dataframe` -- the pandas DataFrame to be used 
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi_df = pd.read_csv('/datasets/pickups_terminal_5.csv')
taxi = spark.createDataFrame(taxi_df)

print(taxi)
```

```Result
DataFrame[date: string, hour: bigint, minute: bigint, pickups: double]
```

### Accessing values from a PySpark DataFrame
#### `take()`
* Retrieves content from an RDD and returns a list of rows
	* Arguments
		1) `number_elements` -- specifies the number of elements to be extracted from the RDD
```Python
# Using take() to access from a SparkContext
from pyspark import SparkContext

sc = SparkContext(appName='TaxiTracker')
taxi_entry = sc.parallelize(['2009-01-01', 0, 0, 24])
print(taxi_entry.take(4))
```

```
[Stage 0:> 
['2009-01-01', 0, 0, 24]
```

```Python
# Using take() to access from a SparkSession
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi_df = pd.read_csv('/datasets/pickups_terminal_5.csv')
taxi = spark.createDataFrame(taxi_df)

collected_taxi = taxi.take(5)
print(collected_taxi)
```

```Result
[Row(date='2009-01-01', hour=0, minute=0, pickups=24.0), 
Row(date='2009-01-01', hour=0, minute=30, pickups=35.0), 
Row(date='2009-01-01', hour=1, minute=0, pickups=25.0), 
Row(date='2009-01-01', hour=1, minute=30, pickups=25.0), 
Row(date='2009-01-01', hour=2, minute=0, pickups=16.0)]
```

### Reading & Loading Data from a CSV 
#### `read.load()`
* Reads information form a CSV file and generates a PySpark DataFrame
	* Arguments
		1) `filepath` -- the path to the file
		2) `format` -- the format of the file being loaded
		3) `inferSchema` -- specifies if the data type should be inferred
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')
```

### Displaying information from a PySpark DataFrame
#### `show()` 
* Returns a nicely formatted printout of the PySpark DataFrame
	* Arguments
		1) `number_rows` -- the number of rows to print
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

print(taxi.show(5))
```

```Result
+-------------------+----+------+-------+
|               date|hour|minute|pickups|
+-------------------+----+------+-------+
|2009-01-01 00:00:00|   0|     0|   24.0|
|2009-01-01 00:00:00|   0|    30|   35.0|
|2009-01-01 00:00:00|   1|     0|   25.0|
|2009-01-01 00:00:00|   1|    30|   25.0|
|2009-01-01 00:00:00|   2|     0|   16.0|
+-------------------+----+------+-------+
only showing top 5 rows

None
```

#### `describe()`
* Returns information about the columns in the DataFrame
* Arguments
	* None
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

print(taxi.describe().show()) # Prints info about columns
```

```Result
+-------+------------------+------------------+------------------+
|summary|              hour|            minute|           pickups|
+-------+------------------+------------------+------------------+
|  count|            128974|            128974|            128969|
|   mean|11.566509529052366|15.004419495402175|29.009451883786028|
| stddev| 6.908556452594711|15.000057500526209|  22.4493784836831|
|    min|                 0|                 0|               1.0|
|    max|                23|                30|             310.0|
+-------+------------------+------------------+------------------+
```

#### `summary()`
* Prints a detailed summary of information about the DataFrame
	* Arguments
		* None
```Python
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
print(taxi.summary().show()) 
```

```Result
+-------+------------------+------------------+------------------+
|summary|              hour|            minute|           pickups|
+-------+------------------+------------------+------------------+
|  count|            128974|            128974|            128974|
|   mean|11.566509529052366|15.004419495402175| 29.00832725975778|
| stddev| 6.908556452594711|15.000057500526209|22.449669931429067|
|    min|                 0|                 0|               0.0|
|    25%|                 6|                 0|              11.0|
|    50%|                12|                30|              27.0|
|    75%|                18|                30|              40.0|
|    max|                23|                30|             310.0|
+-------+------------------+------------------+------------------+
```

#### Displaying specific columns from a PySpark DataFrame
* Individual columns can be accessed using the following syntax
```python
df[['date', 'hour', 'minute']]
```

```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

# Printing the date, hour and minute columns 
print(taxi[['date', 'hour', 'minute']].show(5))
```

### Displaying the Number of Rows
#### `count()`
* Counts the number of records (rows) in a PySpark DataFrame
	* Arguments
		* None
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

print(taxi.count()) # 128974
```


---
# Handling Missing Data
#### `dropna()`
* Drops all rows with missing values 
	* Arguments
```python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.dropna()

print(taxi.count()) # 128969
```

#### `fillna()`
* Replaces missing values with a specific value (passed as an argument)
	* Arguments
		1) `new_value` -- the value to be used when filling missing values
```Python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)

print(taxi.describe().show())
```

```Result
+-------+------------------+------------------+------------------+
|summary|              hour|            minute|           pickups|
+-------+------------------+------------------+------------------+
|  count|            128974|            128974|            128974|
|   mean|11.566509529052366|15.004419495402175| 29.00832725975778|
| stddev| 6.908556452594711|15.000057500526209|22.449669931429067|
|    min|                 0|                 0|               0.0|
|    max|                23|                30|             310.0|
+-------+------------------+------------------+------------------+
```


---
# Grouping & Sorting Data
### Grouping Data 
* The `groupBy()` method can be used to group data
* To use the `groupBy()` function:
	* Use the `groupBy()` method and determine how grouping will be done
	* Chain an aggregate function to the `groupBy()` function
		* `sum()`
		* `mean()`
		* `avg()`
		* `count()`
		* `min()`
		* `max()`
	* Chain the `select()` method to specify how data will be selected
#### `groupBy()`
* Groups data in a DataFrame by specified column
	* Arguments
		1) `column` -- a string containing the column to group data by
```Python
print(taxi.groupBy("date").mean().select("date", "avg(pickups)").show())
```

```Result
+-------------------+------------------+
|               date|      avg(pickups)|
+-------------------+------------------+
|2009-06-10 00:00:00| 28.48936170212766|
|2009-10-15 00:00:00|35.895833333333336|
|2010-03-25 00:00:00|28.458333333333332|
|2010-04-19 00:00:00|33.208333333333336|
|2010-05-03 00:00:00|             44.75|
|2010-08-21 00:00:00|           17.8125|
|2010-10-22 00:00:00|36.208333333333336|
|2010-11-02 00:00:00|            34.625|
|2011-05-25 00:00:00|35.829787234042556|
...

```

## Sorting Data
#### `sort()`
* Sorts the DataFrame by a specified condition
	* Arguments
		1) `condition` -- a string containing the condition to sort by
```Python
print(taxi.groupBy("date").mean().select("date", "avg(pickups)").sort("avg(pickups)", ascending=False).show())
```

```Result
+-------------------+------------------+
|               date|      avg(pickups)|
+-------------------+------------------+
|2012-03-07 00:00:00| 84.41666666666667|
|2011-03-02 00:00:00|             82.75|
|2012-03-09 00:00:00| 71.52083333333333|
|2014-03-05 00:00:00| 69.02083333333333|
|2012-03-10 00:00:00| 66.41666666666667|
|2012-03-22 00:00:00|             64.25|
|2013-03-22 00:00:00|            64.125|
|2013-11-01 00:00:00| 64.02083333333333|
|2013-03-06 00:00:00|62.723404255319146|
...
```


---
# SQL Queries in DataFrames

## Performing SQL Queries on an Existing DataBase
* Steps to perform SQL queries:
	1) MUST register a temporary table to add to the Database
	2) Use the `sql()` to perform a sql query

#### `registerTempTable()`
* Registers a temporary table to add the DataFrame to the data base
```python
import numpy as np
import pandas as pd
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi.registerTempTable('taxi') # Registers a temp table
```

#### `sql()`
* Performs a SQL query on the SparkSession 
	* Arguments
		1) `sql_query` -- a string containing the sql query to be executed
```Python
# Example
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

print(spark.sql("SELECT COUNT(*) FROM taxi WHERE pickups > 100").show())
```

```Result
+--------+
|count(1)|
+--------+
|    1431|
+--------+
```

```Python
# Example
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()

taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

print(spark.sql("SELECT MIN(CAST(date as DATE)), MAX(CAST(date as DATE)) FROM taxi").show())
```

```Result
+-----------------------+-----------------------+
|min(CAST(date AS DATE))|max(CAST(date AS DATE))|
+-----------------------+-----------------------+
|             2009-01-01|             2016-06-30|
+-----------------------+-----------------------+
```

```Python
# Example -- Using the ORDER BY clause in the query to show the first 5 rows of the result

from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()
taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

print(spark.sql("SELECT * FROM taxi ORDER BY pickups DESC").show(5))
```

```Result
+-------------------+----+------+-------+
|               date|hour|minute|pickups|
+-------------------+----+------+-------+
|2015-11-01 00:00:00|   1|    30|  310.0|
|2010-09-23 00:00:00|  22|    30|  288.0|
|2012-03-07 00:00:00|  21|     0|  268.0|
|2011-03-02 00:00:00|  20|    30|  264.0|
|2011-03-02 00:00:00|  18|    30|  263.0|
+-------------------+----+------+-------+
only showing top 5 rows
```


```Python
# Exaple -- Using the ORDER BY and GROUP BY operators
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()
taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

# If your query is too long, the string can be split in two. Python automatically joins the parts if there is no comma.
print(spark.sql('SELECT date, AVG(pickups) FROM taxi ' 'GROUP BY date ORDER BY AVG(pickups) DESC').show())
```

```Result
+-------------------+------------------+
|               date|      avg(pickups)|
+-------------------+------------------+
|2012-03-07 00:00:00| 84.41666666666667|
|2011-03-02 00:00:00|             82.75|
|2012-03-09 00:00:00| 71.52083333333333|
|2014-03-05 00:00:00| 69.02083333333333|
|2012-03-10 00:00:00| 66.41666666666667|
|2012-03-22 00:00:00|             64.25|
|2013-03-22 00:00:00|            64.125|
|2013-11-01 00:00:00| 64.02083333333333|
```

```Python
# Exaple -- Using the ORDER BY and GROUP BY operators
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()
taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

print(spark.sql('SELECT EXTRACT(MONTH FROM date), AVG(pickups) FROM taxi ' 'GROUP BY EXTRACT(MONTH FROM date) ORDER BY AVG(pickups) DESC').show())
```

```Result
+-------------------------+------------------+
|month(CAST(date AS DATE))|      avg(pickups)|
+-------------------------+------------------+
|                        3| 34.61413319776309|
|                       10|31.492839171666343|
|                        2|29.856671982987773|
|                        5| 29.81593638978176|
|                        4|29.313725490196077|
|                        9|29.158446485623003|
|                       11|28.860367558929283|
....
```

```Python
# Exaple -- Using the ORDER BY and GROUP BY operators
from pyspark.sql import SparkSession

APP_NAME = "DataFrames"
SPARK_URL = "local[*]"

spark = SparkSession.builder.appName(APP_NAME).getOrCreate()
taxi = spark.read.load('/datasets/pickups_terminal_5.csv', format='csv', header='true', inferSchema='true')

taxi = taxi.fillna(0)
taxi.registerTempTable("taxi")

print(spark.sql('SELECT hour, AVG(pickups) FROM taxi ' 'GROUP BY hour ORDER BY AVG(pickups) DESC').show(10))
```

```Result
+----+------------------+
|hour|      avg(pickups)|
+----+------------------+
|   8| 48.98208348725527|
|   9| 45.74220335855324|
|  18|45.131967515688444|
|  19| 40.18456995201181|
|  17| 37.68493909191584|
...
```
