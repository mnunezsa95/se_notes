## What is a Server?
* Server --> processes incoming requests and sends responses to them
	* Constantly running

## How do server requests work?
* 3 steps after receiving requests 
	1) Checks to ensure request is correct
	2) Fetches info from database
	3) Returns a response 

## Server-side Languages
* There is a difference between server-side (backend languages) and frontend languages (see [[Frontend Languages v Backend Languages]])
* Most popular (can operate alone)
	* C, C++, Java, Ruby, Python, PHP
* Can work w/ adaptation
	* JavaScript (w/ help from Node.js)

## Node.js  ( [[Node - Introduction to Node.js?]] )
* JS engines had a block I/O model for request processing
	* Requests to the server executed in the order in which they were sent
	* Large operations took more time
	* Small operations took less time
	* Users had to wait a long time to get data (could not run multiple requests at one time)
