See [[SQL - Data Management Commands]]

#### The `CREATE` Command
* `CREATE` --> used to create new databases, schemas, and tables
* Syntax
	* Possible object types: `DATABASE`, `SCHEMA`, `TABLE`
	* Object name
		* Should NOT contain any special characters (underscores are OK)
		* DO NOT use names that are same as a keyword
	* Additional parameters
		* `IF EXISTS <object name>` --> will check if the object exists in the database (command will only execute if it does exist)
		* `WITH ENCODING 'UTF8'` --> will use UTF-8 encoding in the database
```sql
--- Creating a database or schema
CREATE <object type> <object name> <additional parameters> 
```
* Example
```sql
CREATE my_home WITH ENCODING 'UTF8'
CREATE SCHEMA mobile_app
```

#### Creating a table
* The `CREATE` command can be used to create a table
	* If the schema where the table is to be created is NOT specified, it will be created in the 'public' schema by default
* Syntax
	* Field name --> name of field 
	* Data type --> type of data in the field (see [[PostgreSQL - Data Types]])
	* Table field constraints --> prevent records where the value doesn’t meet the condition from being inserted into the table 
		* Order of constrains does not matter
		* Constraints should NOT contradict
		* Constraints can be named using the `CONSTRAINT` keyword
		* Types of constraints (see [[SQL - Database Management Commands and Keywords]])
			* `NOT NULL`
			* `NULL`
			* `UNIQUE`
			* `CHECK` 
			* `PRIMARY KEY`
			* `REFERENCES`
```sql
--- Creating a table
CREATE TABLE <table name> (
    <field name> <data type> <conditions of constraints>,
    <field name> <data type> <conditions of constraints>,
    ...
);
```

* Example
```sql
--- creating a table
CREATE TABLE students (
    student_id integer,
    username text,
    date_created date
); 

-- creating a table in an exisiting schema 
CREATE TABLE sales.students (
    student_id integer,
    username text,
    date_created date
); 

--- creating a table with constriants to the student_id field
CREATE TABLE students (
	student_id integer UNIQUE NOT NULL,
	username text,
	date_recorded date
);

--- the following will lead to an error because NULL and NOT NULL will contradict
CREATE TABLE students (
    student_id integer NULL NOT NULL,
    username text,
    date_created date
); 

--- the CHECK constraint is added and will only add records if price is larger than discount_price
CREATE TABLE courses (
    course_id integer UNIQUE NOT NULL,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price),
    is_open text NOT NULL
); 

--- combining several check constraints
CREATE TABLE courses (
    course_id integer UNIQUE NOT NULL,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price AND price > 0),
    is_open text NOT NULL CHECK (is_open IN ('Y', 'N'))
); 

--- Using PRIMARY KEY constraint to specify the primary key of the table
CREATE TABLE courses (
    course_id PRIMARY KEY,
    course_name text NOT NULL,
    price integer NOT NULL,
    discount_price integer NOT NULL CHECK (price > discount_price AND price > 0),
    is_open text NOT NULL CHECK (is_open IN ('Y', 'N'))
); 

--- Using the REFERENCES constraint to check for linked tables
CREATE TABLE student_x_courses (
    student_id integer REFERENCES students (student_id),
    course_id integer REFERENCES courses (course_id)
); 
```