* By default, Non-Relational Databases did did not have the ability to 'build relationships'
	* Non-relational databases have adopted the ability to build relationships from relational databases (see [[Relational & Non-Relational Databases]]) 

# Steps to Building a Relationship

### 1. Building a Relationship Between Schemas
* The `identifier` is used to set a relationship between two documents (schemas)
	* MongoDB automatically creates an `_id` field used to link two documents together
* How to link two documents together
	1) Set `type` property to `mongoose.Schema.Types.ObjectId` to link two documents together
	2) Set `ref` property to name of the model being linked
* Example
```js
const adSchema = new mongoose.Schema({ 
	title: { 
		type: String, 
		minlength: 2, 
		maxlength: 20, 
		required: true, 
	}, 
	text: { 
		type: String, 
		minlength: 2, 
		required: true, 
	}, 
	// add the creator field 
	creator: { 
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'user', 
		required: true 
	}, 
});
```

### 2. Include the `_id` Field During Document Creation
* Ensure that the `identifier` is recorded whenever a new document is created
	* Destructure creatorId from the request and set it as the value of the creator property when creating a document
```js
// controllers/ads.js 
const Ad = require('../models/ad'); 

module.exports.createAd = (req, res) => { 
  const { title, text, creatorId } = req.body; 
  Ad.create({ title, text, creator: creatorId }) 
    .then(ad => res.send({ data: ad })); 
};
```

### 3. Acquiring Complete Info via the populate() Method
* Once the two models are linked, use the populate() method to get the stored info (see [[MongoDB - Methods & Properties]])
```js
// controllers/ads.js 
const Ad = require('../models/ad'); 

module.exports.getAds = (req, res) => { 
	Ad.find({}) 
		.populate('creator') // use the populate() method
		.then(ad => res.send({ data: ad })); 
};
```