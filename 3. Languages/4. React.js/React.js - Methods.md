See:
* [[React - Introduction to React.js]]
Resources:
* Documentation: [React.js](https://react.dev/)

---
##### `ReactDOM.createRoot()`
* Creates a React root for displaying content inside a browser DOM element
	* Arguments
		* `domNode` -- the DOM node where content will be displayed
		* `options`
```JSX
import React from "react";
import ReactDOM from "react-dom/client";

// Displaying content inside the "root" of the HTML file
ReactDOM.createRoot(document.getElementById("root")).render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

##### `ReactDOM.render()`
* Displays a piece of JSX (React Node) into the React root's browser DOME node
	* Arguments
		* `reactNode` -- A react node to be displayed
```JSX
// Displaying content inside the "root" of the HTML file
ReactDOM.createRoot(document.getElementById("root")).render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

##### `React.createElement()`
* Creates a React element with the given `type`, `props`, and `children`
	* Arguments
		* `type` -- must be a valid React component type (such as `'div'`, `'span'`)
		* `props` -- must either be an object or `null`
			* If `null`, it will be treated the same as an empty object
			* If not `null`, it will create a reactElement using the object
		* `...children` -- Zero or more child nodes.
```JSX
import { createElement } from 'react';  

function Greeting({ name }) {  
	return createElement(  
		'h1',
		{ className: 'greeting' },  
		'Hello'  
	);  
}
```