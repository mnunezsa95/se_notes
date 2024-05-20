See [[React - Introduction to React.js]]

---
#### Importing fetch
```JSX
import fetch from 'fetch';
```

#### Using the fetch module
* Syntax
	* The `then()` method is used to handle the response from the request
```JSX
fetch(url)  
  .then(response => response.json())  
  .then(data => console.log(data));
```

* Example
```JSX
const url = 'https://jsonplaceholder.typicode.com/todos';  
  
fetch(url)  
  .then(response => response.json())  
  .then(todos => {  // Do something with the todos data.  
  });
```