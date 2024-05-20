Resources
* [Official Mongoose Documentation: Custom Model Methods](https://mongoosejs.com/docs/guide.html#statics)

### Creating a Custom Model Method
* Code for checking emails and passwords can be made part of a Schema itself
* Custom methods can be added to a Schema using the `statics` method (see [[MongoDB - Methods & Properties]])
	* The name of the desired custom method is added after this property 
	* The method should NOT be an arrow function (the 'this' keyword needs to be accessible)
* Custom Model Methods can be exported and used in controller functions 

```js
// models/user.js 

const mongoose = require('mongoose'); 
const userSchema = new mongoose.Schema({ 
	email: { 
		type: String, 
		required: true, 
		unique: true 
	}, 
	password: { 
		type: String, 
		required: true, 
		minlength: 8 
	} 
});

// adding the findUserByCredentials methods to the User schema
userSchema.statics.findUserByCredentials = function findUserByCredentials(email, password) {
	// trying to find the user by email 
	return this.findOne({ email }) // this — the User model 
		.then((user) => { // not found - rejecting the promise 
			if (!user) { 
				return Promise.reject(new Error('Incorrect email or password')); 
			}
		// found - comparing hashes 
			return bcrypt.compare(password, user.password)
				.then((matched) => { 
					if (!matched) { // rejecting the promise 
						return Promise.reject(new Error('Incorrect email or                                   password'));
					}
					return user; // return user
				});
		});
};

// exporting schema
module.exports = mongoose.model('user', userSchema); 
```


```js
// controllers/users.js 
module.exports.login = (req, res) => { 
	const { email, password } = req.body; 
	return User.findUserByCredentials(email, password) 
		.then((user) => { 
			// authentication successful! user is in the user variable 
		}) 
		.catch((err) => { // authentication error 
			res.status(401).send({ message: err.message }); 
		}); 
};
```