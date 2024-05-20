See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---
#### What are Arrow Functions?
* A precise syntax for writing functions
* Arrow functions do NOT have their own `this` keyword. It is inherited from the parent scope
* Arrow functions do NOT have their own `arguments` object
* Syntax
```JavaScript
// Basic arrow function  
const add = (a, b) => {  
  return a + b;  
};
```
* Note: IF there is a single expression in the function body, the curly braces `{}` and the `return` keyword can be OMITTED
```JavaScript
const add = (a, b) => a + b;
```
* Note: If there is a single parameter, the parentheses can be OMITTED
```JavaScript
const square = x => x * x;
```
* Note: Arrow functions do NOT have their own `this` keyword. It is inherited from the parent scope
```JavaScript
const obj = {  
name: "John",  
greet: () => {  
  console.log(`Hello, ${this.name}`); // Lexical 'this' refers to the global         scope, not obj  
  }  
};    
obj.greet(); // Output: Hello, undefined
```

#### Examples
* Example: Using an arrow function in a `map()` array method
```JavaScript
const numbers = [1, 2, 3, 4, 5];
const squaredArrow = numbers.map(num => num * num);
```
* Example:
```JavaScript
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbersArrow = numbers.filter(num => num % 2 === 0);
```
* Example: Using an arrow function when fetching from an API
```JavaScript
const fetchFromAPI = () => {  
  return new Promise((resolve, reject) => {  
    fetch('https://api.example.com/data')
      .then(response => response.json())  
      .then(data => resolve(data))  
      .catch(error => reject(error));  
  });  
};  

fetchFromAPI().then(data => console.log(data));
```