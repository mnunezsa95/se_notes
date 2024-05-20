* Before authentication can happen, the user must be created (see [[User Creation]])

### Authentication Logic
* The email and password need to be retrieved from the request body.
	* If email and password match with one in the database --> user is logged in
	* If email and password do not match one in database --> user is not logged in
		* Users receive a message about the mistake

### How to search for credential matches
* There are a few ways to do this:
	1) Search the database for a user using the submitted email
		* If user is found --> hash the submitted password and compare it to password in database
	2) Hash the submitted password and check if there is a user in the database with the submitted password

### Logic: Searching the database for a user using the email
1) Retrieve the email and password from request
2) Look for the email in the database 
3) If not match --> reject the promise and catch the error in the catch() block
4) If match --> use the `bcrypt.compare()` method to compare the two passwords (one submitted and one in database) (see [[Node.js - Methods]])

```js
// controllers/users.js

module.exports.login = (req, res) => { // login controller function
	const { email, password } = req.body; // retreiving email & password from req
	
	User.findOne({ email }) // searching database for email
		.then((user) => { // then statement to do something with email
			if (!user) { // if user does NOT exist in database, reject Promise
				return Promise.reject(new Error('Incorrect password or email')); 
			} 
			// comparing the submitted password and hash from the database 
			return bcrypt.compare(password, user.password); 
		}) 
		.then((matched) => { 
			if (!matched) { // the hashes didn't match, rejecting the promise 
				return Promise.reject(new Error('Incorrect password or email')); 
			} // successful authentication 
			res.send({ message: 'Everything good!' });
		})
		.catch((err) => { // catch errors where user was not found
			res.status(401).send({ message: err.message }); 
		}); 
};
```
