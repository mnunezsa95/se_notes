See: 
* [[SQL - Introduction to SQL]]
Resources:
* Official Documentation: [PostgreSQL](https://www.postgresql.org/docs/current/datatype.html)

---
# Tables

## Structure of Tables
* Table -- a set of rows and columns that form cells where they intersect
	* Table columns are called `fields`
	* Table rows are called `records`
	* Table cells -- a unit where a `record` and `field` intersect
![[table-field.png]]
![[table-record.png]]
![[table-cell.png]]


---
# Keys
## Primary Keys (PK)
* **Primary Key** -- a unique attribute added to each record (row) that ensures that the record is distinguishable from the rest
	* Primary Keys can be a number or set of digits and/or characters 
	* Primary keys should be unique
![[primary-key-table.png]]

## Primary Composite Key
* Primary Composite Key -- a combination of several fields that operate as a primary key
![[primary-composite-key.png]]

## Foreign Keys (FK)
* Foreign Keys -- fields that reference the primary key of another table
	* FKs are responsible for the relationship between the two tables
![[foreign-key.png]]


---
# Types of Relationships Between Tables
* There are 3 types of relationships
	* One-to-One -- each row in a table is connected with only one row in the other table
		![[one-to-one-relationship.png]]
	* One-to-Many -- each row of a table matches multiple rows in another table
		* Example: Client table can only contain a list of unique customers with unique IDs, but the invoice table can have a customer many times (can purchase more than once)
		![[one-to-many-relationship.png]]
	* Many-to-Many -- several rows from one table match several rows from another table
		* This type of relationship produces an association table, which combines the primary keys of both tables. 
		* Example: One table has school subjects. Another table has school teachers. One teacher might teach several subjects and one subject might be taught by several teachers
		![[many-to-many-relationship.png]]
