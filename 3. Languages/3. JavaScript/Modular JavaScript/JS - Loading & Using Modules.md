* What are modules? (see [[JS - What are Modules?]])
### Using Modules
* A few steps need to take place before modules can be used
	1) Browser needs to see that modules are being used
		* Add `module` to the attribute type when connecting a script
	2) Export the module, function or variable to be made available in other files (see [[JS - Importing & Exporting Modules]])
	3) Import the module, function or variables that we want to use (see [[JS - Importing & Exporting Modules]])

```html
<!--Adding the module value to the type attribute-->

<script type="module" src="script-01.js"></script>
<script type="module" src="script-02.js"></script>
```

```js
// script-01.js

// Exporting a variable and function
export const str = "I am a variable from the module script-01.js";
export function myFunc() {
  console.log("I am a function from the module script-01.js");
} 
```

```js
// script-02.js

// importing the function and variable by using their names
import {str, myFunc} from "./script-01.js";

// Now they can be used
console.log(str); // "I am a variable from the module script-01.js"
myFunc(); // "I am a function from the module script-01.js"
```