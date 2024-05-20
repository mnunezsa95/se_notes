See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
* [[SQL - Functions in SQL]]
* [[SQL - Data Slicing]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)

---
# Clause Precedence for Data Organization 
1) `GROUP BY`
2) `HAVING`
3) `ORDER BY`
4) `LIMIT` / `OFFSET`

---
# Data Grouping
* Data can be divided and grouped into groups based on values 

#### `GROUP BY` 
* Groups rows that have the same values into summary rows
	* Fields that are to be grouped should be listed in BOTH the `SELECT` block and `GROUP BY` block.
	* Can be used with any aggregate function
```SQL
--SYNTAX
SELECT
    field_1,
    field_2,
    ...,
    field_n,
    AGGREGATE_FUNCTION (field) AS here_you_are
FROM
    table_name
WHERE
    condition -- if needed
GROUP BY
    field_1,
    field_2,
    ...,
    field_n;

-- The fields that are to be grouped are listed in both the SELECT block and the the GROUP BY block
```

```SQL
SELECT
	author,
	COUNT(name) AS cnt
FROM
	books
GROUP BY
	author;
```

```SQL
SELECT
    author,
    genre,
    COUNT(name) AS cnt
FROM
    books
GROUP BY
    author,
    genre;
```

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

```SQL
SELECT 
	category,
    MAX(CAST(weight AS real)) AS max_weight
FROM
    products_data_all
GROUP BY 
    category
```

```SQL
SELECT 
	name_store,
    AVG(price) AS average_price,
    MAX(price) AS max_price,
    MIN(price) AS min_price
FROM
    products_data_all
GROUP BY
    name_store;
```

```SQL
SELECT 
	name,
    MAX(price) - MIN(price) AS max_min_diff
FROM
    products_data_all
WHERE
	category = 'milk' AND CAST(date_upd AS date) = '2019-06-10'
GROUP BY
    name
```


---
---

# Sorting Data

## How can data be sorted?
* Fields with numeric data types, dates and time can be sorted in descending and ascending order
* Fields with character data types are sorted in lexicographical order (A-Z or Z-A)
	* The lexicographical order -- ordering based on the order of characters in the alphabet

## Ordering Columns and Rows
* Columns (fields) are ordered using the `SELECT` keyword
* Rows (records) are ordered using the `ORDER BY` operator 

## Ways to Sort Data
#### `ORDER BY`
* Sort the result-set in ascending or descending order
	* ONLY fields that are to be sorted should be listed 
	* To be placed at end of query (only `LIMIT` keyword can follow it)
	* Two modifiers can be used with `ORDER BY` 
		* `ASC` -- (the default) sorts data in ascending order
		* `DESC` -- sorts data in descending order
```SQL
--SYNTAX
SELECT
    field_1,
    field_2,
    ...,
    field_n,
    AGGREGATE_FUNCTION (field) AS here_you_are
FROM
    table_name
WHERE 
    condition -- if needed
GROUP BY
    field_1,
    field_2,
    ...,
    field_n,
ORDER BY -- List only those fields by which the data is to be sorted (if needed)
    field_1,
    field_2,
    ...,
    field_n,
    here_you_are;
```

```SQL
-- Example
SELECT
    author,
    COUNT(name) AS cnt
FROM
    books
GROUP BY
    author
ORDER BY
    cnt;
```

```SQL
SELECT
    author,
    COUNT(name) AS cnt
FROM
    books
GROUP BY
    author
ORDER BY
    cnt DESC;
```

```sql
-- Example
SELECT 
	billing_city,
    SUM(total),
	COUNT(total),
    AVG(total)
FROM 
	invoice
WHERE 
	billing_country = 'USA'
GROUP BY 
	billing_city
ORDER BY 
	AVG(total); -- recalculating AVG since alias wasn't used
```

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

```SQL
SELECT 
	billing_country, 
    COUNT(*)
FROM 
	invoice
WHERE 
	billing_postal_code iS NULL
    AND (billing_address LIKE '%Street%' 
	OR billing_address LIKE '%Way%' 
	OR billing_address LIKE '%Road%'
	OR billing_address LIKE '%Drive%')
GROUP BY 
	billing_country
```

```SQL
SELECT 
	EXTRACT(YEAR FROM CAST(invoice_date AS timestamp)),
    MIN(total),
	MAX(total),
	SUM(total),
	COUNT(total),
	ROUND(SUM(total)/COUNT(DISTINCT(customer_id)))
FROM 
	invoice
WHERE 
	billing_country IN ('USA', 'United Kingdom', 'Germany')
GROUP BY 
	EXTRACT(YEAR FROM CAST(invoice_date AS timestamp))
ORDER BY 
	EXTRACT(YEAR FROM CAST(invoice_date AS timestamp)) DESC;
```

```SQL
SELECT 
	date_upd::date AS update_date,
    category,
    COUNT(name) AS name_cnt
FROM
    products_data_all
WHERE
    date_upd::date = '2019-06-05'
GROUP BY 
    category,
    update_date
ORDER BY 
	name_cnt
```

```SQL
SELECT 
    date_upd::date AS update_date,
    name_store,
    category,
	COUNT(DISTINCT name) AS uniq_name_cnt
FROM
    products_data_all
WHERE 
	name_store = 'T-E-B' AND date_upd::date = '2019-06-30'
GROUP BY 
	update_date,
    name_store,
    category
ORDER BY
    uniq_name_cnt DESC
```


---
---

# Processing Data within a Grouping
* Data can be processed once grouped to produce results based on a criteria
* This ensures that the result only includes data that passes the specified criteria

#### `HAVING` 
* Filters grouped rows 
	* Can be used after the `GROUP BY`
	* Needs to include aggregate functions in the condition
```SQL
--SYNTAX
SELECT
    field_1,
    field_2,
    ...,
    field_n,
    AGGREGATE_FUNCTION (field) AS here_you_are
FROM
    table_name
WHERE
    condition -- if needed
GROUP BY
    field_1,
    field_2,
    ...,
    field_n
HAVING
    AGGREGATE_FUNCTION (field_for_grouping) > n
ORDER BY -- List only those fields by which the data is to be sorted (if needed)
    field_1,
    field_2,
    ...,
    field_n,
    here_you_are
LIMIT -- if needed
      n;
```


```sql
SELECT 
	customer_id,
    SUM(total)
FROM 
	invoice
GROUP BY 
	customer_id
HAVING 
	SUM(total) > 41
ORDER BY 
	SUM(total) DESC; 
```


```SQL
SELECT
    author,
    COUNT(name) AS name_cnt
FROM
    books
GROUP BY
    author
HAVING
    COUNT(name) > 1
ORDER BY
    name_cnt DESC;
```

```SQL
SELECT 
	name,
    MAX(price) AS max_price
FROM
    products_data_all
GROUP BY
	name
HAVING
    MAX(price) > 10
```

```SQL
SELECT 
	date_upd::date AS update_date,
    name_store,
    count(name) AS name_cnt
FROM
    products_data_all
WHERE
    date_upd::date = '2019-06-03' 
    AND units ='oz' AND weight::real > 5
GROUP BY
    update_date,
    name_store
HAVING
    COUNT(name) < 20
```

```SQL
SELECT 
	name_store,
    COUNT(DISTINCT name) as name_uniq_cnt
FROM
    products_data_all
GROUP BY
    name_store
HAVING
    COUNT(DISTINCT name) > 30
ORDER BY
    name_uniq_cnt
LIMIT 3
```