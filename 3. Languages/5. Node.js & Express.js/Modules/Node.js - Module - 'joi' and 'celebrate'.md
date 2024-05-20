Resources 
* [joi Official NPM Documentation](https://www.npmjs.com/package/joi)
* [celebrate Official NPM Documentation](https://www.npmjs.com/package/celebrate)

---
# Library: joi 
#### What is joi?
* Joi is a popular Node.js library for validating inbound server data (see [[JS - Validating Inbound Server Data]])
* Allows data to be described in an intuitive way

#### Installing joi
```bash
npm install joi
```


---
# celebrate
* celebrate allows joi validation to be used as a middleware

#### Installing celebrate
```bash
npm install celebrate
```

#### Importing celebrate
* MUST be imported 
* MUST be connected as a middleware
```js
const { celebrate, Joi } = require("celebrate");

router.post('/posts', celebrate({ 
	body: Joi.object().keys({ 
		title: Joi.string().required().min(2).max(30), 
		text: Joi.string().required().min(2), 
	}), 
}), createPost);
```

