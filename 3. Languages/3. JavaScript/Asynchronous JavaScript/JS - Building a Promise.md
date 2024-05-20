What is a promise? (see [[JS - Promises]])

### How to build a promise?
* Promises use a constructor() function (see [[JS - Promise Methods]])
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


### What is Promisifying?
* Converting a callback-based asynchronous behavior to promise-based behavior
	* Allows for priority on the event loop (microtasks take priority over callbacks) (see [[JS - The Event Loop]], [[JS - Async JavaScript Behind the Scenes]])

```js
// Promisifying setTimeout
const wait = function (seconds) {
	return new Promise(function (resolve, _reject) {
		setTimeout(resolve, seconds * 1000); // the setTimemout will return a 
	});                                         // resolve() promise
};

// Consuming the promise
wait(2)
	.then(() => {
		console.log('I waited for 2 seconds');
		return wait(1); // will return a new promise (which needs to be handled)
	})
	.then(() => console.log('I waited for one second'));
```