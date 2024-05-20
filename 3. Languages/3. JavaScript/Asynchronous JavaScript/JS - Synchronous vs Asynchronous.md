# Synchronous Code
* A blocking code structure that executes in a linear fashion (uses an operations queue)
	* Operation queue --> each snippet (piece) of code is prevented from running until all the prior snippets are executed. 

# Asynchronous Code
* A non-blocking code structure that allows for tasks to run simultaneously 

# Synchronous v Asynchronous Code
* Synchronous --> code runs in linear fashion
	* Current line needs to finish, before next one can start
* Asynchronous --> code can run simultaneously (see [[JS - Async JavaScript Behind the Scenes]])
**![](https://lh4.googleusercontent.com/LN1M5P0kMkF35lFnaixGFDPuA9YsG6Ay3Kja0A_wCabosTZPf36iz226RLf_1IWk8PtPAw6QkZVP1oaJk0Av9kzgAkOOYlkQfaen1sNjWkqxJIMJPSqXkl7u8S6IDyMzIsAwi37QT5ltWcHtQqmrze4)

# Important Concepts
* Callbacks alone DO NOT make code asynchronous 
	* Some callbacks (like ones used with `setTimeout()`) do make code asynchronous (see [[Timer Methods]])
* Event Listeners alone DO NOT make code asynchronous
	* Some event listeners have asynchronous behavior that make code async


