See
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)

---

# Commands
##### `SELECT`
* Specifies the necessary columns from the database table
	* Use `*` to select ALL data
```sql
/* the asterisk (*) selects ALL data */
SELECT *
```

```SQL
--Select columns 1, 2 and 3 from the table
SELECT
    column_1,
    column_2,
    column_3...
FROM
    table_name;
```

##### `FROM`
* Specifies the source (which table) to access for data
```sql
-- The FROM keyword specifies from what table we are selecting data from
SELECT 
	* 
FROM 
	genre;
```

```SQL
SELECT
    name,
    author
FROM
    books;
```

##### `AS`
* Used to rename a column or table with an alias (another temporary name) 
	* An alias only exists for the duration of the query.
```SQL
SELECT
	COUNT(store_name) AS store_name_count
FROM
	invoice
WHERE
	price >= 30
```

##### `DISTINCT`
* Returns only unique values
	* If several fields are listed after `DISTINCT`, the query will return all the unique combinations of values in these fields.
```SQL
-- Selecting the distinct values of the billing_country column
SELECT 
	DISTINCT billing_country 
FROM 
	invoice 
```

```SQL
-- Counting the distinct values of the publisher_id column
SELECT
    COUNT(DISTINCT publisher_id) AS publisher_id_uniq_cnt
FROM
    books;
```


---
---
---

# Clauses

##### `WHERE`
* Obtains specific data based on the condition (slices the data)
```sql
-- Example
SELECT 
	album_title, -- fields to be exported
	song_title
FROM 
	albums -- the table they're exported from
WHERE 
	track_id != 5; -- condition for the data slice 
```

##### `GROUP BY`
* Groups rows that have the same values into summary rows
	* Fields that are to be grouped should be listed in BOTH the `SELECT` block and `GROUP BY` block.
```SQL
SELECT
    author,
    AVG(pages) AS avg_pages,
    MAX(pages) AS max_pages
FROM
    books
GROUP BY
    author;
```

```SQL
SELECT 
	name_store,
    COUNT(name) AS name_cnt,
    COUNT(DISTINCT name) AS name_uniq_cnt
FROM
    products_data_all
GROUP BY
	name_store
```

##### `ORDER BY`
* Sort the result-set in ascending or descending order
	* ONLY fields that are to be sorted should be listed 
	* To be placed at end of query (only `LIMIT` keyword can follow it)
	* Two modifiers can be used with `ORDER BY` 
		* `ASC` -- (the default) sorts data in ascending order
		* `DESC` -- sorts data in descending order
```SQL
SELECT 
	billing_city,
    AVG(total)
FROM 
	invoice
WHERE 
	billing_country = 'USA'
GROUP BY 
	billing_city
ORDER BY 
	AVG(total) DESC
LIMIT 5; 
```

```SQL
SELECT 
	billing_country,
    customer_id,
    total
FROM 
	invoice
WHERE 
	billing_country = 'India' OR billing_country = 'Portugal'
ORDER BY 
	billing_country, 
    customer_id,
    total DESC; 
```

##### `LIMIT`
* Specifies the number of rows (records) that should be returned 
```sql
-- Selecting all columns and only returning 2 records
SELECT 
	*
FROM 
	films_i_watched
LIMIT 2;
```

```SQL
-- Will return only the two columns (fields) listed
SELECT title, 
	   my_rating
FROM films_i_watched
LIMIT 2
```

##### `OFFSET`
* Specifies how many records to skip (from the beginning)
* Used to skip a certain number of rows when returning the result set of a query
```SQL
SELECT 
	title,
	my_rating
FROM 
	my_table
LIMIT 3 OFFSET 5; --skips the first 5 rows; prints only 3 rows after that
```

##### `OVER`
* Determines how the rows of the query are split up for processing by the window function. 
```SQL
SELECT
    author_id,
    name,
    price / SUM(price) OVER () AS ratio
FROM
    books_price;
```

##### `PARTITION BY`
* Divides the rows into groups that share the same values of the `PARTITION BY` expression(s)
```SQL
SELECT
    author_id,
    name,
    price / SUM(price) OVER (PARTITION BY author_id) AS ratio
FROM
    books_price;
```


---
---
---

# Expressions
##### `CASE` 
* Returns a new value based on an established condition passing
```SQL
SELECT
    name,
    CASE 
	    WHEN publisher_id IS NULL THEN -1 --Assign publisher_id of -1 is NULL
	    ELSE publisher_id 
	END AS publisher_id_full
FROM
    books;
```

```sql
SELECT 
	total,
    CASE
	   WHEN total < 5 THEN 'small'
	   WHEN total >= 5 AND total < 10 THEN 'medium'
	   WHEN total >= 10 THEN 'large'
	END
FROM 
	invoice
LIMIT 10; 
```

----
----
---

# Operators

##### `*` 
* Called the wildcard operator
* Used to specify "everything" during a query
```SQL
SELECT 
	*
FROM 	
	invoice
```

##### `BETWEEN` 
* Selects values within a given range (begin and end values are included). 
```sql
SELECT 
	*
FROM 
	audience
WHERE 
	age BETWEEN 50 
	AND 65; 
```

