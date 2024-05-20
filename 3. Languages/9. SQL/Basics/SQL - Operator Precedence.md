See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]
* [[SQL - Data Slicing]]
* [[SQL - Joining Tables]]
* [[SQL - Organizing Data]]
* [[SQL - Functions in SQL]]
Resources:


----
# Rules for Queries
1) `SELECT`
2) `FROM`
3) `WHERE` 
4) `GROUP BY`
5) `HAVING` 
6) `ORDER BY` 
7) `LIMIT` 
```SQL 
SELECT
	...
FROM 
	...
WHERE
	...
GROUP BY
	...
HAVING
	...
ORDER BY
	...
LIMIT ... OFFSET...
```

# The Query Execution Order
1. Find where the data is coming from using `FROM`.
2. Give tables shorter names using `AS`.
3. Connect tables together using `JOIN`.
4. Pick out specific rows using `WHERE`.
5. Group similar data together using `GROUP BY`.
6. Do calculations on grouped data (using aggregate functions).
7. Filter grouped data further using `HAVING`.
8. Choose which fields to display and give them names using `SELECT`.
    - Note: Aliases can't be used after `WHERE` and `HAVING` because they haven't been assigned yet.
9. Only show unique values using `DISTINCT`.
10. Arrange the data in a certain order using `ORDER BY`.
11. Limit the number of results using `LIMIT` and `OFFSET`

