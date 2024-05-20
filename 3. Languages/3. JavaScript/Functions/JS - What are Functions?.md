Resources
* [TripleTen: Basic Functions Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/functions.pdf)

### Purpose of Functions
* A function allows for code to be packaged in a way so that it can be reused. 
* Functions make code become more organized
* Functions make programs less “chunky” meaning it can be made shorter

### Ways to declare a Function
* There are 3 ways to declare a function
	1) function declarations (see [[JS - Function Declarations]])
	2) function expressions (see [[JS - Function Expressions]])
	3) arrow functions (see [[JS - Arrow Functions]])

### Calling a function
* Functions MUST be called in order to be executed
```js
// declaring the function
function calculateArea(length, width) {  
  console.log(length * width);
} 

// calling the function
calculateArea(10, 5);
```
