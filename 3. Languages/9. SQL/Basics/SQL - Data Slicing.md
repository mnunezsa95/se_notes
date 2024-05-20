See:
* [[SQL - Introduction to SQL]]
* [[SQL - 0. Info Database]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)


---
# Data Slices in SQL
* Data Slicing will filter out irrelevant data, leaving only useful data
* The comparison operators and logical operators are used to slice data accordingly
## Comparison Operators in SQL
* Comparison operators are often used with the `WHERE` clause
* When comparing a set of characters, dates or times, use ***single quotes*** (double quotes will NOT work)

| Operator  | Meaning                  |
| --------- | ------------------------ |
| =         | Equal to                 |
| <>,<br>!= | Not equal to             |
| >         | Greater than             |
| <         | Less than                |
| >=        | Greater than or equal to |
| <=        | Less than or equal to    |
## Logical Operators in SQL
* Logical Operator precedence can be managed used parentheses `()` to specify which one should be given precedence

| Operator | Meaning                                                                  | Behavior Rules                                                                                    | Order of Precedence |
| -------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- | ------------------- |
| AND      | Selects rows for which every conditions are true                         | `AND` returns `TRUE` if both conditions are also evaluated as `TRUE`                              | 2                   |
| OR       | Selects rows for which only one condition needs to be true               | `OR` returns `TRUE` if at least one condition value is also evaluated to `TRUE`                   | 3                   |
| NOT      | Selects rows for which the condition is false<br><br>Flips the condition | `NOT` changes the expression's value to the opposite one: `TRUE` to `FALSE` and `FALSE` to `TRUE` | 1                   |
## Filtering Data
#### `WHERE` Clause
* Obtains specific data based on the condition (slices the data)
* The `WHERE` block is processed before the `SELECT` block
```SQL
-- SYNTAX
SELECT
	column_1,
	column_2,
FROM
	table_name
WHERE
	condition
```

```SQL
-- Example
SELECT
    name,
    author
FROM
    books
WHERE
    author = 'Stephen King';
```

```SQL
SELECT
    name,
    author
FROM
    books
WHERE
    author != 'Stephen King';
```

```SQL
-- Using "not equals to"
SELECT
    name,
    author,
    pages
FROM
    books
WHERE
    pages > 700;
```

```sql
SELECT 
	billing_address,
	CAST(invoice_date AS date)
FROM 
	invoice
WHERE 
	total >= 8;
```

```SQL
-- Using Logical Operators
SELECT
    name,
    author,
    date_pub,
    pages
FROM
    books
WHERE
    date_pub > '1995-12-31'
    AND date_pub < '2001-01-01';
```

```SQL
SELECT
    name,
    genre
FROM
    books
WHERE
    genre = 'Humor'
    OR genre = 'Fantasy'
    OR genre = 'Young Adult';
```

```SQL
SELECT
    name,
    price,
    name_store,
    date_upd
FROM 
    products_data_all
WHERE
    category = 'milk' AND date_upd = '2019-06-01'
```

```SQL
-- Selecting people from Boston who are over the age of 43
SELECT 
	name 
WHERE 
	city = 'Boston' AND age > 43; 
```

```SQL
-- Selecting people NOT from Boston or Seattle
SELECT 
	name
WHERE 
	NOT city = 'Boston' AND NOT city = 'Seattle';
```

```SQL
-- Include both people from Boston or Seattle over the age of 43
SELECT
	name
WHERE 
	age > 43 AND (city = 'Boston' OR city = 'Seattle'); 
```

#### `BETWEEN` Operator
* Selects values within a given range (begin and end values are included). 
	* The values can be numbers, text, or dates
```SQL
-- Example
SELECT
    name,
    author,
    date_pub,
    pages
FROM
    books
WHERE
    date_pub BETWEEN '1996-01-01'
    AND '2000-12-31';
-- Starting and ending dates are included
```

