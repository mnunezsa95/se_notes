* JavaScript cannot directly work with documents
	* JS needs an Object Document Mapper (ODM) to work with documents (like it does with objects) (see [[Relational & Non-Relational Databases]]) 
		* Different databases have different ODMs 

--- 
# MongoDB's ODM (Mongoose)
* MongoDBs ODM (mapper) is called 'Mongoose'
	* Acts a bridge between the database documents and JavaScript Objects

# Installing and Connecting Mongoose to JavaScript
1) Install Mongoose using npm command
```bash
# installs mongoose
npm i mongoose
```

2) Import mongoose
```js
// import 'mongoose' and set equal to the mongoose variable
const mongoose = require('mongoose');
```

3) Connect to MongoDB server using the mongoose.connect() method (see [[MongoDB - Methods & Properties]])
	* The mongoose.connect() method takes in the server address (made up of two parts) as argument
		1) the default mongoDB address ('mongodb://127.0.0.1:27017')
		2) the database name 

```js
// connecting MongoDB on version 5 or higher
// app.js — input file 
const express = require('express'); 
const mongoose = require('mongoose'); 
const app = express(); 

// connect to the MongoDB server 
mongoose.connect('mongodb://127.0.0.1:27017/mydb'); 

// connect the middleware, routes, etc... 
app.listen(3000);
```

```js
// connecting MongoDB on version 5 or lower
// app.js — input file 
const express = require('express'); 
const mongoose = require('mongoose'); 
const app = express(); 

// connect to the MongoDB server 
mongoose.connect('mongodb://127.0.0.1:27017/mydb', { 
  useNewUrlParser: true, 
  useCreateIndex: true, 
  useFindAndModify: false 
});

// connect the middleware, routes, etc... 
app.listen(3000);
```

4) Run the MongoDB Server 
	* MUST be started before running Node.js
```bash
# running the mongoDB server
mongod
```

