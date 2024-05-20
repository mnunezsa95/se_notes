What is an array? (see [[JS - Arrays in JavaScript]])

### length 
* Description:
	* Used to determine the number of elements in an array
	* Used to find the index of the **last** element in the array 
		* The last element will ALWAYS be 1 less than the total length (b/c array index starts at 0)
* Syntax
```js
arrayName.length
```
* Example
```js
let groceries = ["chips", "lemonade", "grapefruit", "orange", "juice", "milk", "eggs", "cookies", "banana", "cheese"];

// Finding the length of the array
groceries.length // 10 will be logged into the console

// Finding the last element of the array
groceries[groceries.length - 1]
```