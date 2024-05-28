Resources:
* [CS50 Lecture on Algorithms by Harvard and Yale](https://www.youtube.com/watch?v=fykrlqbV9wM&feature=youtu.be)
* [Big O for Beginners](https://hackernoon.com/big-o-for-beginners-622a64760e2)
* [Beginners Guide to Big O Notation](https://www.freecodecamp.org/news/my-first-foray-into-technology-c5b6e83fe8f1/)

See [[Asymptotic Analysis]], [[Complex Operations]]

# Big O Notation: General
**![](https://lh5.googleusercontent.com/FjFWfSy1psbV7ZJfbuDqQvK9kSxQqjrzJT4vt0gA2lxv0Legwm4Hu2Mf47nvTV4YhGVEICxHCStSyDYATn8NIQEsrj8_79kZZWDGbKQN89KJ31qQ2CxssCjGBZWei-v1NXREVYhQC3tkbCR_7Zi-g6Q)

### Constant Time Complexity: 0(1)
* Does not depend on input data
	* Execution time is the same regardless of input data
* Example
```js
function div(a, b) {
	return (a - (a % b) / b);
}
// execution time will be the same regardless of values of a & b
```

### Logarithmic Time Complexity: 0(log(n))
* Complexity changes on a **logarithmic scale** 
	* At each stage in the process -->  amount of data  to be processed is reduced by an order of magnitude
* Comp Science uses base 2 logs
	* Base does not affect complexity of algorithm
* Example: a binary search for an element index within a sorted array
	* With each iteration, the array is divided in half
		* 1st Iteration = 1024 elements
		* 2nd Iteration = 512 elements
		* 3rd Iteration = 256 elements
		* 4th Iteration = 128 elements
	* An array with 1024 elements would take 10 steps to solve: `log2(1024) = 10`
```js
function binarySearch(sortedNumbers, n) {
    // defining the start and end points of the search
    let start = 0;
    let end = sortedNumbers.length;
    
    while (start < end) {
	    // searching for the element in the middle of the array
	    const middle = Math.floor((start + end) / 2);
	    const value = sortedNumbers[middle];
	    // comparing the argument with the value in the middle of the array
	    if (n == value) {
	      return middle;
	    }
	    // if the argument is less than the median of the array, split the array            in half
	    // Now the end of the array is its former median
	    if (n < value) {
	      end = middle;
	    // otherwise, the beginning of the array becomes the element that comes             right after the "median"
	    } else {
	      start = middle + 1;
	    }
	  }
	// if the target number is not found, return -1
	return -1;
} 
```

### Linear Complexity: 0(n)
* Complexity grows in direct proportion to the amount of input data
* When is this usually seen? 
	* A loop that iterates over an array of elements
	* Num of operations -> directly proportional to the length of the array
* Example: finding the highest or lowest value in an unsorted array.
	* Go through array and compare values of different elements against one another
```js
function minMax(numbers) {
	// assigning the first element of the array to the min and max variables
	let min = numbers[0];
	let max = numbers[0];
	for (let i = 1; i < numbers.length; i++) {
	    const n = numbers[i];
	    // comparing the element with min
	    if (n < min) {
		    min = n;
		}
        // comparing the element with max
	    if (n > max) {
	      max = n;
	    }
	  }
    // returning the found pair of values
    return { min, max };
} 
```

### Quadratic Time Complexity: 0(n^2)
* A type of Polynomial Complexity ( `0 (n^k)` )
* Complexity grows quickly (squared growth) based on the input data 
	* Example: If amount of data increases by 100, then number of calculations grows 10,000x
* When is this usually seen? 
	* Nested loops
* Example: Element combinations from two arrays.
```js
function combinations(arr1, arr2) {
	// creating an empty array in which to store the result
	const result = [];
	// creating a couple of nested loops to find all possible pairs
	for (let i = 0; i < arr1.length; i++) {
	    for (let j = 0; j < arr2.length; j++) {
	      result.push([arr1[i], arr2[j]]);
	    }
	}
	return result;
} 
```

