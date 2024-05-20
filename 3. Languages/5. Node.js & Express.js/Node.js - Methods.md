See: [[Node - Introduction to Node.js?]]

--- 
#### require()
* What is the **require()** method?
	* Built in Node.js method 
	* Used to include external modules that exist in separate files
	* How it works
		* Reads a file --> executes it --> returns the exported object
* Syntax
```js
const moduleName = require('moduleName');
```

#### createServer() 
* What is the **createServer()** method?
	* Creates a server
	* Instructs the **libuv library** to connect to the NIC to receive incoming requests
```js
const serverName = http.createServer();
```
#### listen() 
* What is the listen() method?
	* The listen() method is used to specify the port from which Node.js should receive messages
* Syntax
```js
server.listen(portToBeUsed)
```

--- 
# The fs Module Methods
--[Node.js Documentation - the fs Module](https://nodejs.org/api/fs.html)--
#### fs.readFile() 
* What is the fs.readFile() method?
	* An asynchronous function used to read a file
* Arguments
	1) the filename (to be read) (see [[Node.js - Module - path]])
	2) an **options** object
		* An object w/ a set of named parameters 
	3) callback function --> Indicates what to do with the data
		* Parameters
			1) an **err** parameter --> handles potential errors (can have two values)
				* If an err occurs -->  value of 'err' = an object (containing error info)
				* If no err occurs --> value of 'err' = null 
			2) a **data** parameter --> represents contents of a file (in the form of binary code (also called Buffer (see [[Node.js - The Request Object]]))  --> must be converted to a string before use)
				* 2 ways to convert to string
					* Using **toString()** method
						* Takes the encoding format as value
					* Passing the encoding format inside the encoding property of the options object
```js
// Using the readFile() method using the toString() method to convert to string

const fs = require('fs'); // importing the fs module

fs.readFile('data.json', (err, data) => { 
	if (err) { 
		console.log(err); 
		return; 
	} 
	console.log('data: ', data.toString('utf8')); 
});
```

```js
// Using the readFile() method using the Options object

const fs = require('fs'); // importing the fs module

// using the options object as the second parameter to set the encoding format
fs.readFile('data.json', { encoding: 'utf8' }, (err, data) => { 
	if (err) { 
		console.log(err); 
		return; 
	} 
	console.log('data: ', data); 
	// data comes as a string, don't need to call toString() method here 
});
```

#### fs.readdir()
* What is the fs.readdir() method?
	* An asynchronous function used to read a directory
* Arguments
	1) path to the directory (see [[Node.js - Module - path]])
	2) callback function --> indicates what to do with the data returned
		* Parameters
			1) error parameter --> handles potential errors 
			2) an array of filenames
```js
const fs = require('fs'); // importing fs module

fs.readdir('.', (err, files) => { // first arg = path; second arg = callback
	if (err) {    // handles the error
		console.log(err); 
		return; 
	} 
	console.log('data: ', files); // files is an array 
});
```

#### fs.mkdir()
* What is the fs.mkdir() method?
	* An asynchronous function used to create a folder
* Arguments
	1) the path & folder name (see [[Node.js - Module - path]])
	2) callback function
		* Parameters
			1) the error object --> for error processing
```js

const fs = require('fs'); // import the fs module

fs.mkdir('incomingData/data', (err) => { // indicate pathway & folder name 
	if (err) console.log(err); // handle error
});
```

#### fs.writeFile()
* What is the fs.writeFile() method?
	* An asynchronous function used to write in a file
* Arguments
	1) the filename (where data will be written)
	2) the data (in string form)
	3) callback function --> for error processing
		* Parameters
			1) the error object
```js
const fs = require('fs'); // import the fs module

fs.writeFile('data.json', JSON.stringify([1, 2, 3]), (err) => {	
	if (err) console.log(err);
});

```

#### fs.unlink()
* What is the fs.unlink() method?
	* An asynchronous function used to delete a file
* Arguments
	1) the filename 
	2) callback function --> for error processing
		* Parameters
			1) the error object
```js
const fs require('fs') // import the fs module

fs.unlink('data.json', (err) => {
	if (err) { 
		console.log(err);
		return;
	}
	console.log('The file has been deleted!')
});
```

#### fs.createReadStream()
* What is the fs.createReadStream?
	* Creates a readable stream
* Arguments
	1) the file path
	2) an options object --> (possible options below)
		* encoding
* Example
```js
const fs = require('fs');

// create a readable stream from the in.txt file
const reader = fs.createReadStream('./in.txt', { encoding: 'utf8'});
```

#### fs.createWriteStream() 
* What is the fs.createWriteStream?
	* Creates a writable stream
* Writable Stream methods
	* .end() --> ends the writing on a writable stream
* Arguments
	1) the file path
	2) an options object --> (possible options below)
		* encoding
* Example
```js
const fs = require('fs');

// create a writable stream to the out.txt file
const writer = fs.createWriteStream('./out.txt', { encoding: 'utf8'});
```


