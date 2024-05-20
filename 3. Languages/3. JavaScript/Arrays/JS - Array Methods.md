# List of Methods


#### array.includes() 
* Description
	* Checks whether the specified array includes a certain value among its entries and returns a boolean (true or false)
* Arguments
	1) searchElement --> the value to search for
	2) fromIndex (Optional)--> zero-based index at which to start searching 
		* starts at index = 0, if not specified
		* can use negative indexes
* Syntax 
```js
// the fromIndex argument is optional
arrayName.includes(searchElement) 
arrayName.includes(searchElement, fromIndex)
```
* Example
```js
movements = [200, 450, -300, 300, -650, -130, 70, 1300]
const anyDeposits = movements.includes(-130);
```

#### array.some()
* Description
	* Checks whether at least one element in the specified array passes the **condition** specified by the provided function
* Arguments
	1) callbackfn --> has three parameters
		1) element --> the current element being processed 
		2) index --> the index of the current element being processed
		3) array --> the array the `some()` method was called upon
	2) thisArg (optional) --> the value to use as `this` when executing the callbackfn
* Syntax
```js
// the thisArg argument is optional
arrayName.some(callbackfn)
arrayName.some(callbackfn, thisArg)
```
* Example
```js
movements = [200, 450, -300, 300, -650, -130, 70, 1300]
const anyDeposits = movements.some(mov => mov > 5000);
```

#### array.every()
* Description
	* Checks wether all elements in the specified array pass the condition specified by the provided function and returns a boolean
* Arguments
	1) callbackfn --> a function to execute for each element in the array. Should return a truthy value to indicate passing the condition, and falsy value otherwise
		1) element --> the current element being processed 
		2) index --> the index of the current element being processed
		3) array --> the array the `every()` method was called upon
	2) thisArg (optional) --> the value to use as `this` when executing the callbackfn
* Syntax
```js
arrayName.every(callbackfn)
arrayName.every(callbackfn, thisArg)
```
* Example
```js
movements = [200, 450, -300, 300, -650, -130, 70, 1300]

// check if every movement is a deposit
const areAllDeposits = movements.every((mov) => {
	return mov > 0;
});
```

#### array.flat()
* Description
	* Creates a new array with all sub-array elements concatenated into it recursively
* Arguments
	1) depth (optional) --> specifies how deep a nested array structured should be flattened
		* default is 1
* Syntax:
```js 
arrayName.flat()
arrayName.flat(depth)
```
* Example
```js
const arr = [[1,2,3], [4,5,6], [7,8,9]];
arr.flat();

const arrDeep = [[[1,2], 3],[4 [5,6]], 7, 8];
arrDeep.flat(2); // goes two levels deep when flattening
```

#### array.flatMap()
* Description
	* Returns a new array formed by applying a callback function to each element in the array, and then flattening the result by one level
	* Essentially combined the `.map()` and `.flat()` methods
* Arguments
	1) callbackfn --> a function to execute for each element in the array. It should return an array containing new elements of the new array, or a single non-array value to be added to the new array
		1) element --> the current element being processed 
		2) index --> the index of the current element being processed
		3) array --> the array the `flatMap()` method was called upon
	2) thisArg (optional) --> the value to use as `this` when executing the callbackfn
* Syntax
```js
arrayName.flatMap(callbackFn)
arrayName.flatMap(callbackFn, thisArg)
```
* Example
```js
const overalBalance2 = accounts
	.flatMap(acc => acc.movemenets) // maps and flattens the accounts array
	.reduce((acc, mov) => acc + mov, 0); // adds all values together
```

#### array.sort()
* Description
	* Sorts elements of an array (in place) and returns the reference to the same array, now sorted.
		* The default sorting is "ascending."
		* How it works --> converts all elements to strings and compares the strings 
* Arguments
	1) compareFn (optional) --> a function that defines the sort order. The return value should be a whole number, whose sign indicates the relative order of two elements
		1) a --> the first element in the compareFn 
		3) b --> the second element in the compareFn
* Additional
	* If .compareFn is negative (return < 0; a will be placed before b in sort order) (keep order)
	* If compareFn is positive (return > 0; b will be placed before a in sort order) (switch order)
* Syntax:
```js
sort()
sort(compareFn)
```
* Example:
```js
// sorting strings
const owners = ['Jonas', 'Zach', 'Adam', 'Marta'];
owners.sort(); // will sort owners alphabetically (Adam, Jonas, Marta, Zach)

// sorting numbers
movements = [200, 450, -400, 3000, -650, -130, 70, 1300];
movements.sort(); // will convert numbers to strings & sort them (-130, -400, -650, 1300, 200, 3000, 450, 70)

// sorting numbers w/ compareFn
movements.sort((a, b) => {
	if (a > b) return 1;
	if (b > a) return -1;
})

// re-writting the statement above simpler 
movements.sort((a, b) => {
	return a - b;
})
```

#### array.fill()
* Description
	* Changes all elements within a range of indices in an array to a static value, and returns the modified array
* Arguments
	1) value --> value to fill the array with (all elements will get this value)
	2) start (optional) --> Index where filling will start (zero-based index)
	3) end (optional) --> Index where filling will end (zero-based index)
* Additional
	* The only method that can be called on empty arrays (see [[JS - Creating Arrays Programmatically]])
* Syntax
```js
arrayName.fill(value)
arrayName.fill(value, start, end) // start & end are optional
```
* Example
```js
x.fill(1, 3, 5) // will start filling the array with a value of 1 at index 3, end at index 5 
```