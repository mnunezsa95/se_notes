See:
* [[SQL - Introduction to SQL]]
* [[SQL - 0. Info Database]]
* [[SQL - Functions in SQL]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)

---

# Mathematical Operators in SQL
* SQL has several mathematical operators to perform mathematical calculations.
* These mathematical operators **ALWAYS** return a new field (column) containing the result

## Math Operators 

| Operation      | Operator |
| -------------- | -------- |
| Addition       | `+`      |
| Subtraction    | `-`      |
| Multiplication | `*`      |
| Division       | `/`      |

## Working with Mathematical Operators
```sql
--- Adding the drink_cost to meal_cost to find the total_cost
SELECT 
	meal_cost,
    drink_cost,
    drink_cost + meal_cost
FROM 
	order_data
LIMIT 5; 
```

```SQL
--Calling the new field by an alias
SELECT 
    meal_cost,
    drink_cost,
    drink_cost + meal_cost AS total_cost
FROM 
    order_data
LIMIT 5;

```




