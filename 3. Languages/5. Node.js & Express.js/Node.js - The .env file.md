See: [[Node - Introduction to Node.js?]]

--- 

### What is the .env file
* A folder that stores environmental variables (see [[Node.js - Creating a Server]])
#### Installing dotenv
* Use the following code
```bash
npm install dotenv
```
### Loading the .env file in Node.js
1) The `.env` file can be loaded into Node using the `dotenv` module followed by the `.config()` method (see [[Node.js - Module - dotenv]], [[Node.js - Methods]], [[Creating and Storing Secret Keys]])
2) Add the `.env` file to the `.gitignore` file
3) Access the variables when generating a token
```js
require('dotenv').config();

const { NODE_ENV, JWT_SECRET } = process.env;

const token = jwt.sign(
  { _id: user._id },
  NODE_ENV === 'production' ? JWT_SECRET : 'dev-secret'
); 
```

### Who should have access to the .env file?
* Only a small amount of people should have access to this folder
	* Keep this file out of your project repository.