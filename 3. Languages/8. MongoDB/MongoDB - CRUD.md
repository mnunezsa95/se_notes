* Once the model is created, it can be interacted with by a variety of methods
* CRUD is an acronym used in data work
	* C = Create
	* R = Read
	* U = Update
	* D = Delete

* CRUD Methods (see [[MongoDB - Methods & Properties]])
	* Create: `create()`
	* Read: `findById()`, `findOne()`, `find()`
	* Update: `findByIdAndUpdate()`, `findOneAndUpdate()`, `updateOne()`, `updateMany()`
	* Delete: `findByIdAndRemove()`, `findOneAndRemove()`, `delete()`, `deleteMany()`

# Update Methods
* By default, `findByIdAndUpdate()`, `findOneAndUpdate()`, `updateMany()` make it so that the `.then()` handler receives the original document (before it was updated as an input)
	* Can cause user to think that the update did not work
* These methods can take an OPTIONS object that has the following options

| Option        | Description                                             | Default Value | Value Needed to ensure user sees update |
| ------------- | ------------------------------------------------------- | ------------- | --------------------------------------- |
| new           | pass the updated object as input to the .then() handler | false         | true                                    |
| runValidators | validate the new data before recording it in database   | false         | true                                    |
| upsert        | if the document was not found, create it                | false         | true                                        |

* Example
```js
User.findByIdAndUpdate( 
  req.params.id, 
  { name: 'Henry George' }, // pass the options object: 
  { 
    new: true, // the then handler receives the updated entry as input 
    runValidators: true, // the data will be validated before the update 
    upsert: true // if the user entry wasn't found, it will be created 
  } 
) 
  .then(user => res.send({ data: user })) 
  .catch(user => res.send({ 'Data validation failed or another error occured.' }));
```

# Example from Code Exercise
```js
const router = require('express').Router(); // import router for routing
const Film = require('../models/film');
  
router.get('/', (req, res) => { // the route is '/'
  Film.find({}) // find all documents
    .then(films => res.send({ data: films })) // sending all films
    .catch(() => res.status(500).send({ message: 'Error' })); 
    // if an error happens, it will send a 500 error
});

// will be triggered by a POST request to the /films path
router.post('/', (req, res) => {
  const { title, genre } = req.body;
  Film.create({title, genre}) // creates a document in the database
    .then(film => res.send({ data: film }))
    .catch(() => res.status(500).send({ message: 'Error' }));
});

module.exports = router;
```