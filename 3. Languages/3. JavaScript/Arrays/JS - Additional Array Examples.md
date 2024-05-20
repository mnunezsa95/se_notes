Working with Arrays (see [[JS - Arrays in JavaScript]], [[JS - Array Methods]])


* Example 1: Using `flatMap()`, `reduce()`, `filter()`
```js
// flatMap combined map().flat() into one method
// flatMap will create one large array with all account movements
// filter will only return back positive movements
// reduce will combine them down to one value
const bankDepositSum = accounts
  .flatMap(acc => acc.movements)
  .filter(mov => mov > 0)
  .reduce((sum, cur) => sum + cur, 0);

console.log(bankDepositSum);
```

* Example 2: Using `flatMap()`,  `filter()`
```js
// flatMap combined map().flat() into one method
// filter will filter arrays greater than 1000, and return the number of them
const numDeposits1000 = accounts
  .flatMap(acc => acc.movements)
  .filter(mov => mov > 1000).length;

console.log(numDeposits1000);
```

* Example 3: Using `flatMap()`,  `reduce()`
```js
const newNumDeposits1000 = accounts
  .flatMap(acc => acc.movements) // combines all movements into one new array
  .reduce((count, cur) => (cur > 1000 ? count + 1 : count), 0); // count starts at 0, if the cur value > 1000, 1 is added to the count

console.log(newNumDeposits1000);
```

* Example 4: Using `flatMap()`, `reduce()`
```js
// destructuring the two values from the object
const { deposits2, withdrawals2 } = accounts.flatMap(acc => acc.movements) 
	.reduce(
	    (sums, cur) => {
	      sums[cur > 0 ? 'deposits2' : 'withdrawals2'] += cur; 
	      // conditionally grabbing the desired value
	      return sums;
	    },
    { deposits2: 0, withdrawals2: 0 } // setting the initial value as an object      with 2 properties
);

console.log(deposits2, withdrawals2);
```

* Example 5: Using `map()`, `join()`, `include()`, `slice()`
```js
const convertTitleCase = function (title) {
	const capitalize = str => str[0].toUpperCase() + str.slice(1);
	const exceptions = [
	  'a', 'an', 'the', 'but', 'or', 'on', 'in', 'with', 'and', 'is'
	];
	const titleCase = title.toLowerCase().split(' ').map(word =>                        (exceptions.includes(word) ? word : capitalize(word))).join(' ');
	return capitalize(titleCase);
};

console.log(convertTitleCase('this is a nice title'));
console.log(convertTitleCase('this is a LONG title but not too long'));
console.log(convertTitleCase('and here is another title with an EXAMPLE'));
```