```sql
SELECT 
	*
FROM 
	audience
WHERE 
	age BETWEEN 50 
	AND 65; 
```

#### `IN` Operator
* Used to specify multiple values in a `WHERE` clauses (shorthand for multiple `OR` statements)
	* Values are separated by commas and surrounded by parentheses `( )`
```sql
SELECT 
	song_title,
    artist
FROM 
	songs
WHERE 
	artist IN ('DJ Hat', 'Amadeus Mozart', 'Pinkblack'); 
```

```SQL
SELECT
    *
FROM
    table_name
WHERE
    column_name IN ('value_1', 'value_2', 'value_3');
```

```SQL
SELECT
    name,
    price,
    name_store,
    date_upd
FROM
    products_data_all
WHERE
    category = 'milk'
    AND
    date_upd IN ('2019-06-08', '2019-06-15', '2019-06-22', '2019-06-29');
```

#### `NOT IN` Operator
* Used to specify multiple values `NOT` statements in a `WHERE` clause (shorthand for having multiple `NOT` statements)
```sql
SELECT 
	song_title,
    artist
FROM 
	songs
WHERE
	artist NOT IN ('DJ Hat', 'Amadeus Mozart', 'Pinkblack'); 
```

```SQL
SELECT
    name,
    genre
FROM
    books
WHERE
    genre NOT IN ('Humor', 'Fantasy', 'Young Adult');
```


---
---

## Limiting Output

### Setting Limits
* Fields (Columns) can be limited by specifying the actual fields to be pulled
* Rows (Records) can be limited by setting `LIMIT` command 

#### `LIMIT` Command
* Limits the number of rows returned
```sql
SELECT 
	name,
    unit_price
FROM 
	track
LIMIT 20; -- Only returns 20 rows
```

#### `OFFSET` Command
* Specifies a different start point when returning data
* Used to skip a certain number of rows when returning the result set of a query
```sql
SELECT 
	title,
	my_rating
FROM 
	my_table
LIMIT 3 OFFSET 5; --skips the first 5 rows, only returns 3 rows
```


---
---

# Data Searching in Tables
* SQL uses the `LIKE` operator to look for patterns in string data within fields
* SQL uses the `ESCAPE` operator to support string searching by allowing to look for special characters

## Working with `LIKE`
* Using the `%` wildcard
	* `text%` -- Values that start with text
	* `%text` -- Values that end with text
	* `%text%` -- Values that have text in any position
	* `te%xt` -- Values that start with 'te' and end with 'xt'

#### `ESCAPE`
* Accepts a symbol (such as an exclamation point) that becomes the escape character, which is used to search for the special character `%` in the string
	* It means the symbol following it is not a wildcard character, but the character itself, which the substring must include. 
```SQL
--SYNTAX
column_name LIKE '%!%' ESCAPE '!' --Finds all substrings ending with %
```

```SQL
--Example
SELECT
    *
FROM
    products
WHERE
    units LIKE '%!%' ESCAPE '!'
```

#### `LIKE`
* Searches a table for values that follow a given pattern (word or fragment) in a column (field) and returns the value(s) meet the pattern
	* Search template must be a string and is case sensitive
* Used in the `WHERE` clause
* `LIKE` can be used with two wildcards
	* `%` -- represents zero, one or multiple characters
	* `_` -- represents one single character
```SQL
--SYNTAX
column_name LIKE 'regular expression'
```

```SQL
--Example
SELECT
    *
FROM
    books
WHERE
    name LIKE '%Vampire%';
    -- Selects all books whose names include Vampires
```

```sql
SELECT 
	name 
FROM 
	track
WHERE 
	composer LIKE '%Bono%'
			AND (genre_id IN (7,8,9,10)
            AND milliseconds >= 300000)
            OR bytes >= 1000000000
```

```SQL
SELECT
    *
FROM
    products
WHERE
    name LIKE '%Moo%'
```

