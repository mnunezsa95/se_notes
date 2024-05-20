See:
* [[SQL - Introduction to SQL]]
* [[SQL - 0. Info Database]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)

---

# Renaming Fields and Tables

## Why is renaming Fields and Tables useful?
* Sometimes the table is exported with generic field names (such as: round from using the `ROUND()` function
* This can be renamed to be more specific and easily identifiable 

## Limitations to Renaming Fields and Tables
* Cannot address an alias in `WHERE` or `HAVING` (because operators in SQL aren’t executed in the order they’re listed in a query)

## Working with Aliases (Assigning Aliases to Fields or Tables)
#### Fields
* Changing a name to an alias is temporary will NOT change the database name
* How to do it (two ways)
	1) Use the `AS` operator in the `SELECT` statement after the field
	2) Adding the new name after a space in the `SELECT` statement (PostgreSQL Only)
```sql
--- Option #1
SELECT 
	EXTRACT(YEAR FROM CAST(invoice_date AS DATE)) AS year_of_purchase
FROM
	table_1
```

```SQL
--- Option #2 (Only works in PostgreSQL)
SELECT 
	EXTRACT(YEAR FROM CAST(invoice_date AS DATE)) year_of_purchase
FROM
	table_1
```

```SQL
--Example
SELECT 
	rating AS rating_of_epic,
	release_year AS year_of_epic,
	AVG(rental_duration) AS average_rental
FROM 
	movie 
WHERE 
	description LIKE '%Epic%'
GROUP BY 
	rating_of_epic,
	release_year
```

#### Tables
* Changing a name to an alias is temporary will NOT change the database name
* Two way:
	1) Use the `AS` operator in the `FROM` statement after the table
	2) Adding the new name after a space in the `FROM` statement (PostgreSQL Only)
```SQL
--Example
SELECT 
	EXTRACT(YEAR FROM CAST(i.invoice_date AS DATE)) AS year_of_purchase,
	MIN(i.total) AS min_cost,
	MAX(i.total) AS max_cost,
	SUM(i.total) AS total_revenue,
	COUNT(i.total) AS total_purchases,
	ROUND(SUM(i.total)/COUNT(DISTINCT(i.customer_id))) AS average_receipt
FROM 
	invoice AS i
WHERE 
	billing_country IN ('USA', 'United Kingdom', 'Germany')
GROUP BY 
	year_of_purchase
ORDER BY 
	year_of_purchase DESC; 
```
