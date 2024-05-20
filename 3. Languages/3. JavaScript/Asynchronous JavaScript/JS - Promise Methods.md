# Promise() Contructor

#### new Promise()
* Description: 
	* Creates Promise objects (see [[JS - Building a Promise]])
* Arguments
	1) executor --> a function to be executed by the constructor; any errors thrown in the constructor will cause the promise to be rejected
		1) resolveFunc --> a callback function that is executed when the promise is resolved
		2) rejectFunc --> a callback function that is executed when the promise is rejected
* Syntax
```js
new Promise(executor(resolve, reject))
```
* Example
```js
// the Promise() constructor takes function parameter, when in turn takes two callback function (resolveFn and rejectFn)
const lotteryPromise = new Promise(function (resolve, reject) {
	console.log('Lottery draw is happening 🔮');
	setTimeout(() => {
		if (Math.random() >= 0.5) {
			resolve('You WIN 💰'); // calling the resolve() function will 
		} else {                      // resolve this promise
			reject('You lost your money 💩'); // calling the reject() will 
		}                                    // reject this promise
	}, 2000);
});

lotteryPromise.then(res => console.log(res)).catch(err => console.log(err));
```

#### Promise.resolve()
* Description
	* A static method that will immediately resolve the promise; the value passed into the argument becomes the resolved value
* Arguments
	1) value --> the value that will become the resolved value (to be handled in the `then()`)
* Syntax
```js
Promise.resolve(value)
```
* Example
```js
// the promise will automatically be resolved immediately
Promise.resolve('Resolved!').then(res => console.log(res));
```

#### Promise.reject()
* Description
	* A static method that will immediately reject the promise; the value passed into the argument becomes the rejected value
* Arguments
	1) value --> the value that will become the rejected value (to be handled in the `catch()`)
* Syntax
```js
Promise.rejected(value)
```
* Example
```js
// the promise will automatically be rejected immediately
Promise.reject('Rejected!').catch(err => console.log(err));
```

#### Promise.all()
* Description
	* A static method that takes an iterable of promises as input and returns a single Promise as an array. This method will short-circuit when one promise is rejected
		* If all are fulfilled, the promise will return fulfilled
		* If any are rejected, the promise will return rejected
* Arguments
	1) iterable --> an iterable of promises
* Syntax
```js
Promise.all(iterable)
```
* Example
```js
const get3Countries = async function (c1, c2, c3) {

try {
	const data = await Promise.all([
		getJSON(`https://restcountries.eu/rest/v2/name/${c1}`),
		getJSON(`https://restcountries.eu/rest/v2/name/${c2}`),
		getJSON(`https://restcountries.eu/rest/v2/name/${c3}`),
	]);
		console.log(data.map(d => d[0].capital));
	} catch (err) {
		console.error(err);
	}
};

get3Countries('portugal', 'canada', 'tanzania');
```


#### Promise.race()
* Description
	* A Static method takes an iterable of promises as input and returns a single Promise.
		* The value of the returned promise will be the first promise that settles
* Arguments
	1)  iterable --> an iterable of promises
* Syntax
```js
Promise.race(iterable)
```
* Example
```js
(async function () {
	const res = await Promise.race([
		getJSON(`https://restcountries.eu/rest/v2/name/italy`),
		getJSON(`https://restcountries.eu/rest/v2/name/mexico`),
		getJSON(`https://restcountries.eu/rest/v2/name/egypt`),
	]);
	console.log(res[0]);
})();

// The value of the promise will be whichever of the promises above is settled first.
```

#### Promise.allSettled()
* Description
	* A static method takes an iterable of promises as input and returns a single Promise.
		* The value of the returned promise will be the results of the promises (does NOT short-circuit when a promise is rejected)
* Arguments
	1) iterable --> an iterable of promises
* Syntax
```js
Promise.allSettled(iterable)
```
* Example
```js
Promise.allSettled([
	Promise.resolve('Success'),
	Promise.reject("Rejected"),
	Promise.resolve('Another success'),
]).then((res) => console.log(res));

// The res will be the value of all the promises in the iterable. An error will NOT be produced, if one is failed
```

#### Promise.any()
* Description
	* A static method takes an iterable of promises as input and returns a single Promise. 
		* If any are fulfilled, the promise will return fulfilled
		* If all are rejected, the promise will return rejected
* Arguments
	1) iterable --> an iterable of promises
* Syntax
```js
Promise.any(iterable)
```
* Example
```js
Promise.any([
	Promise.resolve('Success'),
	Promise.reject("Rejected"),
	Promise.resolve('Another success'),
]).then((res) => console.log(res));

// The result of this promise will be a fulfilled promise because the one rejected promise is ignored. 
```

---
# Promise.prototype Methods

#### .then()
* Description
	* Returns an equivalent Promise object, allowing you to chain calls to other promise methods.
* Arguments
	1) onFulfilled --> an async function to execute if promise becomes **fulfilled**. The return value becomes the value of the promise returned by then()
		1) value --> the value that the promise was fulfilled with
	2) onRejected --> an async function to execute if promise becomes **rejected**. It's return value becomes the fulfillment value of the promise returned by then()
		1) reason --> the value that the promise was rejected with
* Syntax
```js
promiseInstance.then(onFulfilled, onRejected);
```
* Example
```js
const request = fetch('https://restcountries.com/v3.1/name/portugal');
console.log(request);

const getCountryData = function (country) {
	fetch(`https://restcountries.com/v3.1/name/${country}`)
	    .then(res => res.json())
	    .then(data => renderCountry(data[0]));
};
```

#### .catch()
* Description
	* Returns an equivalent Promise object, when the promise is rejected; can be chained with other promise methods
* Arguments
	1) onRejected --> an async function to execute if promise becomes **rejected**. It's return value becomes the fulfillment value of the promise returned by catch()
		1) reason --> value that the promise was rejected with
* Syntax
```js
promiseInstance.catch(onRejected)
```
* Example
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
      renderError(`The Following Error: ${err} was found!`); // handling error:           rendering error to the UI with a message for user
    });
};
```

#### .finally()
* Description
	* Returns an equivalent Promise object, allowing you to chain calls to other promise methods.
* Arguments
	1) onFinally --> an async function to execute when a promise is settled (either fulfilled or rejected); ALWAYS gets executed
* Syntax
```js
promiseInstance.finally()
```
* Example
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
      renderError(`The Following Error: ${err} was found!`); // handling error:          rendering error to the UI with a message for user
    })
    .finally(() => {
      countriesContainer.style.opacity = 1;
    });
};
```

----
#### .json()
* Description
	* Takes a Response stream and reads it to completion (coverts it to an object)
	* Returns a promise which resolves with the result of parsing the body text as JSON
* Arguments
	* none
* Syntax
```js
res.json();
```
* Example
```js
const request = fetch('https://restcountries.com/v3.1/name/portugal');
console.log(request);

const getCountryData = function (country) {
	fetch(`https://restcountries.com/v3.1/name/${country}`)
	    .then(res => res.json()) // parsing the response
	    .then(data => renderCountry(data[0]));
};
```