See:
* [[React - Introduction to React.js]]
* [[React.js - Methods]]
Resources:
* Documentation: [React.js](https://react.dev/)

---

# The `children` prop
* The `children` prop -- a special prop that allows components or elements to be passed between the opening and closing tags of another component. 
* This is particularly useful for creating reusable and flexible components.
```JSX
import React from "react"

function GreetComponent(props) {
	return (
		<div>
			<h1>Hello, {props.name}</h1>
			{props.children}
		</div>
	)
}

function App() {
	return (
		<GreetComponent name="Marlon">
			<p>This code still works!</p>
		</GreetComponent>
	)
}
```

