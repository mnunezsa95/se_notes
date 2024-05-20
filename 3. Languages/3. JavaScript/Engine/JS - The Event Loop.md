See [[JS - Introduction to JavaScript]]

---

* The **Event Loop** --> allows for Asynchronous JS to work (see [[JS - Async JavaScript Behind the Scenes]])
	* Looks into the call stack and determines if empty
		* **if empty** --> takes the first callback from **microtask queue** or **callback queue** and place it on the call stack (called an event loop tick)
			* Microtasks have priority over callback queue
		* **If not empty** --> will wait for it to become empty
	* The microtask or callback is executed
	* The microtask or callback is removed from call stack

![](https://lh3.googleusercontent.com/KbsaqVPPA3ZgTYpSsxU2jYqZBauhwitHee7Cz83nCF6XhlRBuZtdtIzg67AWNUd0JUiyRTMtqeENjeKn8Qe2bN4klgYKYv3MWx-BlAlBh6uC-RVaKD6jIIXXug1W5D_7vFY0RKnowXUOTjOvbYw7CeI)

* Example: The event loop
	* Order of execution: **1 --> 4 --> 3 --> 2**
		* The resolved promise will be logged first because microtasks take priority over callbacks
```js
console.log("1) Test start"); 
setTimeout(() => console.log("2) 0 sec timer"), 0);
Promise.resolve("3) Resolved promise 1").then((res) => console.log(res));
console.log("4) Test end");
```