---
# The path Module Methods
--[Node.js Documentation - the path Module](https://nodejs.org/api/path.html)--
#### path.join()
* What is the path.join() Method?
	* Joins the specified path segments together and returns what's referred to as a normalized path
* path.join() accounts for the operating system being used
* Arguments
	* The sections to be joined
* Example
```js
const fs = require('fs')
const file = require('path')

module.exports.readFile = () => {
	const filepath = path.join(__dirname, 'file.txt'); // joining path segments
	const file = fs.readFile(filepath, {encoding: 'utf8'}, (err, data) => {
		console.log(data)
	})
}
```

#### path.normalize() 
* What is the path.normalize() Method?
	* Normalizes the specified path by resolving the ' . . ' and ' . ' segments
* Arguments
	1) the file path
* Example
```js
path.normalize('/foo/bar//baz/asdf/quux/..'); // /foo/bar/baz/asdf
```

#### path.dirname()
* What is the path.dirname() Method?
	* Returns the directory name of the given path
* Arguments
* Example
```js
path.dirname(require.main.filename); // /usr/local/my-project
```

#### path.extname()
* What is the path.extname() Method?
	* Returns the extension of a file path
* Arguments
	1) a filename or file path
```js
path.extname('app.js'); // .js 
```

---
# The bcryptjs Module Methods

#### bcrypt.hash()
* Description
	* Creates a hash password (see [[Node.js - Module - bcryptjs]])
* Arguments
	1) the password --> the password to be hashed
	2) a number --> length of the salt (a random string added to the password before hashing is performed)
* Example
```js
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

#### bcrypt.compare() 
* Description
	* Compares two passwords (the one in the database and the one sent by the user); hashes the password sent by the user in the request
	* Returns true if the passwords match and false if they do not
* Arguments
	1) the password --> the password in the database
	2) the hashPassword --> the password the user submitted
* Example
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

--- 
# The jsonwebtoken Module Methods
#### jwt.sign()
* Description
	* Creates a JSON web token
* Arguments
	1) the payload --> an encrypted user object that can carry as much information as desired. 
	2) the secrectKey --> 
	3) options (optional) --> allows for specific settings to be set
		* espiresIn --> the length of time (in number form) that specifies how long a token will be valid in seconds; 
			* if no value is defined --> token will never expire
			* Can be entered in str form to change the specified  units can be milliseconds (ms), minutes (m), hours (h), days (d)
* Example
```js
const jwt = require('jsonwebtoken'); 

module.exports.login = (req, res) => { 
	const { email, password } = req.body; 
	return User.findUserByCredentials(email, password) 
		.then((user) => { 
			// create a token with 3 arguments
			const token = jwt.sign(
				{ _id: user._id }, 
				'some-secret-key', 
				{ expiresIn: 3600 }
			); 
			// return the token 
			res.send({ token }); 
		}) 
		.catch((err) => { res .status(401).send({ message: err.message }); 
	}); 
}
```

#### jwt.verify() 
* Description
	* Used to verify tokens (check to ensure it was the same one sent to user previously)
	* This method returns the decoded payload of this token
	* Should be handled in a try...catch statement
* Arguments
	1) the token --> the token that was replaced 
	2) the secret key --> the secret key that was sent to the user
* Example
```js
// middleware/auth.js 
const jwt = require("jsonwebtoken");

module.exports = (req, res, next) => { 
	// getting authorization from the header 
	const { authorization } = req.headers; 
	// let's check the header exists and starts with 'Bearer ' 
	if (!authorization || !authorization.startsWith('Bearer ')) { 
		return res.status(401).send({ message: 'Authorization required' }); 
	} 
	// getting the token 
	const token = authorization.replace('Bearer ', '');
	// verifying the token 
	let payload; 
	try { 
		// trying to verify the token 
		payload = jwt.verify(token, 'some-secret-key'); 
	} catch (err) { // we return an error if something goes wrong return 
		res.status(401).send({ message: 'Authorization required' }); 
	}
};
```

---
# The crypto Module Methods
Resources:
* [[Node.js - Module - crypto]]
#### crypto.randomBytes()
* Description
	* Creates a cryptographic and pseudorandom secret key (see [[Creating and Storing Secret Keys]])
* Arguments
	1) numberOfKeyBytes --> the number of key bytes (1 byte = 8 bits); usually 16 or 32 are popular numbers
* Example
```js
const crypto = require('crypto'); // importing the crypto module

// generating a random sequence of 16 bytes (128 bits) 
const randomString = crypto.randomBytes(16).toString('hex'); // converting it into a string

console.log(randomString); // 5cdd183194489560b0e6bfaf8a81541e
```

--- 
# The dotenv Module Methods
* Resources
	* [The .dotenv modules: Official Documentation](https://www.npmjs.com/package/dotenv)
	* [[Node.js - Module - dotenv]]
#### dotenv.config()
* Description
	* Used to load and configure the `.env` folder
* Arguments
	* none
* Example
```js
// in app.js
require('dotenv').config(); // load and configure the .env folder

console.log(process.env.NODE_ENV); // production 
```

---
# The escape-html Module Methods

#### escape() 
* Description
	* Replaces special characters in a string with the appropriate character entities 
* Arguments
	1) str --> the string that contains the special characters to be escaped
* Example
```js
const escape = require('escape-html'); 

escape('<script>alert("hacked")</script>'); 
// '&lt;script&gt;alert(&quot;hacked&quot;)&lt;/script&gt;
```

--- 
