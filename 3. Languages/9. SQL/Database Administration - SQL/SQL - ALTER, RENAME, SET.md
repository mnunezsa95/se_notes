See [[SQL - Data Management Commands]]
#### ALTER
* `ALTER` --> Used to drop, rename or set a field (see [[SQL - Database Management Commands and Keywords]])
	* Allows for the table to be selected first, then altered
* Syntax
	* `ALTER` cannot be used alone, and must always be used with an action (`SET`, `RENAME`, `DROP`, `ADD`)
```sql
ALTER <object type> <object name> <action> 
```
* Example
```sql
ALTER TABLE users 
DROP COLUMN username;

--- ALTER used to select the flats table of the mobile_app schema, then update the column type to numeric
ALTER TABLE mobile_app.flats
ALTER COLUMN area TYPE numeric(1);
```

#### SET
* `SET` --> Used to set an object's properties (see [[SQL - Database Management Commands and Keywords]])
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
* `RENAME` --> Used to change the names of various objects such as databases, schemas, tables or fields (see [[SQL - Database Management Commands and Keywords]])
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