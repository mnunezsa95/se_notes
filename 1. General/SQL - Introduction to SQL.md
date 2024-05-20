See:


---

## What is  Structured Query Language (SQL)? 
- SQL -- a special, declarative, programming language used to work with and manage data in relational databases
	- SQL can be used to insert, modify, or remove data and manage data tables
- SQL has many **dialects** (a set of additional commands that expand the general capabilities of the SQL language)
- There are different types of SQL databases
	- PostgreSQL (see [[SQL - Installing PostgreSQL 1]])

## What is a SQL Statement?
- Statement (query)  -- a request written using commands and using the SQL syntax to access data from the database

## General SQL Syntax Rules 
- `SQL` is not case-sensitive
- Lines after operators should be indented
- Statement should end with a semicolon (`;`)
- Comments are used to document code
	- Single-line comments are marked with two hyphens ( `--` )
	- Multi-line comments use `/* */`
- Commands are written in uppercase letters (common, but not required)
- Line breaks are inserted after each keyword (common, but not required)
```sql
-- Select columns from the table 
SELECT 
  column_1, 
  column_2, 
  column_3 ... 
  
FROM 
  table_name;
```

```sql
-- Select all columns from stock
SELECT 
  *
FROM 
  Stock;
```

```sql
SELECT 
  * 

FROM 
  Stock 

WHERE 
  Price < 100;   -- Defining the condition of row selection**
```