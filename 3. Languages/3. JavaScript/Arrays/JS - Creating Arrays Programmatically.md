# Using the new Array() constructor
* The `new Array()` constructor can be used to create an empty array
	* The array length will be equal to value specified in the `Array()` constructor
	* The only method that can be used empty arrays --> `array.fill()` (see [[JS - Array Methods]])
```js
const x = new Array(7); // will create an empty array
x.fill(1); // will fill the array with a value of 1
```

# Using the Array.from() 
* The `new Array()` is NOT an array; this is a function!
* Arguments
	1) an object (with the length property)
	2) a callbackFn --> to specify the value used to fill the array
```js
const y = Array.from({ length: 7 }, () => 1);
const z = Array.from({ length: 7 }, (_, i) => i + 1); 
// the _ is a throwaway function
// i is the current index
```

# Using querySelectorAll()  & Array.from()
* Using querySelectorAll() produces an "array-like" structure, but it is not a real array. 
	* Array.from() can be used to convert this "array-like" structure into a real array
```js
// creating an Array of nodes using from() and querySelectorAll()
const movementsUI = Array.from(document.querySelectorAll('.movements__Value'));

movementsUI.map(el => Number(el.textContent.replace("€", ""))); // mapping the results of the new real array
```