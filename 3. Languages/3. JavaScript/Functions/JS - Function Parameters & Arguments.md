See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---
# What are Function Parameters?
* Parameters are optional inputs that a function can take in
	* Without parameters a function will ALWAYS do the same thing
	* Parameters allow for different results (depending on the input received)

### How to indicate multiple parameters
* Separated by commas
* Using the spread operator

### Which functions can take parameters?
* All types of functions can take in parameters (see [[JS - Function Declarations]], [[JS - Function Expressions]], [[JS - Arrow Functions]])

### Default Parameters
* Can be used to assign a default value to the parameter
	* Useful when getting information from an API or outside sources
* Prevents the function from returning 'undefined, NaN, or an error' (see [[JS - null, undefined, and NaN]])
* Declaring default parameters
	* use the equal sign ( = ) & the value
```js
function calculateArea(length, width = 1) { // giving width a default value of 1
  console.log(length * width);
}

calculateArea(5);  // output: 5 
```

---
# What are Function Arguments?
* The values passed into the function in the place of parameters when calling the function (see [[JS - What are Functions?]])
* **Object properties** cannot be used as function parameters (but can be used as arguments)

```js

// parameters are used when declaring a function
function calculateArea(length, width) { 
  console.log(length * width);
}

calculateArea(10, 2); // arguments are passed when calling the function
// 20  
```