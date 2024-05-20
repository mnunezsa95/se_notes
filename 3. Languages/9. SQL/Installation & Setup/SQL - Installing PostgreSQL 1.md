See:
* [[SQL - Introduction to SQL]]
* [[Relational & Non-Relational Databases]]
* [[Database Management Systems (DBMS)]]

---
# Using Relational Databases in Express.js Apps
- To use relational databases in an application, choose an appropriate **database management system (DBMS)**** and use it’s node drier to connect it to the app
	- **PostgreSQL** (or Postgres) is a free and open-source relational database management system

## Installing PostgreSQL (Node.js Project)
1) Install the NPM module called `pg-promise` using the following command:
	* `pg-promise` is a PostgreSQL client for Node.js that is based on a powerful query-formatting engine and supports methods that return a promise
```bash
# Installs pg-promise (a PostgreSQL client for Node.js)
npm install pg-promise
```

2) Connect PostgreSQL to Express.js app
```js
// Import the pg-promise package into Node.js
var pgp = require('pg-promise')(/* options */) 

// Connect express to PostgreSQL
var db = pgp('postgres://username:password@host:port/database') 

// Connect to your local database 
db.one('SELECT $1 AS value', 123) // Create a query to pull desired data
  .then(function (data) { 
    console.log('DATA:', data.value) 
  }) 
  .catch(function (error) { 
    console.log('ERROR:', error) 
})
```
