# Mongoose Methods

#### mongoose.connect()
* Connects the application to the mongoDB server
* Arguments
	1) Server address (made up of two parts)
		* the default mongoDB address
		* the name of the database
	2)  OPTIONS object (Version MongoDB 5 or lower)
		*  OPTIONS needed for Versions older than 5
			* useNewUrlParser: true
			* useCreateIndex: true
			* useFindAndModify: false
* Additional
	* Sometimes, 'localhost' will be used instead of 127.0.0.1
		* Preferable to use 127.0.0.1 in the mongoose connection streams
* Example
```js
// connecting MongoDB on version 5 or higher

// import mongoose to the app.js
const mongoose = require('mongoose'); 

// connect to the MongoDB server 
mongoose.connect('mongodb://127.0.0.1:27017/mydb');
```

```js
// connecting MongoDB on version 5 or lower

const mongoose = require('mongoose'); 

// connect to the MongoDB server 
mongoose.connect('mongodb://127.0.0.1:27017/mydb', { 
  useNewUrlParser: true, 
  useCreateIndex: true, 
  useFindAndModify: false 
});
```

#### mongoose.disconnect()
* Used to disconnect to a database
* Arguments
	* None
* Example
```js
mongoose.disconnect();
```

#### mongoose.dropDatabase();
* Completely resets a database
* Example
```js
mongoose.connection.db.dropDatabase(); 
```

#### mongoose.Schema()
* Creates a new instance of the schema to validate data
* Arguments
	1) an object (used to house the 'set of rules' for the schema)
* Additional
	* **enum** option (enumerations) --> data type that restrict a variable to take only one value from a predefined set
		* enum adds a validator to the field which checks whether it's strictly equal ( === ) to one of the unique values of the array
	* **validate** property --> an object that includes the following properties
		* validator --> a validation function (returns a boolean value)
		* message --> an error message (rendered if validator returns 'false')
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

#### mongoose.model() 
* Creates a model in mongoose.
* Arguments
	1) the name of the model (MUST be singular noun; mongoose adds 's' automatically)
	2) the schema which will describe future document
* Example
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
# CRUD Methods (see [[MongoDB - CRUD]])
Resource
* [Model CRUD Methods](https://mongoosejs.com/docs/api/model.html)

#### modelName.create() 
* Creates documents on a database
	* Works like a promise : `then()` and `catch()` can be used 
* Arguments
	1) an object (with data as an input)
```js
// routes/users.js 

/* code for creating routers, etc. */ 
// import the model 
const User = require('../models/user'); 

router.post('/', (req, res) => { 
	const { name, about } = req.body; // get the name & description of the user 
	User.create({ name, about }); // create a document based on the input data
		// returns the recorded data
		.then(user => res.send({data: user}))
		// prompt an error if data is not recorded
		.catch(err => res.status(500.send({message: 'Error'}))); 
});
```

#### modelName.findById() 
* Uses an `identifier` to find a specific document
	* `identifier` = the __id property assigned to document by mongoDB
* Arguments
	1) identifier (in form of a string)
		* `req.params.id` can be used
* Example
```js
// routes/users.js 
/* code for creating routers, etc. */ 

const User = require('../models/user'); 
router.get('/:id', (req, res) => { 
	User.findById(req.params.id) // looking for specific document
		.then(user => res.send({ data: user })) 
		.catch(err => res.status(500).send({ message: 'Error' })); 
});
```

#### modelName.findOne() 
* Searches and returns the first document that matches the request parameters
* Arguments
	1) a query (in form of an object with specific inputs)
* Example
```js
// find the first match with a field that equals "Elise Taylor" 
User.findOne({ name: 'Elise Taylor' });
```

#### modelName.find() 
* Searches and returns the ALL document that matches the request parameters
* Arguments
	1) a query (in form of an object with specific inputs)
* Example:
```js
// find all 30-year-old users 
User.find({ age: 30 }); 

// find all users 
User.find({});
```

