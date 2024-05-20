See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
* [[SQL - 0. Info Database]]
Resources:
* Tech on the Net: [PostgreSQL MIN() Function](https://www.techonthenet.com/postgresql/functions/min.php)
* Tech on the Net: [PostgreSQL MAX() Function](https://www.techonthenet.com/postgresql/functions/max.php)
* Documentation: [PostgreSQL String Functions](https://www.postgresql.org/docs/9.1/functions-string.html)
* Documentation: [PostgreSQL Window Functions](https://www.postgresql.org/docs/9.1/tutorial-window.html)

---
# Aggregate Function
* SQL has specific functions (called Aggregate Functions) for calculating the total number of rows, sums, averages, minimum values, and maximum values
* Aggregate Functions -- collect (or aggregate) all objects within a group to calculate a single summary value
```SQL
-- General Syntax
SELECT
    AGGREGATE_FUNCTION (field) AS here_you_are -- name of the column to store                                                               the function's output
FROM
    table_name;
```

## Aggregate Functions

#### `COUNT()`
* Returns the number of Non-NULL records (rows) in a table or field 
	* Arguments
		* `field` -- the column to count
			* If `*` is used, `COUNT()` will return the total number of records (rows)
```SQL
--- Counting the number records in a table
SELECT
    COUNT(*) AS cnt
FROM
    books;
```

```SQL
```sql
SELECT 
	COUNT(billing_postal_code)
FROM 
	invoice; 
```

```SQL
-- Counting total number of rows where 'Dean Koontz' is the author
SELECT
    COUNT(*) AS cnt
FROM
    books
WHERE
    author = 'Dean Koontz';
```

```SQL
SELECT
    COUNT(*) AS cnt,
    COUNT(publisher_id) AS publisher_id_cnt,
    COUNT(DISTINCT publisher_id) AS publisher_id_uniq_cnt
FROM
    books;
```

#### `SUM()`
* Returns the sum of the values in a `column`. 
	* `SUM()` ignores missing values and only works with numerical values
	* Arguments
		* `field` -- the column for which to sum values
```SQL
SELECT
    SUM(pages) AS total_pages
FROM
    books;
```

```SQL
SELECT 
	SUM(price) as total_cost
FROM
    products_data_all
WHERE
    name_store = 'T-E-B'
```

#### `AVG()`
* Returns the average (arithmetic mean) of `column` values
	* `AVG()` only works with numerical values
	* Arguments
		* `field` -- the column for which to average values
```SQL
SELECT
    AVG(pages) AS average_pages
FROM
    books;
```

```SQL
SELECT 
	AVG(price) AS average
FROM
    products_data_all;
```

```SQL
SELECT 
	AVG(price) AS average
FROM
    products_data_all
WHERE
    name = 'Borden Whole Milk, 1 gal'
    AND name_store = 'Wise Penny';
```

#### `MIN()`
* Returns the minimum value in a field
	* `MIN()` only works on numerical values
	* Arguments
		* `field` -- the column for which to find the minimum
```SQL
SELECT 
	MIN(total)
FROM 
	invoice; 
```

```SQL
SELECT 
	MAX(price) - MIN(price) AS max_min_diff
FROM
    products_data_all
WHERE
    name = 'Meyenberg Goat Milk, 1/2 gal' AND name_store = 'Milk Market'
```

#### `MAX()`
* Returns the minimum value in a field
	* `MIN()` only works on numerical values
	* Arguments
		* `field` -- the column for which to find the minimum
```SQL
SELECT 
	MAX(total) AS max_total
FROM 
	invoice; 
```

```SQL
SELECT 
	MAX(price) AS max_price
FROM
    products_data_all;
```


---
---

# Mathematical Functions in SQL
* PostgreSQL has several mathematical functions for working with data
* These mathematical functions work similar to Aggregate Functions 
	* Often used in the `SELECT` block

## Summary of Mathematical Functions

| Function | Description                                                                                                                                | Example                              | Result      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------ | ----------- |
| ABS      | Returns the number magnitude                                                                                                               | `ABS(-14)`                           | 14          |
| CEILING  | Returns the number rounded up to a whole number                                                                                            | `CEILING(42.8)`                      | 43          |
| FLOOR    | Returns the number rounded down to a whole number                                                                                          | `FLOOR(42.8)`                        | 42          |
| ROUND    | Rounds the value to the nearest whole number, or rounds a number to a particular decimal place                                             | `ROUND(42.4) ROUND(42.4382, 2)`      | 42<br>42.44 |
| TRUNC    | Shortens the value to the nearest whole number, or shortens the number to a specified amount of decimal places without rounding the number | `TRUNC(42.4)`<br>`TRUNC(42.4382, 2)` | 42<br>42.43 |
| POWER    | Returns the number raised to the nth power; the necessary power is put as the second argument                                              | `POWER(9, 3)`                        | 729         |
| SQRT     | Takes the square root of the number                                                                                                        | `SQRT(9)`                            | 3           |


## Types of Mathematical Functions
#### `ABS()`
* Returns the magnitude (absolute value) of a number (without the + or - sign)
	* Arguments
		1) `number` -- the number to be used when determining absolute value
```sql
SELECT 
	number,
    ABS(number)
FROM 
	table_1; 
```

#### `FLOOR()`
* Returns the number rounded down to the nearest whole number (floors the value)
	* Arguments
		1) `number` -- the number to be floored
```sql
SELECT 
	number,
    FLOOR(number)
FROM 
	table_1; 
```

#### `CEILING()`
* Returns the number rounded up to the nearest whole number (ceils the value)
	* Arguments
		1) `number` -- the number to be used when ceiling
```SQL
SELECT 
	number,
    CEILING(number)
FROM 
	table_1;
```

#### `ROUND()`
* Returns the values to the nearest whole number
	* Argument
		1) `number` -- the number to be rounded
		2) `precision` -- the number of decimal places to use when rounding
```sql
SELECT 
	number,
    ROUND(21.5595743, 2); -- 21.56
FROM 
	table_1;
```

#### `TRUNC()`
* Returns a shortened number to a specified amount of decimal places but does not round
	* Arguments
		1) `number` -- the number to be truncated
		2) `precision` -- the number of decimal places to use when rounding
```sql
SELECT 
	number,
    TRUNC(21.5595743, 2); -- 21.55
FROM 
	table_1;
```

#### `POWER()`
* Returns the number raised to the *nth* power.
	* Arguments
		1) `number` -- number to be raised
		2) `degree_of_power` -- the value to raise the `number` to the power of
```sql
SELECT 
	number,
    POWER(number, 2)
FROM 
	table_1; 
```

#### `SQRT()`
* Returns the square root of a number (cannot take square root of a negative number)
	* Arguments
		* `number` -- the number to take the square root of
```sql
SELECT 
	number,
	SQRT(ABS(number))
FROM 
	table_1; 
```


---
---

# String Functions (PostgreSQL)
* PostgreSQL provides numerous functions for working with strings in fields and records.
* The majority of these strings can be applied to a single string for a field of strings

## The Types of String Functions
#### `LENGTH()`
* Returns the number of characters within a string (including: leading, trailing spaces, and spaces between words)
	* Arguments
		1) `string` -- the string to be used when determining length
```sql
SELECT 
	LENGTH('I study SQL');
FROM
	movie
```

#### `REPLACE()`
* Replaces a substring that's longer than one character with a new string of any size
	* Arguments
		1) `string` -- the original string
		2) `old_string` -- the string to be replaced
		3) `new_string` -- the new replacement string
```sql
SELECT 
	REPLACE('Winston/Salem', '/', '-');  -- Result: Winston-Salem
FROM
	movie
```

```sql
SELECT 
	UPPER(title),
    LOWER(REPLACE(rating, '-', ' '))
FROM 
	movie;
```

#### `INITCAP()`
* Converts every word to title-case (first letter in word uppercase, rest are lowercase)
	* Arguments
		1) `string` -- the string to be title-cased
```sql
SELECT 
	INITCAP ('kay layla smith'); --- Result: Kay Layla Smith
FROM 
	movie;
```

#### `LOWER()`
* Lowercases all letters in a given string and returns the string
	* Arguments
		1) `string` -- the string to be lower-cased
```sql
SELECT 
	LOWER('ProBLEms wiTh striNGS'); --- Result: problems with strings
FROM 
	movie;
```

#### `UPPER()`
* Uppercases all letters in a given string and returns the string
	* Arguments
		1) `string` -- the string to be upper-cased
```sql
SELECT 
	UPPER('ProBLEms wiTh striNGS'); --- Result: PROBLEMS WITH STRINGS
FROM 
	movie;
```

#### `LTRIM()`
* Deletes characters (or empty spaces, by default) from the left side of the string and returns the result
	* Arguments:
		1) `orginal_string` -- the string to be trimmed
		2) `trim_string` -- the part of the string to be trimmed
```sql
SELECT 
	LTRIM('Kayak', 'Ka'); --- Result: yak
FROM 
	movie;
```

#### `RTRIM()`
* Deletes characters (or empty spaces, by default) from the right side of the string and returns the result
	* Arguments:
		1) `orginal_string` -- the string to be trimmed
		2) `trim_string` -- the part of the string to be trimmed
```sql
SELECT 
	RTRIM('Kayak', 'ak'); --- Result: Kay
FROM 
	movie;
```

```sql
SELECT 
	title,
    RTRIM(REPLACE(description, 'Saga', 'Myth'), 'in A MySQL Convention')
FROM 
	movie
WHERE 
	release_year <= 2006 AND description LIKE '%Saga%';
```

#### `CONCAT()`
* Returns a concatenated string from several string values, which are separated by commas
	* Arguments
		* `string_1` -- the first string to concatenate
		* `string_2` -- the second string to concatenate
		* `string_n...`
```sql
SELECT 
	CONCAT('SQL', ' ', 'Masters', ' ', 'Rule'); 
FROM 
	movie;
```

```sql
SELECT 
	CONCAT(first_name, ', ', last_name, ', ', address, ', ', phone)
FROM 
	client
WHERE 
	country = 'Czech Republic';
```


---
---

# Window Functions

## What is a window function?
* Window functions -- perform calculations across a set of table rows that are somehow related to the current row.
* Window functions -- do not group rows into a single output row
* Window functions -- perform operations within **windows**

## What is a window in SQL?
* Window -- a sequence of rows on which the calculations are made
	* A window can be either:
		* An entire table
		* Any number of rows from a table

## Characteristics of Window Functions
* Window functions can use the same aggregate functions used under normal circumstance:
	* `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
* Window functions allow for special aggregate functions to be used:
	* `RANK()`, `NTILE()`, `LAG()`, `LEAD()`
* Window functions always contain an `OVER` clause DIRECTLY following the window functions name and arguments.
	* The `OVER` clause determines how the rows of the query are split up for processing by the window function. 
* The `PARTITION BY` clause (within the `OVER` clause) divides the rows into groups that share the same values of the `PARTITION BY` expression(s)
	* For each row, the window function is computed across the rows that fall into the same partition as the current row.


## Special Aggregate Functions (for Window Functions)

#### `RANK()`
* Assigns a rank to every row within a partition of a result set
	* Arguments:
		1)
```SQL
--SYNTAX
--- The PARTITION BY clause distributes rows of the result set into partitions to which the RANK() function is applied.
--- The ORDER BY clause specifies the order of rows in each a partition to which the function is applied.

SELECT
	RANK() OVER (
	    [PARTITION BY partition_expression, ... ]
	    ORDER BY sort_expression [ASC | DESC], ...)
FROM
	table_name
```

```SQL
--Example

-- Ranking books based on the number of pages for each author
SELECT
    author_id,
    name,
    pages,
    RANK() OVER (PARTITION BY author_id ORDER BY pages)
FROM
    books_price;
```

```SQL
--Example

SELECT DISTINCT
    name_store AS store_name,
    category,
    date_upd::date AS sale_date,
    name,
    price,
    RANK() OVER (PARTITION BY name_store, category ORDER BY price) AS rank
FROM
    products_data_all
WHERE
    date_upd = '2019-06-02'
ORDER BY
    store_name,
    category,
    rank
```

#### `NTILE()`
* Divides ordered rows in the partition into a specified number of ranked groups as equal size as possible. These ranked groups are called buckets.
	* Arguments
		1) `buckets` -- the number of groups (buckets) to divide data into
```SQL
--SYNTAX
--- The PARTITION BY clause distributes rows into partitions to which the function is applied.
--- The ORDER BY clause sorts rows in each partition to which the function is applied.

SELECT
	NTILE(buckets) OVER (
	    [PARTITION BY partition_expression, ... ]
	    [ORDER BY sort_expression [ASC | DESC], ...])
FROM
	table_name
```

```SQL
--Example

--Divides the books into five categories based on price.
SELECT
    author_id,
    name,
    price,
    ntile(5) OVER (ORDER BY price)
FROM
    books_price;
```

#### `LAG()`
* Accesses data of the previous row from the current row
* Useful for comparing the value of the current row with the value of the previous row.
	* Arguments:
		1) `field_name` -- the name of the field to evaluate when looking at LAG
		2) `offset` -- (default, 1) specifies the number of rows that come before the current row from which to access data.
