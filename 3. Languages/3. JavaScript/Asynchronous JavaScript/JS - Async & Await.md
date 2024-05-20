Resources:
* [JavaScript.Info: Async/Await](https://javascript.info/async-await)

Example:
* See [[JS - Async & Await - Examples]]
# What is an Async Function?
* Allows us to write promises-based code as if it was synchronous and it checks that we are not breaking the execution thread (see [[JS - Why is Asynchronous Code needed?]], [[JS - Async JavaScript Behind the Scenes]])
	* Operates asynchronously via the event loop (see [[JS - The Event Loop]])
* Async functions will always return a value.

# How does async/await work?
* async / await --> syntactic sugar over the `then()` method in promises (see [[JS - Promise Methods]])
	* Behind the scenes, this uses promises, just consumed  in a different way (see [[JS - Promises]])

# Why are async/await functions useful?
* Remove the need for `then()` method to be used
	* The `await` statement can be directly tied to a variable

### Syntax: Async/Await
* Can ONLY contain one `async` keyword
* Can contain 1 or more `await` statements
```js
async functionName() {
	name1 = await statement1;
	name2 = await statement2;
	nameN = await statementeN;
}
```

#### How to create an async function
* Use the `async` keyword before the function declaration, expression or arrow function
* Use the `await` keyword to stop the code execution of the function until the promise has been fulfilled 
	* Stopping execution in an async function does not block the main thread of execution

```js

// declaring an async function using the 'async' keyword
const whereAmI2 = async function (country) {
	// the await statement will pause the code until execution
	const {} = await getPosition();
	const { latitude: lat, longitude: lng } = pos.coords;
	
	// the await statement will pause the code until execution of code above
	const resGeo = await fetch(`https://geocode.xyz/${lat},${lng}?geoit=json`);
	const dataGeo = await resGeo.json(); // res.json() can be stored in 'dataGeo'

	// the await statement will pause the code until execution
	const res = await fetch(`https://restcountries.com/v3.1/name/${country}`);
	const data = await res.json(); // res.json() can be stored in 'data'
	renderCountry(data[0]);
};

whereAmI('portugal');
```

### Catching Errors in Async Functions
* Using `try...catch` statements (see [[JS - try...catch]])