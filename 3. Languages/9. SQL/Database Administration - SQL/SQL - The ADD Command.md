See [[SQL - Data Management Commands]]
#### ADD
* Used to add objects and properties to existing objects (see [[SQL - Database Management Commands and Keywords]])
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