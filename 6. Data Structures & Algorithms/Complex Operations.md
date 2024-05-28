### Elementary v Complex Operations
* Elementary Operations --> do not depend on the structure and amount of data possessed
	* Happen relatively quickly '
	* Are considered to have a single unit of complexity
	* Examples:
		* assigning values to a variable ( `a = 5` )
		* checking logical conditions ( `a > 5` )
		* mathematical operations ( `2 * 2` )

* Complex operations
	* Examples
		* calling a function 
		* using methods ( `map ()`, `join()` )

### Example: Complex Operations
```js
function printNames(people) {
  const names = people.map(p => p.name); // О(n), counts as n operations
  return names.join(', '); // О(n), counts as n operations
} 
```
* Analysis
	* Complexity of `printNames()` is equal to the sum of complexities of the two functions called inside of it, which are `.map()` and `join()`.
	* Complexity of `join()` only depends on the length of the array, therefore it is `0(n)`
	* Complexity of `map()` depends on the length of the array & the number of operations inside the callback function, therefore it is equal to `0(n * 1`), because only one operation happens inside the body (can be simplified to `0(n)`)
	* Adding the complexities --> `0(n) + 0(n) = 0(2n)`, the 2 can be omitted (get a complexity of `0(n)`)
	* 