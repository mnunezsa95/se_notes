Objects are a data type in JavaScript (see [[JS - Data Types in JavaScript]])
Objects widely underline, just about everything: numbers, arrays, functions, etc

# Objects in JS
* Objects --> allow for storing data of mixed data types in **hierarchical** structure

# Creating an object 
* Uses curly braces ` { } ` 
* Contains properties inside curly braces in the form of ` key-value ` pairs
	* Key --> MUST be string data type
	* Value --> any data type

#### Syntax: Objects
```js
variable_name = {
  key_1: "value_1",        
  key_2: value_2,      
  key_3: "value_3"          
}; 

// the key will ALWAYS be a string
// the values can be any data type (boolean, string, number, undefined, object, array)
```

#### Example: Creating an Object
```js
let user = {
  name: "Karen",
  dotaLevel: 29,
  dogName: "Boulder"
}; 
```
