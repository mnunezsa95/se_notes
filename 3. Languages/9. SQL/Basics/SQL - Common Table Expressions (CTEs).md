See [[SQL - Structured Query Language (SQL)]]
#### Common Table Expressions
* CTEs help structure subqueries and take them outside the main query
#### Creating CTEs
* Assign the result of a subquery to an alias (see [[SQL - Joining Tables & Subqueries (dep)]])
	* Syntax:
		* Start with the `WITH` keyword
		* Alias comes first, then followed by `AS` keyword, then the subquery in parentheses
* Separate multiple CTEs with commas (but not after final subquery)
#### Using CTEs
* **Using:** Write the main query and substitute in the CTE

#### Example: Creating and using CTEs
* General syntax
```sql
WITH
-- assigning aliases and forming subqueries
alias_1 AS (subquery_1),
alias_2 AS (subquery_2),
alias_3 AS (subquery_3),
....
alias_n AS (subquery_n)

SELECT -- the main query
-- within the main query, you can work with aliases assigned 
FROM alias_1 INNER JOIN alias_2 ... 
...
```

* Example
```sql
WITH 
-- the first subquery with the alias i
i AS (SELECT billing_country AS country,
             COUNT(total) AS total_invoice
      FROM invoice
      GROUP BY billing_country
      ORDER BY total_invoice DESC
      LIMIT 5), -- subqueries are separated by commas
-- the second subquery with the alias c
 c AS (SELECT country AS country,
              COUNT(customer_id) AS total_clients
              FROM client
              GROUP BY country)

-- the main query where we specify the aliases for subqueries
SELECT i.country,
       i.total_invoice,
       c.total_clients
FROM i LEFT OUTER JOIN c ON i.country = c.country
ORDER BY i.total_invoice DESC; 
```

#### Examples
* Example 1
```sql
--first subquery
WITH 
top AS (SELECT title,
               rental_rate,
               length,
               rating
        FROM movie
        WHERE rental_rate > 2
        ORDER BY length DESC
        LIMIT 40
)

-- Main query
SELECT top.rating,
       MAX(top.length) AS max_length,
       MIN(top.length) AS min_length,
       AVG(top.length) AS avg_length,
       MIN(top. rental_rate) AS min_rental_rate,
       MAX(top. rental_rate) AS max_rental_rate,
       AVG(top. rental_rate) AS avg_rental_rate
FROM TOP
GROUP BY top.rating
ORDER BY avg_length;
```

* Example:
```sql
WITH 

i_1 AS (SELECT 
			EXTRACT(MONTH FROM CAST(invoice_date AS date)) AS invoice_month,
			COUNT(*) AS year_2011
		FROM invoice
	    WHERE EXTRACT(YEAR FROM CAST(invoice_date AS date)) = '2011'         
	    GROUP BY invoice_month),
i_2 AS (SELECT 
			EXTRACT(MONTH FROM CAST(invoice_date AS date)) AS invoice_month,
	        COUNT(*) AS year_2012  
	    FROM invoice
        WHERE EXTRACT(YEAR FROM CAST(invoice_date AS date)) = '2012'
        GROUP BY invoice_month),
i_3 AS (SELECT 
			EXTRACT(MONTH FROM CAST(invoice_date AS date)) AS invoice_month,
            COUNT(*) AS year_2013
        FROM invoice
        WHERE EXTRACT(YEAR FROM CAST(invoice_date AS date)) = '2013'
        GROUP BY invoice_month)
SELECT i_1.invoice_month,
       i_1.year_2011,
       i_2.year_2012,
       i_3.year_2013
FROM i_1
FULL OUTER JOIN i_2 ON i_1.invoice_month = i_2.invoice_month
FULL OUTER JOIN i_3 ON i_1.invoice_month = i_3.invoice_month;
```