There are several ways to perform user authorization & authentication (see [[Identification, Authentication & Authorization]])
* JWTs (see [[JWTs (JSON Web Tokens)]])
* Sessions (session-based authorization)
* OAuth (Open Authorizations)
* Multi-Factor Authentication

# Sessions (session-based authorization)
* What is a session?
	* A session is an object that contains the user's login information

* How it works:
	1) A session is created when the user enters their account info
	2) The client receives a session identifier 
	3) On every request, the user sends this session to the server
	4) When logging out --> the server deletes the session from the database
		* User will need to re-login next time
* Resources
	1) [Node.js Server & Authentication Basics: Express, Sessions, Passport, and cURL](https://medium.com/@evangow/server-authentication-basics-express-sessions-passport-and-curl-359b7456003d)
	2) [NPM Express-Session (a module for working with sessions in Express.js)](https://www.npmjs.com/package/express-session)

# OAuth (open authorization)
* What is open authorization?
	* OAuth is authorization through a third party account (FaceBook, Yahoo, Google, Apple, etc)
* Benefits of OAuth
	* Allows for quicker sign-in experience
* How it works
	* Does NOT send account info (username and password)
	* Instead --> an exchange takes place to verify that the user trying to log in has been authenticated by the third party site
* Resources
	* [Passport.js](http://www.passportjs.org/) (popular library for authentication for OAuth)

# Multi-Factor Authentication 
* Multi-factor authorization can include many forms
	* 2-factor authorization (2fa)
	* 3-factor authorization (3fa)
	* etc...
* Common multi-factor authorization methods
	* SMS authentication --> a text message is sent to the phone number that is registered on the account
	* Email authentication --> an email is sent to the email address that is registered on the account
* Benefits
	* Increased security
		* Increases difficulty of hacking into an account
* How it works
	* Multi-factor authentication --> uses TOTP (time-based one-time password) algorithm 
* Resources
	* [Otplib](https://github.com/yeojz/otplib) (popular Node.js library for Multi-factor authentication)
