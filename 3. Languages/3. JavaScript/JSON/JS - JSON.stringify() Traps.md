See [[JS - Introduction to JavaScript]], [[JS - Working with JSON]]

---

* JSON.stringify() in JavaScript is a powerful function for converting JavaScript objects into JSON-formatted strings.
#### 1. Handling Undefined, Functions and Symbol Values
* `undefined`, `Function`, and `Symbol` values are **not** valid JSON values
	* Either omitted or `null` in arrays
```JS
const obj = { foo: function() {}, bar: undefined, baz: Symbol('example') };  
const jsonString = JSON.stringify(obj);  
console.log(jsonString); // Output: '{"foo":null}'  
  
const obj2 = {arr: [function(){}]};  
console.log(JSON.stringify(obj2)); // Output: {"arr":[null]}
```

#### 2. Primitive Values for Boolean, Number, and String Objects
* Boolean, Number, and String objects are converted to their corresponding primitive values during stringification.
```JS
const boolObj = new Boolean(true);  
const jsonString = JSON.stringify(boolObj);  
console.log(jsonString); // Output: 'true'
```

#### 3. Ignoring Symbol-Keyed Properties
* Symbol-keyed properties are completely ignored during stringification, even when using a replacer function. 
* Any data associated with Symbol keys will be excluded from the resulting JSON string
```JS
const obj = { [Symbol('example')]: 'value' };  
const jsonString = JSON.stringify(obj);  
console.log(jsonString); // Output: '{}'  
  
const obj2 = {arr: [function(){}]};  
console.log(JSON.stringify(obj2)); // Output '{}'
```

#### 4. Handling Infinity, NaN, and Null Values
* Infinity, NaN, and null values are all considered `null` during stringification
```JS
const obj = { value: Infinity, error: NaN, nothing: null };  
const jsonString = JSON.stringify(obj);  
console.log(jsonString); // Output: '{"value":null,"error":null,"nothing":null}'
```

#### 5. `toJSON()` Method Responsibility
* If an object has a `toJSON()` method, it is responsible for defining what data will be serialized. 
* This allows custom serialization logic for objects.
```JS
const obj = {  
data: 'important information',  
toJSON: function() {  
return { customKey: this.data };  
},  
};  
const jsonString = JSON.stringify(obj);  
console.log(jsonString); // Output: '{"customKey":"important information"}'
```

#### 6. Date Objects Treated as Strings
* Instances of Date implement the `toJSON()` function by returning a string (same as `date.toISOString()`), resulting as strings during stringification.
```JS
const dateObj = new Date();  
const jsonString = JSON.stringify(dateObj);  
console.log(jsonString); // Output: '"2023–12–06T12:34:56.789Z"'
```

#### 7. Circular References Exception
* If `JSON.stringify()` encounters an object with circular references, it throws an error.
	* Circular references occur when an object references itself in a loop.
```JS
const circularObj = { self: null };  
circularObj.self = circularObj;  
JSON.stringify(circularObj); // Throws an error
```
#### 8. Serialization of Enumerable Properties
* For Object instances like Map, Set, WeakMap, and WeakSet, only their enumerable properties are serialized. 
	* Non-enumerable properties are excluded.
```JS
const mapObj = new Map([['key', 'value']]);  
const jsonString = JSON.stringify(mapObj);  
console.log(jsonString); // Output: '{}'
```

#### 9. Error on BigInt Conversion
* An error is thrown when attempting to convert a value of type BigInt using `JSON.stringify()`
```JS
const bigIntValue = BigInt(42);  
JSON.stringify(bigIntValue); // Throws an error
```