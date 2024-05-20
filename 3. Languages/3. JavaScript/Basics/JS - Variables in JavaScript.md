### What are variables?
* Variables --> can be thought of as a box that store data or information

### Working with Variables
* Variables --> need to be declared when being used for the first time 
	* Once a variable is declared --> can be used in code

### Rules for Naming Variables
1) Should be written to  describe the kind of information contained
2) Should be nouns (ie: username, sum, productID)
3) The only valid special characters in variables
	* dollar sign ($)
	* underscore ( _ ).
4) Numbers CANNOT be used in the beginning of the name
	* Should be avoided in general
5) Spaces are NOT allowed 
6) Use camelCase to separate multiple words
7) Javascript keywords (such as let and const) cannot be used as variable names ([see complete list here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#keywords))

### Declaring Variables
* Variables can be declared in 3 ways
	* let --> declares a variable (value can be changed)
	* const --> declares a constant variable (value cannot be changed)
	* var --> declares a variable (this variable can be used before declaration)
		* variables declared with 'var' are hoisted (see [[Hoisting in JavaScript]])
```js
let username = "JazzFan1999"; // this variable is called “username” and given a value of JazzFan1999 */

const username2 = "Elise"; // the username2 variable is locked in with the value “Elise” and cannot be changed

console.log(x); // the variable is used before being declared; this is possible because var was used 
var x = 10;
```

### Declaring Multiple Variables
* multiple variables --> can be declared 3 ways:
	* The one-line style (not recommended)
	* The multi-line style 
	* The multi-line-comma-first style
```js
let user = 'John', age = 25, message = 'Hello'; // the one-line style

// can also be declared using multiple lines
let user = 'John',
  age = 25,
  message = 'Hello';
  
// can also be declared using multi-line-comma-first style
let user = 'John'
  , age = 25
  , message = 'Hello';
```

# Common Practice: Using constants
* Constants can be as aliases or difficult-to-remember values 
* Naming constants
	* Use capital letters
	* Use underscores
```js
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...when we need to pick a color
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```