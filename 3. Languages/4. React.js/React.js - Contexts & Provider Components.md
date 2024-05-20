# What is a Context?
* Allows for data to be passed through multiple components without having to pass each component individually
	* Allows for values to be easily shared in components, regardless of location within the component hierarchy
* Uses a **context** --> a tool for passing data through the subtree without the need to manually pass props through every level

# General Context: Context
1) Create a context using `React.createContext()` method
2) Import the context, use the Provider component and wrap desired components inside of it
3) Store values in the **value** property
4) Subscribe desired components to the Provider using `React.useContext()`

--- 
## Creating a Context
* Uses the `React.createContext()` method (see [[React.js - Methods]])
	* Comes with a `Provider` component (which re-renders any time the value of the provider changes)

#### the Provider
* Has a prop called **value** that can be assigned to all children (values assigned to the value property can be accessed by the children)

* Example
```jsx
// AppContext.js

import React from 'react';
// creating a context
export const AppContext = React.createContext(); 
```

```jsx
// App.js
import { AppContext } from './AppContext';

// the JSX inside of the App component's render() method
// using the Provider component
<AppContext.Provider value={{state: this.state, handleLogin: this.handleLogin}}>
	<Switch>
		<ProtectedRoute path="/ducks" component={Ducks} />
		<ProtectedRoute path="/my-profile" component={MyProfile} />
		<Route path="/login">
			<div className="loginContainer">
				<Login />
			</div>
		</Route>
		<Route path="/register">
			<div className="registerContainer">
				<Register />
			</div>
		</Route>
		<Route>
		  {this.state.loggedIn ? <Redirect to="/ducks" /> : <Redirect                       to="/login" />}
		</Route>
	</Switch>
</ AppContext.Provider> 
```

#### Subscribing
* The `React.useContext()` method is used to subscribe to a context
	* Returns the context value that was passed to the provider’s value props
* Example
```jsx
// ProtectedRoute.js

import React from 'react';
import { Route, Redirect } from 'react-router-dom';
import { AppContext } from './AppContext.js'; // importing the context

const ProtectedRoute = ({ component: Component, ...props }) => {
	const value = React.useContext(AppContext); // getting the values
		return (
		<Route>
			{
				() => value.state.loggedIn === true ? <Component {...props}                      userData={value.state.userData} /> : <Redirect to="./login" />
			}
		</Route>
)}

export default ProtectedRoute; 
```
