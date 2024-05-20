See:
* [[SQL - Introduction to SQL]]
* [[SQL - Tables]]

---
# ER (Entity-Relationship) Diagrams

## What is an ER Diagram?
* ER Diagram -- show tables and relationships between tables
## When are ER Diagrams created?
* Created during database design stage
## Characteristics of ER Diagrams
* Tables are shown as rectangles with two parts:
	1) Table name (upper part)
	2) List of table fields (lower part) with an indication to which keys they are related to: primary or foreign.
		* The fields that are designated as the `PK` or `FK`.
		![[er-diagram-table.png]]
		
* Relationships are shown by a line connecting two tables
	* The symbols are useful in identifying the type of relationship between tables
		![[er-diagram-relationship.png]]

### Symbols Used to Show Relationships
* One-to-One
		![[er-diagram-one-to-one.png]]
* One-to-Many
		![[er-diagram-one-to-many.png]]
* Many-to-Many
		![[er-diagram-many-to-many.png]]
