See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
Resources:


---
# Joining Tables
* Data is not typically stored in one table
* Theres two ways to join tables **HORIZONTALLY**:
	1) `INNER JOIN`
	2) `OUTER Join`
* There is two way to join tables **VERTICALLY**:
	1) `UNION`
	2) `UNION ALL`
## Summary: Joining Tables
| Operators          | Shorthand Operator | Direction  |
| ------------------ | ------------------ | ---------- |
| `INNER JOIN`       | `JOIN`             | Horizontal |
| `LEFT OUTER JOIN`  | `LEFT JOIN`        | Horizontal |
| `RIGHT OUTER JOIN` | `RIGHT JOIN`       | Horizontal |
| `FULL OUTER JOIN`  | `OUTER JOIN`       | Horizontal |
| `UNION`            |                    | Vertical   |
| `UNION ALL`        |                    | Vertical   |


---
---
# Horizontal Joining
## `INNER` vs `OUTER` Joining
* `INNER` (`JOIN`) join returns only those rows that have matching values from table to table (the table's intersection).
		![[inner-join-venn-diagram.png]]
		![[inner-join-table-example.png]]
* `OUTER` join retrieves all data from one tables and adds data from the other one when there are matching rows
	* There are three kinds of `OUTER` join:
		* `LEFT OUTER JOIN` (`LEFT JOIN`)
		* `RIGHT OUTER JOIN` (`RIGHT JOIN`)
		* `FULL OUTER JOIN`  (`OUTER JOIN`)
		![[outer-join-venn-diagram.png]]
		![[left-join-table-example.png]]
		![[right-join-table-example.png]]
		![[full-outer-join-table-example.png]]

## Characteristics of Joining Tables
* `INNER JOIN`, `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, and `FULL OUTER JOIN` take place in the `FROM` clause
* `ON` precedes the join condition
	* This mean ONLY the table rows that match this condition are joined
* Fields are referred to by both table name and field name


---
---

# `INNER JOIN`

### How does `INNER` join work?
* `INNER JOIN` ONLY selects data for which the join condition is met. 
* The order in which the tables are joined DOES NOT affect the final result.

#### Theoretical Example: `INNER JOIN`
* ***BEFORE JOINING**
	* Table 1: Data on domestic animals
	* Table 2: Data on the lengths of animal tails

| Table 1 |         |     | Table 2 |      |
| ------- | ------- | --- | ------- | ---- |
| id      | name    |     | id      | tail |
| 1       | cat     |     | 1       | 10   |
| 2       | dog     |     | 2       | 5    |
| 3       | hamster |     | 4       | 1    |
* ***AFTER JOINING**
	* One table including data for name an tail for Ids that were mutual to both tables

| id  | name | tail |
| --- | ---- | ---- |
| 1   | cat  | 10   |
| 2   | dog  | 5    |
#### `INNER JOIN`
* Selects records that have matching values in both tables
```SQL
--SYNTAX
SELECT --Listing the fields that are needed
    TABLE_1.field_1 AS field_1,
    TABLE_1.field_2 AS field_2,
    ...
	TABLE_2.field_n AS field_n
FROM
    TABLE_1
    INNER JOIN TABLE_2 ON TABLE_2.field_1 = TABLE_1.field_2;
```

```SQL
--Example
SELECT
    books.name AS name,
    books.author_id AS books_author_id,
    author.author_id AS author_id,
    author.first_name AS first_name,
    author.last_name AS last_name
FROM
    books
    INNER JOIN author ON author.author_id = books.author_id
LIMIT 3;
```

```SQL
SELECT
    books.name AS name,
    author.first_name AS first_name,
    author.last_name AS last_name
FROM
    books
    INNER JOIN author ON author.author_id = books.author_id
WHERE
    author.first_name = 'Dean'
    AND author.last_name = 'Koontz';
```

```SQL
SELECT 
    transactions.id_transaction AS id_transaction,
    products.category AS category,
    products.name AS name
FROM
    transactions
    INNER JOIN products ON products.id_product = transactions.id_product
ORDER BY 
    id_transaction
LIMIT 10
```

```SQL
SELECT 
	DISTINCT transactions.date AS date,
    weather.temp AS temp,
    weather.rain AS rain,
    transactions.id_transaction AS id_transaction
FROM
    transactions
    INNER JOIN weather ON CAST(weather.date AS date) = 
      CAST(transactions.date AS date)
ORDER BY 
	date DESC
```

```SQL
SELECT 
	DISTINCT products.name AS name
FROM
    products
    INNER JOIN products_stores ON products_stores.id_product = 
    products.id_product
WHERE 
    products_stores.price > 5
```

```SQL
SELECT 
	transactions.date AS date,
    transactions.id_transaction AS id_transaction,
    products.category AS category,
    products.name AS name
FROM
    transactions
    INNER JOIN products ON products.id_product = transactions.id_product
WHERE 
    category = 'butter' AND date::date = '2019-06-20'
```

```SQL
SELECT 
	products.name AS name,
	products.category AS category,
	products.units AS units,
	products.weight AS weight,
	products_stores.price AS price
FROM
	products
    INNER JOIN products_stores ON products_stores.id_product = 
    products.id_product
WHERE 
	products.units = 'oz' AND products_stores.date_upd::date = '2019-06-13';
```

```SQL
--- c is the alias for the client table
--- i is the alias for the invoice table
SELECT 
	c.first_name,
    c.last_name,
    MIN(i.total) AS min_cost,
	MAX(i.total) AS max_cost,
	ROUND(AVG(i.total), 2) AS average_cost,
	COUNT(i.total) AS total_purchases
FROM 
	invoice AS i
	INNER JOIN client AS c ON i.customer_id = c.customer_id
WHERE 
	i.billing_country = 'USA'
GROUP BY 
	first_name,
	last_name
ORDER BY 
	max_cost DESC
LIMIT 10; 
```

```SQL
-- Joining multiple tables
SELECT 
	t.name,
	i.unit_price,
	pt.playlist_id,
    p.name AS playlist_name
FROM 
	track AS t
	INNER JOIN invoice_line AS i ON t.track_id=i.track_id
	INNER JOIN playlist_track AS pt ON t.track_id=pt.track_id
	INNER JOIN playlist AS p ON pt.playlist_id=p.playlist_id
LIMIT 20
```

```SQL
-- Joining multiple tables
SELECT
    books.name AS books_name,
    books.author_id AS books_author_id,
    author.first_name AS author_first_name,
    author.last_name AS author_last_name,
    books.genre_id AS books_genre_id,
    genre.name AS genre_name
FROM
    books
    INNER JOIN author ON author.author_id = books.author_id
    INNER JOIN genre ON genre.genre_id = books.genre_id;
```

```SQL
-- Joining multiple tables
SELECT 
	transactions.id_transaction AS id_transaction,
    stores.name_store AS name_store,
    products.category AS category,
    products.name AS name
FROM
    transactions
    INNER JOIN products ON products.id_product = transactions.id_product
    INNER JOIN stores ON stores.id_store = transactions.id_store
WHERE
    transactions.date::date = '2019-06-05'
```

```SQL
-- Joining using a subquery result
SELECT 
	AVG(temp.all_count)
FROM (
		SELECT 
			alb.title,
			COUNT(track_id) AS all_count
	    FROM 
		    album as alb
		    INNER JOIN track AS t ON t.album_id = alb.album_id
	    WHERE 
		    alb.title LIKE '%Rock%'
	    GROUP BY 
		    alb.title
	    HAVING 
		    COUNT(track_id) >=8
	) as temp
```

```SQL
--Using an aggregate function when joining tables
SELECT
    genre.name AS genre_name,
    COUNT(books.name) AS name_cnt
FROM
    books
    INNER JOIN genre ON genre.genre_id = books.genre_id
GROUP BY
    genre_name;
```

```SQL
--Using an aggregate function when joining tables
SELECT
    genre.name AS genre_name,
    author.first_name AS author_first_name,
    author.last_name AS author_last_name,
    COUNT(books.name) AS name_cnt
FROM
    books
    INNER JOIN genre ON genre.genre_id = books.genre_id
    INNER JOIN author ON author.author_id = books.author_id
GROUP BY
    genre_name,
    author_first_name,
    author_last_name;
```

```SQL
--Using an aggregate function when joining tables
SELECT 
	transactions.id_transaction AS id_transaction,
    COUNT(products.name) AS name_cnt,
    COUNT(DISTINCT products.name) AS name_uniq_cnt
FROM
    transactions
    INNER JOIN products ON products.id_product = transactions.id_product
GROUP BY 
    id_transaction
LIMIT 10
```

```SQL
--Using an aggregate function when joining tables
SELECT 
	transactions.id_transaction AS id_transaction,
    COUNT(products.name) AS name,
    COUNT(DISTINCT products.name) AS name_uniq_cnt
FROM
    transactions
    INNER JOIN products ON transactions.id_product = products.id_product
GROUP BY
    id_transaction
HAVING
	COUNT(products.name) != COUNT(DISTINCT products.name)
```

```SQL
--Using an aggregate function when joining tables
SELECT 
	weather.rain as rain,
    COUNT(DISTINCT transactions.id_transaction) AS uniq_transactions
FROM
    transactions
    INNER JOIN weather ON CAST(weather.date AS date) = 
    CAST(transactions.date AS date)
GROUP BY 
	rain
```


---
---

# `LEFT OUTER JOIN` (`LEFT JOIN`)
### How does `LEFT OUTER JOIN` join work?
* `LEFT OUTER JOIN` (`LEFT JOIN`) select all the data from the LEFT table together with the rows from the RIGHT table that match the join condition
* The order in which the tables are joined DOES AFFECT the final result.

#### Theoretical Example: `LEFT OUTER JOIN`
* ***BEFORE JOINING**
	* Table 1: Data on domestic animals
	* Table 2: Data on the lengths of animal tails

| Table 1 |         |     | Table 2 |      |
| ------- | ------- | --- | ------- | ---- |
| id      | name    |     | id      | tail |
| 1       | cat     |     | 1       | 10   |
| 2       | dog     |     | 2       | 5    |
| 3       | hamster |     | 4       | 1    |
* ***AFTER JOINING**
	* All the rows from the first (left) table together with the data from the second (right) table that matches the condition. There is an empty value for the length of hamster tails since the hamster row didn't match the condition.

| id  | name    | tail |
| --- | ------- | ---- |
| 1   | cat     | 10   |
| 2   | dog     | 5    |
| 3   | hamster | NULL |
#### `LEFT OUTER JOIN` (`LEFT JOIN`)
* Returns all records from the left table (table1), and the matching records from the right table (table2). 
```SQL
--SYNTAX
SELECT
    TABLE_1.field_1 AS field_1,
    TABLE_1.field_2 AS field_2,
    ...
	TABLE_2.field_n AS field_n
FROM
    TABLE_1
    LEFT JOIN TABLE_2 ON TABLE_2.field = TABLE_1.field;
```

```SQL
--Example
SELECT
    author.first_name AS first_name,
    author.last_name AS last_name,
    author.author_id AS author_id,
    books.name AS name,
    books.author_id AS books_author_id
FROM
    author
    LEFT JOIN books ON books.author_id = author.author_id;
```

```SQL
SELECT 
	products.id_product AS id_product,
    products.name AS name,
    products_stores.id_store AS id_store
FROM
    products
    LEFT JOIN products_stores ON products_stores.id_product = 
    products.id_product
WHERE
	id_store IS NULL
```

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

```sql
SELECT 
	s.last_name AS employee_last_name,
    COUNT(c.customer_id) AS all_customers
FROM 
	staff AS s
	LEFT OUTER JOIN client AS c ON s.employee_id = c.support_rep_id
GROUP BY 
	s.employee_id
ORDER BY 
	all_customers DESC,
	employee_last_name;
```

```sql
SELECT 
	art.name
FROM 
	artist as art
	LEFT OUTER JOIN album AS alb ON alb.artist_id = art.artist_id
GROUP BY 
	art.name
HAVING 
	COUNT(alb.title) = 0
```

```sql
-- Joining multiple tables
SELECT 
	t.name,
	CAST(inv.invoice_date AS DATE)
FROM 
	track AS t
	LEFT OUTER JOIN invoice_line AS i ON i.track_id = t.track_id 
	LEFT OUTER JOIN invoice AS inv ON inv.invoice_id = i.invoice_id
```

```SQL
-- Joining multiple tables
SELECT
    books.name AS name,
    genre.name AS genre_name,
    author.first_name AS first_name,
    author.last_name AS last_name
FROM
    books
    INNER JOIN author ON author.author_id = books.author_id
    RIGHT JOIN genre ON genre.genre_id = books.genre_id;
```

```SQL
-- Joining multiple tables
SELECT
	CAST(weather.date AS date) AS date,
    weather.temp AS temp,
    weather.rain AS rain,
    products.name AS name
FROM
    weather
    LEFT JOIN transactions ON CAST(transactions.date AS date) = 
       CAST(weather.date AS date)
    LEFT JOIN products ON products.id_product = transactions.id_product
ORDER BY 
	date DESC,
    name ASC
LIMIT 30
```

```SQL
-- Joining multiple tables
SELECT 
	transactions.id_transaction AS id_transaction,
    products.name AS name
FROM
    transactions
    INNER JOIN products ON products.id_product = transactions.id_product
    INNER JOIN weather ON CAST(weather.date AS date) = 
    CAST(transactions.date AS date)
WHERE 
	weather.rain = False
```

```SQL
-- Joining a subquery result with another table
SELECT 
	DISTINCT products.name AS name
FROM
    products
    LEFT JOIN ( 
        SELECT 
            id_product
        FROM
            transactions
        WHERE
            id_store = 3
	    ) AS subquery 
	ON subquery.id_product = products.id_product
WHERE
    subquery.id_product IS NULL;
```

```SQL
-- Joining a subquery result with another table
SELECT 
    DISTINCT products.name AS name
FROM
    products
    LEFT JOIN (
        SELECT
            id_product,
            id_store
        FROM
            transactions
        WHERE
            CAST(transactions.date AS date) = '2019-06-11'
        ) AS subquery 
    ON subquery.id_product = products.id_product
WHERE
    subquery.id_store IS NULL;
```

```SQL
--Using an aggregate function when joining tables
SELECT 
	weather.date::date AS date,
    weather.temp AS temp,
    COUNT(DISTINCT transactions.id_transaction) AS uniq_transactions
FROM
    weather
    LEFT JOIN transactions ON CAST(weather.date AS date) = 
    CAST(transactions.date AS date)
GROUP BY 
	weather.date::date,
    temp
ORDER BY 
	weather.date::date
```

```SQL
--Joining tables on more than one condition (using several AND)
SELECT 
	transactions.id_transaction AS id_transaction,
    SUM(products_stores.price) AS total,
    COUNT(products_stores.id_product) AS amount
FROM
    transactions
    LEFT JOIN products_stores ON CAST(products_stores.date_upd AS date) =
    CAST(transactions.date AS date) 
    AND products_stores.id_product = transactions.id_product
    AND products_stores.id_store = transactions.id_store
GROUP BY 
	id_transaction
HAVING
    SUM(products_stores.price) > 35
```

```SQL
-- Joining a subquery result with another table
SELECT
    DISTINCT products.name as name
FROM products
    LEFT JOIN (
        SELECT
			id_product
        FROM
			transactions 
        WHERE
			CAST(transactions.date AS date) = '2019-06-08'
    ) AS subq ON products.id_product = subq.id_product
WHERE
    subq.id_product IS NOT NULL;
```


---
---

# `RIGHT OUTER JOIN` (`RIGHT JOIN`)
## How does `RIGHT OUTER JOIN` join work?
* `RIGHT OUTER JOIN` (`RIGHT JOIN`) select all the data from the RIGHT table together with the rows from the LEFT table that match the join condition
* The order in which the tables are joined DOES AFFECT the final result.

#### Theoretical Example: `RIGHT OUTER JOIN`
* ***BEFORE JOINING**
	* Table 1: Data on domestic animals
	* Table 2: Data on the lengths of animal tails

| Table 1 |         |     | Table 2 |      |
| ------- | ------- | --- | ------- | ---- |
| id      | name    |     | id      | tail |
| 1       | cat     |     | 1       | 10   |
| 2       | dog     |     | 2       | 5    |
| 3       | hamster |     | 4       | 1    |
* ***AFTER JOINING**
	* This table contains every row from the second (right) table and the data from the first (left) table that matched the condition. There's a cell with `NULL` whose tail is one inch long

| id  | name | tail |
| --- | ---- | ---- |
| 1   | cat  | 10   |
| 2   | dog  | 5    |
| 3   | NULL | 1    |

#### `RIGHT OUTER JOIN` (`RIGHT JOIN`)
* Returns all records from the right table (table2), and the matching records from the left table (table1). 
```SQL
--SYNTAX
SELECT
    TABLE_1.field_1 AS field_1,
    TABLE_1.field_2 AS field_2,
    ...
	TABLE_2.field_n AS field_n
FROM
    TABLE_1
    RIGHT JOIN TABLE_2 ON TABLE_1.field = TABLE_2.field;
```

```SQL
--Example
SELECT
    books.name AS name,
    genre.name AS genre_name
FROM
    books
    RIGHT JOIN genre ON genre.genre_id = books.genre_id;
```

```SQL
--Example
SELECT
    books.name AS name,
    genre.name AS genre_name
FROM
    genre
    RIGHT JOIN books ON books.genre_id = genre.genre_id;
```

```SQL
--Example
SELECT 
	art.name,
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

```SQL
SELECT 
	cast(weather.date AS date) AS date
FROM
    transactions
    RIGHT JOIN weather ON CAST(weather.date AS date) = 
    CAST(transactions.date AS date)
WHERE 
    transactions.date IS NULL
```

```SQL
-- Joining a subquery result with another table
SELECT
     products.name AS name
FROM ( SELECT DISTINCT --select unique products from the store 3
		transactions.id_product
    FROM
        transactions		
    WHERE
		transactions.id_store = 3
        ) AS subquery
    RIGHT JOIN products ON products.id_product = subquery.id_product
WHERE 
    subquery.id_product IS NULL
```


---
---

# `FULL OUTER JOIN` (`OUTER JOIN`)
### How does `FULL OUTER JOIN` join work?
* `FULL OUTER JOIN` (`OUTER JOIN`) combines all the data from the left and right table
	* The order in which the tables are joined DOES NOT affect the final result.
* Used for printing all records from the left and right tables

#### Theoretical Example: `FULL OUTER JOIN`
* ***BEFORE JOINING**
	* Table 1: Data on domestic animals
	* Table 2: Data on the lengths of animal tails

| Table 1 |         |     | Table 2 |      |
| ------- | ------- | --- | ------- | ---- |
| id      | name    |     | id      | tail |
| 1       | cat     |     | 1       | 10   |
| 2       | dog     |     | 2       | 5    |
| 3       | hamster |     | 4       | 1    |
* ***AFTER JOINING**
	* This table contains every row from the first (left) table and the data from the second (table) table that matched the condition. 

| id  | name    | tail |
| --- | ------- | ---- |
| 1   | cat     | 10   |
| 2   | dog     | 5    |
| 3   | hamster | null |
| 4   | null    | 1    |
#### `FULL OUTER JOIN` (`OUTER JOIN`)
* Returns all records when there is a match in left (table1) or right (table2) table records
```SQL
--SYNTAX
SELECT
    TABLE_1.field_1 AS field_1,
    TABLE_1.field_2 AS field_2,
    ...
	TABLE_2.field_n AS field_n
FROM
    TABLE_1
    FULL OUTER JOIN TABLE_2 ON TABLE_1.field = TABLE_2.field;
```

```SQL
--Example
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


---
---

# Vertical Joining

## `UNION` vs `UNION ALL` Joining
* `UNION` -- combines the result-set of two or more `SELECT` statements
	* Only distinct values by default
* `UNION ALL` -- combines the result-set of two or more `SELECT` statements
	* Allows for duplicate values
		![[union-table-example.png]]

## Characteristics of Union Tables
- The fields (columns) in the `SELECT` statements must also be in the same order
- The number number of fields (columns) in the `SELECT` statements should be the same
- The fields (columns) must also have similar data types


---
# `Union` 

#### Theoretical Example: `UNION`
* ***BEFORE UNION***
	* Table 1 and Table 2 are going to undergo a `UNION`

| year_tag | name      | weight | breed        |
| -------- | --------- | ------ | ------------ |
| 234657   | Betty Sue | 350    | Belgian Blue |
| 456721   | Penelope  | 500    | Holstein     |
| 567243   | Dorothy   | 400    | Belgian Blue |

| tag    | name     | weight | breed        |
| ------ | -------- | ------ | ------------ |
| 456721 | Penelope | 500    | Holstein     |
| 567243 | Dorothy  | 400    | Belgian Blue |
| 778958 | Olivia   | 300    | Holstein     |
| 653216 | Moon     | 450    | Holstein     |
* ***AFTER UNION***
	* A table without duplicates is produced

|year_tag|name|weight|
|---|---|---|
|234657|Betty Sue|350|
|456721|Penelope|500|
|567243|Dorothy|400|
|778958|Olivia|300|
|653216|Moon|450|

#### `UNION`
* Used to join tables vertically (combine rows from different tables that have the same fields)
	* Ignores absolute duplicates
```SQL
--SYNTAX
SELECT
    column_name_1
FROM
    table_1
UNION 
SELECT
    column_name_1
FROM
    table_2;
```

```SQL
--Example
SELECT
    year_tag,
    name,
    weight
FROM
    cows_grandpa
UNION
SELECT
    tag,
    name,
    weight
FROM
    cows_grandma;
```

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

```SQL
SELECT
    COUNT(SUBQ.name)
FROM (
	SELECT 
		DISTINCT products.name AS name
    FROM
        products
	    LEFT JOIN (
	        SELECT
	            id_product
	        FROM
	            transactions
	        WHERE
	            CAST(transactions.date AS date) = '2019-06-01'
	    ) AS SUBQ1 ON products.id_product = SUBQ1.id_product
WHERE
	SUBQ1.id_product IS NOT NULL
UNION
    SELECT 
	    DISTINCT products.name AS name
    FROM
        products
	    LEFT JOIN (
	        SELECT
	            id_product
	        FROM
	            transactions
	        WHERE
	            CAST(transactions.date AS date) = '2019-06-08'
	    ) AS SUBQ2 ON products.id_product = SUBQ2.id_product
WHERE
	SUBQ2.id_product IS NOT NULL) AS SUBQ
```

---
# `UNION ALL`
#### Theoretical Example: `UNION ALL`
* ***BEFORE UNION***
	* Table 1 and Table 2 are going to undergo a `UNION ALL`

| year_tag | name      | weight | breed        |
| -------- | --------- | ------ | ------------ |
| 234657   | Betty Sue | 350    | Belgian Blue |
| 456721   | Penelope  | 500    | Holstein     |
| 567243   | Dorothy   | 400    | Belgian Blue |

| tag    | name     | weight | breed        |
| ------ | -------- | ------ | ------------ |
| 456721 | Penelope | 500    | Holstein     |
| 567243 | Dorothy  | 400    | Belgian Blue |
| 778958 | Olivia   | 300    | Holstein     |
| 653216 | Moon     | 450    | Holstein     |
* ***AFTER UNION***
	* A table without duplicates is produced

|year_tag|name|weight|
|---|---|---|
|234657|Betty Sue|350|
|456721|Penelope|500|
|567243|Dorothy|400|
|778958|Olivia|300|
|653216|Moon|450|
|567890|Cowboy|600|
|987260|Duke|500|
|675364|Homer|550|

#### `UNION ALL`
* Used to join tables vertically (combine rows from different tables that have the same fields) 
	* Includes ALL records (even duplicates)
```SQL
--SYNTAX
SELECT
    column_name_1
FROM
    table_1
UNION ALL
SELECT
    column_name_1
FROM
    table_2;
```

```SQL
--Example
SELECT
    year_tag,
    name,
    weight
FROM
    cow
UNION ALL
SELECT
    year_tag,
    name,
    weight
FROM
    bulls;
```

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

```SQL
SELECT
    COUNT(SUBQ.name)
FROM (
	SELECT 
		DISTINCT products.name AS name
    FROM
        products
	    LEFT JOIN (
	        SELECT
	            id_product
	        FROM
	            transactions
	        WHERE
	            CAST(transactions.date AS date) = '2019-06-01'
	    ) AS SUBQ1 ON products.id_product = SUBQ1.id_product
WHERE
	SUBQ1.id_product IS NOT NULL
UNION ALL
	SELECT DISTINCT
		products.name AS name
	FROM
		products
		LEFT JOIN (
            SELECT
                id_product
            FROM
                transactions
            WHERE
                CAST(transactions.date AS date) = '2019-06-08'
        ) AS SUBQ2 ON products.id_product = SUBQ2.id_product
WHERE
	SUBQ2.id_product IS NOT NULL) as SUBQ
```