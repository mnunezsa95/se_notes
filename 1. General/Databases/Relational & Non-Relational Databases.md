See:
* 

---
## What are Databases?
* A place where structured data is stored
* Convenient structures for organizing information 
* Allow for quick and safe operations with data
## Types of Databases
* There are two types of Databases:
	1) Relational Databases
	2) Non-Relational Databases
### Relational Databases
- Organize data into tables that can be linked to one another (uses several tables)
- Information is stored across different tables and checked across different linked tables
- Are scalable (by increasing power of hardware)
### Non-Relational Databases
- Use collections (which are non-rigid data structures) consisting of documents
- Are scalable (horizontally – by adding more servers)
# Pros and Cons: Relational v Non-Relational

| Type of Database | Pros                                                                      | Cons                                                                                            |
| ---------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Relational       | Data is stored in specific independent tables                             | Requires alot of RAM and more powerful processor; increase the load on the server's RAM and CPU |
| Non-Relational   | Speeds up and simplifies request processing; almost indefinitely scalable | Requires duplication of some data                                                               |

# Popular Databases
* RavenDB 
* Cassandra 
* MongoDB (Non-Relational)
	* Popular with Node.js (see [[MongoDB - Installing MongoDB]])
	* ODM: Mongoose (see [[MongoDB - Connecting MongoDB to JS via Mongoose]])
* Redis
* BigTable
* PostgreSql (Relational)
	* Works on Windows, Linux, macOS
	* No database size limitations
	* Compatible with many programming languages
	* Ability to create unique data types
* Firebase
* Snowflake

# NoSQL (Not Only SQL) Databases
- Why NoSQL (Not Only SQL)?
	- NoSQL combines all the advantages of non-relational databases with some advantages of relational databases
	- NoSQL databases store data in structures similar to JSON (easily processed with JavaScript)
		- Less trouble with data conversion
