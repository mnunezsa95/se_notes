See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---

* JS Engine Rule for scopes --> If it cannot find a variable inside current scope, it will continue the search one level further outside until it is found (see [[JS - Scopes & Lexical Environments]])

### Closures
* What is a closure? 
	* Functions remember the scope in which they are declared
		* Remembers which identifiers existed in the same scope along with it at the moment of creation
* A closure allows access to the scope of an enclosing, outer function from within an inner function. 
* Closures are created each time a JavaScript function is created.
* Closures are created at the same time as the outer `LexicalEnvironment` object.

### Calling a function from outside of its scope
1) Call a function in the same scope where it was declared in 
2) Call a function inside any nested scopes
```js
function abc() {
	console.log('Hello');
	function xyz() {
    // the scope of the xyz() function. Here we can call the abc() function.
	    abc();
	}
		// the scope of the abc() function. Here we can call xyz() because it is            within the scope of the abc() function.
	xyz();
}
// this will result in an error: there is no function named xyz() in the global scope.
xyz(); 
```

3) Call a function that returns another function (closure example)
```js
function callMe() { 
	const internet = 'Internet'; 
	function callMeToo() {  
		console.log(internet); 
	} 
	return callMeToo; 
}

// calling callMe() and assigning it to a variable will allow callMeToo() to be accessed from the outer scope

const newCallMeToo = callMe(); // the callMeToo() closure is created here
console.log(newCallMeToo);

newCallMeToo(); // Result: "Internet" 

// the callMeToo() function now exists in the global scope stored inside the newCallMeToo variable. Even though the internet variable is not available in this scope, callMeToo() still has access to it
```

### Closure Analogy
1) Closure is like a briefcase that the function collects at the moment of declaration. 
2) The function brings the briefcase along with it, wherever it goes
3) The function stores all the variables from the scope where it was declared in this briefcase

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_JS3_2___1__3_1600100585.png)

### Closures Behind the Scenes
* When created, a function gets an internal property called `[[Environment]]` (refers to the outer object called `LexicalEnvironment`)
	* `LexicalEnvironment` --> contains all the local variables from the scope in which the function was created.  
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_13.06.3_1652110348.png)

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_S13_15_work_1600100624.png)

## Closures in Practice

#### Example 1:
* When `handler` is called, it will have access to the `hint` variable
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_JS3_3___1_1600100730.png)

#### Example 2:
* Preventing the use of global variables (like adding the `counter` variable In this code outside the function)
* Using a combination of public and private methods.
	* Private methods ensure the counter cannot be rewritten from the outside
	* Public methods makes the `increaseCounter()` and `resetCounter()` available 
* `createCounter()` returns an object, and we can add new methods to this object as required.
```js
/* our code */
const button = document.querySelector('button');

function createCounter(event) {
	const div = document.querySelector('div');
	let counter = 0; // this variable can't be accessed from the outer code
	
	// but the increaseCounter() function has access to it
	function increaseCounter() {
		counter += 1;
	    div.textContent = counter;
	}
	
	// let's add resetCounter() that also has access to the counter
	function resetCounter() {
		counter = 0;
	    div.textContent = counter;
	  }  
	/* we return an object with two functions, which are the public methods of 
	our module */ 
	return { increaseCounter, resetCounter };
}

// create a counter
const counter = createCounter();

// add handlers
increaseButton.addEventListener('click', counter.increaseCounter);
resetButton.addEventListener('click', counter.resetCounter); 

// All these counters will be independent
const counter1 = createCounter();
const counter2 = createCounter();
const counter3 = createCounter(); 
```