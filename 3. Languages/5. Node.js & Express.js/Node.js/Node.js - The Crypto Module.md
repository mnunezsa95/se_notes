See: 
* [[Node - Introduction to Node.js]]
* [[Node.js - Methods]]
* [[Node.js - Crypto Methods]]
* [[JWTs (JSON Web Tokens)]]
Resources:
* Documentation: [Node.js - Crypto](https://nodejs.org/api/crypto.html)


---

# Crypto Module
* Crypto module is useful for creating strong cryptographically and pseudorandom Secret Keys and Hashing data

## Secret Keys
* When tokens are generated for users, they are accompanied by secret keys.
* Characteristics of Secret Keys
	* **Unpredictable Nature:** To enhance security, secret keys should avoid forming coherent words.
	* **Randomness Importance:** Lengthy strings of randomly generated characters serve as an effective means to safeguard the confidentiality of secret keys.
* Key Features
	* **Strong Cryptography:** Data generated via an algorithm makes analysis difficult, ensuring heightened security.
	* **Pseudorandom:** Despite appearing random, the characters in these keys are actually generated through a predetermined mathematical process.
* Specifications
	* It's recommended that secret keys:
		* Consist of binary digits (0s and 1s).
		* Be either 128 or 256 characters in length.
* Key Storage
	- It is advisable NOT to store keys within the codebase.
	- Ensuring Secure Key Storage:
	    1. Establish an `.env` file at the root directory.
	    2. Safely store keys within this designated file.
```bash
NODE_ENV=production JWT_SECRET=eb28135ebcfc17578f96d4d65b6c7871f2c803be4180c165061d5c2db621c51b
```


# Creating Secret Keys
1. Utilize the `crypto` module.
2. Specify the desired number of bytes.
3. Convert the bytes into a string format using the `toString()` method.
```JavaScript
// Import the crypto module 
const crypto = require('crypto');  

// Generate a random sequence of 16 bytes (128 bits) & convert it to a string 
const randomString = crypto.randomBytes(16).toString('hex');  
console.log(randomString); // 5cdd183194489560b0e6bfaf8a81541e`
```

- This can also be accomplished directly in the console.
```bash
# Generating a 256-bit key directly in the console 
node -e console.log(require('crypto').randomBytes(32).toString('hex'));
```

# Creating a Hash
1. Utilize the `crypto` module.
2. Specify the algorithm to encrypt the data
3. Encrypt using algorithm
```JavaScript
// Import the crypto module 
const crypto = require('crypto'); 

const string = 'Hello World!'
const hash = crypto.createHash('sha256')
const hashData = hash.update(string)
const result = hash.digest('hex')

console.log(result) 
// '7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069'
```