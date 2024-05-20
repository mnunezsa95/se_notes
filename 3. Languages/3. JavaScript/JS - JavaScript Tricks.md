See [[JS - Introduction to JavaScript]]
Resources:
* [10 JavaScript Tricks You Didn’t Know🤞🚀](https://medium.com/@khushi1399gupta/10-javascript-tricks-you-didnt-know-cb23d4bd23e6)
* [20 JavaScript Tips and Tricks You Can Use Right Now](https://medium.com/@satyamv57/20-javascript-tips-and-tricks-you-can-use-right-now-e698880db0f1)

---

#### 1. Destructuring with Aliasing
```JS
// renaming `prop1` and `prop2` to `newName1` and `newName2`, respectively
const { prop1: newName1, prop2: newName2 } = object;
```

#### 2. Memorization for Performance
* Memoization is a technique to cache function results for better performance.
```JS
const memoizedFunction = (function () {  
  const cache = {};  
  return function (args) {  
  if (!(args in cache)) {  
    cache[args] = computeResult(args);  
  }  
  return cache[args];  
  };  
})();
```

#### 3. Currying for Function Composition
* Currying allows creating reusable and composable functions
```JS
const curry = (fn, ...args) =>  
args.length >= fn.length ? fn(...args) : (...moreArgs) => curry(fn, ...args, ...moreArgs);
```

#### 4. Dynamic Object Keys
* Dynamically create object keys using square bracket notation
	* Useful when the key is determined at runtime
```JS
const dynamicKey = 'key';  
const obj = { [dynamicKey]: 'value' };
```

#### 5. Optional Chaining
* Optional chaining simplifies accessing nested properties without the need for numerous checks
* Long way
```JS
let nestedValue;  
if (object && object.property && object.property.nested) {  
  nestedValue = object.property.nested;  
  } else {  
  nestedValue = 'default';  
  }
```

* Using optional chaining
```JS
// nestedValue gets a value of "default" if object?.property?.nested is null or undefined
let nestedValue = object?.property?.nested ?? 'default';
```

#### 6. Array Destructuring
* Long way
```JS
const array = [1, 2, 3];  
const first = array[0];  
const second = array[1];
```
* Using Array Destructuring
```JS
// assigns a value of 1 to first and 2 to second
const [first, second] = [1, 2, 3];
```

#### 7. Object Destructuring
* Long way
```JS
const user = { name: 'John', age: 30 };  
const name = user.name;  
const age = user.age;
```
* Using Object Destructuring
```JS
const { name, age } = { name: 'John', age: 30 };
```

#### 8. Proxy for Validation
* Proxies can intercept and validate property assignments, providing robust input control
```JS
const validator = new Proxy({}, {  
  set: function (target, prop, value) {  
    if (prop === 'age' && typeof value !== 'number') {  
      throw new Error('Age must be a number.');  
    }  
    target[prop] = value;  
  }  
});
```

#### 9. Clone Arrays and Merge Objects
* The spread operator (`...`) lets you create copies of arrays and merge objects
```JS
// Cloning an array
const originalArray = [1, 2, 3];  
const clonedArray = [...originalArray];  
console.log(clonedArray); // Output: [1, 2, 3]
```
* Merging Objects
```JS
const obj1 = { a: 1, b: 2 };  
const obj2 = { b: 3, c: 4 };  
const merged = { ...obj1, ...obj2 };  
console.log(merged); // Output: { a: 1, b: 3, c: 4 }
```

#### 10. **Short-circuit with `&&` and `||`
* Use `&&` and `||` to create clean and concise conditionals
```JS
const name = user.name || 'Guest';  
console.log(name); // Output: Guest
```

#### 11. Chaining `setTimeout()`
* Chaining `setTimeout()` creates a sequence of delayed actions
```JS
function delayedLog(message, time) {  
  setTimeout(() => {  
    console.log(message);  
  }, time);  
}  
delayedLog('Hello', 1000); // Output (after 1 second): Hello
```

#### 12. Mastering `Promise.all()`
* Combine multiple promises and handle them collectively using `Promise.all()`
```JS
const promise1 = fetch('url1');  
const promise2 = fetch('url2');  
Promise.all([promise1, promise2])  
  .then(responses => console.log(responses))  
  .catch(error => console.error(error));
```

#### 13. NaN Checking
* Use `Number.isNaN()` to accurately check if a value is NaN
```JS
const notANumber = 'Not a number';  
console.log(Number.isNaN(notANumber)); // Output: false
```

#### 14. Optional Chaining (`?.`)
* Avoid errors with optional chaining when dealing with nested properties
```JS
const user = { info: { name: 'Alice' } };  
console.log(user.info?.age); // Output: undefined
```

#### 15. `JSON.parse()` to transform data
* The `reviver` parameter in `JSON.parse()` lets you transform parsed JSON
```JS
const data = '{"age":"30"}';  
const parsed = JSON.parse(data, (key, value) => {  
  if (key === 'age') return Number(value);  
  return value;  
});  
console.log(parsed.age); // Output: 30
```

#### 16. Fetch with `async`/`await`
* Using `async`/`await` with `fetch()` simplifies handling asynchronous requests
```JS
async function fetchData() {  
  try {  
    const response = await fetch('url');  
    const data = await response.json();  
    console.log(data);  
  } catch (error) {  
    console.error(error);  
  }  
}  
fetchData();
```

#### 18. Intersection Observer
* Use the Intersection Observer API for lazy loading and scroll animations
```JS
const observer = new IntersectionObserver(entries => {  
  entries.forEach(entry => {  
    if (entry.isIntersecting) {  
      entry.target.classList.add('fade-in');  
      observer.unobserve(entry.target);  
    }  
  });  
});  
  
const elements = document.querySelectorAll('.animate');  
elements.forEach(element => observer.observe(element));
```

#### 19. ES6 Modules for Clean Code
* Use ES6 modules for clean, modular code
```JS
// math.js  
export function add(a, b) {  
return a + b;  
}  
  
// app.js  
import { add } from './math.js';  
console.log(add(2, 3)); // Output: 5
```

#### 20. Pattern Matching
* Allows for conditional matching
```JS
const fruit = ['apple', 'banana'];

const message = match(fruit) {
  case ['apple', 'banana']: return "Delicious Choice!";
  case ['orange', 'grapefruit'] return "Citrusy goodness";
}

console.log(message) // Output: Delicious choice!
```

```JS
const user = { name: 'Jane', age: 25, isAdmin: false };  
  
const status = match(user) {  
  case { name, age, isAdmin: true }: return `${name} is an admin`;  
  case { age, isAdmin: false }: return `${age}-year-old user`;  
  default: return 'Unknown status';  
}  
  
console.log(status); // Output: 25-year-old user
```