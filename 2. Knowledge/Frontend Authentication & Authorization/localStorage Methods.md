* Methods to be used with the localStorage global object (see [[Local Storage]])

# localStorage Methods
#### setItem()
* Description
	* used to save data to browser storage
* Arguments
	1) key --> a name for the content to be stored
	2) value --> the value for the content to be stored (can only be a string); can use the JSON.stringify() method to convert to string
* Syntax
```js

```
* Example
```js
localStorage.setItem('username', 'Dr_Marvin_Quack');

// creating a username
localStorage.setItem('user', JSON.stringify({
  firstName: 'Marvin',
  lastName: 'Quack'
}));
```

### getItem()
* Description
	* used to get saved data
* Arguments
	1) key --> name of the content to be pulled; if the value of the content is in JSON string, use the JSON.parse() method to convert it back to an object
* Syntax
```js

```
* Example
```js
localStorage.getItem('username'); // "Dr_Marvin_Quack"

// getting the username
JSON.parse(localStorage.getItem('user'));
```

### removeItem()
* Description
	* used to save data from memory
* Arguments
	1) key
	2) value
* Syntax
```js

```
* Example
```js
localStorage.removeItem('username');
```