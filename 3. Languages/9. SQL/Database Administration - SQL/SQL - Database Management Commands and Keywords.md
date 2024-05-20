See [[SQL - Data Management Commands]], [[SQL - Introduction to SQL]]

---
# Commands
#### CREATE
* `CREATE` used to create new databases, schemas, and tables
* Syntax (see [[SQL - The CREATE Command]])
	* Can use a variety of additional parameters (options)
```SQL
--- Creating a schema or database
CREATE <object type> <object name> <additional parameters> 

--- Creating table
CREATE TABLE <table name> (
    <field name> <data type> <conditions of constraints>,
    <field name> <data type> <conditions of constraints>,
    ...
);
```
* Example
```sql
CREATE my_home WITH ENCODING 'UTF8'
CREATE SCHEMA mobile_app

CREATE TABLE mobile_app.courses (
    course_id integer UNIQUE NOT NULL,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price AND price > 0),
    is_open text NOT NULL CHECK (is_open IN ('Y', 'N'))
); 
```

#### DROP
* `Drop` --> used to delete a table, schema or database
* Syntax (see [[SQL - The DROP Command]])
	* Can use a variety of additional parameters (options)
```sql
DROP <object type> <object name> <additional parameters> 
```
* Example
```sql
DROP DATABASE goodwebschool; -- deletes a database called goodwebschool
DROP TABLE practicum; -- deletes a table called practicum
DROP TABLE goodwebschool.practicum; -- deletes a table that is part of a schema
```

#### ALTER
* `ALTER` --> Used to drop, rename or set a field (see [[SQL - Database Management Commands and Keywords]])
* Syntax
	* `ALTER` cannot be used alone, and must always be used with an action (`SET`, `RENAME`, `DROP`, `ADD`)
```sql
ALTER <object type> <object name> <action> 
```
* Example
```sql
ALTER TABLE users 
DROP COLUMN username;
```

#### SET
* `SET` --> Used to change an object's properties
* Syntax
```sql
SET <object property> <new value> 
```
* Example
```sql
-- ALTER used to select the table students, then add it to a new schema
ALTER TABLE students
SET SCHEMA new_schema;

-- ALTER used to select the 'courses' table, then ALTER used to set the type of a column
ALTER TABLE courses
ALTER COLUMN course_id TYPE text;
```

#### RENAME
* `RENAME` --> Used to change the names of various objects such as databases, schemas, tables or fields
	* Uses the `TO` operator
* Syntax
```sql
RENAME TO <new object name>
```
* Example
```sql
-- ALTER used to select the table practicum, RENAME used to change the database name
ALTER DATABASE practicum
RENAME TO practicum_awesome; 

-- ALTER used to select the table 'students', RENAME used to specify the field to rename, followed by the new name
ALTER TABLE students
RENAME username TO user_name; 

--- ONLY one action can be used for each action (SET or RENAME), so this will cause an error
ALTER TABLE users
ALTER COLUMN email TYPE varchar
RENAME TO customers; 

-- This is how to correctly have two actions (split into two queries)
ALTER TABLE users
ALTER COLUMN email TYPE varchar;
ALTER TABLE users
RENAME TO customers; 
```

#### ADD
* Used to add objects and properties to existing objects 
* Syntax
	* When using additional parameters (`PRIMARY KEY`, `REFERENCES`, `NOT NULL`, and `UNIQUE`, put the field the constraints apply to in parentheses)
```SQL
ADD <object or property type> <object name> <additional parameters> 
```
* Example
```sql
-- adding a field to a table
ALTER TABLE courses
ADD COLUMN course_type text; 

-- Adding a column with specific constraints
ALTER TABLE courses
ADD COLUMN course_type text CHECK(course_type IN ('free', 'paid'));

-- Adding a constraint to an existing field
ALTER TABLE courses
ADD CONSTRAINT course_valuation CHECK(course_valuation IN (1, 2, 3)); 

ALTER TABLE courses
ADD CONSTRAINT pk_course_id PRIMARY KEY(course_id); 
```


---
# Keywords

#### CONSTRAINT
* Used to name a constraint when it is declared
* Example
```sql
--- text constraint is named 'flag'
CREATE TABLE courses (
    course_id integer UNIQUE NOT NULL,
    course_name text NOT NULL,
    price integer NOT NULL,
    is_open text CONSTRAINT flag NOT NULL CHECK (is_open IN ('Y', 'N'))
); 
```


---
# Constraints

#### NOT NULL
* `NOT NULL` --> bans records of values equal to `NULL` (see [[SQL - Null Values]], [[SQL - The CREATE Command]])
* Examples
```sql
CREATE TABLE students (
	student_id integer UNIQUE NOT NULL,
	username text,
	date_recorded date
);
```

#### NULL
* `NULL` --> inserts `NULL` as a value to a record when a value is not specified (see [[SQL - The CREATE Command]])
* Example
```sql
CREATE TABLE students (
	student_id integer UNIQUE NOT NULL,
	username text,
	date_recorded date NULL
);
```

#### UNIQUE
* `UNIQUE` --> checks the uniqueness of a particular field before it is recorded (see [[SQL - The CREATE Command]])
```SQL
CREATE TABLE students (
	student_id integer UNIQUE NOT NULL,
	username text,
	date_recorded date NULL
);
```

#### CHECK
* `CHECK` --> specify which values can and can't be recorded in a field (see [[SQL - The CREATE Command]])
	* If condition returns `FALSE`, an error will occur and the record is NOT added to the table; it will be added if the condition is `TRUE`
	* Several conditions can be combined with `AND` or `OR` operators (see [[SQL - Commands, Clauses, Statements, Operators and Functions]])
* Example
```sql
CREATE TABLE courses (
    course_id integer UNIQUE NOT NULL,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price AND price > 0),
    is_open text NOT NULL CHECK (is_open IN ('Y', 'N'))
); 
```

#### PRIMARY KEY
* `PRIMARY_KEY` -> specifies that values in one column (or combinations of values in several columns) will be the primary key of this table
	* The database's metadata will specify that this is the primary key
	* Same as using `UNIQUE NOT NULL`
* Example
```SQL
CREATE TABLE courses (
    course_id PRIMARY KEY,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price AND price > 0),
    is_open text NOT NULL CHECK (is_open IN ('Y', 'N'))
); 
```

#### REFERENCES
* `REFERENCES` --> checks whether records from the primary and foreign keys exist in both connected tables
	* If a value does not exist in the table, an error occurs
	* The database's metadata will be updated when foreign key is created
* Syntax
	* Put parentheses around the field that has a link in the database
```sql
REFERENCES <table> (<field in the table>) 
```
* Example
	* We can create the `student_x_courses` table and check that the student is recorded in the `students` table and the bootcamp is recorded in the `courses` table.
```sql
CREATE TABLE student_x_courses (
    student_id integer REFERENCES students (student_id),
    course_id integer REFERENCES courses (course_id)
); 
```

#### `IF EXISTS`
* Can be used to delete something only if it exists
```SQL
--- Dropping a table if it exists
DROP TABLE IF EXISTS users; 
```

#### `Restrict`
* Forbids an object from being deleted if there are other object that refer to it
	* Example: Prevents the deletion of a table that is connected to another table
```SQL
-- Prevents the deletion of an object connected to another object
DROP TABLE practicum.users RESTRICT; 
```

#### `Cascade`
* Deletes a table (regardless of linkage to other objects). The relationship with the dependent table is also deleted
```SQL
-- Deleting a table regardless of whether or not it is linked to another document
DROP TABLE practicum.users CASCADE; 
```