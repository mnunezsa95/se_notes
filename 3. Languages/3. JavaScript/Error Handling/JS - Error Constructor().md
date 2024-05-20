## Error Constructor()
* 3 Main properties [[JS Properties]]
	1) message --> contains the error text
		* user-readable
		* by default, it is an empty string
	2) stack --> contains the 'stack trace' [stack trace]
		* helps understand what functions were called up to error point
	3)  name --> contains the name of error
		* works as identifier to identify error when handling
		* by default, named 'error'
	4) statusCode --> contains the status code 
		* can be manually set

```JS
// create a standard error with the text "Object not found"
let err = new Error("Object not found" { statusCode: 404 });

// change the error name to "NotFoundError"
err.name = "NotFoundError"; 

console.log(err.name); // make sure the new name is stored inside the error object
```

#### Using Errors
* After being created, errors can be thrown (see [[JS - Throwing Errors Manually]])

