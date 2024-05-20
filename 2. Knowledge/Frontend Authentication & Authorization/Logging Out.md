### General Logic: Logging Users Out
1) User clicks on 'sign out' button
2) JWT is removed from localStorage
3) Handle the sign out in app.js 
	* Can use `handleLogout()` and add it the `signOut()`
4) User is redirected to the login

```jsx
import React from 'react';
import { Link, useHistory } from 'react-router-dom';
import Logo from './Logo.js';
import './styles/NavBar.css';

function NavBar() {
	const history = useHistory();
	function signOut() { 
		localStorage.removeItem('jwt'); // remove the JWT from localStorage
	    history.push('/login'); // push to the login page
	}
	return (
		<div className="navbar">
			<div className="navbar__logo">
		        <Logo/>
			</div>
			<ul className="navbar__nav">
				<li><Link to="ducks" className="navbar__link">Ducks</Link></li>
				<li><Link to="my-profile" className="navbar__link">My 
					profile</Link></li> {// signOut fires onClick }
		        <li><button onClick={signOut} className="navbar__link 
					navbar__button">Sign out</button></li> 
			</ul>
		</div>
	)
}

export default NavBar; 
```