See [[SQL - Data Management Commands]]

#### The DROP Command
* `Drop` --> used to delete a table, schema or database
	* Cannot be undone
* Syntax
	* Possible object types: `DATABASE`, `SCHEMA`, `TABLE`, `Field`
	* Name of the object
	* Additional parameters
		* `IF EXISTS` operator --> can be used to delete something only if it exists 
		* `Restrict` --> forbids an object from being deleted if there are other object that refer to it
			* Example: Prevents the deletion of a table that is connected to another table
		* `Cascade` --> deletes a table (regardless of linkage to other objects). The relationship with the dependent table is also deleted
```sql
--- Creating a database or schema
DROP <object type> <object name> <additional parameters> 
```
* Example
```sql
DROP DATABASE goodwebschool; -- deletes a database called goodwebschool
DROP TABLE practicum; -- deletes a table called practicum
DROP TABLE goodwebschool.practicum; -- deletes a table that is part of a schema

--- Dropping a table if it exists
DROP TABLE IF EXISTS users; 

-- Prevents the deletion of an object connected to another object
DROP TABLE practicum.users RESTRICT; 

-- Deleting a table regardless of whether or not it is linked to another document
DROP TABLE practicum.users CASCADE; 
```