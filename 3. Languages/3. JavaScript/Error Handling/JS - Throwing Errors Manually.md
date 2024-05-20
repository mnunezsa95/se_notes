# Errors in JavaScript
* JS has an Error() constructor used to create new errors (see [[JS - Error Constructor()]])
* JS errors can also be created from classes (see [[JS - Error Classes]])

### Throwing an Error
* The `throw` statement is used to manually 'throw' errors
* When an error is thrown --> promise is immediately rejected
	* Must be handled in the `catch()` method (see [[JS - Catching Promises]])

#### Examples
* Manually throwing an error
```js
const getCountryData = function (country) {
	fetch(`https://restcountries.com/v3.1/name/${country}`)
		.then(res => {
			if (!res.ok) {
				throw new Error(`Country not found ${res.status}`);
			}
			res.json();
	    })
		.catch(err => { // catching all error
			console.error(`${err}`); // logging error to the console
			renderError(`Something went wrong ${err.message}. Try again!`); 
		})
		.finally(() => {
			countriesContainer.style.opacity = 1;
		});
};
```