#### modelName.findByIdAndUpdate() 
* Searches for a specific document using an identifier and updates it
* Arguments
	1) identifier (in form of a string)
		* `req.params.id` can be used
	2) an object (with the properties that need to be updated)
	3) OPTIONS object --> ensures that the `.then()` handler receives the updated info before sending it back to the user (use the options below; see [[MongoDB - CRUD]] for more info)
		* `new: true`
		* `runValidators: true`
		* `upsert: true
* Example
```js
// routes/users.js
const User = require('../models/user'); 
router.patch('/:id', (req, res) => { 
	// updating the name of the user found by _id 
	User.findByIdAndUpdate(req.params.id, { name: 'Henry George' }) 
		.then(user => res.send({ data: user })) 
		.catch(err => res.status(500).send({ message: 'Error' })); 
});
```

```js
// using the options object
User.findByIdAndUpdate( 
  req.params.id, 
  { name: 'Henry George' }, // pass the options object: 
  { 
    new: true, // the then handler receives the updated entry as input 
    runValidators: true, // the data will be validated before the update 
    upsert: true // if the user entry wasn't found, it will be created 
  } 
) 
  .then(user => res.send({ data: user })) 
  .catch(user => res.send({ 'Data validation failed or another error occured.' 
}))
```
#### modelName.findOneAndUpdate() 
* Searches and updates the first document that matches the request parameters
* Arguments
	1) an object (to be updated)
	2) an object (with the info that should be updated)
	3) OPTIONS object --> ensures that the `.then()` handler receives the updated info before sending it back to the user (use the options below; see [[MongoDB - CRUD]] for more info)
		* `new: true`
		* `runValidators: true`
		* `upsert: true
* Example
```js
// find the first match with the name field that equals to "Sam Taylor" and replace is with "Henry George" 
User.findOneAndUpdate({ name: 'Sam Taylor' }, { name: 'Henry George' }));
```

#### modelName.updateMany() 
* Finds and updates all documents that match the request
* Arguments
	1) an object (to be updated)
	2) an object (with the info that should be updated)
	3) OPTIONS object --> ensures that the `.then()` handler receives the updated info before sending it back to the user (use the options below; see [[MongoDB - CRUD]] for more info)
		* `new: true`
		* `runValidators: true`
		* `upsert: true`
* Example
```js
// find all matches with the name field that equals to "Sam Taylor" and replace it with "Henry George" 
User.updateMany({ name: 'Sam Taylor' }, { name: 'Henry George' });
```

#### modelName.findByIdAndRemove() 
* Finds and deletes a specific document
* Arguments
	1) an `identifier` (in string form)
		* `req.params.id` can be used
* Example
```js
const User = require('../models/user'); 

router.delete('/:id', (req, res) => { 
  User.findByIdAndRemove(req.params.id) 
    .then(user => res.send({ data: user })) 
    .catch(err => res.status(500).send({ message: 'Error' })); 
});
```

#### modelName.findOneAndRemove() 
* Finds and deletes the first document that matches the request parameters
* Arguments
	1) an object (with the query for what should be deleted)
* Example
```js
// delete a user with a specific name 
User.findOneAndRemove({ name: 'Sam Taylor' });
```

#### modelName.deleteMany() 
* Finds and deletes all documents that match the request parameters
* Arguments
	1) an object (with the query for what should be deleted)
* Example
```js
// delete all 30-year-old users 
User.deleteMany({ age: 30 });
```

#### modelName.deleteOne() 
* Used to delete a document from the database; the first document matching the query passed as an argument will be deleted
* Arguments
	1) an object (with the query for what should be deleted)
* Example
```js
// find a document whose username field is 'Will':
User.deleteOne({ email: fixtures.user.email });
```


---

# Schema Properties 
* `type` --> sets the type of data
	* `String` 
	* `Number`
	* `Boolean`
	* `Date`
	* `Array`
	* `mongoose.Schema.Types.ObjectId` --> used when linking Schemas together (see [[MongoDB - Building Relationships]])
* `minlength`
* `maxlength`
* `required`
* `enum` --> data type that restrict a variable to take only one value from a predefined set
* `ref` --> used when linking Schemas together; to set the name of the model being linked (see [[MongoDB - Building Relationships]])
* `validate` --> used to validate the data; has a `validator` function and `message` sub-properties
* `unqiue` --> ensures that the database ONLY records record with unique info
* `statics` --> allows the attachment of a custom method to a schema (see [[MongoDB - Custom Methods for Mongoose Models]])

# populate() method
Resources
* [Official MongoDB Documentation: Populate Method in MongoDB](https://mongoosejs.com/docs/populate.html)

* What is the `populate()` method?
	* The `populate()` method is used to reference other documents and get the reference (see [[MongoDB - Building Relationships]])
* Arguments
	* The property name (being referenced)
		* To reference multiple properties use an Array
```js
// controllers/ads.js 
const Ad = require('../models/ad'); 

module.exports.getAds = (req, res) => { 
	Ad.find({}) 
		.populate('creator') // use the populate() method
		.then(ad => res.send({ data: ad })); 
};
```