##### `IN`
* Used to specify multiple values in a `WHERE` clauses (shorthand for multiple `OR` statements)
```sql
SELECT 
	song_title,
    artist
FROM 
	songs
WHERE 
	artist IN ('DJ Hat', 'Amadeus Mozart', 'Pinkblack'); 
```

##### `NOT IN`
* Used to specify multiple values `NOT` statements in a `WHERE` clause (shorthand for having multiple `NOT` statements)
```SQL
SELECT
    name,
    genre
FROM
    books
WHERE
    genre NOT IN ('Humor', 'Fantasy', 'Young Adult');
```

##### `IS NULL`
* Returns `TRUE` if the value is `NULL`
```SQL
SELECT
    name,
    publisher_id
FROM
    books
WHERE
    publisher_id IS NULL;
```

##### `IS NOT NULL`
* Returns `TRUE` if a value is not `NULL`
```SQL
SELECT
    name,
    publisher_id
FROM
    books
WHERE
    publisher_id IS NOT NULL;
```

##### `ELSE`
* Returns the specified result when all conditions are NOT met by a particular 
* Example
```sql
SELECT 
	total,
	CASE
	   WHEN total >= 5 AND total < 10 THEN 'medium'
	   WHEN total >= 10 THEN 'large'
	   ELSE 'small'
	END
FROM 
	invoice
LIMIT 10; 
--- The ELSE block is triggered when the above conditions are not satisified
```

##### `ESCAPE`
* Accepts a symbol (such as an exclamation point) that becomes the escape character, which is used to search for the special character `%` in the string
```SQL
SELECT
    *
FROM
    products
WHERE
    units LIKE '%!%' ESCAPE '!'
```

##### `LIKE`
* Searches a table for values that follow a given pattern (word or fragment) in a column (field) and returns the value(s) meet the pattern
```SQL
SELECT
    *
FROM
    books
WHERE
    name LIKE '%Vampire%';
    -- Selects all books whose names include Vampires
```

##### `NOT LIKE`
 * Searches a table for values that follow a given pattern (word or fragment) in a column (field) and returns the value(s) that DO NOT meet the pattern
```SQL
SELECT 
	* 
FROM 
	invoice
WHERE 
	CAST(invoice_date AS date) BETWEEN '2009-03-04' 
	AND '2012-02-09'
	AND total < 5 
    AND billing_country NOT IN ('Canada', 'Brazil', 'Finland');
```

##### `INNER JOIN`
* Selects records that have matching values in both tables
```sql
SELECT 
	c.first_name,
	c.last_name,
    i.total
FROM 
	invoice AS i
	INNER JOIN client AS c ON i.customer_id = c.customer_id
LIMIT 10; 
```

##### `LEFT OUTER JOIN` (`LEFT JOIN`)
* Returns all records from the left table (table1), and the matching records from the right table (table2). 
```SQL
SELECT 
	art.name,
	COUNT(alb.title) AS total_album
FROM 
	artist AS art
	LEFT OUTER JOIN album AS alb ON art.artist_id = alb.artist_id
GROUP BY 
	art.name
ORDER BY 
	total_album DESC
LIMIT 10; 
```

##### `RIGHT OUTER JOIN` (`RIGHT JOIN`)
* Returns all records from the right table (table2), and the matching records from the left table (table1). 
```SQL
SELECT art.name,
       COUNT(alb.title) AS total_album
FROM 
	album AS alb
	RIGHT OUTER JOIN artist AS art ON alb.artist_id = art.artist_id
GROUP BY 
	art.name
ORDER BY 
	total_album DESC
LIMIT 10; 
```

##### `FULL OUTER JOIN` (`OUTER JOIN`)
* Returns all records when there is a match in left (table1) or right (table2) table records
```SQL
SELECT 
	a.actor_id,
    a.first_name,
    a.last_name,
    c.first_name,
    c.last_name
FROM 
	actor AS a
	FULL OUTER JOIN client AS c ON a.last_name = c.last_name
LIMIT 10; 
```

##### `UNION`
* Used to join tables vertically (combine rows from different tables that have the same fields) 
	* Excludes duplicates
```SQL
SELECT 
	i.billing_country,
    COUNT(i.total) AS total_purchases
FROM 
	invoice AS i
WHERE 
	i.billing_country IN ('USA', 'Germany', 'Brazil')
	AND EXTRACT(YEAR FROM cast(invoice_date AS date)) = 2009
GROUP BY 
	i.billing_country
UNION
SELECT 
	i.billing_country,
    COUNT(i.total) AS total_purchases
FROM 
	invoice AS i
WHERE 
	i.billing_country IN ('USA', 'Germany', 'Brazil')
	AND EXTRACT(YEAR FROM cast(invoice_date AS date)) = 2013
GROUP BY
	i.billing_country; 
```

##### `UNION ALL
* Used to join tables vertically (combine rows from different tables that have the same fields) 
	* Includes ALL records (even duplicates)
