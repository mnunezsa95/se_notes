
[TripleTen Video: React.js Registration](https://www.youtube.com/watch?v=sJoQ9YSXSsM&t=1s)

### Step 1: A function for registering
* Create a functional component that will be used for registration
* Create some handlers
	* handleSubmit --> to handle form submission
	* handleChange --> to handle changes to the input fields 
* Create an auth.js utils --> houses all authentication logic
	* Declare a BASE_URL variable
	* Declare any necessary functions (register, login, etc)
		* Should go to the required route
		* Should have required method, headers, and body
			* Body can be values from the register function
* Import the auth.js file into the necessary component
	* Use the methods inside auth.js

### What is a Computed Property?
* Computed Property --> evaluating what is placed inside the brackets and using the result as the property's key.
	* If brackets are omitted, it will assume literal string
	* Example
```js
const handleChange = (event) => {
	const { name, value } = event.target;
	setValues({ ...values, [name]: value }) // [ ] is a computed property
}	
```

### Redirecting a user after Sign up
* The `useHistory` hook can be used to redirect users after signing up (in functional components)
* The `withRouter HOC` can be used to redirect users after signing up (in class components)
	* Provides `history`, `location`, and `match` objects generated by React Router to a component as props
		* history --> redirect users, simulate browser back and forward 
		* location --> extra info about current URL
		* match --> extra info about current Route 

# Example: Registration
```jsx
import React, { useState } from 'react';
import { Link, useHistory } from 'react-router-dom';
import * as auth from './auth.js'; // import auth file

function Register() {
	// create necessary state variables
	const [username, setUsername] = useState('');
	const [email, setEmail] = useState('');
	const [password, setPassword] = useState(''); 
	const [confirmPassword, setConfirmPassword] = useState(''); 
	const history = useHistory();
	
	const handleSubmit = (e) => {
    e.preventDefault();
	if (password === confirmPassword){
	    // calling register function
	    auth.register(username, email, password) 
		    .then((res) => {
			    console.log(res)
			    history.push('/login')
		    })
		    .catch(console.log); // catching an error thrown
		}
	}
		
	const handleChange = (event) => {
		const { name, value } = event.target;
		setValues({ ...values, [name]: value }) // [ ] is a computed property
	}	// the ...values object holds the values

	return(
		<div className="register">
	        <p className="register__welcome">
		        Please register.
		    </p>
        <form className="register__form">
	        <label>
	            {'Username: '}
		        <input 
			        className="register__input"
			        name="username" 
			        type="text" 
			        value={values.username} 
			        onChange={handleChange} 
			    />
	        <label>
	            {'Email: '}
		        <input 
			        className="register__input"
			        name="email" 
			        type="text" 
			        value={values.email} 
			        onChange={handleChange} 
			    />
	        <label>
	            {'Password: '}
		        <input 
			        className="register__input"
			        name="password" 
			        type="text" 
			        value={values.password} 
			        onChange={handleChange} 
			    />
		    </label>
	        <label>
	            {'Username: '}
		        <input 
			        className="register__input"
			        name="confirm-password" 
			        type="password" 
			        value={values.confirmPassword} 
			        onChange={handleChange} 
			    />
		    </label>
		</form>
		    <div className="register__button-container">
			    <button onClick={handleSubmit} className="register__link">Sign                       up</button>
			</div>
			{/* link to login page */}
			<div className="register__signin">
				<p>Already a member?</p>
				<Link to="login" className="register__login-link">Log in                            here</Link>
			</div>
		</div>
    )
}

export default Register
```

```js

const BASE_URL = 'https://register.nomoreparties.co'; // url for all requests

// a function to handle registration
// confirmPassword not needed since it was already verified during sign up
export const register = (username, email, password) => {
	return fetch(`${BASE_URL}/signup`, {
		method: 'POST',
		headers: {
			'Accept': 'application/json',
			'Content-Type': 'application/json'
	    },
	    //stringfy() method turns values into JSON string
	    body: JSON.stringify({ username, password, email }) 
	})
	.then((res) => res.json()) // converting response to object
	.then((data) => {
		if (data.error) {
			throw new Error(data.error);
		}
		console.log(data)) // logging response (called data)
	});
	
}
```