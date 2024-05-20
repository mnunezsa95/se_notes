# Changing Element Values
* An element's value can be changed by accessing the index
* How to do this:
	1) Access the item that will be changed (see [[JS - Accessing Array Elements]])
	2) Set this equal to the new value
```js
let groceries = ["chips", "lemonade", "grapefruit", "orange", "juice", "milk", "eggs", "cookies", "banana", "cheese"];

groceries[0] = "carrot";

/* the array will NOW look like this: 

["carrot", "lemonade", "grapefruit", "orange", "juice", "milk", "eggs", "cookies", "banana", "cheese"];

*/
```

# Setting Element Values
* An element's value can be set by accessing the index
* How to do this: 
	1) Specify the array that should be selected (see [[JS - Accessing Array Elements]])
	2) Add the items at the desired index
```js
let array = [];            // here is an empty array, called “array”
array[0] = "first";        // using the 1st index to add a string named first
array[1] = "second";      // using the 1st index to add a string named second

// the array will NOW look like this: ["first", "second"]
```