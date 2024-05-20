See [[SQL - Structured Query Language (SQL)]]



#### Nested FROM Subqueries
* Subqueries can be placed inside of subqueries
* Example
```SQL
SELECT ROUND(AVG(best_rating.average_rental), 2)
FROM   (SELECT films_from_2010.rating,
               AVG(films_from_2010.rental_rate) AS average_rental
        FROM   (SELECT *
                FROM   movie
                WHERE  release_year = 2010) AS films_from_2010
        GROUP  BY films_from_2010.rating
        ORDER  BY average_rental DESC
        LIMIT  5) AS best_rating; 
```



* Example 2: Nesting subqueries
```sql
SELECT AVG(temp.min_length) AS avg_min_length,
       AVG(temp.max_length) AS avg_max_length
FROM (
     SELECT top.rating,
       MIN(top.length) AS min_length,
	     MAX(top.length) AS max_length,
	     AVG(top.length) AS avg_length,
	     MIN(top.rental_rate) AS min_rental_rate,
	     MAX(top.rental_rate) AS max_rental_rate,
	     AVG(top.rental_rate) AS avg_rental_rate
     FROM (SELECT title,
             rental_rate,
	           length,
	           rating
       FROM movie
       WHERE rental_rate > 2
       ORDER BY length DESC
       LIMIT 40) AS top
     GROUP BY top.rating
     ORDER BY avg_length) AS temp;
```