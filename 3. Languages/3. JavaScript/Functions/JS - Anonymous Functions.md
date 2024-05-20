See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---
#### What are anonymous functions?
* A function that does not have any name associated with it
	* Useful if the function is NOT going to be used elsewhere in the code is by including the handler’s code inside the `addEventListener()` method (see [[JS - DOM Events]])

* Example: Using an anonymous function in an IFEE
```js
// IIFE using an anonymous function  
(function() {  
  console.log("This is an example of IIFE.");  
})();
```

* Example: Using an anonymous function as a callback
```js
// Using an anonymous function as a callback  
setTimeout(function() {  
  console.log("This is invoked after 2 seconds");  
}, 2000);
```

* Example: Using an anonymous function in an event handler
```js
// Using an anonymous function in an event handler function
let element = document.querySelector(".my-element");
element.addEventListener("click", function () {
  console.log("You have clicked on the element");
});
```