# What does the dotenv module do?
* Loads environment variables from a `.env` file into `process.env`.  (see [[Node.js - The .env file]])
* Storing configuration in the environment separate from code is based on The Twelve-Factor App methodology.

#### Installing the dotenv module
* Install the `dotenv` module using the following line and import it into `app.js`.
```bash
* Installing the dotenv module
npm install dotenv
```

#### Importing the dotenv module
* Import the `dotenv` module
* Use the `config()` method to configure it (see [[Node.js - Methods]])
```js
// importing and configuring the module
require('dotenv').config();
```


### Loading the .env folder in Node.js
1) The `.env` file can be loaded into Node using the `dotenv` module followed by the `.config()` method (see [[Node.js - Methods]], [[Node.js - The .env file]], [[Node.js - Module - dotenv]])
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