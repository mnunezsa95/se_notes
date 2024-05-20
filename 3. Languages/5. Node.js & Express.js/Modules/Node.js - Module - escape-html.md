# What does the escape-html Module do?
* Helps prevent XSS by automatically escaping special characters with their html entity (see [[Cross-Site Scripting (XSS)]])

#### Installing escape-html
* Import the module into the project

#### Using escape-html
* Pass a string into the escape variable (see [[Node.js - Module - escape-html]])
	* escape is a function that will take a string as an argument and replace the special characters
```js
// importing escape-html
const escape = require('escape-html'); 

// Using the escape variable (with contains a function to convert a string into an escaped equivalent

escape('<script>alert("hacked")</script>'); // '&lt;script&gt;alert(&quot;hacked&quot;)&lt;/script&gt;
```