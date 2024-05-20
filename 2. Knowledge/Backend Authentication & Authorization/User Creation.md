### Registration
* Registration --> the creation of a new user in the database

### Adding a user to the database
1) Create a user model in the database (see [[MongoDB - Schemas & Models]])
	* Add the unique property to the schema entries that should be unique (see [[MongoDB - Methods & Properties]])
		* If the `unique: true` field is added, but the collection already has duplicates, the constraint will not work
			* How to resolve the issue --> delete the offending data
2) Save users to the database
	* The login info can be retrieved from the request (using a controller function) (see [[MongoDB - Controllers]])
		* Use the catch() statement to handle errors (such as: user info not saving due to a duplicate email) (see [[JS - Error Handling]])
3) Hash the password --> adds security layer (makes password encrypted)
	* Use a module called `bcryptjs` (see [[Node.js - Module - bcryptjs]], [[Node.js - Methods]])
### Example: user creation
```js
// models/user.js 
const mongoose = require('mongoose'); 
const userSchema = new mongoose.Schema({ 
	email: { 
		type: String, 
		required: true, 
		unique: true // ensures that the email IS UNIQUE
	}, 
	password: { 
		type: String, 
		required: true, 
		minlength: 8 
	} 
}); 

module.exports = mongoose.model('user', userSchema);
```

```js
// controllers/users.js 
const User = require('../models/user'); 
const bcrypt = require('bcryptjs'); // importing bcrypt

// controller function to retrieve the email and user from the req
exports.createUser = (req, res) => { 
	// hashing the password 
	bcrypt.hash(req.body.password, 10) 
		.then(hash => User.create({ // create user after hashing password
			email: req.body.email, 
			password: hash, // adding the hash to the database 
	})) 
	.then((user) => res.send(user)) 
	.catch((err) => res.status(400).send(err)); 
};
```

# Salts and Hash Tables
* Hashing without salt is dangerous 
	* The hacker can match up the hash to a database and find the user's passwords
![Three columns representing columns in two databases. An arrow is pointing from a hash in a column named “hashes” in a database named“Your DB” to an identical hash in a hacker’s database. Another arrow points from the hacker’s recorded hash to a password in the “Passwords” column of the hacker’s database.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_15.02.02_1652114573.png)

* Salt is a random string added to the password before hashing is performed (see [[Node.js - Module - bcryptjs]]); salting is added using the `bcrypt.hash()` method (see [[Node.js - Methods]])
	* Salting will add a random symbols to the hash and completely change the final hash
		* Even identical passwords will get a different hash 
![A screenshot of two columns in “Your DB” containing hashes and salt columns. Beside it are two pairs of columns in “Hacker’s DB.” The first contains hashes and “Password 1 + salt”, while the second one contains hashes and “Password 2 + salt”.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_293_1602277070.png)