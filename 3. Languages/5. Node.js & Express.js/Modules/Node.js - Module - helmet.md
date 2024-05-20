Resources:
* [NPM: helmet: Documentation](https://www.npmjs.com/package/helmet)

# What does the helmet Module do?
* Sets security headers automatically to help prevent XSS (see [[Cross-Site Scripting (XSS)]], [[Web Application Checklist]])

#### Installing helmet
* Install the module 
```bash
npm install helmet
```

#### Importing helmet
```js
const helmet = require('helmet');
```

#### Using helmet
```js
app.use(helmet());
```