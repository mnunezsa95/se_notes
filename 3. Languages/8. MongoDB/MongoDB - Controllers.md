# What are controllers?
* Controller --> a collection of **request handler functions** responsible for interacting with a particular model
	* These functions (called **request handler** or **controller functions**) can CRUD documents and send a response back to the client (see [[MongoDB - CRUD]], [[MongoDB - Methods & Properties]])

---
# Controllers and Routes

| Type       | What should the folder contain? | What do the files                    |
| ---------- | ------------------------------- | ------------------------------------ |
| Routes     | Contain all route files         | define the routes                    |
| Controller | Contain all controller files    | responsible for handling the request |
 * The **controller** file describes the logic of **request processing**
 * The route file determines when controller logic should be applied (depending on the requested path and HTTP method) (see [[Express.js - Routing]])

# Controllers in Express.js
* Each request handler is the LAST middleware function executed (it does not call the next() method), but returns an answer to the user
```js
// controllers/users.js 
// this file is the user controller 

const User = require('../models/user'); 

// the getUser request handler 
module.exports.getUser = (req, res) => { 
  User.findById(req.params.id) 
    .then(user => res.send({ data: user })) 
    .catch(err => res.status(500).send({ message: 'Error' })); 
}; 

// the createUser request handler 
module.exports.createUser = (req, res) => { 
  const { name, about } = req.body; 
  User.create({ name, about }) 
    .then(user => res.send({ data: user })) 
    .catch(err => res.status(500).send({ message: 'Error' })); 
};
```

```js
// routes/users.js 
// this is the routes file 

const { getUser, createUser } = require('../controllers/users'); // import the controller functions 

// route definitions 
router.get('/:id', getUser); // use the controller functions
router.post('/', createUser);
```

