See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
Resources


---
# Subqueries

## What is a subquery?
* Subquery -- (also known as inner queries or nested queries) is a tool for performing operations in multiple steps
* Subqueries can be performing in multiple places:
	* `FROM` Statement
	* `WHERE` Statement -- to combine data from different tables
## Subquery Characteristics
* Subqueries are ALWAYS placed in parentheses `()`
* Subqueries should be in new lines and indented 
* Subqueries should be named
* Subqueries DO NOT use semi-colons 
* The name of the table is indicated within the inner query, and the outer query refers to the table's columns

## Helpful Tips for Writing Subqueries
* Start with inner-most query and work outwards

## Types of Subqueries
### `FROM` Subquery
* `FROM` subqueries are placed in parentheses immediately after the `FROM` statement
	* If a subquery is inside the `FROM` block, `SELECT` will select data from the table that gets generated by the subquery.
![[from-subquery.png]]

```SQL
-- SYNTAX
SELECT 
	SUBQUERY_1.column_name, 
	SUBQUERY_1.column_name_2
FROM -- subqueries should be in new lines and indented 
    (SELECT 
        column_name,
        column_name_2
    FROM 
        table_name
    WHERE 
        column_name = value) AS SUBQUERY_1; -- nameing the subquery
```

```SQL
-- Example
SELECT 
    AVG(Sub.count_rating) AS avg_count_rating
FROM
    (SELECT 
        COUNT(rating) as count_rating
    FROM 
        books
    GROUP BY genre) AS Sub;
```

| Explanation (above)                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The inner query calculated the number of book ratings for each genre and saved the values in the count_rating field. Now the outer query can take the resulting table and do its job. |

```SQL
-- Example
SELECT
	ROUND(AVG(best_rating.average_rental), 2)
FROM 
	(SELECT 
		m.rating,
        AVG(m.rental_rate) AS average_rental
	FROM   
		movie AS m
	GROUP  BY 
		m.rating
	ORDER  BY 
		average_rental DESC
	LIMIT  5) AS best_rating; 
```

```SQL
SELECT 
	t.rating,
    MAX(t.length) AS max_length,
    MIN(t.length) AS min_length,
    AVG(t.length) AS avg_length,
    MAX(t.rental_rate) AS max_rental_rate,
    MIN(t.rental_rate) AS min_rental_rate,
    AVG(t.rental_rate) AS avg_rental_rate
FROM 
	(SELECT 
		title,
        rental_rate,
	    length,
	    rating
	FROM 
	   movie
	WHERE 
	   rental_rate > 2
	ORDER BY 
	   length DESC
	LIMIT 40) AS t
	
GROUP BY rating
ORDER BY avg_length ASC
```

```SQL
SELECT 
    EXTRACT(WEEK FROM SUBQ.trunc_date) AS week_number,
    AVG(SUBQ.transactions_per_day) AS avg_week_transaction
FROM
	(SELECT
        COUNT(DISTINCT id_transaction) AS transactions_per_day,
        DATE_TRUNC('day', date) AS trunc_date
    FROM
        transactions
	GROUP BY
        trunc_date) AS SUBQ
GROUP BY
    week_number
```




#### `WHERE` Subquery
* `WHERE` subqueries are placed in parentheses immediately after the `WHERE` statement
	* If a subquery is placed in the `WHERE` block, then the main query will compare the results of the subquery with values from the table in the outer `FROM` block
		* Data will only be selected if it is a match
* The data in the parentheses is used as condition
![[where-subquery.png]]

```SQL
--SYNTAX
SELECT 
    column_name, 
    column_name_1
FROM 
    table_name
WHERE 
    column_name IN  
            (SELECT 
                column_1
            FROM 
                table_name_2  
            WHERE 
                column_1 = value_1 OR column_1 = value_2);
```

```SQL
--Example
SELECT 
    name,
    publisher_id
FROM 
    books
WHERE 
    publisher_id = 
            (SELECT 
                 publisher_id
            FROM 
                publisher
            WHERE 
                name ='Knopf');
```

| Explanation (above)                                                                                                                                                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The subquery selects from the `publisher` table only those `publisher_id` values that match the publisher name Knopf. The result is 10. There is only one `publisher` table value related to Knopf.<br><br>Then the outer query selects names and publisher IDs from the `books` table, but only those that match the result of our inner query (i.e. whose publisher ID is 10). |

```SQL
SELECT 
    name,
    publisher_id
FROM 
    books
WHERE 
    publisher_id IN 
            (SELECT 
                 publisher_id
            FROM 
                publisher
            WHERE 
                name IN ('Knopf', 'Collins', 'Crown'));
```

| Explanation (above)                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The inner query's IN statement selects the publisher IDs associated with the names Knopf, Collins, and Crown from the `publisher` table, giving us 10, 15, and 19. These values are then passed to the outer query.<br><br>The outer query, in turn, selects from the `books` table the names and publishers associated with the `publisher_id` values selected by the inner query: our old friends 10, 15, and 19. |

```sql
SELECT 
	*
FROM 
	client
WHERE 
	customer_id IN 
		(SELECT 
			customer_id
        FROM 
	        invoice
		GROUP BY 
			customer_id
		ORDER BY 
			SUM(total) DESC
		LIMIT 10); 
```

```sql
SELECT 
	name
FROM 
	genre
WHERE genre_id IN 
	(SELECT 
		genre_id
	FROM 
		track
    ORDER BY 
	    milliseconds ASC
	LIMIT 10);
```

```sql
SELECT 
	DISTINCT billing_city
FROM 
	invoice
WHERE 
	total > 
		(SELECT 
			AVG(total) as avg_total
		FROM 
			invoice
        WHERE 
	        EXTRACT(YEAR FROM CAST(invoice_date AS DATE)) = 2009);
```

```SQL
SELECT 
    DISTINCT user_id
FROM 
	transactions
WHERE 
    id_product IN 
        (SELECT 
        	id_product 
    	FROM 
        	products_data_all
    	WHERE 
        	(category='milk' AND  price > 17) OR 
        	(category='butter' AND price > 9));
```

##### Using Multiple `WHERE` Subqueries
* Multiple `WHERE` subqueries can be joined using logical operators
```sql
SELECT 
	*
FROM 
	invoice
WHERE 
	customer_id IN 
		(SELECT 
			customer_id
		FROM 
			invoice
		WHERE 
			billing_country = 'Brazil') AND 
			total > 
				(SELECT 
					AVG(total)
				FROM invoice); 
```

```sql
SELECT 
	billing_country,
    MIN(total) AS min_total,
	MAX(total) AS max_total,
	AVG(total) AS avg_total
FROM 
	invoice
WHERE 
	invoice_id IN 
		(SELECT 
			invoice_id
        FROM 
	        invoice_line
        GROUP BY 
	        invoice_id
		HAVING 
			COUNT(invoice_id) > 5) AND 
			total > 
				(SELECT 
					AVG(unit_price)
				FROM 
					invoice_line)
GROUP BY billing_country
ORDER BY avg_total DESC;
```