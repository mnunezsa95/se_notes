* Declarative Programming --> being used more in JavaScript libraries (like React & Redux) (see [[React - Introduction to React.js]])

### Imperative & Declarative Programming

* **Imperative programming** = describe the sequence of steps that need to be followed to achieve the desired result
	* Explains HOW to do
* **Declarative programming** = specifies what needs to be achieved without going through the details of how to do it
	* Explains WHAT to do 
	* Easier to maintain and improve 
	* Less confusion

### Examples
* Imperative
```js
const a = [1, 2, 3];
const b = [];

for (let i = 0; i < a.length; i += 1) {
  b[i] = a[i] * 2;
} // we'll refer to the original array elements by indices, multiply them by 2, and write the result in a new array 

console.log(b); // [2, 4, 6] 
```

* Declarative
```js
const a = [1, 2, 3];

const b = a.map(function (item) {
    return item * 2;
}); // create a new array using the original one; elements of a new array have to be the original array elements multiplied by 2

console.log(b); // [2, 4, 6] 
```

