Resources 
* [JWT: Official Documentation](https://jwt.io/)

# Tokens: What are they?
* Token --> a set of characters, generated and structures according to a set of rules 
	* Rules are defined by a token creation standard
* Token implementation allows for user authentication & authorization (see [[Identification, Authentication & Authorization]])
	* Allows users to stay logged in

# Other Authorization & Authentication Methods
* JWTs are not the ONLY way to authorize and authenticate (see [[Other Authentication & Authorization Methods]])

# Authentication Process: Algorithm
1) User enters account details (username & password)
2) Server generates a token (unique set of symbols)
3) Server sends token to user
4) Token is saved on browser
5) During next login, browser sends token to server instead of prompting user to enter account details again
6) Server checks token to determine if it matches the one previously sent to user (Authentication)
	* If it matches --> user if authorized
	* If it DOESN'T match --> error message displayed to user
7) When user logs out, browser deletes the token 
	* User will need to re-enter their info

# Structure of JWTs
* Based on JSON data type 
* JWTs consist of 3 parts (separated by dots)
	1) header --> contains metadata about the token
	2) payload --> contains data the token will carry 
	3) signature --> ensure info in the token cannot be changed
![A depiction of a JWT token, broken down to show the header, payload, and signature.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Artboard_1_1601294494.png)

### JWTs: Header
* Consists of 2 fields
	1) The creation algorithm (usually one of the following)
		* 'HMAC'
		* 'SHA256' 
		* 'RSA'
	2) The type of token
		* 'JWT'
* The JSON object is encoded using the **Base64URL** algorithm
* Example
```json
{ 
	"alg": "HS256", 
	"typ": "JWT" 
}
```

### JWTs: Payload
* Contains the actual info that is encoded
* Example
```json
{ 
	"name": "Elise Bouer", 
	"_id": "39dow8ak8402jf23u4do057s" 
}
```

### JWTs: Signature
* Ensures that the header and payload are not changes after creation
* A special algorithm does two things:
	1) generates the signature from the contents of the header and the payload
	2) uses a secret key (only known by the server)

# Creating JWTs
* The `jsonwebtoken` package can be used to create JWTs (must be imported)
* The `jwt.sign()` method can be used to create an actual token (see [[Node.js - Methods]])
	* Can be used to specify what info should be sent in the token, the secret key and when the token will expire
		* Secret keys can be created and stored (see [[Creating and Storing Secret Keys]])
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