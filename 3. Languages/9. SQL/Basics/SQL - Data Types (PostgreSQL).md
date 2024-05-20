See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)
* [Tutorials Point: Data Types in PostgreSQL](https://www.tutorialspoint.com/postgresql/postgresql_data_types.htm)
* [PostgreSQL Tutorial: PostgreSQL Data Types](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-data-types/)

---
# Data Types 
* All data stored in a database has a data type
* Many data types have shorter forms called aliases
* The Data Type defines:
	1) The format that data has in the database
	2) The available range of values for that data
	3) The operations that can be performed with the data
* The number at the end of an data type shows the number of bytes the data type can take (i.e: `int4`, `float8`)

## Common Data Types

| Data Group    | Data Type              | Alias         | What it stores                                                                                                                       |
| ------------- | ---------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Numeric       | integer                | `int`, `int4` | whole numbers                                                                                                                        |
| Numeric       | real                   | `float4`      | real numbers                                                                                                                         |
| Numeric       | double precision       | `float8`      | a wide range of real numbers                                                                                                         |
| Character     | character              | `char(n)`     | a string with a fixed length                                                                                                         |
| Character     | character varying      | `varchar(n)`  | a string with an unfixed length                                                                                                      |
| Character     | text                   |               | a string with any length                                                                                                             |
| Date and Time | timestamp w/o timezone | `timestamp`   | date and time without timezone information                                                                                           |
| Date and Time | timestamp w/ timezone  | `timestampz`  | date and time with timezone information                                                                                              |
| Date and Time | date                   | `date`        | date in various formats                                                                                                              |
| Date and Time | time                   | `time`        | time from 00:00:00 to 24:00:00                                                                                                       |
| Date and Time | interval               |               | an interval between dates, times, or timestamps                                                                                      |
| Logical       | boolean                | `bool`        | `TRUE` & its alternatives: `true`, `t`, `yes`, `y`, `on`, `1`<br><br>`False` & its alternatives: `false`, `f`, `no`, `n`, `off`, `0` |
#### Numeric Data Types
* `integer` -- an `integer` data type ranges from -2147483648 to 2147483648
* `real` -- a real data type is a floating-point number. Number of precision for the `real` data type is 6-decimal points

#### Character Data Types
* `varchar(n)` -- a varying-length character string, where `n` is the maximum number of characters
* `text` -- a string of any length

#### Date and Time
* `timestamp` -- a date and time
	* Used to store events that occur several times a day
* `date` -- a date

#### Logical
* `boolean` -- a logical data type (`TRUE`, `FALSE`, `NULL`)


---
---

# Converting the Data Type
* The data type can be converted from one data type to another 
* Ways to convert
	1) Use the `CAST()` function
	2) Use the double-colon feature

## Ways to Convert Data
####  `CAST()` 
* Converts the data type of a field (column) and casts it as a different data type
	* Arguments:
		* `field` -- the field to be casted and the data type to cast to
```SQL
-- SYNTAX
CAST(column_name AS data_type)
``` 

```sql
SELECT 
	CAST(track_id AS varchar),
    CAST(album_id AS varchar)
FROM 
	track; 
```

```SQL
SELECT
    AVG(CAST(rating AS real)) AS average
FROM
    books;
```

```SQL
SELECT 
	CAST(field AS data type)
FROM 
	table1; 
```

```SQL
SELECT 
	AVG(CAST(weight AS real)) AS average
FROM
    products_data_all
WHERE 
    units = 'oz'
```

```SQL
SELECT 
	MAX(CAST(weight AS real)) AS max_weight
FROM
    products_data_all
WHERE
    category = 'milk'
```

```SQL
SELECT 
    MAX(CAST(date AS date)) AS max_date,
    MIN(CAST(date AS date)) AS min_date
FROM
    transactions;
```

#### Double Colons
* Converts the data type of a field (column) and from one type to another 
```SQL
-- SYNTAX
column_name :: data_type
```

```SQL
SELECT
    AVG(rating::real) AS average
FROM
    books;
```



---
---

# Working with Dates
* There are two major functions (`EXTRACT()` and `DATE_TRUNC()`) used when working with date and time values.
	* These functions are called in the `SELECT` block

#### `EXTRACT()`
* Extracts the information needed from the timestamp; automatically turns the `date` and `time` types into `timestamp with time zone`.
	* Arguments
		* `date_fragment` -- the fragment to be extracted, from a specific column
			* `century`
			* `day`
			* `doy` -- day of year (ranging from 1, 365/366)
			* `dow` -- day of the week (where 0  is Sunday, 6 is Saturday)
			* `isodow` -- day of week under ISO 8601 (where Monday is 1, Sunday is 7)
			* `hour`
			* `milliseconds`
			* `minute`
			* `second`
			* `month`
			* `quarter`
			* `week` -- week of the year (ranging from 1, 52)
			* `year`
		* `FROM` -- the `FROM` keyword
		* `column_name` -- the name of the column to use when extracting 
```SQL
-- SYNTAX
SELECT
    EXTRACT(date_fragment FROM column_name) AS new_column_with_date
FROM
    Table_with_all_dates;
```

```SQL 
-- Example
SELECT
	id_user,
	EXTRACT(MONTH FROM log_on) AS month_activity,
	EXTRACT(DAY FROM log_on) AS day_activity
FROM
	user_activity;
```

```sql
SELECT 
	EXTRACT(YEAR FROM birth_date)
FROM 
	staff
LIMIT 5; 
```

```SQL
SELECT 
	customer_id,
    invoice_date,
    total,
	EXTRACT(WEEK FROM CAST(invoice_date AS timestamp))
FROM 
	invoice
WHERE 
	customer_id BETWEEN 20 AND 50;
```

```SQL
SELECT 
	 EXTRACT(HOURS FROM date) AS hours
FROM
    transactions;
```

```SQL
SELECT 
    EXTRACT(HOURS FROM date) AS hours,
    COUNT(id_product) as cnt
FROM
    transactions
GROUP BY
    hours
ORDER by
    hours ASC
```

```SQL
SELECT 
    EXTRACT(DAY FROM date) AS days,
    COUNT(id_product) AS cnt
FROM
    transactions
GROUP BY
    days
ORDER BY
    days ASC
```

#### `DATE_TRUNC()`
* Truncates the date when only a certain level of precision is needed; automatically turns the `date` and `time` types into `timestamp with time zone`.
	* Arguments:
		* `date_fragment` -- a string indicating the date fragment to use when truncating
			* `'microseconds'`
			* `'milliseconds'` 
			* `'second'` 
			* `'minute'`
			* `'hour'`
			* `'day'`
			* `'week'`
			* `'month'`
			* `'quarter'` 
			* `'year'` 
			* `'decade'` 
			* `'century'`
		* `column_name` -- the name of the column to truncate
* Example: Useful when only the day is needed, and the hour does not matter
```SQL
-- SYNTAX
SELECT
    DATE_TRUNC('date_fragment', column_name) AS new_column_with_date
FROM
    Table_with_all_dates;
```

```SQL
-- Example
SELECT
    DATE_TRUNC('hour', log_on) AS date_log_on
FROM
    user_activity;
```

```sql
SELECT 
	DATE_TRUNC('year', birth_date)
FROM 
	staff
LIMIT 5; 
```

```SQL
SELECT
    DATE_TRUNC('day', date) AS date_month,
    COUNT(id_product) AS cnt
FROM
    transactions
GROUP BY
    date_month
ORDER BY
    date_month
```