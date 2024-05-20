What is a JSON Web Token (JWT)?
* See [[JWTs (JSON Web Tokens)]]

# Using the jsonwebtoken Module
* The module must be imported into the controller file
* The `jwt.sign()` method can be used to create a token (see [[Node.js - Methods]])
* The `jwt.verify()` method can be used to verify a token (see [[Node.js - Methods]])
	* verifying a token --> ensuring it was the same one sent to the user previously