(See [[SQL - Introduction to SQL]], [[SQL - Database Management Commands and Keywords]])

#### DDL Commands (Data Definition Language Commands)
* DDL commands --> used for managing data structures such as:
	* assigning names to tables and fields
	* specifying field data types
	* deleting tables or fields
* Example(s)
```sql
--- creating a database
CREATE DATABASE university; 

--- creating a table
CREATE TABLE students (
    student_id INTEGER PRIMARY KEY NOT NULL,
    date_created DATE,
    username TEXT,
    email TEXT
); 

--- changing the data type or field name in the table
ALTER TABLE students
ALTER COLUMN student_id TYPE BIGINT;

ALTER TABLE students
RENAME username 
TO user_name; 

--- deleting a table from the database
DROP TABLE users
```


#### DML Commands (Data Manipulation Language Commands)
* DML commands --> used for creating, deleting, and modifying records in tables
* Example(s)
```sql
--- creating records in a table
INSERT INTO table_name (user_id, date_created, username, email)
VALUES (1, '2021-01-01', 'username', 'username@goodweb.org'); 

--- deleting records with a created_at field greater than one specified in code
DELETE FROM users
WHERE date_created > '2020-01-01';

--- change a record that has specified email in the table
UPDATE users
SET username = 'student'
WHERE email = 'username@goodweb.org';
```