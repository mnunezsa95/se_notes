# Redirecting Users
#### How to redirect users
1) Add a root route to the JSX markup
	* Typically added at the end of all routes
		* If added before, it will superceed all routes
2) Provide logic showing to redirect user based on their authentication
	* Utilize the `useState()` hook
	* Use the Redirect component (from **react-router-dom**) (see [[React.js - Redirect Component]])


# Protecting Routes on Front End
#### How to protect routes 
1) Create a wrapper component (usually called ProtectedRoute) that is reusable (see [[React.js - Wrapper Components]])
	* Should return a Route component

# Example 
[Youtube Video: Redirecting Users](https://www.youtube.com/watch?v=YEnfuJBLg4I)
[Youtube Video: Protecting Routes on Front End](https://tripleten.com/trainer/web/lesson/5e75e7b0-a403-4a5b-8601-805ec0c357f8/task/998ba1f0-85c8-4b28-bf8d-2d1dca045cf7/?theory_open=false)

```jsx
// Creating a Protected Route

import React from 'react';
import { Route, Redirect } from 'react-router-dom';

const ProtectedRoute = ({ isLoggedIn, children, ...props }) => {
	return (
		<Route {...props}> // props are being passed arbirtary 
			{isLoggedIn ? children : <Redirect to='/login' />}
		</Route>
	);
};

export default ProtectedRoute;
```

```jsx
// app.js

import { Redirect } from "react-router-dom"; // importing Redirect component
import ProctectedRoute from './components/ProtectedRoute/ProtectedRoute'

function App() {
	// using the useState hook for state management
	const [isLoggedIn, setIsLoggedIn] = React.useState(false);
	return (
		<div className='app'>
			<Switch>
				<Route path="/register">
					<Register />
				</Route>
				<Route path="/login">
					<Login />
				</Route>
				<ProtectedRoute isLoggedIn={isLoggedIn} path="/profile"> 
					<Profile />
				</ProtectedRoute >
				<Route path="/"> // conditionally redirecting user to routes
					{isLoggedIn && <NavBar /> ? <Redirect to='/profile' /> :                            <Redirect to='login' />}
				</Route>
			</Switch>
		</div>
	);
}

// the && <NavBar /> conditionally renders the NavBar
```