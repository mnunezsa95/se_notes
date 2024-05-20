Resources:
* NPM Documentation: [winston](https://www.npmjs.com/package/winston)
* NPM Documentation: [express-winston](https://www.npmjs.com/package/express-winston)

#### What is Winston?
* A library that allows for flexible logging (see [[JS - Logging]])

#### Installing Winston
* Install winston 
```bash
npm install winston
```

* Install express-winston
	* Convenient for working with express.js
```bash
npm install express-winston
```

#### Importing winston
* Import **winston** and **express-winston** into a for use 
```js
// middlewares/logger.js

const winston = require('winston'); 
const expressWinston = require('express-winston');
```

#### Using winston
see [[JS - Logging]]