```SQL
--SYNTAX
SELECT
	LAG(expression [,offset [,default_value]]) OVER (
	    [PARTITION BY partition_expression, ... ]
	    ORDER BY sort_expression [ASC | DESC], ...)
FROM
	table_name
```

```SQL
--Example

-- Find out whether a book is shorter than the author's previous one
SELECT
    author_id,
    name,
    pages,
    LAG(pages) OVER (PARTITION BY author_id ORDER BY date_pub)
FROM
    books_price;
```

#### `LEAD()`
* Accesses data of the following row from the current row
* Useful for comparing the value of the current row with the value of the following row.
	* Arguments
		1) `field_name` -- the name of the field to evaluate when looking at LEAD
		2) `offset` -- (default, 1) specifies the number of rows that come after the current row from which to access data.
```SQL
--SYNTAX
SELECT
	LEAD(expression [,offset [,default_value]]) OVER (
	    [PARTITION BY partition_expression, ... ]
	    ORDER BY sort_expression [ASC | DESC], ...)
FROM
	table_name
```

```SQL
--Example
SELECT
	sale_year, 
	amount,
	group_id,
	LEAD(amount, 1) OVER (PARTITION BY group_id ORDER BY sale_year) AS 
	    next_year_sales
FROM
	sales;
```


## Performing a Window Function on an Entire Table
* Task: Find the ratio of each book's price to the total cost
```SQL
--Example
SELECT
    author_id,
    name,
    price / SUM(price) OVER () AS ratio
FROM
    books_price;
```

