Resources:
* [Official Mongoose Documentation: Schemas](https://mongoosejs.com/docs/schematypes.html)
* [Schema Types in Mongoose](https://mongoosejs.com/docs/schematypes.html)

--- 
What is a Schema?
* A **schema** is a set of rules for the data that will  impose restrictions on the data that can be recorded in the database.
	* Example: Set the number of fields a record has, the length of each field value, and which characters are allowed in it 
* Schemas help validate data
* Non-relational databases do not have schemas (but can be implemented if necessary) (see [[Relational & Non-Relational Databases]])

---
# Creating a Schema
* The **mongoose.schema()** method creates a new instance of the schema to validate data before it is inserted into the database (see [[MongoDB - Methods & Properties]])
* When creating schemas, 5 basic data types are used
	* String
	* Number
	* Date
	* Boolean
	* Array
* Arrays in a Schema --> used to store multiple data items of the same type
* Example
```js
const mongoose = require('mongoose'); 
const userSchema = new mongoose.Schema({
  name: {  // every user has a name field, the requirements are described below: 
    type: String,       // the name is a string 
    required: true,    // every user has a name, so it's a required field 
    minlength: 2,     // the minimum length of the name is 2 characters 
    maxlength: 30,   // the maximum length is 30 characters 
  },
  hobbies: [{ // describe the schema for a single element
    type: String,
    minlength: 2,
    maxlenght: 30,
  }],
  pronouns: { 
    type: String,     // the pronouns are a string 
    enum: ['they/them', 'she/her', 'he/him', 'other pronouns'] // every user can choose their pronouns
  },
	age: { // every user has an age field 
		type: Number, // the age type is a number 
		required: true, // the user has to specify their age 
		validate: { // describe the validate feature 
			validator(v) { // v is the age value 
				return v >= 18; // if the age is < 18, it will return false 
			}, 
			message: 'Sorry. You have to be at least 18 years old',  
		} // message dsiplayed when validator returns false
	},
});
```

### Creating Subdocuments
* To create another schema, the mongoose.Schema() method will need to be called a second time
	* The 1st call --> needed to create a schema that will describe the property's structure
	* The 2nd call --> will pass the schema to the property 
* Example
```js
// models/user.js 

const mongoose = require('mongoose'); // create a schema for the "Pet" document 
const petSchema = new mongoose.Schema({ 
	name: { 
		type: String, 
		required: true, 
		minlength: 2, 
		maxlength: 30, 
	},
	age: Number 
});

// once the schema is ready, pass it to the property which should correspond to this template: 
const userSchema = new mongoose.Schema({ 
	... 
	pet: petSchema // describe the pet property with this schema 
});
```

### Creating a Model Based on Schema
* To create a document itself, a model needs to be built based on the schema
* A **model** is a wrapper around the schema. 
	* Allows for the document to be read, added, deleted, and updated
* The **mongoose.model()** method is used to create models (see [[MongoDB - Methods & Properties]])
```js
const mongoose = require('mongoose'); 

// Describe the schema: 
const userSchema = new mongoose.Schema({ 
  name: { 
    type: String, 
    required: true, 
    minlength: 2, 
    maxlength: 30, 
  }, 
  about: String, 
  }); 
  
// create the model and export it 
module.exports = mongoose.model('user', userSchema);
```

---
# Summary: Model Creation
1) Set the API resources
2) Describe the resource schemas
3) Create models based on the schemas
