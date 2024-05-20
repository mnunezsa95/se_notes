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