| Explanation (above)                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The function preceding the `OVER` keyword will be executed on the data inside the window.<br><br>Since parameters are not used inside the `()` then the result of the query is used; the result is named `ratio` |
* Task: Find the ratio of the price of each book to the total cost of that author's books.
```SQL
--Example
SELECT
    author_id,
    name,
    price / SUM(price) OVER (PARTITION BY author_id) AS ratio
FROM
    books_price;
```

| Explanation (above)                                                    |
| ---------------------------------------------------------------------- |
| `PARTITION BY` is similar to `GROUP BY` but works for window functions |

```SQL
--Example
SELECT 
    name AS product_name, 
    name_store AS store_name,
    category,
    price AS product_price,
    price / AVG(price) OVER (PARTITION BY category, name_store) AS product_mul
FROM
    products_data_all
ORDER BY
    id_product;
```

```SQL
SELECT DISTINCT
    name_store AS store_name,
    date_upd::date AS sale_date,
    category,
    SUM(price) OVER (PARTITION BY date_upd, name_store, category) * 100 / 
       SUM(price) OVER (PARTITION BY name_store, date_upd) AS percent
FROM
    products_data_all
WHERE
    date_upd::date BETWEEN '2019-06-01'
    AND '2019-06-06'
ORDER BY
    date_upd::date,
    name_store;
```