```SQL
SELECT 
	i.billing_country,
    COUNT(i.total) AS total_purchases
FROM 
	invoice AS i
WHERE 
	i.billing_country IN ('USA', 'Germany', 'Brazil')
	AND EXTRACT(YEAR FROM cast(invoice_date AS date)) = 2009
GROUP BY 
	i.billing_country
UNION ALL
SELECT 
	i.billing_country,
    COUNT(i.total) AS total_purchases
FROM 
	invoice AS i
WHERE 
	i.billing_country IN ('USA', 'Germany', 'Brazil')
	AND EXTRACT(YEAR FROM cast(invoice_date AS date)) = 2013
GROUP BY 
	i.billing_country; 
```

##### `CURRENT_DATE` 
* Returns the current date
```sql
SELECT CURRENT_DATE;
```

##### `CURRENT_TIME`
* Returns the current time
```sql
```

##### `CURRENT_TIMESTAMP`
* Returns both the current date and time
```sql

```


---
---
---

# Functions

##### `CAST()` 
* Converts the data type of a field (column) and casts it as a different data type
	* Arguments:
		* `field` -- the field to be casted and the data type to cast to
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

##### `EXTRACT()`
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

##### `DATE_TRUNC()`
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


##### `TO_HEX()`
* Converts an integer into a hexadecimal value
```SQL
SELECT
	TO_HEX(arms) AS arms
FROM
	monsters
```


---
---
---

# Aggregate Functions
##### `COUNT()`
* Returns the number of Non-NULL records (rows) in a table or field 
	* Arguments
		* `field` -- the column to count
			* If `*` is used, `COUNT()` will return the total number of records (rows)
```SQL
SELECT
    COUNT(*) AS cnt,
    COUNT(publisher_id) AS publisher_id_cnt,
    COUNT(DISTINCT publisher_id) AS publisher_id_uniq_cnt
FROM
    books;
```

##### `SUM()`
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

##### `AVG()`
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
    products_data_all
WHERE
    name = 'Borden Whole Milk, 1 gal'
    AND name_store = 'Wise Penny';
```

##### `MIN()`
* Returns the minimum value in a field
	* `MIN()` only works on numerical values
	* Arguments
		* `field` -- the column for which to find the minimum
```SQL
SELECT 
	MAX(price) - MIN(price) AS max_min_diff
FROM
    products_data_all
WHERE
    name = 'Meyenberg Goat Milk, 1/2 gal' AND name_store = 'Milk Market'
```

##### `MAX()`
* Returns the minimum value in a field
	* `MIN()` only works on numerical values
	* Arguments
		* `field` -- the column for which to find the minimum
```SQL
SELECT 
	MAX(price) AS max_price
FROM
    products_data_all;
```


---
---
---

# Special Aggregate Function

##### `RANK()`
* Assigns a rank to every row within a partition of a result set
	* Arguments:
		1) 
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

##### `NTILE()`
* Divides ordered rows in the partition into a specified number of ranked groups as equal size as possible. These ranked groups are called buckets.
	* Arguments
		1) `buckets` -- the number of groups (buckets) to divide data into
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

##### `LAG()`
* Accesses data of the previous row from the current row
* Useful for comparing the value of the current row with the value of the previous row.
	* Arguments:
		1) `field_name` -- the name of the field to evaluate when looking at LAG
		2) `offset` -- (default, 1) specifies the number of rows that come before the current row from which to access data.
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

##### `LEAD()`
* Accesses data of the following row from the current row
* Useful for comparing the value of the current row with the value of the following row.
	* Arguments
		1) `field_name` -- the name of the field to evaluate when looking at LEAD
		2) `offset` -- (default, 1) specifies the number of rows that come after the current row from which to access data.
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


---
---
---

# Mathematical Functions (PostgreSQL)

##### `ABS()`
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

##### `FLOOR()`
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

##### `CEILING()`
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

##### `ROUND()`
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

##### `TRUNC()`
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

##### `POWER()`
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

##### `SQRT()`
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
---

# String Functions

##### `LENGTH()`
* Returns the number of characters within a string (including: leading, trailing spaces, and spaces between words)
	* Arguments
		1) `string` -- the string to be used when determining length
```sql
SELECT 
	LENGTH('I study SQL');
FROM
	movie
```

##### `REPLACE()`
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

##### `INITCAP()`
* Converts every word to title-case (first letter in word uppercase, rest are lowercase)
	* Arguments
		1) `string` -- the string to be title-cased
```sql
SELECT 
	INITCAP ('kay layla smith'); --- Result: Kay Layla Smith
FROM 
	movie;
```

##### `LOWER()`
* Lowercases all letters in a given string and returns the string
	* Arguments
		1) `string` -- the string to be lower-cased
```sql
SELECT 
	LOWER('ProBLEms wiTh striNGS'); --- Result: problems with strings
FROM 
	movie;
```

##### `UPPER()`
* Uppercases all letters in a given string and returns the string
	* Arguments
		1) `string` -- the string to be upper-cased
```sql
SELECT 
	UPPER('ProBLEms wiTh striNGS'); --- Result: PROBLEMS WITH STRINGS
FROM 
	movie;
```

##### `LTRIM()`
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

##### `RTRIM()`
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

##### `CONCAT()`
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


