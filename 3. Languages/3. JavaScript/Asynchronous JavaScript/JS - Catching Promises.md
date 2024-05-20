# How to Catch Errors
* There are 2 ways to handle (or catch an error)
	1) Using the second argument of the then() method (see [[JS - Catching Promises]])
		* (a callback function called onRejected)
	2) Using the catch() method (see [[JS - Promise Methods]])

* Example: Catching errors in the `then()`
```js
const getCountryData = function (country) {
	fetch(`https://restcountries.com/v3.1/name/${country}`)
	    .then(
	      res => res.json(), // the onFulfilled callback
	      err => alert(err) // the onRjected callback
	    )
}
```

* Example: Catching errors in the `catch()`
```js
const getCountryData = function (country) {
  fetch(`https://restcountries.com/v3.1/name/${country}`)
    .then(res => res.json())
    .then(data => {
      renderCountry(data[0]);
      const neighbor = data[0].borders[0];
    })
    // catching all error
    .catch(err => {
      console.error(`${err}`); // logging error to the console
      renderError(`The Following Error: ${err} was found!`); // handling error:             rendering error to the UI with a message for user
    });
};
```