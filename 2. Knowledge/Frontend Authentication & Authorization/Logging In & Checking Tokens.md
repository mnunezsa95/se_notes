# Logging In

### General Logic: Logging Users In
1) Initial Login --> check credentials that the user has entered
	* if correct --> log user in & send JWT; store JWT inside the browser
	* if incorrect --> display message
2) Future Logins --> grab JWT from browser & check the validity 
	* if correct --> user will have access to data 
	* if incorrect --> user will not see data

### Example: Logging Users In
1) Create a function in auth.js that will authorize the user
2) Call this function in the Login Component inside a submit handler
3) Change the value inside of the LoginIn logic inside of app.js to true
	* Change the state using some kind of function


# Checking Tokens
### General Logic: Checking User Tokens
1) Check localStorage to see if a token is present
	* if yes --> make an API request with the token to verify it truly belongs to the user
	* if no --> 
2) Change the value of the `isLoggedIn` state to true
3) Redirect users to the needed path

### Example: Checking Tokens
1) Create a `componentDidMount()` function to check for token every time the component mounts
2) Create a `tokenCheck()` method to check and grab the token from local storage
3) Create a function (API call) to grab content from server and import into app.js call it inside the `tokenCheck()`

### Example: Logging In & Checking Tokens
```js
// auth.js

export const authorize = (identifier, password) => {
  return fetch(`${BASE_URL}/auth/local`, { 
	method: "POST",
	headers: {
	    Accept: "application/json",
	    "Content-Type": "application/json",
	},
	body: JSON.stringify({ identifier, password }), // sending user's credentials
	})
	.then((response) => response.json()); // returns a promise 'data'
	.then((data) => { 
		if (data.jwt) {  // check if there's a 'jwt' property in data object
			localStorage.setItem("jwt", data.jwt); // save token for future use
			return data; // return data object with user data
		} else {  // otherwise return nothing
			return; // we need to do this to avoid ESLint errors 
		} 
	}); 
};


// grabbing content 

export const getContent = (token) => { // takens a JSON web token as an arg
  return fetch(`${BASE_URL}/users/me`, {
	method: 'GET',
	headers: {
		'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${token}`, 
    } // if the token is valid, it will return a response that contains user 
  })  // information.
    .then(res => res.json())
    .then(data => data)
} 
```

```js
// Login.js

handleSubmit(e) { 
	e.preventDefault(); 
	if (!this.state.username || !this.state.password) { 
		return; 
	}
	auth.authorize(this.state.username, this.state.password) // call authorize()
		.then((data) => { // check data in authorize() 
			if (data.jwt) { // if jwt is valid, set the state
				this.setState({
					username: '',
					password: ''
	        }, () => { 
		        this.props.handleLogin(); // updating the state inside App.js
		        this.props.history.push('/ducks'); // send users to right path
		    })
		}
    })
    .catch(err => console.log(err)); // this is fired if the user not found
} 
```

```js
// App.js

constructor(props) {
	super(props);
	this.state = { 
		loggedIn: false // originally set to false by default
	}
	this.handleLogin = this.handleLogin.bind(this);
	this.tokenCheck = this.tokenCheck.bind(this);
}

componentDidMount() {
  this.tokenCheck();
};

handleLogin(e) { // function will change the value to "true"
	e.preventDefault();
	this.setState({
		loggedIn: true
	})
}

tokenCheck() {
	// if the user has a token in localStorage, this function will check that           the user has a valid token
	const jwt = localStorage.getItem('jwt');
	if (jwt) {
		// we'll need to verify the token here
		auth.getContent(jwt).then((res) => {
		    if (res) {
	        // we'll log the user in
		        this.setState({
					loggedIn: true,
		        }, () => {
			        // we've also wrapped App.js with the withRouter HOC so we                          now have access to this method
					this.props.history.push("/ducks");
		        });
			}
    });
  }
}
```

```jsx
// passing 'handleLogin' as a prop to `Login`:

<Route path="/login"> 
	<div className="loginContainer"> 
		<Login handleLogin={this.handleLogin} /> 
	</div> 
</Route>
```

