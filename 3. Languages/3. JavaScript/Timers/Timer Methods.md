What are Timers? (see [[Timers in JavaScript]])

### setTimeout()
* Description
	* Sets a timer which executes a function or specified piece of code once the timer expires.
* Arguments
	1) functionRef --> A function to be executed after the timer expires
	2) delay --> The time (in milliseconds) that the timer should wait before the specified function or code is executed.
	3) param1...paramN --> additional arguments that must be passed to the functionRef
* Syntax
```js
setTimeout(functionRef, delay, param1, param2, /* …, */ paramN)
```
* Example
```js
setTimeout(function () {
	myArray.myMethod();
}, 2.0 * 1000); // prints "zero,one,two" after 2 seconds
```

```js
function showMessage(message) { 
   console.log(message); 
} 

setTimeout(showMessage, 10000, "10 seconds have passed since the page was loaded"); 
// 10 seconds (or 10 thousand milliseconds) after the page has been loaded, a message will appear in the console.
```

### clearTimeout()
* Description
	* Cancels a timeout previously established by setTimeout().
* Arguments
	1) timeoutID --> The identifier of the timeout you want to cancel. This is usually the name of the variable that the setTimeout() saved to
* Syntax
```js
clearTimeout(timeoutID)
```
* Example
```js
function logOut() { 
	// The logic for logging user out after a certain period of inactivity 
}

let timer = setTimeout(logOut, 300000); // Log the user out of the system after 300 seconds has elapsed 

// If the user clicks somewhere on the page, reset the timer and wait for another user interaction 
window.addEventListener("click", function () { 
  clearTimeout(timer); // cancel the timer if  user clicks anywhere on the page
  timer = setTimeout(logOut, 300000); // set the timer again if user interacts
}); 
```

### setInterval()
* Description
	* Repeatedly calls a function or executes a code snippet, with a fixed time delay between each call
* Arguments
	1) functionRef --> A function to be executed every delay milliseconds. The first execution happens after delay milliseconds.
	2) delay --> The time (in milliseconds) the timer should delay in between executions of the specified function 
	3) arg0, …, argN --> additional arguments that must be passed to the functionRef
* Syntax
```js
setInterval(func, delay, arg0, arg1, /* …, */ argN)
```
* Example
```js
// calling a function to print time to console every second
setInterval(function () { // function is executed every time interval
	const now = new Date();
	console.log(now)
}, 1000)
```

### clearInterval()
* Description
	* Cancels a timed, repeating action which was previously established by a call to setInterval().
* Arguments
	1) intervalID --> The identifier of the repeated action you want to cancel. This is usually the name of the variable that the setInterval() was saved to
* Syntax
```js
clearInterval(intervalID)
```
* Example
```js
const interval = setInterval(function () { // function is executed every time interval
	const now = new Date();
	console.log(now)
}, 1000)

clearInterval(interval); // clears the interval that was set above
```