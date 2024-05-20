Resources:
* Article: [CommonJS …what, why and how](https://medium.com/@cgcrutch18/commonjs-what-why-and-how-64ed9f31aa46)
### What is CommonJS?
* CommonJS is a module formatting system (see [[JS - What are Modules?]])
	* A standard for structuring and organizing JavaScript code

### How to use CommonJS?
* Wraps each module in a function called `require,` and includes an object called `module.exports`, which exports code for availability to be required by other modules 
```js
// Exporting
export.addToCart = function(product, quantity) {
	cart.push({product, quantity});
		console.log(
			`${quantity} ${product} added to cart`
		);
};


// Importing
const { addToCart } = require('./shoppingCart.js');
```