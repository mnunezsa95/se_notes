### How are algorithms evaluated?
* Based on two parameters
	1) execution time (temporal complexity)
	2) memory consumption (spatial complexity)
* The parameters depend on 
	1) The device on which executed
	2) The amount of input data
* Rule of thumb: 
	* execution time ↑, memory consumption ↑ 

### What is Asymptotic Analysis?
* An approach to analysis algorithms without the considering the device of execution
	* Still considers input amount
* Temporal complexity --> defined by how long a program takes to run
	* #'s of operations ↑, runtime ↑ 
* Spatial complexity --> measures the amount of memory an algorithm will consume
	* #'s of variables ↑, memory ↑
* In asymptotic analysis
	* calculate how much the complexity of an algorithm increases relative to the amount of input data.

### Example: Exploring temporal complexity
```js
function sum(numbers) {
	let sum = 0;
	for (let i = 0; i < numbers.length; i++) {
        sum += numbers[i]
	}
	return sum;
} 
```
* List of operations
	* `let sum = 0` — initializing a variable
	* `let i = 0` — initializing a variable
	* `i < numbers.length` — checking against the condition
	* `i += 1` — incrementing the variable's value by one
	* `numbers[i]` — accessing an element in the array
	* `sum += numbers[i]` — incrementing the value of the sum variable
* Calculating total number of operations
	* The four operations that make up the loop * the number of loop iterations + the first two operations in the function (end up with `2 + 4 * n`)
**![](https://lh3.googleusercontent.com/5CP9F6UZuzbPqJU0QLoWGdJ4if7lEGtD_1YP0hdsF6aRtu4oQivlGyz66xh17J6IOVnf-qRfU-5EtH3N3aGcafmboT8bWCh9zJ3Es140TYAWFtLEuuK4WWByy7cIf5ohatke49zNvWq_O37y54meDWQ)
* Analysis
	* When n changes by a factor of 10, the growth rate of the function changes to be close to the factor change. As the factor increases, it gets closer to 10.
	* The function above can be said to have a complexity of `0(n)` (Big O of n) which means the function does not grow any faster than the n function multiplied by a constant. 
	* Spatial complexity is 0(1)