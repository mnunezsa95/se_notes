See [[SQL - Structured Query Language (SQL)]]

#### Exploring table joining and subqueries
* Most times, the result attained by joining tables, can also be done via subqueries
* Subqueries can be joined together (see [[SQL - Types of Table Joining]])
* Syntax
```sql
...
-- there are 4 different types of join
FROM (......) LEFT OUTER JOIN (......) ON ...
... 
```

* Example
![](https://lh7-us.googleusercontent.com/Bu1KUacNVz8bj1aEEViDQb_qKhw-sXd9JSCmY1Ij4X6YjD23vhmOS79jnXQDirzG3q6debcnNYLY1dnWUR7hnLcJtykMgdCHuT4vQ-8f4OLpA6mVrI2COnv2LdHzzK0UlwE5PjPDKVOLD5YN4qunUc8)

* Subqueries should be given aliases
```sql
SELECT i.country,
       i.total_invoice,
       c.total_clients
FROM
  (SELECT billing_country AS country,
          COUNT(total) AS total_invoice
   FROM invoice
   GROUP BY billing_country
   ORDER BY total_invoice DESC
   LIMIT 5) AS i
LEFT OUTER JOIN
  (SELECT country,
          COUNT(customer_id) AS total_clients
   FROM client
   GROUP BY country) AS c ON i.country = c.country
ORDER BY i.total_invoice DESC; 
```

#### Example
* Example 1
```sql
SELECT DISTINCT c.last_name
FROM invoice AS i
LEFT JOIN client AS c ON i.customer_id = c.customer_id
WHERE i.customer_id IN
    (SELECT customer_id
     FROM invoice
     WHERE CAST(invoice_date AS date) BETWEEN '2013-01-01' AND '2013-01-31')
  AND CAST(invoice_date AS date) BETWEEN '2013-02-01' AND '2013-12-31';
```