#### `NOT LIKE`
* Searches a table for values that follow a given pattern (word or fragment) in a column (field) and returns the value(s) that DO NOT meet the pattern
* Used in the `WHERE` clause
```SQL
SELECT
    *
FROM
    books
WHERE
    name NOT LIKE '%Vampire%'; 
    -- Selects all books whose names do not include Vampires
```

```sql
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


---
---

# Identifying Empty Values
* Empty cells are considered to be `NULL`
## What is a `NULL` value?
* `NULL` indicates the absence of specific data (not equal to anything)
* `NULL` cannot be compared to another value using comparison operators

### Searching for `NULL` Values
* There are two operators for working with `NULL` values:
	1) `IS NULL`
	2) `IS NOT NULL`
#### `IS NULL`
* Returns `TRUE` if the value is `NULL`
```SQL
SELECT
    *
FROM
    table_name
WHERE
    column_name IS NULL;
```

```SQL
SELECT
    name,
    publisher_id
FROM
    books
WHERE
    publisher_id IS NULL;
```

```SQL
SELECT 
	email,
	fax
FROM 
	client
WHERE 
	fax IS NULL
LIMIT 5; 
```

```SQL
SELECT
    name,
    units,
    weight
FROM
    products
WHERE 
    weight IS NULL
```

```SQL
-- Coutning number of NULL values in 'weight' field
SELECT
    COUNT(*)
FROM
    products
WHERE
    weight IS NULL
    
```

#### `IS NOT NULL`
* Returns `TRUE` if a value is not `NULL`
* Useful for excluding `NULL` values from the output
```SQL
SELECT
    *
FROM
    table_name
WHERE
    column_name IS NOT NULL;
```

```SQL
SELECT
    name,
    publisher_id
FROM
    books
WHERE
    publisher_id IS NOT NULL;
```

```SQL
SELECT 
	email,
    fax
FROM 
	client
WHERE 
	fax IS NOT NULL
LIMIT 5; 
```


---
---

# `CASE` Expressions

## What is a `CASE` Expression?
* The `CASE` expression goes through conditions and returns a value when the conditions are met (like an if-then-else statement).
	* Once a condition is met, the rest of the conditions are NOT checked

## Characteristics of a `CASE` Expression
* The `CASE` expression creates new fields in the table
* Returns `NULL` when a condition is NOT met
* Can be used with the `ELSE` operator

## `CASE` Expression Syntax
* Starts with a `CASE` keyword
* Has one or more indented `WHEN` statements, followed by a condition. 
	* A `THEN` keyword is on the same line, with the name of the category specified
* Ends with an `END` operator
```SQL
--SYNTAX
CASE  
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2 
    WHEN conditionN_ THEN resultN  
    ELSE result 
END;
```

## Using a `CASE` Expression

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

```SQL
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
--- ELSE operator specifies what to do when condition 1 or 2 are NOT met
```

```sql
SELECT 
	last_name,
	first_name,
	title,
	CASE 
		WHEN title LIKE '%IT%' THEN 'development'
		WHEN title LIKE '%Manager%' AND title NOT LIKE '%IT%' THEN 'sales'
		WHEN title LIKE '%Support%' THEN 'customer support'
	END
FROM 
	staff;
```

```SQL
SELECT
    name,
    CASE
        WHEN weight IS NULL AND units = 'oz' THEN '23.0705263269575'
        WHEN weight IS NULL AND units = 'ct' THEN '10.0'
        WHEN weight IS NULL AND units = 'pk' THEN '12.0909090909091'
        WHEN weight IS NULL AND units = '%' THEN '1.0'
        WHEN weight IS NULL AND units = 'pt' THEN '1.0'
        WHEN weight IS NULL AND units = 'qt' THEN '1.0'
        WHEN weight IS NULL AND units = 'gal' THEN '0.650793650793651'
        ELSE weight
    END AS weight_full
FROM
    products;
```