## Performing a Window Function on a Table Fragment
* When working with window functions on a table fragments the `ORDER BY` and `ROWS` keywords can be used to build the query

#### `ORDER BY`
* Defines the sorting order of the rows through which the window function will run
#### `ROWS`
* Indicates the window frame over which an aggregate function is to be calculated
	* Frames (`ROWS`) can be indicated in several ways & can be combined:
		- `UNBOUNDED PRECEDING` — all rows that are above the current one
		- `N PRECEDING` — the _n_ rows above the current one
		- `CURRENT ROW` — the current row
		- `N FOLLOWING` — the _n_ rows below the current one
		- `UNBOUNDED FOLLOWING` — all rows below the current one
```SQL
SELECT
    author_id,
    name,
    SUM(price) OVER 
	    (ORDER BY author_id ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
FROM
    books_price;
```

```SQL
--Example
SELECT
    author_id,
    name,
    pages,
    SUM(pages) OVER (PARTITION BY author_id 
	    ORDER BY author_id ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
FROM
    books_price;
```

```SQL
--Example

SELECT 
    name_store AS store_name,
    category,
    name AS product_name,
    price, 
    SUM(price) OVER 
    (PARTITION BY category ORDER BY id_product ROWS BETWEEN UNBOUNDED 
    PRECEDING AND CURRENT ROW) AS category_accum,
    SUM(price) OVER 
    (ORDER BY id_product ROWS BETWEEN UNBOUNDED 
    PRECEDING AND CURRENT ROW) AS store_accum
FROM
    products_data_all
WHERE 
    date_upd = '2019-06-02'
    AND name_store = 'Four'
ORDER BY
    id_product;
```